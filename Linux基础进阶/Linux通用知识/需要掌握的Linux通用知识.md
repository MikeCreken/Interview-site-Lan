>噗。。，这篇笔记是学习的Li


<!-- TOC -->

- [一 Linux通用知识](#一-linux通用知识)
    - [1 vmvare](#1-vmvare)
    - [2 进行网络配置](#2-进行网络配置)
    - [3 安装xshell](#3-安装xshell)
    - [4 基本命令的使用](#4-基本命令的使用)
    - [5 用户管理](#5-用户管理)
    - [6 软件的安装方法](#6-软件的安装方法)
    - [7 shell](#7-shell)
    - [8 awk文本处理工具](#8-awk文本处理工具)
    - [9 进程管理与定时任务和后台执行](#9-进程管理与定时任务和后台执行)
    - [10后台运行](#10后台运行)

<!-- /TOC -->

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->


![Linux排查问题套路](https://img-blog.csdnimg.cn/20201108204253751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

----



![Linux命令详解](https://img-blog.csdnimg.cn/20201108204306325.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

# 一 Linux通用知识

>说到操作系统，如果读大学的时候是计算机专业，那肯定就会上这门课，我猜测当时的你们想法是这样的

- 上大学使用的都是Windows系统，界面友好，上手快，习惯性的点点点操作
- 大部分的课程在windows中操作，比如C++用的Vistual Studio，学数据库的SQL Server
- 大学中的操作系统更加偏向理论研究，至于到底是怎么运作的可能懵懵懂懂

直到上了研究生到了实验室，我发现实验室的怎么都是对着一个窗口操作，瞬间觉得以前的计算机知识白学了，于是开启了Linux之路。

其实大部分的系统，团购，打车，快递都部署在服务端，其中都包含Linux，什么云计算，虚拟化，大数据等也是基于Linux，那为啥在大学里都是windows？


![在这里插入图片描述](https://img-blog.csdnimg.cn/20201108204502314.gif#pic_center)




> 为什么说了解Linux的生态，会让你学到更多的新技术?

我们要知道很多的大牛通过Linux来开发各种如那件，数据库Mysql，kafka，Spark等技术都会默认提供Linux的安装运维手册，所以尽快的进入Linux的世界对于个人的进步和职业发展都是非常有好处的

每当我们买了手机，买了电脑，上手就可以用，这是因为预装了操作系统。所以呀，那有什么岁月静好，其实有人帮我们负重前行了，操作系统就是这样一个角色。

> 那么操作系统帮助我们做了哪些事儿呢？

- 抛几个问题，桌面上的图标是什么，为啥子敲一下键盘就出来了画面
- 电脑咋个知道我们鼠标点击的那个位置
- 为什么我一回车，这些字符就飞出去了

这几个任何一个操作，基本上都覆盖了操作系统的所有功能，那我来认识熟悉而默认的操作系统

## 1 vmvare

> 虚拟机是什么？

虚拟机通过软件来模拟具有完整硬件系统功能的，运行在完全隔离的完整计算机系统。每个虚拟计算机可以独立运行并安装各种软件和应用

- 首先从官方下载并解压虚拟机安装包，然后双击运行

![双击VMVARE](https://img-blog.csdnimg.cn/20201105222231878.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 下一步

![接受许可进行下一步](https://img-blog.csdnimg.cn/20201105222247108.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 选择安装位置，最好不要出现中文

![自定义路径](https://img-blog.csdnimg.cn/20201105222300793.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 设置用户体验选项，都可以选择

![设置用户体验](https://img-blog.csdnimg.cn/20201105222311641.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 在桌面和开始菜单程序文件夹创建快捷方式。

![创建快捷方式](https://img-blog.csdnimg.cn/20201105222328883.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 百度一个许可证ZG1WH-ATY96-H80QP-X7PEX-Y30V4

![输入许可证密钥](https://img-blog.csdnimg.cn/20201105222347197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 打开vmvare

![打开vmvare](https://img-blog.csdnimg.cn/20201105222751580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 点击新建虚拟机向导 选择文件-新建虚拟机打开

![新建虚拟机](https://img-blog.csdnimg.cn/20201105222807132.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 选择自定义 下一步

![选择自定义](https://img-blog.csdnimg.cn/20201105222822827.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 下一步

![选择下一步](https://img-blog.csdnimg.cn/20201105222833694.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 安装客户机操作系统，选择稍后安装操作系统

![选择稍后安装操作系统](https://img-blog.csdnimg.cn/2020110522284469.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 命名虚拟机 更改虚拟机名称并选择安装得位置

![命名虚拟机](https://img-blog.csdnimg.cn/20201105222856973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 更改主机配置进行处理的分配

![处理器核心数分配](https://img-blog.csdnimg.cn/20201105222915110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 虚拟内存分配：注意内存分配不能大于主机内存

  ![虚拟内存分配](https://img-blog.csdnimg.cn/20201105222928638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 设置虚拟机网络得类型，这里选择NAT

![网络类型暂设为NAT](https://img-blog.csdnimg.cn/20201105222940902.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_16,color_FFFFFF,t_70#pic_center)


- IO控制器选择，选择LSILogic
- 磁盘类型选择SCSI即可

![](https://img-blog.csdnimg.cn/20201105222953221.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 创建磁盘选择创建新虚拟磁盘

![创建新虚拟磁盘](https://img-blog.csdnimg.cn/20201105223007207.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 指定磁盘文件

![指定磁盘文件](https://img-blog.csdnimg.cn/20201105223019493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)


- 修改路径


- 选择自定义硬件

![选择自定义硬件](https://img-blog.csdnimg.cn/20201105223053904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 选择centos得ISO镜像文件，先选择CDDVN---ISO镜像文件---浏览找到镜像、

![导入镜像](https://img-blog.csdnimg.cn/20201105223118875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 点击完成

![完成](https://img-blog.csdnimg.cn/20201105223129203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 开启虚拟机 选择配置好的虚拟机

![开启虚拟机](https://img-blog.csdnimg.cn/20201105223140157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 鼠标移动到虚拟机内部，上下键选择install centos7然后回车

![install centos7](https://img-blog.csdnimg.cn/20201105223157876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 选择软件选择最小安装，选择语言

  ![选择最小化安装](https://img-blog.csdnimg.cn/20201105223210101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 软件安装

![软件安装](https://img-blog.csdnimg.cn/20201105223227389.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 选择计算节点

![选择计算节点](https://img-blog.csdnimg.cn/20201105223239890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 开始安装

![开始安装](https://img-blog.csdnimg.cn/20201105223256438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

- 设置root密码，点击完成配置
- ![设置root密码](https://img-blog.csdnimg.cn/20201105223331954.png#pic_center)



## 2 进行网络配置

> 现在我们的centos还是个空壳子，如果我们需要访问外网，则需要进一步配置一波

- 打开配置文件

```shell
#vi /etc/sysconfig/network-scripts/ifcfg-eth0
```

- 更改相应的配置

```shell
DEVICE=eth0 #设备名称，可根据ifcofnig命令查看到。
BOOTPROTO=dhcp #连接方式，dhcp会自动分配地址，此时不需要在下面设置ip和网关
HWADDR=00:0C:29:AD:66:9F #硬件地址，可根据ifcofnig命令查看到。
ONBOOT=yes #yes表示启动就执行该配置，需要改为yes
```

- service restart network完事 ping www.baidu.com

![网络检测](https://img-blog.csdnimg.cn/20201105223340488.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0wxNTUxOTU0MzgzNw==,size_1,color_FFFFFF,t_70#pic_center)

## 3 安装xshell

> 我们已经完成了安装vmvare并导入了centos，那么我们如何去玩儿这个看似很牛皮的玩意？直接上手？不习惯吧，那我们用个远程工具连连

Xshell 是一个强大的安全终端模拟软件，Xshell 可以在 Windows 界面下用来访问远端不同系统下的服务器，从而比较好的达到远程控制终端的目的。除此之外，其还有丰富的外观配色方案以及样式选择。

- 下载xshell(别去下了，贼慢麻烦)
- 链接测试(因为使用的ssh，那么确保centos中22端口已经打开了)
- 文件-----属性进行XHSELL相关的配置，比如配色，字体大小等

## 4 基本命令的使用

> 命令太多，必须要全部记忆，但是要学会如何查每个命令的参数。我画了个思维导图可以当作小字典查看，下面列出可能我们使用频率会更高的命令

| 执行命令              | 含义                                  |
| --------------------- | ------------------------------------- |
| cd ~                  | 切换到登录用户的主目录即/home/用户名  |
| cd /                  | 进入根目录                            |
| cd /home/lj           | 将/home/LJ作为当前的目录              |
| cd ..                 | 返回到上一层目录                      |
| cd -                  | 回到上次所在的目录                    |
| cd ../../             | 去上上层目录                          |
| ls                    | 查看当前目录                          |
| ls -la                | 查看当前目录的文件信息 包含了隐藏文件 |
| pwd                   | 查看当前目录的绝对路径                |
| cp /目录/1.txt /目录/ | 复制                                  |
| rm                    | 删除                                  |
| q！                   | 不保存文件退出                        |
| wq！                  | 保存退出                              |
| hostname              | 查看当前主机名                        |
| ifconfig              | 查看网卡相关信息                      |
| firewall-cmd --state  | centos7查看卡其关闭防火墙状态         |

## 5 用户管理

>  刚才说了可以创建自己的用户，那么怎么创建自己的用户呢?

添加用户

```shell
useradd -d /home/lanj -m lanj
```

更改密码

```shell
passwd lanj
```

系统有很多的用户，怎么进行用户的切换？

```shell
su -lanj
```

```shell
su -root
```

> 如果需要

用户之间的切换使用su命令实现。root用户可以无需输入密码切换到lj用户，如果普通用户lj切换到root用户则需要输入密码，我们看看

su -lj

su -root

> 如何切换路径，绝对路径和相对路径

## 6 软件的安装方法

> 在Linux安装相关的工具分为三种方式，分别为源码安装，RPM包安装以及YUM安装方式

**源码安装方式**

> 开源软件都会提供源码下载的方式，对于源代码安装方式的好处即可以定制软件功能，安装需要的模块，不需要的模块可以屏蔽，方便管理，卸载等。

对于源码安装的步骤如下

- 下载解压源码

> 一般下载下来源码以后都会存在一个Readme文件，首先应该仔细阅读这个文件，可能有很多需要修复的以前人家遇见的问题都会在上面做记录，以免入坑不回头

- 分析平台环境
- 编译安装软件

这里会使用make工具，make工具就会通过makefile文件来实现。makefile文件是一种按照某种语法来编写且定义了各个文件的依赖关系。

在Linux中，习惯使用Makefile替代makefile，当用户执行configure后，就会在当前目录生成这个makefile文件，然后用户输入make就开始运行。我们看看Makefile是怎么个有样子

```shell
edit : main.o kbd.o command.o display.o \
		insert.o search.o files.o utils.o       /*注释:如果后面这些.o文件比edit可执行文件新,那么才会去执行下面这句命令*/
	cc -o edit main.o kbd.o command.o display.o \
		insert.o search.o files.o utils.o

main.o : main.c defs.h
	cc -c main.c
kbd.o : kbd.c defs.h command.h
	cc -c kbd.c
command.o : command.c defs.h command.h
	cc -c command.c
display.o : display.c defs.h buffer.h
	cc -c display.c
insert.o : insert.c defs.h buffer.h
	cc -c insert.c
search.o : search.c defs.h buffer.h
	cc -c search.c
files.o : files.c defs.h buffer.h command.h
	cc -c files.c
utils.o : utils.c defs.h
	cc -c utils.c
clean :
	rm edit main.o kbd.o command.o display.o \
		insert.o search.o files.o utils.o
```

> make和make install的关系

当我们输入make命令过后即进入了编译阶段，编译时间根据软件的程序规模大小以及硬件配置有关，当输入make install就会开始安装软件，我们可以指定安装目录也可以不指定，系统将给你默认指定目录为/user/local，这样安装完毕。

**RPM安装方式**

> RPM是Red Hat公司开发出来的Linux下的软件包管理工具。这些以.rpm结尾的包包含了已经编译好的二进制可执行文件，一句话即将源代码进行编译，安装，然后封装为RPM包

优点即安装简单，方便，因为已经编译完成，安装只是用来验证和解压过程，缺点也比较明显，过于依赖于操作系统，要求RPM包的安装环境必须和RPM封装时的环境保持一致，

> RPM包是怎么个样子？

```shell
server-2.1.0-22.I386.rpm
```

其中：server为如那件的名称

2.1.0：软件的版本号

22：软件更新发行的次数

i386:适合硬件发行的次数

.rpm:rpm软件包的标识

**YUM安装方式**

- 查看是否存在yum

```shell
rpm -qa | grep yum
```

- 没有则安装

```shell
rpm -ivh yum-*.noarch.rpm
```

- 自定义yum的配置。我们可以通过打开/etc/yum.repos.d/Centos-Base.repo进行源的配置

> YUM有哪些特点呢

- 安装方便
- 可以同时配置多个源
- 配置文件简单明了

> 推荐个不错的yum源

- EPEL

是一个针对红帽企业版Linux及衍生发行版的一个高质量附加软件包项目。网址：http://fedoraproject.org/wiki/EPEL/zh-cn

- RPMForge

> 这是一个第三方软件仓库，被centos社区认为是一个最安全最稳定的一个软件仓库

## 7 shell

> 大部分情况都是Linux操作系统，那么熟悉命令的用法以外，熟悉使用shell脚本能介绍不少时间

**shell是什么**

> “ 平时经常在Linux操作系统中使用各种命令，比如查看当前的目录文件，我们会使用"ls"或者"ls -l"，这些字符串参数实际上会被"某段程序"执行并启动它。这个负责将用户输入的字符串转换为需要执行程序的东西叫做"shell"。即帮用户更方便使用操作系统接口的“壳”。同样的壳还有当我输入Maven+相关参数的时候是不是就会去执行相应的功能，我们驶入sql语句的时候，数据库引擎是不是也会各种调用，一样的道理

**尝试编写第一个shell**

> vim创建打开一个文件，扩展名为.sh。如下所示

```python
#!/bin/bash #告诉系统使用什么解析器
echo "Hello xiaolan !" # echo进行输出
```

- 执行方法1

```shell
 chmod +x ./hello.sh ./hello.sh
```

- 执行方法2

```shell
 /bin/sh hello.sh
```

**变量**

> “ 变量名和等号之间不能有空格

定义变量注意事项

- 命名首个字符不能是数字，只能使用英文字母、数字和下划线
- 不能使用标点符号
- 不能使用bash中关键字

**变量使用**

> “ 使用变量(使用变量的过程中，最好加上花括号)，只需要在变量前面加上美元符号即可

```python
#!/bin/bash
James="小皇帝"
echo $James
```

**只读变量**

> “ 使用readonly将变量定义为只读，只读意味着不能改变

```python
#!/bin/bash
James="小皇帝"
readonly James
James="登哥"
```

删除变量

> “ 使用unset删除变量 变量删除以后不能再次使用，且不能删除只读变量

```python
#!/bin/bash
James="小皇帝"
unset James
echo $James #不会有任何输出
```

变量类型

- 局部变量

> “ 仅当前shell可用

- 环境变量

> “ 所有程序都能访问环境变量

- shell变量

> “ 通过一部分环境变量和shell变量保证shell的正常运行

字符串

> “ 使用字符串的过程中，既可以用双引号也可以用单引号，也可以不用

- 单引号

> “ 单引号内容原样输出，不能包含变量，且不能出现单独单引号

- 双引号

> “ 可以出现转义字符

```python
#!/bin/bash
James="小皇帝"
str="\"$ James\"! oh my gad \n "
echo -e $str 
```

**获取字符串长度**

> “ 使用#

```python
string="qwert"
echo $(#string)

# 提取子字符串
echo $(string:1:3)
#查找字符串
echo 
```

**数组**

> “ 支持以为数组 

定义数组

> “ 数组元素使用“空格”隔开

```python
array=(value1,value2,value3)
```

读取数组

```
value1=${array[0]}
```

使用@输出数组所有元素

```
echo ${array[@]}
```

获取数组中所有元素以及数组长度

```python
#! /bin/bash
# author：xiaolan
array[0]=a
array[1]=b
array[3]=c

echo “数组的元素为：${array[*]}”
echo “数组的元素为：${array[@]}”
echo “数组的个数为：${#array[*]}”
echo “数组的个数为：${#array[@]}”

```

执行

```shell
./array.sh
```

结果

![img](https://img-blog.csdnimg.cn/img_convert/358e14d25f4c55c38c65baacd5295c22.png)

**注释**

**单行注释**

>  使用#开头的行为注释，会被解释器忽略

多行注释

**shell传递参数**

> **在执行**shell的时候，命令行指定参数，如下所示

```python
#!/bin/bash
James="小皇帝"
echo "执行的文件名为:$0"
echo "第一个参数为:$1"
echo "第二个参数为:$2"
```

**执行**

>  ./param.sh 1 2

**结果**

![img](https://img-blog.csdnimg.cn/img_convert/474702aee41c48c85912ae5e9dfae176.png)

**几个特殊字符**

![img](https://img-blog.csdnimg.cn/img_convert/3286152ee3826cd61b390081596f35f6.png)



案例(partionnal.sh)

```shell
#!/bin/bash
# author:xiaolan

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done
```

执行

```shell
./demo2.sh 1 2 3
```

结果

![img](https://img-blog.csdnimg.cn/img_convert/c54d1fa3eaeb4fa3eeecd0796f02c8aa.png)

相同点：都是会引用所有参数

不同点：在使用双引号的时候。如果脚本运行时两个参数为a,b，则"*"等价于"ab",而"@"等价于"a","b"

```python
#!/bin/bash
# author:xiaolan

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done

```

8 printf

> “ 使用printf格式化字符串，同时可以指定字符串宽度和对齐方式，格式如下 

```python
printf format-string [arguments...]

#!/bin/bash
# author:xiaolan
 
printf "%-8s %-8s %-4s\n" 姓名 科目 分数  
printf "%-8s %-8s %-4f\n" 小明 数学 97
printf "%-8s %-8s %-4f\n" 小话 语文 89
printf "%-8s %-8s %-4f\n" 王三 英语 93
```

**结果**

![img](https://img-blog.csdnimg.cn/img_convert/4d5065c4c989d48be8343b906cb2acb9.png)

**9 test**

>  shell中的test用于检查某个条件是否成立 

![img](https://img-blog.csdnimg.cn/img_convert/d7d500d2e657f64ccc6d481f3d0831a5.png)

案例

```python
#!/bin/bash
# author:xiaolan
num1=55
num2=55
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```

结果

![img](https://img-blog.csdnimg.cn/img_convert/07f80f0e15501aedf8e961f755a96de9.png)

字符串比较

![img](https://img-blog.csdnimg.cn/img_convert/6a2d770c29cf352323b4a445012739b2.png)

```python
#!/bin/bash
# author:xiaolan
num1="xiaolan"
num2="xiaolna"
if test $num1 = $num2
then
    echo '两个字符串相等!'
else
    echo '两个字符串不相等!'
fi
```

结果

![img](https://img-blog.csdnimg.cn/img_convert/1b9aa7602f8c14550e669c8f5eafadbf.png)

**流程**

if语句语法格式

```python
if condition
then
    exec1 
    exec2
    ...
    execN 
fi
```

如果简化为一行

```
if [$(ps -ef | grep -c "httpd") -gt 1];then echo "true";fi

```

if else-if else

```python
if condition1
then
    exec1
elif condition2 
then 
    exec2
else
    execn
fi

```

案例 判断两数值是否相等

```python
#!/bin/bash
# author:xiaolan
a=2
b=3
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi

```

for循环

```python
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done

```

while语句

> “ 通常用于从输入文件不断读取数据 

```python
while condition
do
    exec
done

#!/bin/bash
# author:xiaolan
int=1
while(( $int<=6 ))
do
    echo $int
    let "int++"# 用于执行一个或者多个
done

```

无限循环

```shell
while true
do
    exec
done

```

case语句

> “ 多选择语句。取值后面为单词in，每一个模式以")"结束。匹配发现取值符合某一模式后，其间所有命令开始执行直至 ";;"。 

```python
#!/bin/bash
# author:xiaolan
echo '输入 1 到 3 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    *)  echo '你没有输入 1 到 3 之间的数字'
    ;;
esac


```

输入不同的内容，会有不同的结果，例如：

```
输入 1 到 4 之间的数字:
你输入的数字为:
3
你选择了 3

```

跳出循环

break

> “ break命令允许跳出所有循环 

```python
#!/bin/bash
# author:xiaolan
while :
do
    echo -n "输入 1 到 3 之间的数字:"
    read aNum
    case $aNum in
        1|2|3) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 3 之间的! 游戏结束"
            break
        ;;
    esac
done


```

continue

> “ 跳出当次循环

```python
#!/bin/bash
while :
do
    echo -n "输入 1 到 3 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 3 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done


```

**10 shell函数**

> “ 用户定义函数，然后在shell脚本中随便调用，格式如下

```python
[ function ] funname [()]

{

    action;

    [return int;]

}

```

例子

```python
#!/bin/bash
# author:xiaolan

Fun1(){
    echo "这是我的第一个 shell 函数!"
}
echo "-----函数开始执行-----"
Fun1
echo "-----函数执行完毕-----"


```

带return语句

```python
#!/bin/bash
# author:xiaolan

FunReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
FunReturn
echo "输入的两个数字之和为 $? !"


```

函数参数

```python
#!/bin/bash
# author:xiaolan

funParam(){
    echo "第一个参数为 $1 !"
    echo "第二个参数为 $2 !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funParam 1 2 3 4

```

**shell重定向**

输出重定向

> “ command1 > file # 如果file中存在内容将被清空覆盖。如果追加使用command1 >>file

```shell
ls -l > dir.txt

```

cat dir.txt

![img](https://img-blog.csdnimg.cn/img_convert/9457812978ea3efd903278ad73a1344a.png)

/dev/null文件

> “ 写入到它的内容都会被丢弃，会起到"禁止输出"的效果，如果希望屏蔽stdout和stderr  “ command > /dev/null 2>&1

注意：Linux命令行都会打开三个文件

- 标准输入文件:stdin文件描述符为0
- 标准输出文件:stdout文件描述符为1
- 标准错误文件:stderr文件描述符2

**12 运算符**

下表列出了常用的算术运算符，假定变量 a 为 2，变量 b 为 3：

算术运算符

![img](https://img-blog.csdnimg.cn/img_convert/cd8539f4eab65e4ffbe0fe081fb20cbe.png)

关系运算符

![img](https://img-blog.csdnimg.cn/img_convert/fa782127a1263b2f9395bbc63de6b56a.png)

布尔运算符

![img](https://img-blog.csdnimg.cn/img_convert/6de9b1f6fcdbe274cdfdf7572bf570d3.png)

逻辑运算符

![img](https://img-blog.csdnimg.cn/img_convert/6757d589cfbe7e0fd14e421bf57059b4.png)

字符串运算符

![img](https://img-blog.csdnimg.cn/img_convert/c92c0937b99611a5a48d631eb5ae1c34.png)

**12 shell实战**

- 请将当前目录中demo.txt第二行第三列数据输出到demo2.txt中

```shell
 cat demo.txt|awk ’NR==2{print $3}’ >demo2.txt 
```

- 日志如下统计访问ip最多的前10个

```shell
awk ’{print $1}’ *.log | sort | uniq -c | sort -nr | head -n 
```

uniq - 删除排序文件中的重复行 sort对于文本进行排序 -l 按照当前环境排序. -m 合并已经排序好的文件,不排序. -n 按照字符串的数值顺序比较,暗含-b -r 颠倒比较的结果.

- 如何检查文件系统中是否存在某个文件

```shell
if [-f /var/log/messages]
then
echo "File exts"
fi
```

- 每个脚本开始的 #!/bin/sh 或 #!/bin/bash 表示什么意思 ?

> “ #!/bin/bash 表示脚本使用 /bin/bash。对于 python 脚本，就是 #!/usr/bin/python 

- &和&&区别

> “ “&” 脚本在后台运行时使用它。“&&”当前一个脚本成功完成才执行后面的命令 

- 脚本文件中，如何将其重定向标准输出和标准错误流到 log.txt 文件 ?

```shell
./a.sh >log.txt 2>&1
```

- 如何计算本地用户的数目

```shell
wc -l /etc/passwd | cut -d
```

- shell中进行字符串比较和数字比较

```
[ $A == $B ] – 用于字符串比较
[ $A -eq $B ] – 用于数字比较
```

- 去掉字符串空格

> “ echo $string | tr -d " " 

- 统计内存使用

```shell
#! /bin/bash
# author:xiaolan
sum=0
for mem in `ps aux |awk '{print $6}' |grep -v 'RSS' `
do
    sum=$[$sum+$mem]
done
echo "The total memory is $sum""k"                    
```

结果

![img](https://img-blog.csdnimg.cn/img_convert/856b5e703e00b5f366ec9f291072127c.png)

- 批量更改文件名

> “ 批量修改123目录下txt为txt.temp。将temp打包为test.tar.gz 

```python
#!/bin/bash
##查找txt文件
find /123 -type f -name "*.txt" > /tmp/txt.list
##批量修改文件名
for f in `cat /tmp/txt.list`
do
    mv $f $f.temp
done
##创建一个目录，为了避免目录已经存在，所以要加一个复杂的后缀名
d=`date +%y%m%d%H%M%S`
mkdir /tmp/123_$d
##把.temp文件拷贝到/tmp/123_$d
for f in `cat /tmp/txt.list`
do
    cp $f.temp /tmp/123_$d
done
##打包压缩
cd /tmp/
tar czf 123.tar.gz 123_$d/

```

## 8 awk文本处理工具

> awk是一个处理文本文件的应用程序，几乎所有的Linux系统都自带了这个程序

依次处理每一行，并读取里面的每一个字段。对于处理生产环境的日志有着非常高校的作用

**基本用法**

```shell
# 格式
awk 做什么 文件吗
awk 'print $0' lan.txt
```

上面lan.txt是awk需要处理的文本文件。前面单引号里面有一个大括号，单引号里面就是每一行的处理动作。其中print为打印命令，$0位当前行，所以执行结果就是把每一行原样打印出来

**上菜**

```shell
echo 'my name is lanlan' | awk '{print $0}'
```

上面代码中，print $0即将标准输入my name is lanlan ,c重新打印一遍

awk根据空格和制表符，将每一行分成若干段，依次为$1 $2 $3代表第一个字段，第二个字段，第三个字段

```shell
echo 'my name is lanlan'| awk '{print $3}'
```

为了方便，我们直接使用/etc/passwd文件进行操作，

```SHELL
awk -F ':' '{ print $1 }' demo.txt
```

**3 变量**

上面我们说了，可以使用符号 “$+” 数字的方式表示第几个字段，其实还有一些变量可以直接表示相应的字段。比如 “$NFb” 表示最后一个字段

```shell
echo 'my name is lanlan'| awk '{print $NF}'
awk -F ':' '{print NR ") " $1}' demo.txtshe
```

这里出现了双引号，表示原样输出

其他常用的内置变量

- FILENAME：当前文件名
- FS：字段分隔符，默认是空格和制表符。
- RS：行分隔符，用于分割每一行，默认是换行符。
- OFS：输出字段的分隔符，用于打印时分隔字段，默认为空格。
- ORS：输出记录的分隔符，用于打印时分隔记录，默认为换行符。
- OFMT：数字输出的格式，默认为％.6g。

**4 函数**

既然算是一门语言，函数当然少不了，下面看一波常用的函数

函数toupper()用于将字符转为大写

```shell
awk -F ':' '{ print toupper($1) }' demo.txt
```

可以发现第一个字段输出的时候变成了大写

- tolower()：字符转为小写。
- length()：返回字符串长度。
- substr()：返回子字符串。
- sin()：正弦。
- cos()：余弦。
- sqrt()：平方根。
- rand()：随机数。

**5 条件**

通过使用相应的条件，过滤出自己想要的内容

```shell
awk '条件 动作' 文件名
```

上菜

```shell
$ awk -F ':' '/usr/ {print $1}' demo.txt
root
daemon
bin
sys
```

这里/usr/表示只输出包含usr的行

这个例子输出奇数行

```shell
# 输出奇数行
$ awk -F ':' 'NR % 2 == 1 {print $1}' demo.txt
root
bin
sync
# 输出第三行以后的行
$ awk -F ':' 'NR >3 {print $1}' demo.txt
sys
sync
```

下面的例子输出第一个字段等于指定值的行。

```shell
$ awk -F ':' '$1 == "root" {print $1}' demo.txt
root
$ awk -F ':' '$1 == "root" || $1 == "bin" {print $1}' demo.txt
root
bin
```

**5 if语句**

通过if语句编写比较复杂的内容

```shell
$ awk -F ':' '{if ($1 > "m") print $1}' demo.txt
root
sys
sync
```

上面代码输出第一个字段的第一个字符大于`m`的行。

if结构还可以指定else部分。

## 9 进程管理与定时任务和后台执行

> crond是什么？

crond是一个可以在指定时间执行一个shell脚本或者一系列的Linux命令。和Windows下的计划任务类似。当安装完操作系统后，默认会安装这个服务工具，并且会自动启动crond进程。

在Linux中任务的调度分为**两类**

- 系统任务的调度

> 系统会周期性的执行一些工作，比如说写缓存的数据到硬盘，清理日志等

- 用户任务的调度

> 用户定期也会执行一些任务，比如用户数据的备份，定时的邮件提醒等，这些都是通过crondtab来设置

**那么crontab到底怎么用么**

首先看看crontab的使用格式：

```shell
crontab -u user file
```

**常见的选项**

- -u user:很明显是需要表明是那个用户的crontab服务，别瞎搞
- file:file是命名文件的名字，表示将file作为crontab的任务列表文件并载入到crontab中
- -e:e为edit，表示标记某个用户的crontab文件内容
- -l:显示用户的crontab文件、

crontab的含义

创建的crontab文件，每一行代表一项任务，每个字段都有对应的设置规则，一共分为6个字段，分别为：

```shell
minute hour day month week command
```

- minute:区间 0-59
- hour:区间0-23
- day:区间0-31
- month:区间1-12
- week:区间0-7 周日可以是0/7
- command

这里的command代表的是需要执行的而命令，通常为脚本文件，

除了上面几个字段，还需要注意几个特殊字段

- *:代表所有可能的值
- ，:通过，来表示区间范围的值
- _:整数之间的中杠表示一个证书范围
- 正斜线：表示时间的间隔频率，比如0-23/2表示每两个小时执行一次

**开始放几个例子**

```shell
crontab -e
0 5 * * * /root/bin/backup.sh
```

这代表的是每天早上5点运行backup.sh

> 每个工作日11:59pm进行备份作业

```shell
59 11 * * 1-5 /root/bin/backup.sh
```

> 每五分钟运行一个命令

```shell
*/5 * * * * /root/bin/check-status.sh
```

> crontab有哪些选项

crontab -e:修 改crontab文件，如果文件不存在会自动创建

crontab -l：显示crontab文件

crontab -r：删除crontab 文件

crontab -ir:删除crontab文件前提醒用户

##  10后台运行

**用途**：不挂断的运行命令

**语法**：nohup Command [ Arg … ] [&]

- 无论是否将 nohup 命令的输出**重定向**到终端，输出都将附加到当前目录的 nohup.out 文件中。

- 如果当前目录的 "nohup.out" 文件不可写，输出重定向到“\$HOME/nohup.out ”文件中。

- 如果没有文件能创建或打开以用于追加，那么 Command 参数指定的命令不可调用。

**退出状态**：该命令返回下列出口值： 　

- 126 可以查找但不能调用 Command 参数指定的命令。 　

- 127 nohup 命令发生错误或不能查找由 Command 参数指定的命令。 　

- 否则，nohup 命令的退出状态是 Command 参数指定命令的退出状态。

**使用 &**

用途：在后台运行

一般两个一起用

```shell
nohup command &
```

> 才疏学浅，难免有纰漏，如果你发现错误的地方，麻烦告诉我，我对其修正。


唠嗑

为了方便大家沟通交流，资源共享。小蓝准备创建一个面试交流群，让正在面试或即将面试的小伙伴能够一起沟通交流，当然群里也会不定期的发发小红包，群里不会存在任何的广告。欢迎有兴趣的小伙伴加入。加群方式扫描下方二维码，备注加群即可


<div style="align: center">
<img src="https://img-blog.csdnimg.cn/20200926153826650.png#pic_center"/>

**我是小蓝，一个专为大家分享面试经验的蓝人。如果觉得文章不错或者对你有点帮助，感谢分享给你的朋友，也可在给小蓝给个star，这对小蓝非常重要，谢谢你们，下期再会。**