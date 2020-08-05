---
title: buffalo 安装xware
tags:
  - buffalo
categories:
  - Hardware
  - buffalo
id: '172'
abbrlink: 796663220
date: 2015-01-21 21:19:00
---

首先必须已root

  

安装过程

1、查buffalo cpu架构\_指令集\_c库类型

> 我的是 arm\_v5tel(v5l)\_glibc

> ![buffalo 安装xware - leaf - ------坚持雅操------](http://img2.ph.126.net/uKY8dKq7LBVr4tyOOAbEjw==/6630390466535784962.png "buffalo 安装xware - leaf - ------坚持雅操------")

2、去迅雷下载相应的软件  

> 我的是Xware1.0.31\_armel\_v5te\_glibc.zip 

> http://luyou.xunlei.com/thread-12545-1-1.html?\_t=1421842121

3、安装

> 我放在/opt下面
> 
> 先解压，
> 
> 然后运行目录下的portal文件，
> 
> 把运行后得到的激活码输入到迅雷远程下载里面
> 
> 设置一下下载目录即可

4、随系统自启动

> 我这款是linux系统，所以在/etc/init.d里面建一下链接即可

> > echo '/opt/xware/portal' >/etc/init.d/xunleiyuancheng.sh
> 
> > chmod 755 /etc/init.d/xunleiyuancheng.sh
> 
> > ln -s /etc/init.d/xunleiyuancheng.sh /etc/rc.d/sysinit.d/S99xunleiyuancheng.sh
> 
> > chmod 777 /etc/rc.d/sysinit.d/S99xunleiyuancheng.sh
> 
>   

![buffalo 安装xware - leaf - ------坚持雅操------](http://img2.ph.126.net/YH452L67KxUXZYl8aqrV0w==/3363907446770522960.png "buffalo 安装xware - leaf - ------坚持雅操------")