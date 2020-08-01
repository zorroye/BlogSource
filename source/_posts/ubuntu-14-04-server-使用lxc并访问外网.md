---
title: Ubuntu 14.04 Server 使用lxc并访问外网
tags:
  - 未分类
id: '294'
date: 2015-04-29 14:13:00
---

1、安装

> sudo apt-get install lxc

>   

2、配置网络

> 设置宿主网络：创建桥接接口 sudo nano /etc/network/interfaces

> auto eth0
> 
> iface eth0 inet manual
> 
>   
> 
> \# The primary network interface
> 
> auto br0
> 
> iface br0 inet static
> 
> address 192.168.1.20
> 
> netmask 255.255.255.0
> 
> gateway 192.168.1.1
> 
> dns-nameservers 192.168.1.1
> 
> bridge\_portseth0
> 
> bridge\_stpoff
> 
> bridge\_maxwait0
> 
> bridge\_fd0
> 
>   
> 
> 说明：特权容器和普通容器选一个设置即可 不用全部设置。
> 
>   
> 
> 设置特权容器网络：sudo nano /etc/lxc/default.conf 接口由lxcbr0改为br0
> 
> lxc.network.type = veth
> 
> #lxc.network.link = lxcbr0
> 
> lxc.network.link = br0
> 
> lxc.network.flags = up
> 
> lxc.network.hwaddr = 00:16:3e:xx:xx:xx
> 
>   
> 
>   
> 
> 设置普通容器网络：sudo nano /etc/lxc/lxc-usernet
> 
> \# USERNAME TYPE BRIDGE COUNT
> 
> ywz veth br0 2  #2表示有2个网络接口，也就是能开2个容器

  

>  nano ~/.config/lxc/default.conf (用于普通容器连外网)
> 
> lxc.id\_map = u 0 100000 65536
> 
> lxc.id\_map = g 0 100000 65536
> 
> lxc.network.type = veth
> 
> lxc.network.link = br0
> 
>   

> /etc/default/lxc-net 可以设置LXC是否提供net网络。USE\_LXC\_BRIDGE 

  

3、创建容器和使用

> lxc-create --template download --name Y011

> 特权容器存放位置  /var/lib/lxc

> 普通容器存放位置~/.local/share/lxc
> 
>   
> 
> 设置固定IP：
> 
>  在容器存放地址的/rootfs/etc/network/interfaces和/rootfs/etc/resolv.conf设置
> 
>   

4、设置容器自启动

> ~/.local/share/lxc/Y011/config 添加
> 
> lxc.start.auto = 1
> 
> lxc.start.delay = 5
> 
> lxc.start.order = 100
> 
> lxc.group = ubuntu
> 
>   

5、限制内存容量

> ~/.local/share/lxc/Y011/config 添加
> 
> lxc.cgroup.memory.limit\_in\_bytes = 134217728
> 
>   

6、克隆和快照

> lxc-clone -o Y011 -n Y012
> 
> lxc-snapshot -n Y011
> 
>