> 我们只知道在四次挥手的过程中，先发起关闭的一方会进入TIME_WAIT状态，为什么会出现TIME_WAIT状态以及如果TIME_WAIT状态过多，是什么原因？

<!-- TOC -->

- [1 出现的场景](#1-出现的场景)
- [2 TIME_WAIT什么作用](#2-time_wait什么作用)
- [3 TIME_WAIT哪些危害](#3-time_wait哪些危害)
- [4 TIME_WAIT如何优化](#4-time_wait如何优化)

<!-- /TOC -->


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->


## 1 出现的场景

> 在TCP建立连接对外提供服务的过程中，每个链接会占用一个本地端口，如在高并发的情况下，TIME_WAIT状态过多，势必会占用大量的端口，端口又有限，以致于耗尽端口，所以会出现偶尔链接的上，偶尔断开的情况

这么多的TIME_WAIT哪里来的呢？先复习下四次挥手

![四次挥手](https://static01.imgkr.com/temp/1da55578b7264156b50866890f62ac89.png)

[FIN_WAIT1] :FIN_WAIT1和FIN_WAIT2均为等待对方的FIN报文。两者区别为，当SOCKET在ESTABLISHED状态时，想主动关闭连接从而想对方发送FIN报文，此时进入FIN_WAIT1状态。当收到ACK报文进入FIN_WAIT2状态。

[FIN_WAIT_2]：此状态下的socket实际上表示半连接的状态。什么是半连接，是一方想要关闭连接，另一方说稍等下，我还有点数据给你哈

[FIN_WAIT] :表示收到了对方的FIN报文，并发送出了ACK报文，就等2MSL后即可回到CLOSED可用状态了

[CLOSE_WAIT] : 反过来读比较好，WAIT_CLOSE即「等待关闭」。在被动关闭连接情况下，在已经接收到FIN，但是还没有发送自己的FIN的时刻，连接处于CLOSE_WAIT状态。

[LAST_ACK] ：被动关闭乙方发送FIN后，等待对方的ACK，收到ACK即进入CLOSED状态

在TCP/IP协议栈中，假设主机A想要进行链接终止操作，于是发送FIN报文给主机B，主机B收到从而进入CLOSE_WAIT状态并发送ACK作为应答，同时主机B会告诉应用程序也要关闭操作，于是发送FIN报文。主机A收到FIN报文发送ACK表示收到并进入TIME_WAIT


在Linux系统中有一个字段，名称为TCP_TIME_WAIT_LEN，其数值为60s，也就是需要在TIME_WAIT阶段停留60s

![](https://static01.imgkr.com/temp/d4cccc089a7243d5b70c17b187f40fcc.png)


## 2 TIME_WAIT什么作用

从上图我们知道TIME_WAIT过后还有CLOSE状态，为什么不直接进入CLOSED状态，而是要过一会呢？

第一点，在TIME_WAIT后，为了确保ACK能让被动方接收并辅助其关闭。假设这样的情况

如果主机A的ACK报文传输失败，那么在TCP/IP协议栈设计中，主机B会重传FIN报文，但是此时主机A没有维护好TIME_WAIT状态而是CLOSED状态，此时主机A只好发送RST，从而被动关闭失败。

第二点，为了让就连接的重复节点在网络中自然消失。怎么理解？

我们知道，在网络传输的过程中，总会因为各种故障导致报文不能准时到达目的地。现在我们假设使用[源IP,源端口，目的IP，目的端口]代表连接A，在通信的过程中，链接A因为某种原因中断，暂时迷路，从而创建了类似于A的连接B，可是迷路的连接A到达了，势必就会对TCP通信产生影响。所以设置了2MSL，足够的时间让两个方向的分组都消失,使得下一个新的连接不会出现旧的连接请求报文


## 3 TIME_WAIT哪些危害

- 内存资源占用

- 端口占用。端口资源有限，一般可开启端口为32768～61000，可以通过修改net.ipv4.ip_local_port_range指定，如果TIME_WAIT太多将无法建立连接

你可以通过下面命令查看当前TIME_WAIT数量

> ```
> netstat -nt | awk '/^tcp/ {++state[$NF]} END {for(key in state) print =key,"t",state[key]}' TIME_WAIT 28233
> ```

这里为什么是28233呢，取决于内核参数net.ipv4.ip_local_range

![](https://static01.imgkr.com/temp/c47dab033bdc487aab40d3e23ba6f5f0.png)


因为端口范围是一个闭区间，所以实际可用的端口数量是：

```
shell> echo $((61000-32768+1)) 28233
```

## 4 TIME_WAIT如何优化

- 暴力执法------net.ipv4.tcp_max_tw_buckets

> 一旦TIME_WAIT状态过多就重置，方法是使用sysctl将系统值减小，太粗鲁不推荐

- 调低 TCP_TIMEWAIT_LEN

> 了解内核编译即可操作

- SO_LINGER设置

> int setsockopt(int sockfd, int level, int optname, const void *optval,
> socklen_t optlen);

- 调整tcp_tw_recycle

我们先看看RFC1323中怎么描述的

> An additional mechanism could be added to the TCP, a per-hostcache of the last timestamp received from any connection.This value could then be used in the [PAWS] mechanism to rejectold duplicate segments from earlier incarnations of theconnection, if the timestamp clock can be guaranteed to haveticked at least once since the old connection was open. Thiswould require that the TIME-WAIT delay plus the RTT togethermust be at least one tick of the sender’s timestamp clock.Such an extension is not part of the proposal of this RFC.

- net.ipv4.tcp_tw_reuse 复用连接

> 使用这个选项有个前提，需要打开TCP时间戳的支持net.ipv4.tcp_time stamps=1，在RFC1323中，为了保证TCP的高可用，引入了两个4字节的时间戳选项，用于记录 TCP 发送方的当前时间戳和从对端接收到的最新时间戳。这就有意思了，之前说的2MSL就不存在了，因为如果重复的数据包会因为时间戳的过期而被丢弃

1. 只适用于连接发起方（C/S 模型中的客户端),这里为什么强调是客户端，我们看看源码；

![](https://static01.imgkr.com/temp/a3277a3290f94ac4ae11a4d1f0d05020.png)

其调用路径仅仅出现在tcp_v4_connect->inet_hash_connect->__inet_check_established->twsk_unique->twsk_unique。  也就是说tcp_tw_reuse仅在TCP套接字作为客户端，调用connect时起作用。作为服务端很少主动发起链接，所以对于服务端而言不用打开此选项

2. 对应的 TIME_WAIT 状态的连接创建时间超过 1 秒才可以被复用。


最后引用一下W. Richard Stevens在《UNIX网络编程》的一句话

> The TIME_WAIT state is our friend and is there to help us (i.e., to let old duplicate segments expire in the network). Instead of trying to avoid the state, we should understand it.

> 译者：存在即合理，勇敢面对，而不是逃避。

巨人的肩膀
- 《Coping with the TCP TIME-WAIT state on busy Linux servers》
- Tuning TCP and nginx on ec2 -p30
- TIME_WAIT and its design implications for protocols and scalable client server systems
- tcp_tw_recycle和tcp_timestamps导致connect失败问题
- https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt
- tcp_tw_recycle参数引发的系统问题 - http://blog.csdn.net/zhuyiquan/article/details/68925707