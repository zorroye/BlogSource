---
title: '[转载]快速理解Docker - 容器级虚拟化解决方案'
tags:
  - 未分类
id: '293'
abbrlink: 1535462288
date: 2014-09-15 16:06:00
---

http://blog.csdn.net/colorant/article/details/20608157  

其他:

docker用户指南  

http://www.widuu.com/chinese\_docker/userguide/README.html  

  

是什么

简单的说Docker是一个构建在LXC之上的,基于进程容器(Processcontainer)的轻量级VM解决方案

拿现实世界中货物的运输作类比,为了解决各种型号规格尺寸的货物在各种运输工具上进行运输的问题,我们发明了集装箱

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img2.ph.126.net/z8sb7loU42BTjg2aaQpjPQ==/6608641027027329422.png "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

Docker的初衷也就是将各种应用程序和他们所依赖的运行环境打包成标准的container/image,进而发布到不同的平台上运行

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img2.ph.126.net/eTbtT_pQbARMS5PlNNaYUA==/6608415627144727628.png "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

从理论上说这一概念并不新鲜,各种虚拟机Image也起着类似的作用

Docker container和普通的虚拟机Image相比,最大的区别是它并不包含操作系统内核.

   

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img1.ph.126.net/CXoaOka-9j2ea9B9I_K0RA==/6608886218120322808.png "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

普通虚拟机将整个操作系统运行在虚拟的硬件平台上,进而提供完整的运行环境供应用程序运行,而Docker则直接在宿主平台上加载运行应用程序.本质上他在底层使用LXC启动一个Linux Container,通过cgroup等机制对不同的container内运行的应用程序进行隔离,权限管理和quota分配等

每个container拥有自己独立的各种命名空间(亦即资源)包括:

 PID进程, MNT文件系统, NET网络, IPC, UTS主机名等

 **与****LXC****有什么不同**

基本上你可以认为目前的Docker是LXC的一个高级封装,提供了各种辅助工具和标准接口方便你使用LXC,你可以依靠LXC和各种脚本实现与docker类似的功能，就像你不使用APT/yum等工具也可以自己搞定软件包安装一样，你使用他们的关键原因是方便易用！

实际使用中，你一般不用关心底层LXC的细节,同时也不排将来docker实现基于非LXC方案的可能性

在LXC的基础上, Docker额外提供的Feature包括：标准统一的打包部署运行方案，历史版本控制， Image的重用，Image共享发布等等

**Container****构建方案**

除了LXC，Docker的核心思想就体现在它的运行容器构建方案上

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img0.ph.126.net/eXtQagb1L5uBGARuybnwwQ==/6619114974793163385.png "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

为了最大化重用Image，加快运行速度，减少内存和磁盘footprint, Docker container运行时所构造的运行环境，实际上是由具有依赖关系的多个Layer组成的。例如一个apache的运行环境可能是在基础的rootfs image的基础上，叠加了包含例如Emacs等各种工具的image，再叠加包含apache及其相关依赖library的image，这些image由AUFS文件系统加载合并到统一路径中，以只读的方式存在，最后再叠加加载一层可写的空白的Layer用作记录对当前运行环境所作的修改。

有了层级化的Image做基础，理想中，不同的APP就可以既可能的共用底层文件系统，相关依赖工具等，同一个APP的不同实例也可以实现共用绝大多数数据，进而以copy on write的形式维护自己的那一份修改过的数据等

历史和生态环境

Docker项目从启动到现在不过一年多时间，发展势头还是很迅猛的

2013.01做为dotcloud内部项目开始启动

2013.03.27正式作为public项目发布

2014.1被BLACK DUCK评选为2013年10大开源新项目“TOP 10 OPEN SOURCE ROOKIE OF THE YEAR”

目前的状态 ( 2014.3 )

Docker 0.8.1

10000+ github stars(top 50)

350+ contributors

1500+ fork

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img1.ph.126.net/5jnIDzPs61Bgt2koJe_xTQ==/6619476714118700914.jpeg "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

具体应用方面，可以看到百度至少在2013年10月份就已经成功使用Docker支持其BAE平台的Paas服务

安装运行和使用

Docker虽然是号称build once， runeverywhere。但是实际上还是受其引擎依赖关系的限制的，目前的版本具体来说对系统要求：

*   Linux Kernel 3.8+
*   LXCsupport
*   64bitOS
*   AUFS

以上要求，以ubuntu为例，需要12.04配合 3.8kernel升级，或者 ubuntu 13.04+

在ubuntu12.04上，基本安装步骤如下

sudoapt-get update sudo apt-get install linux-image-generic-lts-raringlinux-headers-generic-lts-raring

sudoapt-key adv --keyserver keyserver.ubuntu.com --recv-keys36A1D7869245C8950F966E92D8576A8BA88D21E9

sudosh -c "echo deb [http://get.docker.io/ubuntu](http://get.docker.io/ubuntu)docker main\\ > /etc/apt/sources.list.d/docker.list"

sudoapt-get update

sudoapt-get install lxc-docker

如果你在安装之前想要先体验一下docker的基本操作命令等的话，可以尝试一下这个在线的live教程[https://www.docker.io/gettingstarted/#h\_tutorial](https://www.docker.io/gettingstarted/#h_tutorial)

常用命令

分类列一下常用的CLI命令

*   仓库相关

search/ pull / push / login etc.

例：docker pull ubuntu从仓库下载ubuntuimage

*   Images操作相关

images/ rmi / build / export  / import / save /load etc.

例：docker images -t以树形结构列出当前本地Image

*   运行相关

run / start / stop / restart / attach /kill etc.

docker run -i -t ubuntu /bin/bash 启动ubuntu image，并交互式的运行shell

*   杂项

Docker diff  / commit

Dockerinfo / ps / inspect / port / logs / top / history etc.

具体docker命令的使用参见[http://docs.docker.io/en/latest/reference/commandline/](http://docs.docker.io/en/latest/reference/commandline/)

常见问题

*   使用Non root用户

目前版本的docker由于使用Socket进行通讯，因此需要root用户权限 sudo xxx，或者将需要使用Dockerclient的用户加入docker用户组

sudogpasswd -a ${USER} docker

*   网络相关问题

当你在网关背后需要通过代理连接docker的index数据库时，可以手动加上http\_proxy环境变量来启动dockerdaemon

HTTP\_PROXY=http://proxy\_server:port docker -d &

更好的做法是修改/etc/default/docker ( on ubuntu ),添加exporthttp\_proxy=proxy\_server:port

同样，docker container如果无法自动正确的从host环境中获得DNS的配置，则需要手动指定DNS服务器地址，这可以通过 docker -run --dns=xxx 来实现，也可以修改/etc/default/docker添加例如DOCKER\_OPTS="-dns 8.8.8.8"

*   特权模式

在正常情况下在container内部你没有权限操作device设备，而当前版本中，container内部部分文件例如/etc/hosts;/etc/hostname; /etc/resolve.conf等文件是动态通过mount动态以只读的形式加载上来的，理论上说你应该找到合适的方法去保证这些自动生成并加载的文件的正确性 (例如通过\--dns设置 resolve.conf )，但是如果由于特殊原因你需要手动修改，那么你可以通过特权模式启动 docker client ： docker run --privileged，然后你可以卸载这些文件，自己再创建新的版本

*   过多的层级依赖关系

以Layer的方式实现APP和相关library的cheap reuse和fast update是Docker的关键所在，不过受目前AUFS文件系统的限制，默认Layer的层级最多只能达到127（曾经只有42），在实际使用中有多种情况可能导致你的container的层级关系快速增长到这个极限值，撇开这么多layer叠加以后AUFS的效率不谈，更多情况下是你无法再更新构建你的image了

1.  使用Dockerfile构建Image时，每条指令都会给最终的Image增加一层layer依赖关系.
2.  以修改，提交，再修改再提交的方式不停的调整，更新你的Image
3.  从仓库中下载的别人的Image已经包含众多的层级依赖关系，而你需要进一步更新以创建你自己的版本

前两者在一定程度上还是你自己可能把控的，最后一种情况就没办法了。这个问题最终必将影响Docker的实际可用性，目前的解决方案包括：

*   使用Dockerfile时,尽可能合并多个操作：例如使用 "&&" 或 ";"合并运行多个shell命令；将多个shell命令写成脚本，在dockerfile中添加并运行这个脚本
*   通过Export再Import Image，丢弃所有历史信息和依赖关系，创建一个全新的image

将来可能的解决方案包括：

*   在Dockerfile中添加对多步操作的合并提交的支持
*   外部的image Flat工具的支持，目标是能够保留历史信息等
*   非AUFS的其它Storage解决方案

Future development

虽然Docker目前默认使用LXC和AUFS，但是Docker的核心思想本身，并不强制绑定这两者，0.8版本已经可以使用BTRFS，而整个Docker框架也改成了插件式的架构，便于添加替换各个功能模块

![[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------](http://img2.ph.126.net/EA-pQxpo2Gr5sAmgsNlEzg==/6619206234258267968.png "[转载]快速理解Docker - 容器级虚拟化解决方案 - leaf - ------坚持雅操------")

 

例如更多的Storage方案的支持，规避AUFS当前的问题，除了LXC以外更多的虚拟化方案等