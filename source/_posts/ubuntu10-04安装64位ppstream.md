---
title: ubuntu10.04安装64位ppstream
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '34'
abbrlink: 421653662
date: 2012-11-08 11:19:00
---

  
参考：  
http://hi.baidu.com/flashgive/item/6904fb09798fc1e5fe240d33  
  
下载：  
http://ppa.launchpad.net/cnav/ppa/ubuntu/pool/main/p/ppstream/ppstream\_1.0.0-3lucid2\_amd64.deb  
http://packages.ubuntu.com/zh-tw/lucid-updates/libphonon4    下载32位版本的libphonon  
  
安装  

> 安装ppstream没有出现什么错误  

  
运行  

> 运行时提示缺少libphonon.so.4文件  
> 1.1我找了下系统的库文件，发现/usr/lib/下面有libphonon.so.4  
> 1.2做了链接 sudo ln -s /usr/lib/libphonon.so.4 /opt/pps/lib/libphonon.so.4  
> 1.3需要32位版本的。  
> 2.1下载了32位版本的libphonon  
> 2.2解压后把libphonon.so.4.4.0复制为/opt/pps/lib/libphonon.so.4  
> 2.3正常了  

  

![ubuntu10.04安装64位ppstream - leaf - ------坚持雅操------](http://img9.ph.126.net/JfPH-3hX2qmGlGVh5kmQag==/6597818534074982489.jpg "ubuntu10.04安装64位ppstream - leaf - ------坚持雅操------")