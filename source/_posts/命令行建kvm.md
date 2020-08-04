---
title: 命令行建kvm
tags:
  - kvm
categories:
  - Virtualization
  - Kvm
id: '301'
abbrlink: 312231816
date: 2016-04-14 22:39:00
---

  
一、建kvm  

> 1、新建磁盘  
> 
> > qemu-img create -f qcow2 centos.img -opreallocation=metadata 30G  
> >   
> 
> 2、建kvm虚拟机  
> 
> > virt-install --name=centos7 --ram=2048 --vcpus=2 --os-type=linux --hvm \\  
> > \--cdrom=/home/ywz/iso/ubuntu-12.04.5-server-amd64.iso \\  
> > \--file=/home/ywz/img/centos7.img,format=qcow2,bus=virtio \\  
> > \--network bridge=virbr0  \\  
> > \--vnc --vncport=5992 --vnclisten=0.0.0.0 --force --autostart  
> >   
> 
> 3、挂在裸设备(lvm)装虚拟机  
> 
> > virt-install --name=centos7-lvm --ram=2048 --vcpus=2 --os-type=linux  --hvm\\  
> > \--cdrom=/home/ywz/iso/centos7-custom.iso \\  
> > \--file=/dev/kvmvg/kvmlv \\  
> > \--network bridge=br0  \\  
> > \--vnc --vncport=5992 --vnclisten=0.0.0.0 --force --autostart  

>   

二、备份kvm虚拟机配置  

> virsh dumpxml centos7-lvm >> centos7-lvm.xml  

  
三、xml文件设置  

> CPU方面  
> 1、最大可用cpu  
> 
> > <vcpu placement='static' current='2'>4</vcpu>  
> 
> 2、绑定CPU  
> 
> >   <cputune>  
> >     <vcpupin vcpu='0' cpuset='15'/>  
> >     <vcpupin vcpu='1' cpuset='31'/>  
> >   </cputune>  
> >   
> 
> >   
> 
> >   
> >   
> >   
> >   
> >