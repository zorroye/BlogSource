---
title: 基础补充7：FC4安装Geforce MX 420驱动
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '90'
abbrlink: 1267475429
date: 2014-12-02 14:59:00
---

0、安装编译环境。  

> 主要是安装kernel-src ，kernel-devel ，gcc , glibc , ncurse 等。  
>   

1、下载nvidia驱动  

> http://www.nvidia.cn/object/unix-cn.html  
> 我下载的是NVIDIA-Linux-x86-96.43.23-pkg1.run。已经加了x权限了。  
>   

2、进 init 3环境  

> nano /etc/inittab     
> 
> 　　id:5:initdefault:   把5改为3  
> 
>   

3、安装nvidia驱动  

> sh NVIDIA-Linux-x86-96.43.23-pkg1.run  
> 然后点配置xorg.conf文件。 或者运行 nvidia-xconfig 也可以  
>   

4、进init 5 环境  

> 改 /etc/inittab  
> 
> > id:3:initdefault:   把3改为5
> 
>   

5、遇到的问题（问题才开始）  

> （EE） failed to initialize GLX Extension  
> 1、看/var/log/Xorg.0.log ，模块的存放地址没有问题(/usr/X11R6/xorg/modules)  
> 2、init 3，然后modprobe nvidia 能加载nvidia，startx正常。说明驱动安装没有问题。  
> 3、感觉应该是图形启动之前模块还没加载，导致这个问题。  
> 
> > 做法是在电脑开机加载模块的时候添加显卡模块。  
> > cd /etc/sysconfig/modules/  
> > nano nvidia.modules  
> > 加入 /sbin/modprobe nvidia 保存。  
> 
>   
> 进度条的时候白屏死机  
> 进/etc/X11/xorg.conf   设置成16位色  
>