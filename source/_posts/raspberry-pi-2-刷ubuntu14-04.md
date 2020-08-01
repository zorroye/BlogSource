---
title: raspberry pi 2 刷ubuntu14.04
tags:
  - 未分类
id: '178'
abbrlink: 565288185
date: 2015-05-04 13:05:00
---

[https://wiki.ubuntu.com/ARM/RaspberryPi](https://wiki.ubuntu.com/ARM/RaspberryPi)  

  
1、下载镜像并解压  
2、写入SD  

> sudo apt-get install bmap-tools  
> sudo bmaptool copy --bmap ubuntu-trusty.bmap ubuntu-trusty.img /dev/sdc  

3、启动后扩容  

> sudo fdisk /dev/mmcblk0  
> 
> > Delete the second partition (d, 2),  
> > then re-create it using the defaults (n, p, 2, enter, enter),  
> > then write and exit (w).  
> > Reboot the system, then:  
> 
> sudo resize2fs /dev/mmcblk0p2  
> 建交换分区  
> sudo apt-get install dphys-swapfile  

4、安装桌面  

> sudo apt-get update  
> `sudo apt-get install` xubuntu-desktop

5、安装显卡驱动  

> sudo apt-get install xserver-xorg-video-fbturbo  
> nano /etc/X11/xorg.conf  
> 
> > Section "Device"  
> > Identifier "Raspberry Pi FBDEV"  
> > Driver "fbturbo"  
> > Option "fbdev" "/dev/fb0"  
> > Option "SwapbuffersWait" "true"  
> > EndSection
> 
> sudo apt-get install libraspberrypi-bin libraspberrypi-dev  
> sudo ln -s /usr /opt/vc  
> sudo apt-get install libraspberrypi-bin-nonfree  

6、安装其他软件  

> sudo apt-get install openssh-server  
> sudo apt-get install vnc4server  
> 
> > #!/bin/sh  
> >   
> > \# Uncomment the following two lines for normal desktop:  
> > \# unset SESSION\_MANAGER  
> > \# exec /etc/X11/xinit/xinitrc  
> >   
> > \[ -x /etc/vnc/xstartup \] && exec /etc/vnc/xstartup  
> > \[ -r $HOME/.Xresources \] && xrdb $HOME/.Xresources  
> > xsetroot -solid grey  
> > vncconfig -iconic &  
> > #x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &  
> > #x-window-manager &  
> >   
> > sesion-manager & xfdesktop & xfce4-panel &  
> > xfce4-menu-plugin &  
> > xfsettingsd &  
> > xfconfd &  
> > xfwm4 &  
> 
> sudo apt-get install hwloc  
> 
> ![raspberry pi 2 刷ubuntu14.04 - leaf - ------勤解万难------](http://img0.ph.126.net/yrbxBSz1CEeOkAoy1NSi4Q==/6631308558750619908.png "raspberry pi 2 刷ubuntu14.04 - leaf - ------勤解万难------")
> 
>    

7、设置无线网络  

> 我的无线网卡免驱  
> 
> sudo nano /etc/network/interfaces  
> 
> > auto wlan0
> > 
> > allow-hotplug wlan0  
> > iface wlan0 inet dhcp  
> > 
> > #iface wlan0 inet static  
> > 
> > #address 192.168.1.17
> > 
> > #netmask 255.255.255.0
> > 
> > #gateway 192.168.1.1
> > 
> > wpa-scan-ssid 1                #这个设置成1 可以连接到隐藏的网络
> > 
> > wpa-ap-scan 1                  #这个设置成1 可以连接到隐藏的网络
> > 
> > wpa-ssid "HELLO"
> > 
> > wpa-psk "123456"
> > 
> > #wpa-roam /etc/wpa\_supplicant/wpa\_supplicant.conf
> > 
> > iface default inet dhcp
> 
>   
> 
> 修复断线问题。设置无线网卡不节能。
> 
> > lsmod
> > 
> > > 8192cu                550797  0
> > 
> > 创建sudo nano /etc/modprobe.d/8192cu.conf
> > 
> > \# Disable power saving
> > 
> > options 8192cu rtw\_power\_mgnt=0 rtw\_enusbss=1 rtw\_ips\_mode=1
> 
>