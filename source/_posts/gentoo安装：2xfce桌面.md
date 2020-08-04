---
title: gentoo安装：2xfce桌面
tags:
  - gentoo
categories:
  - Linux
  - gentoo
id: '235'
abbrlink: 3933523040
date: 2012-11-30 16:40:00
---

  
参考：  
http://www.gentoo.org/doc/en/xorg-config.xml  
http://www.gentoo.org/doc/zh\_cn/xorg-config.xml  
http://www.gentoo.org/doc/zh\_cn/xfce-config.xml  
http://blog.csdn.net/fo1\_sky/article/details/6339910  
1、安装Xorg  

> nano -w /etc/portage/make.conf  
> 
> > INPUT\_DEVICES="keyboard mouse"  
> > VIDEO\_CARDS="vmware"  
> >   
> 
> emerge libdrm  
> emerge mesa  
> emerge --autounmask-write  xorg-x11  
> dispatch-conf  
> emerge xorg-x11  

> #要安装125个包  
> env-update  
> source /etc/profile  
> Xorg -configure  
> X -config /root/xorg.conf.new  
> cp /root/xorg.conf.new /etc/X11/xorg.conf  
> startx 进行测试  

  
2、安装xfce  

> 由于安装gnome出现问题解决不了，所以安装了xfce  
> libdiscid   rarian(包含在hal下) 这2个软件不知道怎么装。  
>   
> USE="-gnome -kde -minimal -qt4 branding dbus hal jpeg lock session startup-notification thunar X"  
> emerge thunar-volman  
> emerge python  
> emerge pambase  
> emerge -avt xfce4-meta  
> for x in plugdev cdrom cdrw usb ; do gpasswd -a leaf $x ; done  
> env-update && source /etc/profile  
> echo "exec startxfce4" > ~/.xinitrcemerge xf86-input-evdev  #解决鼠标动不了的问题  
> startx  
> 后面的附加程序都没有装  
>   

界面如下：  

> ![gentoo安装：2xfce桌面 - leaf - ------坚持雅操------](http://img3.ph.126.net/ybaTpHC0ug5NfXM9OjlNIQ==/6597557949819376093.jpg "gentoo安装：2xfce桌面 - leaf - ------坚持雅操------")  
>   
>   
> 对以后LFS装桌面有好处～。。。  
> 
>  

>