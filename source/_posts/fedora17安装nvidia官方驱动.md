---
title: fedora17安装nvidia官方驱动
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '211'
abbrlink: 2095604229
date: 2012-10-10 12:25:00
---

版本：fedora17 x64位  
CPU：AMD Athlon(tm) II X4 635 Processor × 4  
主板：AMD 870 (无板载显卡)  
内存：DDR3-1333 8G  
显卡：8500GT  
  
0、设置了sudoers、yum源  

> sudo gedit /etc/sudoers  
> 
> > \# User privilege specification  
> > root    ALL=(ALL) ALL  
> > 加入   你的账户名   ALL=(ALL) ALL  
> 
> yum源就加163的就好了  
> 
> > mirrors.163.com  
> > 点fedora使用帮助，里面有详细信息  
> 
>   

1、安装相关编译包  

> gcc、make、kernel-devel、kernel-headers、dkms  
> sudo yum -y install gcc make dkms  
> kernel-devel和kernel-headers是从DVD安装光盘里找的  
> #也可以把kernel更新到最新版，再用yum下载kernel源码  
>   

2、相关设置  

> 1、阻止nouveau模块的加载  
> 
> > sudo gedit /etc/modprobe.d/blacklist.conf  
> > 添加一行：blacklist nouveau  
> 
> > sudo gedit /boot/grub2/grub.cfg  
> > 在menuentry 'Fedora Linux' 这一段的linux    /boot/vmlinuz 这一行末尾rhgb quiet后面添加 nouveau.modeset=0  
> 
> 2、降低selinux级别  
> 
> > sudo setsebool -P allow\_execstack on  
> 
> 3、下载nvidia官方驱动和设置权限  
> 
> > 下载最新的就可以：NVIDIA-Linux-x86\_64-304.51.run  
> > chmod a+x NVIDIA-Linux-x86\_64-304.51.run  

  
3、操作  

> 1、进文本模式  
> 
> > 重启进菜单后-按e进编辑模式-找到rhgb quiet，输入 3   然后按F10启动  
> 
> 2、nvidia安装  
> 
> > sh ./NVIDIA-Linux-x86\_64-304.51.run
> 
> > 里面就是选accept，然后再要不要生成xorg.conf的时候按ok 就好了  
> 
> 3、设置分辨率  
> 
> > 重启后发现分辨率只有640x480  
> > 1、查看频率  
> > 
> > > gtf 1280 1024 60  -x  
> > 
> >   # 1280x1024 @ 60.00 Hz (GTF) **hsync: 63.60 kHz; pclk: 108.88 MHz**  
> >   Modeline "1280x1024\_60.00"  108.88  1280 1360 1496 1712  1024 1025 1028 1060  -HSync +Vsync  
> > 2、设置频率  
> 
> > sudo gedit /etc/X11/xorg.conf  
> > 
> > > Section "Monitor"  
> > >     Identifier     "Monitor0"  
> > >     VendorName     "Unknown"  
> > >     ModelName      "Unknown"  
> > >     HorizSync       28.0 - **63.60**  
> > >     VertRefresh     43.0 - **108.88**  
> > >     Option         "DPMS"  
> > > EndSection  

  
4、查看模块  

> lsmod  
> 
> > nvidia              11262717  40  
> > nouveau               785691  0  
> 
> modinfo nvidia  
> 
> > filename:       /lib/modules/3.3.4-5.fc17.x86\_64/extra/nvidia.ko  
> > alias:          char-major-195-\*  
> > version:        304.51  
> > supported:      external  
> > license:        NVIDIA

  
后记  

> 碰到的问题就是屏幕分辨率的问题，没碰到安装不了驱动的问题，也没有黑屏和蓝进度条的问题  

> >   

参考：  

> [fedora15安装nvidia官方驱动](http://www.2cto.com/os/201109/104395.html)

> [解决linux低分辨率](http://www.xufangxi.cn/Linux/11.html)  
> [xorg.conf配置详解](http://www.cnblogs.com/ZJoy/archive/2011/03/15/1984938.html)  
> [linux gtf和cvt命令](http://hi.baidu.com/cxkipq/item/99a2229216b58736336eebc2)  

> >   

效果  

> ![fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------](http://img4.ph.126.net/DvYtJ6ZJGYgSLMun86veQg==/6598258338725711534.jpg "fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------")

> ![fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------](http://img7.ph.126.net/B1auivZnvejbCt67buGBDQ==/6597256683634379457.jpg "fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------")
> 
> ![fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------](http://img5.ph.126.net/74zwresWU4eSY0k7iIXNOA==/2682175053093706855.jpg "fedora17安装nvidia官方驱动 - leaf - ------坚持雅操------")
> 
>