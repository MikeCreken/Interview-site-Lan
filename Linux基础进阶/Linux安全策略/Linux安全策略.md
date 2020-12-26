> 相信通过上一篇的分享，已经架设了属于自己的Linux，就这样得空客就安全了吗？当然不是，今天我们一起看看Linux本省得一些安全策略。对了，关于Linux的内容是系列内容，希望大家可以从0开始搭建，然后按步骤操作，后续涉及的集群，大数据，可视化等一些的学习都会基于这个环境，所以mark住没问题。

下午回到家就想睡觉，醒来以为快早上了，一看时间原来才晚上十一点了，感冒了两周，颓废了半个月，心态不咋好，现在又来和你们见面了，加油！

是的，偶尔出现广告了，放心一个月最多四个，用来补贴点生活水电费，生活有点困难，理解的支持一下，不想看却想打赏的也没事，每个月发最后一篇原创的时候会开打赏(嘻嘻)，问题不大，保持一颗白嫖的心，会越走越远的。

对了，上一期的思维导图还在更新中，很快就会和大家见面



----



## 1 Linux安全策略

在生产环境几乎都是Linux，为了保护我们程序，防止我们功能被破坏，会采取一些列的措施，所以提前学习和了解这些策略势必也会为后面的学习打下不错的基础

> 常见的攻击类型有哪些呢

- **密码暴力破解**

目的比较明确，通过爆破工具破解用户的密码，进入服务器获取资源进行系统的破坏。我们可以想象一个字典，字典足够强大，逐一匹配就可以找到服务器的密码

- **拒绝服务攻击**

通过大量的请求来占用足够多的服务资源，使得网络阻塞或者服务器死机，导致Linuxf服务器无法给用户提供服务。常见的拒绝服务攻击有Dos与分布式拒绝服务攻击。黑客通常是利用伪装的源地址或者控制其他的目标机器发出大量的连接请求，由于服务器无法在短时间接受这么多情趣，从而导致系统资源耗尽，服务挂起

- **应用程序漏洞攻击**

这种情况一般是黑客通过类似扫描工具扫描服务器可能存在的漏洞，然后根据漏洞渗入到服务器进行相应的破坏，常见比如sql注入，漏洞攻击，网页权限漏洞等

> 如何进行防范呢

彻底的防范是不可能，但是可以尽全力的防范，通常需要一系列的安全设备和规则进行约束

![超简部署](https://img-blog.csdnimg.cn/20201117211057545.png#pic_center)



- **网络传输的安全**

常见的网络安全设备有**硬件防火墙**，**网络入侵检测**，**路由器**，**交换机**等。防火墙对进出网络的主机进行规则匹配，尽量保证合法的主机进入网络，可是有些攻击行为是在防火墙允许的范围内，这个时候防火墙就无所能及了，就需要诸如IDS设备来辅助。IDS会对系统的整体运行情况进行监控，尽全力发现攻击企图，从而保证网络系统资源的机密性，完整性和可用性

- **操作系统的安全**

操作系统安全即服务器本身的一些安全设置和优化。比如系统内核的定期升级，自带软件的更新，配置 iptable 规则，关闭无关服务等

很多常见的病毒程序，防火墙很难阻止，此时如果系统存在杀毒工具也是可以直接破掉第一道防线

- **应用软件安全**

应用软件安全顾名思义即部署在服务器中应用的安全策略配置，比如我们会对数据库进行配置防止非规则内的连接数据库等

再比如  SQL注入，跨站脚本都属于应用软件安全漏洞造成的攻击

> 那么常用的安全策略有哪些呢

- **软件及时更新**

这一块我估计很多人都不会在意，毕竟需要重新安装比较麻烦，但是很多时候需要更新，是因为有漏洞了，意味着Hack利用这些漏洞就很容易进你的系统，所以需要尤其注意

- **端口服务**

一般一个有效的连接，即客户端和服务端端口的建立过程。而端口在系统中也是有一些规则的

在Linux操作系统中，系统定义了 **65535** 个端口，这些端口又分为两个部分，按照 **1024** 分割，分为只有 root 用户才能启用的端口和客户端的端口，对于只有root用户才能启动的端口：

也就是 **0-1023** 的端口，需要 root 才能启用，因为这些端口预留给一些预设的服务使用，不经常使用的端口最好关闭，比如 Ftp 的21端口，25的 Mail 服务端口

**客户端的端口**

1024端口以上的通常给客户端软件使用，由软件随机分配，对于大于1024的端口不受root的限制，比如默认的3306就是数据库的默认端口

> 如何查看端口的状态呢？

通过 netstat -tunl 查看

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211153737.png#pic_center)


从上图可以发现启用了22端口，这是默认就打开了，我的远程工具XSHELL即就是连接的这个端口

> 如何查看链接的状态呢

```shell
netstat -tun
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211138731.png#pic_center)


> 如果查看端口对应的什么服务，执行什么命令呢

```shell
netstat -anlp
```

> 服务与端口是什么关系

我们可能经常听到什么服务对应什么端口，他们两是一一对应的关心，没有服务运行即没有端口对应，那是不是这些服务都必须使用默认的端口呢

当然不是，大部分的软件都会有配置文件，根据相应的配置就好了

> 一定要记得关闭不必要的服务

在Linux中，服务的启动和关闭管理有两种方式，第一种方式是直接启动脚本，在 Centos7 之前是在 /etc/init.d 目录下的服务启动和关闭。在 Centos7 以后，使用 **systemctl** 工具来完成，这个在后续的系统管理会详细给大家说说。

如果要启动 sshd 服务，可以使用下面的命令

```shell
systemctl restart sshd
```

另外一种情况是通过超级服务管理一些常用的网络服务，比如 Centos 的超级服务 Xinetd，这个服务可以管理的服务如 Vsftpd 等，我们可以通过 /etc/init.d/xinted restart 来完成服务的重启

在Linux中，通过 chkconfig 命令或者 systemctl 判断服务是否开启

```shell
chkconfig --list sushi
```

> 我们怎么知道关闭哪些不必要的服务呢

这里列出一个表格

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211115435.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_16,color_FFFFFF,t_70#pic_center)


> 还有一些其他的安全设置

- 禁止系统响应任何从外部来的ping请求

ping通过用来检查网络的连通性，如果能够ping通，攻击者就知道这是一个活跃的机器，那么怎么禁止ping请求呢

```shell
echo "1" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

- 删除不必要的用户组

删除系统不必要的用户 userdel username

删除系统不必要的组 groupdel groupname

- 关闭selinux

首先它是内核强制访问控制安全系统，，由于它和现在的linux应用程序和内核模块有一些兼容问题，如果要查看是否已启用

通过使用 getenforce，如果要关闭selinux，修改下面的文件

```shell
vi /etc/sysconfig/selinux
```

## 2 说说防火墙

防火墙有硬件防火墙和软件防火墙，在这里主要介绍软件防火墙。根据工作方式的不同又分为**封包式防火墙**和**应用层网关防火墙**

硬件防火墙使用专有的操作系统，如果按照工作方式来划分，那么防火墙也分为过滤式防火墙、应用层网关防火墙两种，后面给大家介绍的 iptable 即属于**过滤式防火墙**

Iptable 是 Linux 中内嵌好的防火墙软件，集成在内核中，因此效率非常高的。它可以通过你设置一些封包过滤规则来定义什么数据包可以接受，什么数据包剔除

>  iptable的使用环境?

- 保护自身本机

windows中有防火墙软件，iptables类似，在Linux中的位置如下

![保护自身本机](https://img-blog.csdnimg.cn/2020111902031161.png#pic_center)


从上图可以发现，在交互的过程中，首先要经过 Linux 自身的 iptables 防火墙，作为第一层的安全过滤，随后经过防火墙的第二层的过滤最终到达互联网，所以可以说Linux自带的iptables是系统安全的最后一道防线。

- 独立的Linux主机对整个网络进行防护

如下图所示，部署在Linux路由器上对整个局域网进行安全防护

![独立的Linux主机对整个网络进行防护](https://img-blog.csdnimg.cn/20201119015246505.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

从位置来看，位于外网与局域网之间，防火墙在路由器的上面，所以先对进入局域网的数据包进行过滤，这样不就对局域网主机进行了访问控制，以此来保护局域网的安全


- 多台Linux主机对Lan进行多层安全防护

通常局域网划分了子网，在子网钱部署一道Linux防火墙，然后将一些保密的资源放在这个子网里，子网通过设置第二道Linux防火墙设置相对更高的安全等级

![多台Linux主机对Lan进行多层安全防护](https://img-blog.csdnimg.cn/20201119015307435.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 对DMZ进行安全防护

DMZ区域通常将互联网与局域网隔离开的一个特殊网络区域，通常部署一些不包含机密信息的服务器，比如ftp，这样来自外网的访问者可以通过Linux防火墙来访问DMZ的服务，即使DMZ服务器遭到破坏，也不会影响另一部分网络

![对DMZ进行安全防护](https://img-blog.csdnimg.cn/20201119015329854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

> iptables的基本使用是如何的？

- iptables 的前生后世

Linux最早出现的防火墙叫做 ipfw，是基于Linux2.0内核的。随后在 Linux2.2 中推出了ipchains，语法更容易理解且功能更强大，随后 iptables 在 Linux2.4 出现，同时也包含了 ipchains，但是两者无法兼容，iptables防火墙越来越强大，Linux2.4以后就基本上使用iptables防火墙了

- iptables的组成

iptables=ip tables，意味着是**IP表**的意思，对的，它是由多个表组成，且每个表的用途不一样，在每个表中定义了很多链，通过这些链设置规则和策略

iptables呢有三种表的选项，管理本机数据进出的 **filter** 表，管理防火前内部主机的 **NAT** 表和改变包头内容的**mangle**表

先来看看filter进行信息表的过滤，分别包含了INPUT、OUTPUT和FORWARD链

![filter表](https://img-blog.csdnimg.cn/20201119015354924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


NAT表主要用于网络地址转换，再上一个篇也有说过，它包含了PREROUTING、POSTROUTING和OUTPUT链

![NAT表](https://img-blog.csdnimg.cn/20201119015412168.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


mangle表包含了一些用于标记高级路由的信息报，可以改变包以及包头内容，如TTL、TOS，MARK。它知识在内核空间为包设置一个标记而已，这个表内置了五个链：PREROUTING、POSTROUTING、OUTPUT、INPUT和FORWARD

通过多个路由规则和预设规则组成了功能链，然后多个功能链组成功能表，多个功能表组成iptables防火墙

> iptables的执行过程是怎么样的呢？

当数据包到达Linux主机，首先进行 iptables 过滤，如果数据包满足规则1指定的条件则直接执行相应的操作，后面的2，3规则就不再理会

![基本过滤规则](https://img-blog.csdnimg.cn/20201119015432193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)



**举个例子**

> 假设目前这个 LInux 可以对外提供 www 的服务，对于网络 192.168.50.0/24 中的网络主机开放访问www服务，但是禁止192.168.50.133访问www服务，规则如下

- 规则1：禁止192.168.50.133主机访问www服务 
- 规则2：允许本地网络访问www服务

这样子设置完规则后，本地的网络除了133不能访问以外，其他的都能访问。如果反过来

- 规则1：允许本地网络192.168.50.0/24访问www服务
- 规则2：禁止192.168.50.133主机访问www服务、

此时的规则1允许所有主机访问Linux服务器的www服务，自然也包含了133主机，规则2将显得毫无意义

> iptables的使用语法是怎么样的呢

- 启动和关闭iptables

```shell
servcie iptables start//启动
service iptables stop//关闭
chkconfig --level 35 iptables on //设置iptables开机默认启动
```

> iptables的防火墙规则如何查看以及如何清除修改？

```shell
格式：iptabls [-t tables] -L -vn -FXZ
```

- 查看当前系统filter表的几条链规则

```shell
iptables -L -n
```

## 3 用户以及用户组的管理

**用户组**

Linux是一个真实且多用户多任务的操作系统，意味着张三王五李四都可以同时使用同一个Linux操作系统，但是他们三儿不能互相访问各自的内容，不同的用户有不同的权限，每个用户在权限范围内完成不同的任务，Linux正是通过这样的权限划分和管理实现多用户的运行机制

> Linux用户的分类是怎么样的呢

- 超级用户

超级用户，默认为root，具有最高的权限

- 普通用户

只能对自己目录下的文件进行访问

- 虚拟用户

最大的特点是不能访问登录系统，他们的存在主要是为了方便系统管理，满足相关系统进程对文件属性的要求

**用户和组**

用户通过向Linux申请用户访问系统，这样可以合理的利用和控制系统，同时也可以帮助用户组织文件，达到提供对用户文件的安全性保护的目的

> 什么是用户组呢

有时候需要协同办公，假设一共10个人，让这10个人对文件的操作具有相同的权限，需要给每个用户授权，这样岂不是太麻烦了，Linux就使用**组**的概念，让属于组的用户都具有相同的权限

> 用户和组的关系

用户和组的关系可以是一对一，也可以是一对多设置多对多

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211235541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_16,color_FFFFFF,t_70#pic_center)



- 一对一：这个组就只有一个用户
- 一对多：这个用户存在于多个组中，具有多个组的共同权限
- 多对1:多个用户存在一个组，具有相同权限
- 多对多：多个用户存在于多个组

> 用户的配置文件在哪儿？

用户和组相关配置文件，我们分别查看如下几个文件

- /etc/passwd

这个文件是系统用户配置文件，起格式如下

> 用户名：密码：用户标识号：组标识号：注释描述：主目录：默认shell

看看/etc/passwd是什么样子


![/etc/passwd](https://img-blog.csdnimg.cn/2020111721163042.png#pic_center)



**详细说说这些都是什么意思**

- 用户名：用户账户
- 密码：为了保护用户隐私，这里面存放的都是一个特殊字符，加密的用户密码存放在/etc/shadow中
- 用户标识号：用户的UID，每个用户都会有一个UID且唯一，0是超级用户的标识，1-99由系统保留，

作为普通用户，UID从500开始，用户的权限和角色也是根据 UID 而定，如果把普通用户的 UID 设置为0，将拥有root权限，这个非常的危险

- 组标识号：组的GID，记录用户所在组，对应于/etc/group文件的一条记录
- 主目录：用户登录默认所处的目录
- 默认shell：默认使用的用户解析器，用户的所有操作都是通过shell传递给内核的

为了保证用户的密码安全，使用了/etc/shadow

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211615748.png#pic_center)


- 用户名：与/etc/passwd的用户名相同的含义
- 加密密码：存放的是加密以后的用户密码字符串，如果字段是* ！等，对应的用户不能登录系统
- 最后一次的修改时间：表示从某个时间起，到用户最近一次修改密码的间隔天数
- 最小间隔时间：两次修改密码之间的最小时间间隔
- 最大时间间隔：两次修改密码之间的最大时间间隔
- 警告时间：系统开始警告到密码正式失效的时间
- 不活动时间：表示用户密码作废以后多少天，系统禁止这个用户
- 失效时间：用户的账号生存期

> /etc/group是干啥的

- 组名：用户组的名称，组名不能重复
- 密码：存放用户组加密后密码字串，默认设置在/etc/shadow文件中，而这里的x代替
- 组标识号：Gid与/etc/passwd中组标识号对应
- 组内用户列表：多个用户使用逗号分隔

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211753879.png#pic_center)

> /etc/default/useradd文件

为什么我们通过 useradd 命令创建一个用户后，默认在 /home 下且使用的shell是 /bin/bash ，看看 /etc/default/useradd 就明白了

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211808896.png#pic_center)


/etc/default/useradd 定义了新建用户的一些默认属性，比如用户的主目录，使用 shell 等，通过更改增额文件就可以改变新建用户的默认属性值

> 用户的管理工具有哪些？

- groupadd命令

groupadd用来新建用户组，其语法格式如下所示

```shell
groupadd -g gid group
```

这里的选项 -g 表示指定新建用户组的GID，这个GID必须唯一

选项-o：一般和-g同时使用，表示新用有的一直y户组gid和系统已y

此时创建一个lan_group1用户组和lan——group2用户组

```shell
group -g 1110 lan_group1
Group -g 1120 lan_group2
More /etc/group| grep lan_group1
```


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117211716485.png#pic_center)



- groupdel命令

>  groupdel用于删除用户组

groupdel 名称

> 如果删除lan_group1

```shell
groupdel lan_group1
```

> 详细说说useradd/usermod等命令

- useradd

如果在使用useradd的时候，不使用任何的参数，那么系统首先会读取配置文件/etc/login.defs和/etc/default/useradd，然后根据这两个配置文件来添加用户。随后想/etc/passwd和/etc/group添加用户和用户组记录，同时会在/etc/passwd中添加队以ing的加密文件。接着系统就会在/etc/default/useradd中增加用户主目录，这样一个主目录就算建立了。

useradd的基本使用和常用选项

- -u uid：唯一用户标识号
- -g group：指定用户登录的默认组
- -d home：指定新建用户的默认主目录，如果不指定在，则会在etc/default/useradd中创建用户主目录
- -e expire：指定用户的账号过期时间

> 如何更改用户的账户属性信息

通过usermod修改用户的账户信息。

```shell
usermod -u -g -G -d .....
```

常用的选项

- -u uid：指定用户新uid，唯一
- -d 主目录：修改用户登陆的主目录
- -c 注释：修改用户的注释信息
- -f：失效日

> 如果要删除用户呢

通过userdel删除用户，指定"-r"参数不仅删除用户，还会删除用户的主目录

> 好了举一个完整一点的例子

- 添加一个用户lan_linux，所属用户组为base_linux，附加用户组为forme_linux，同时指定用户的默认主目录为/opt/base_linux
- 添加用户test，指定UID为666，默认shell为/bin/sh，指定用户组为上面的
- 修改用户test的主用户组为test_modify，同时修改test的附加组

![案例练习](https://img-blog.csdnimg.cn/20201119024657322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

## 4 文件权限

> 通过 ls 命令就可以查看文件以及目录的权限信息，如果使用 ls -al则还可以查看隐藏文件

为了更加详细的了解每一行各个段什么意思，我们取出一行

![文件权限](https://img-blog.csdnimg.cn/20201117215329813.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

第一列由10个字符组成，其中分为4个部分，拆解如下

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201117215349614.png#pic_center)




- 文档类型，其中d表示目录，l 表示软连接。当为 - 表示是文件，为 c 表示字符设备文件

接下来的三个部分，3个字符为一组，**r-读，w-写，x-执行**

- 第二个部分 user 部分，是对文档所有者权限的设定，rwx 表示用户对 xxx 有读写执行的所有权
- group部分，是文档所属用户组权限的设定
- other部分是对文档所有者之外的其他用户的权限设定

第二列表示文档的连接数，表示有多少文件执行一个inode

- 第三列表示文档所属的用户和用户组
- 第四列是文档的大小
- 第五列表示最后一次修改的日期
- 第六列是文档名称

> 这些权限如何去修改呢

通过chown改变文件和目录的权限，所有者包含了用户和用户组。

> 使用方法：chown -R y 用户名称 文件 目录

-R: 进行递归式的权限更改，意味着将目录下所哟肚饿文件，子目录都更新为指定的用户组权限，这个操作需要多多谨慎

> 如果需要修改访问的权限呢？

使用 chmod 来改变文件或目录的访问权限。使用方法有两种，一种是字母和操作符表达式的字符设定法，另一种是包含数字的数字设定法

**先来看第一种---字符设定法**

语法：chmod [who] [+ | - | =] [mode] 文件名

下面详细说一下各个选项的含义

- who表示操作的对象，可以是下面字母中的任何一个
  - 如果是u，则代表用户，即文件或者目录的所有者
  - 如果为g，则代表用户组，即文件或目录所属组
  - 如果为o，表示其他用户，
  - 如果为a，表示所有用户
- 操作符有哪些
  - “+”表示添加某个权限
  - “-”表示取消某个权限
  - “=”表示赋予给定可执行的权限，其中可以是可读，可写，可执行

- mode表示可以执行的权限，其中可以是r，w，x以及他们的组合
- 文件名可以是以空格分开的文件列表，支持通配符

**案例**

> 修改文件test.log文件，使其所有者具有所有权限，用户组和其他用户具有只读权限

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119030040559.png#pic_center)

**数字设定法**

> 即上面的r用数字4代替，w用2代替，x用1代替，所以如果想让文件的属主拥有读写权限，可以通过4+2的方式来实现，

- 755：第一个 7代表文件所有者的权限，通过4+2+1得到。第二个5标识文件所属组的权限，通过4+0+1实现

举个例子

> 修改文件test.log的权限为644

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201119030519162.png#pic_center)

## 5 总结

> 今天从Linux的安全策略，防火墙到用户的基本管理和文件的权限，当我们知道怎么用了以后，是不是就需要去了解他是怎么个设计理念呢，我们下期再见！