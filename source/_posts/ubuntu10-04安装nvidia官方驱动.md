---
title: ubuntu10.04安装nvidia官方驱动
tags:
  - 未分类
id: '212'
abbrlink: 2285331920
date: 2012-10-10 14:57:00
---

  
系统：ubuntu10.04 x64  
CPU：AMD Athlon(tm) II X4 635 Processor × 4  
主板：AMD 870 (无板载显卡)  
内存：DDR3-1333 8G  
显卡：8500GT  
  
1、安装环境  

> sudo apt-get install build-essential pkg-config linux-headers-$(uname -r)  
> 下载驱动并设置权限 chmod a+x NVIDIA-Linux-x86\_64-304.51.run  
>    

2、删除已有的模块和软件  

> 移除旧的nvidia模块和组件  
> 
> > sudo apt-get --purge remove nvidia-glx nvidia-glx-legacy nvidia-glx-new nvidia-settings

> 检查无关的nvidia软件是否已被完全删除  
> 
> > dpkg -l | grep nvidia

> 删除这些软件  
> 
> > sudo aptitude purge $(dpkg -l | grep nvidia | awk '{print $2}')  

> 移除xorg-nv驱动  
> 
> > sudo apt-get --purge remove xserver-xorg-video-nv  
> 
> 禁用`nouveau  
> `
> 
> > `sudo gedit /etc/modprobe.d/blacklist.conf  
> > 添加blacklist nouveau  
> > `

> #总之就是将新立得里面所有的nvidia选项全删除，里面的jockey\*这个不用删除没事。  
>   

3、重启并安装  

> 重启后按ctrl+alt+f1 ，进tty1，关闭gdm：sudo /etc/init.d/gdm stop  
> 安装  
> 
> > sudo su  
> > sh ./NVIDIA-Linux-x86\_64-304.51.run  
> > 1、前面如果模块没有删除干净，装的时候会帮我们先卸载再安装的  
> > 2、/usr/lib/xorg/modules/extensions/libglx.so 会帮我们自动做符号连接，连接到同目录下面的libglx.so.304.51  
> 
> 安装完后重启  
> 
> > sudo reboot  
> >   

4、仍然碰到分辨率的问题  

>  gtf 1152 864 60 -x  
> 
> >   # 1152x864 @ 60.00 Hz (GTF) **hsync: 53.70 kHz; pclk: 81.62 MHz**  
> >   Modeline "1152x864\_60.00"  81.62  1152 1216 1336 1520  864 865 868 895  -HSync +Vsync  
> 
> sudo gedit /etc/X11/xorg.conf  
> 
> > Section "Monitor"  
> >     Identifier     "Monitor0"  
> >     VendorName     "Unknown"  
> >     ModelName      "Unknown"  
> >     HorizSync       28.0 - **53.70**  
> >     VertRefresh     43.0 - **81.62**  
> >     Option         "DPMS"  
> > EndSection  

  
参考：  

> [Ubuntu中安装NViDIA官方驱动](http://www.5dlinux.com/article/1/2011/linux_42055.html)  
>   
>   

效果  

> ![ubuntu10.04安装nvidia官方驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/SXMSsuyEqs9UR3TzM5dSmg==/30117822525904591.jpg "ubuntu10.04安装nvidia官方驱动 - leaf - ------坚持雅操------")
> 
>  

>   
>   

继续问题：  

> 问题1：firefox开2个页面，一个页面放视频，另一个开网页，看网页的这个页面会出现视频画面  
> 
> > ![ubuntu10.04安装nvidia官方驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/YgLW2bK4xbMjpXSwbQRzlA==/6597256683634594001.jpg "ubuntu10.04安装nvidia官方驱动 - leaf - ------坚持雅操------")  
> 
> 问题2：firefox---帮助---故障排除信息：图像列表显示  
> 
> > 适配器描述        Mesa Project -- Software Rasterizer  
> > 厂商 ID              Mesa Project  
> > 设备 ID              Software Rasterizer  
> > 驱动程序版本    2.1 Mesa 7.7.1  
> > WebGL 渲染器  因您的显卡驱动版本已屏蔽。尝试更新您的显卡驱动至版本 304.51 或更新版本。  
> > GPU 加速窗口   0. 因您的显卡驱动版本已屏蔽。尝试更新您的显卡驱动至版本 304.51 或更新版本。  
> 
> 问题3：点外观---视频效果，开不起来说驱动没有装  

解决方法：  

> 20121206：终于找到原因了，我把nvidia模块关掉了竟然。。。。  
> `查看 /etc/modprobe.d/blacklist.conf`。发现里面加入了 blacklist nvidiafb  

> 删除blacklist nvidiafb，然后我又重装了驱动就好了，重装同步骤3  

  
附：删除nvidia操作：  
上面的步骤2无效，使用如下命令  
sudo /usr/sbin/dkms remove -m nvidia -v 304.51 --all  
  
参考：[http://www.mystone7.com/2012/05/20/ubuntu\_install\_nvidia/](http://www.mystone7.com/2012/05/20/ubuntu_install_nvidia/)