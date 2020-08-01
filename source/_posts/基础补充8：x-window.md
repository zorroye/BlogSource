---
title: 基础补充8：X window
tags:
  - 未分类
id: '91'
date: 2014-12-13 09:34:00
---

1、只开X server 。一片黑屏，鼠标可以动  

> X :1&  
> 
> ![基础补充8：X window - leaf - ------坚持雅操------](http://img1.ph.126.net/DewYm4SOrcTGz8A4WqtyCA==/6619130367956356525.jpg "基础补充8：X window - leaf - ------坚持雅操------")
> 
>    

2、开X client 。屏幕左上角有终端输入界面，但是没有窗口,不能移动  

> xterm -display ：1&  
> 
> ![基础补充8：X window - leaf - ------坚持雅操------](http://img0.ph.126.net/FId_qUF5cLsqT31gHlh5-Q==/887490601669063227.jpg "基础补充8：X window - leaf - ------坚持雅操------")
> 
>    

3、开窗口管理器，twm或者metacity 。有窗口，还可以移动  

> twm -display :1 -f /etc/X11/twm/system.twmrc &  
> 或者  
> metacity -display :1&  
> 
> ![基础补充8：X window - leaf - ------坚持雅操------](http://img2.ph.126.net/jwi6o_qmZj1nSWmxpMCstQ==/145241088082979159.jpg "基础补充8：X window - leaf - ------坚持雅操------")
> 
>  
> 
> ![基础补充8：X window - leaf - ------坚持雅操------](http://img1.ph.126.net/vgEWzw9txT0xb9imd50knA==/887490601669063228.jpg "基础补充8：X window - leaf - ------坚持雅操------")
> 
>    

4、Widget   图形库  

> 包括gtk+ 和QT 。窗口的颜色，按钮，图案啥的都需要图形库的支持  
>   

5、Display Manager  

> 提供登陆界面和 会话协议XDMCP  
>   

6、Desktop Manager  

> 包括gnome、KDE等 。  
> 是以上的集合，然后再加上自行开发的界面。  
>   
>   

init5和startx的区别  

> init 5  

![基础补充8：X window - leaf - ------坚持雅操------](http://img1.ph.126.net/U-DEBwBEJ4tm1B-mvJrwtg==/2206200867558479713.png "基础补充8：X window - leaf - ------坚持雅操------")  

> startx  

 

![基础补充8：X window - leaf - ------坚持雅操------](http://img0.ph.126.net/SfJv_fMGdbtlnwy2Pc1KjQ==/3261169080270047412.png "基础补充8：X window - leaf - ------坚持雅操------")

   

> init 5 是启动prefdm，然后通过gdm启动X server。进gnome会话后还要开启Xsession登陆界面  
> startx 是启动xinit来启动X server，然后直接进gnome会话  

  

>   
>