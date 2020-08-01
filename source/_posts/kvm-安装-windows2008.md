---
title: kvm 安装 windows2008
tags:
  - 未分类
id: '299'
abbrlink: 3226075993
date: 2016-04-10 13:39:00
---

1、建镜像  

> qemu-img create -f qcow2 win2008.qcow2 -opreallocation=metadata 100G  
>   

2、建虚拟机  

> virt-install -n windows2008 -r 2048 --vcpus=2 --os-type=windows --accelerate -c /home/ywz/ISO/win2008.iso --disk path=/home/ywz/ISO/virtio-win.iso,device=cdrom --disk path=/home/ywz/ISO/windows2008.img,format=qcow2,bus=virtio --network bridge=virbr0 --vnc --vncport=5992 --vnclisten=0.0.0.0 --force --autostart  
> 备注：  
> 1、安装的时候直接装上virtio驱动。驱动我选的是viostor里面的驱动  
> virtio最新版本是0.1.113  
> 2、取消boot分区方法  
> 安装完virtio驱动后，显示出硬盘容量，这时候按shift+f10 出来命令行窗口  
> 输入 diskpart  
> list disk  
> select disk 0  
> create partition primary  
> active  
> exit  
> exit  
> 然后安装windows2008  

> http://www.mamicode.com/info-detail-126255.html  
>   

  
3、windows激活问题  

> 网上都是改BIOS之后激活的  

>