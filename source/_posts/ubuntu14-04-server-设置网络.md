---
title: Ubuntu14.04 Server 设置网络
tags:
  - 未分类
id: '279'
date: 2015-04-28 17:02:00
---

静态地址设置

> cat /etc/network/interfaces
> 
> \# This file describes the network interfaces available on your system
> 
> \# and how to activate them. For more information, see interfaces(5).
> 
>   
> 
> \# The loopback network interface
> 
> auto lo
> 
> iface lo inet loopback
> 
>   
> 
> \# The primary network interface
> 
> auto eth0
> 
> iface eth0 inet static
> 
> address 192.168.1.20
> 
> netmask 255.255.255.0
> 
> gateway 192.168.1.1
> 
> dns-nameservers 192.168.1.1  #dns在这边改了，不是在/etc/resolv.conf改

  

改网络接口名称（原先接口名称为p2p1）

1、查mac地址

2、新建文件

> nano /etc/udev/rules.d/70-persistent-net.rules

>   
> 
> SUBSYSTEM=="net", ACTION=="add",  ATTR{address}=="00:e0:4c:60:d1:59",  NAME="eth0"

3、更改上面的文件

> /etc/network/interfaces