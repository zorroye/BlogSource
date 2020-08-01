---
title: '[摘录] ubuntu server 10.04 安装dhcp服务器'
tags:
  - 未分类
id: '151'
abbrlink: 1791050251
date: 2010-10-13 10:56:00
---

<转载自：http://xy.zhubajie.com/html/2009/03-30/207077.html>  
  
DHCP服务器提供以下两种配置方法：

　　地址池

　　这种方法指定了一个用来动态的提供给第一个访问网络的DHCP客户端的IP地址池（有时也称作区域或范围）。当DHCP客户端离开网络超过一定时间后，IP地址就会被回收到地址池以供其它DHCP客户端使用。

　　MAC地址

　　这种方法强制使用DHCP来区别每一块连接上网络的网卡的硬件地址，之后这块网卡每次连上网络请求DHCP服务时都为它提供这个固定的IP地址。

![[摘录] ubuntu server 10.04 安装dhcp服务器 - leaf - ------坚持雅操------](http://img.ph.126.net/oHeiM9j9UsG7QWm69cUsrQ==/3269331854495906752.png "[摘录] ubuntu server 10.04 安装dhcp服务器 - leaf - ------坚持雅操------")

 

　　在ubuntu中安装DHCP服务

　　sudo apt-get install dhcp3-server

　　这样就完成安装了。

　　配置DHCP服务器

　　如果你的Ubuntu服务器上用友2块网卡，你需要选择哪一块网卡用来监听DHCP服务。默认监听的是eth0。可以通过编辑/etc/default/dhcp3-server这个文件来改变这个默认值。

　　sudo vi /etc/default/dhcp3-server

　　找到这行，

　　INTERFACES=”eth0″

　　使用下面这行替代它

　　INTERFACES=”eth1″

　　保存并退出。这一步可选。

　　接下来你需要为/etc/dhcp3/dhcpd.conf文件创建一个备份。

　　cp /etc/dhcp3/dhcpd.conf /etc/dhcp3/dhcpd.conf.back

　　使用下面的命令编辑/etc/dhcp3/dhcpd.conf文件

　　sudo vi /etc/dhcp3/dhcpd.conf

　　使用地址池的方法

　　你需要修改/etc/dhcp3/dhcpd.conf这个配置文件的以下部分：

`default-lease-time 600;  
max-lease-time 7200;  
option subnet-mask 255.255.255.0;  
option broadcast-address 192.168.1.255;  
option routers 192.168.1.254;  
option domain-name-servers 192.168.1.1, 192.168.1.2;  
option domain-name “yourdomainname.com”;  
subnet 192.168.1.0 netmask 255.255.255.0 {  
range 192.168.1.10 192.168.1.200;  
}`

　　保存并退出文件

　　这会导致DHCP服务器提供一个从192.168.1.10-192.168.1.200这个范围的IP地址给客户端。如果客户端没有请求一个租期的话，服务器会默认提供600秒的地址租期给客户端。最大的（允许的）地址租期是7200秒。

　　使用MAC地址的方法

　　使用这种方法你可以保留一个固定地址给一些或者所有机器。在下面的示例中我给server1,server2,printer1和priner2保留了固定的IP地址。

`default-lease-time 600;  
max-lease-time 7200;  
option subnet-mask 255.255.255.0;  
option broadcast-address 192.168.1.255;  
option routers 192.168.1.254;  
option domain-name-servers 192.168.1.1, 192.168.1.2;  
option domain-name “yourdomainname.com”;  
subnet 192.168.1.0 netmask 255.255.255.0 {  
range 192.168.1.10 192.168.1.200;  
}  
host server1 {  
hardware ethernet 00:1b:63:ef:db:54;  
fixed-address 192.168.1.20;  
}  
host server2 {  
hardware ethernet 00:0a:95:b4:d4:b0;  
fixed-address 192.168.1.21;  
}  
host printer1 {  
hardware ethernet 00:16:cb:aa:2a:cd;  
fixed-address 192.168.1.22;  
}  
host printer2 {  
hardware ethernet 00:0a:95:f5:8f:b3;  
fixed-address 192.168.1.23;  
}`

　　现在你需要使用下面命令来重启dhcp服务器。

　　sudo /etc/init.d/dhcp3-server restart

　　配置Ubuntu的DHCP客户端

　　如果你想配置你的Ubuntu桌面为DHCP客户端，使用以下步骤。你需要打开/etc/network/interface文件

　　sudo vi /etc/network/interfaces

　　确保你的配置文件含有以下行（eth0只是一个示例）

`auto lo eth0  
iface eth0 inet dhcp  
iface lo inet loopback`

　　保存并退出文件

　　你需要使用下面的命令重启网络服务

　　sudo /etc/init.d/networking restart

　　如何找到DHCP服务器的IP地址

　　你需要使用下面的命令

　　sudo dhclient

　　或者

　　tail -n 15 /var/lib/dhcp3/dhclient.\*.leases

未知