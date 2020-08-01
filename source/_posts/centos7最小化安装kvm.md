---
title: centos7最小化安装kvm
tags:
  - 未分类
id: '300'
abbrlink: 2474284125
date: 2016-04-10 19:40:00
---

  
1、升级到最新版  

> yum update -y  

2、安装必要软件  

> yum install pciutils net-tools  

3、安装kvm相关软件  

>  yum install libvirt\*  
> yum install ipxe-roms-qemu  
> yum install python-virtinst  
> yum install qemu-kvm  
> yum install virt-manager  
> yum install virt-viewer  
> yum install virt-top  
> yum install virt-what  
> yum install qemu-img  
> yum install virt-install  
> yum install libguest\*  

  
4、设置网络  

> nano /etc/sysctl.conf  
> 
> > net.ipv4.ip\_forward = 1  
> 
> cd /etc/sysconfig/network-scripts/  
> 
> > cp ifcfg-enp0s25 ifcfg-br0  
> > nano ifcfg-br0  
> > 
> > > TYPE="Bridge"  
> > > BOOTPROTO="static"  
> > > DEFROUTE="yes"  
> > > IPV4\_FAILURE\_FATAL="no"  
> > > NAME="br0"  
> > > UUID="1eb3d327-b535-44d1-8558-b369c6db3a80"  
> > > DEVICE="br0"  
> > > ONBOOT="yes"  
> > > IPADDR="192.168.3.128"  
> > > PREFIX="24"  
> > > GATEWAY="192.168.3.1"  
> > > DNS1="192.168.3.1"  
> > >   
> > 
> > nano ifcfg-enp0s25  
> > 
> > > NAME="enp0s25"  
> > > DEVICE="enp0s25"  
> > > ONBOOT="yes"  
> > > BRIDGE=br0  
> 
>   
> 关闭SELINUX  
> 
> > nano /etc/selinux/config  
> > SELINUX=disabled  
> 
> > >   

5、用virt-manager远程管理kvm虚拟机  

> ![centos7最小化安装kvm - leaf - ------勤解万难------](http://img2.ph.126.net/N4N0xNRH578sApZUEmfWKg==/6598296821694261878.png "centos7最小化安装kvm - leaf - ------勤解万难------")
> 
>