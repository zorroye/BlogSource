---
title: 'root nas :  buffalo LS-WVL'
tags:
  - 未分类
id: '169'
abbrlink: 3073781033
date: 2014-02-04 20:19:00
---

![root nas :  buffalo LS-WVL - leaf - ------坚持雅操------](http://img0.ph.126.net/BWHcgE8BPLbb463K2lF4NA==/4791267053669049027.png "root nas :  buffalo LS-WVL - leaf - ------坚持雅操------")

2011年就买了，半年后跌价到600多块钱了，伤心。。。

我买了2个500G希捷硬盘做RAID1模式。当时硬盘才270光景，后来硬盘涨了100多 赚了！

  

今天有幸看了篇文章，决定试试root  
参考资料：

http://i.592.net/?post=360

#这篇介绍非常详细了

http://buffalo.nas-central.org/wiki/Category:LS-WXL#LinkStation\_Duo\_.28LS-WXL.29

#这篇是指导教材

http://downloads.buffalo.nas-central.org/TOOLS/ALL\_LS\_KB\_ARM9/ACP\_COMMANDER/

#这里下载软件：acp\_commander.jar

  

  

过程：

打开终端，依次输入代码即可

备注：

> 我的IP地址是192.168.3.6

> 我的网页登陆密码是：mima
> 
> 我将root密码改为：123456
> 
>   

java -jar acp\_commander.jar -t 192.168.3.6 -ip 192.168.3.6 -pw mima -c "ls /"

#使用ls 命令列出目录，以证明使用mima可以登陆

  

java -jar acp\_commander.jar -t 192.168.3.6 -ip 192.168.3.6 -pw mima -c "(echo 123456;echo 123456)|passwd"

#将root密码改为123456

  

java -jar acp\_commander.jar -t 192.168.3.6 -ip 192.168.3.6 -pw mima -c "sed -i 's/UsePAM yes/UsePAM no/g' /etc/sshd\_config"

#关掉PAM，用sed -i 's///g' 将yes改为no

  

java -jar acp\_commander.jar -t 192.168.3.6 -ip 192.168.3.6 -pw mima -c "sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' /etc/sshd\_config"

#允许root使用ssh登陆

  

java -jar acp\_commander.jar -t 192.168.3.6 -ip 192.168.3.6 -pw mima -c "/etc/init.d/sshd.sh restart"

#重启sshd服务

  

\----------------------------------------

我的配置如下：

Processor: Feroceon 88FR131 rev 1 (v5l)

BogoMIPS: 598.01

MemTotal:         117496 kB

\----------------------------------------

  

安装ipkg包管理器

cd /tmp

wget http://ipkg.nslu2-linux.org/feeds/optware/cs05q3armel/cross/stable/teraprov2-bootstrap\_1.2-7\_arm.xsh

sh ./teraprov2-bootstrap\_1.2-7\_arm.xsh

  

vi /opt/etc/ipkg.conf 

添加

src cs08q1 http://ipkg.nslu2-linux.org/feeds/optware/cs08q1armel/cross/stable/

\# src cs08q1-unstable http://ipkg.nslu2-linux.org/feeds/optware/cs08q1armel/cross/unstable/

保存 :wq

更新： ipkg update

  

  

安装NFS

ipkg install e2fslibs

ipkg install portmap

cd /mnt/array1

wget http://downloads.buffalo.nas-central.org/Users/kenatonline/NFSKernel/nfstools.tar.gz

cd /

tar xvzf /mnt/array1/nfstools.tar.gz

配置好/etc/exports

然后

cd /opt/etc/init.d

./S55portmap start

./S99nfs start