---
title: '[转载] lubuntu自动登录(lxde)'
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '52'
abbrlink: 872591790
date: 2014-08-13 16:27:00
---

1\. /etc/lxdm/default.conf

> sudo vi /etc/lxdm/default.conf
> 
> autologin=username

  

2./etc/lightdm/lightdm.conf

> sudo vi /etc/lightdm/lightdm.conf 
> 
> \[SeatDefaults\]
> 
> autologin-user=username
> 
> autologin-user-timeout=0
> 
> greeter-session=lightdm-gtk-greeter
> 
> user-session=Lubuntu
> 
>   

转载自：http://www.cnblogs.com/xiangzi888/archive/2012/06/20/2557093.html