---
title: ubuntu10.04安装官方ati显卡驱动
tags:
  - 未分类
id: '32'
abbrlink: 2936125880
date: 2012-10-13 07:31:00
---

配置  
系统：ubuntu10.04 X64  
CPU：INTEL T4500(等价格降了换个p8700，或者T9600)  
主板：PM45  
内存：DDR2-800 2GX2  
显卡：ATI Mobility Radeon HD 5470  
  
1、安装编译相关软件  

> sudo apt-get install build-essential cdbs fakeroot dh-make debhelper debconf libstdc++6 dkms libqtgui4 wget execstack libelfg0  

  
2、下载ati显卡驱动  

> http://www2.ati.com/drivers/linux/amd-driver-installer-12-8-x86.x86\_64.zip  
> 解压之后是run文件  

  
3、制作deb包  

> 其实直接装也没关系的  
> sudo su  
> sh amd-driver-installer-8.982-x86.x86\_64.run --buildpkg Ubuntu/lucid  
> 出来5个文件  
> 
> > fglrx\_8.982-0ubuntu1\_amd64.deb  
> > fglrx-amdcccle\_8.982-0ubuntu1\_amd64.deb  
> > fglrx-dev\_8.982-0ubuntu1\_amd64.deb  
> > fglrx-installer\_8.982-0ubuntu1\_amd64.changes  
> > fglrx-modaliases\_8.982-0ubuntu1\_amd64.deb  

  
4、删除原有驱动和配置  

> sudo apt-get remove --purge fglrx fglrx\_\* fglrx-amdcccle\* fglrx-dev\* xorg-driver-fglrx xserver-xorg-video-ati xserver-xorg-video-radeon  

> sudo mv /etc/X11/xorg.conf  /etc/X11/xorg.con.old  

4.1、禁用`nouveau`  

> `sudo gedit /etc/modprobe.d/blacklist.conf  
> 添加blacklist nouveau`  

  
5、安装  

> 重启  
> 进桌面后，按ctrl+alt+f1  
> sudo /etc/init.d/gdm stop            #sudo /etc/init.d/lightdm stop   #ubuntu12.04

> sudo dpkg -i fglrx\*.deb  
> sudo aticonfig --initial -f              #建配置文件xorg.conf  

> 重启  
>   

6、测试  

> lsmod | grep fglrx  
> 
> > fglrx                2690265  115  

> fglrxinfo  
> 
> > display: :0.0  screen: 0  
> > OpenGL vendor string: Advanced Micro Devices, Inc.  
> > OpenGL renderer string: ATI Mobility Radeon HD 5400 Series  
> > OpenGL version string: 4.2.11762 Compatibility Profile Context  
> 
> amdcccle

> > ![ubuntu10.04安装官方ati显卡驱动 - leaf - ------坚持雅操------](http://img4.ph.126.net/mmKFXj0V8YZNpMDVBPLfkA==/6597647010260863324.jpg "ubuntu10.04安装官方ati显卡驱动 - leaf - ------坚持雅操------")
> > 
> >  

7、参考：  

> http://wiki.cchtml.com/index.php/Main\_Page  

其他  

> 过时的软件：envyng  
> 解决花屏的：http://hi.baidu.com/ypqnwahlyjbcmtq/item/35cabf25f6acba0873863e5e