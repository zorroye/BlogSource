---
title: 关于mate版本
tags:
  - ubuntu
categories：
  - Ubuntu
  - 基础
id: '33'
abbrlink: 2713717643
date: 2012-10-17 10:20:00
---

  
一种是ubuntu12.04安装mate  

> sudo add-apt-repository "deb http://packages.mate-desktop.org/repo/ubuntu $(lsb\_release -cs) main"  
> sudo apt-get install mate-archive-keyring  
> sudo apt-get update  

> sudo apt-get install mate-core mate-desktop-environment  
> 跟10.04的界面有点差别，不过还算习惯  

  
一种是用mint版本  

> 但是mint对中文的支持实在不怎么样，默认安装连个中文输入法多没有。。。  

> 问题：安装语言包出错主要是源的问题，更新到http://mirrors.ustc.edu.cn/的源即可  
> 
> > deb ftp://mirrors.ustc.edu.cn/linuxmint/ maya main upstream import  
> > deb-src ftp://mirrors.ustc.edu.cn/linuxmint/ maya main upstream import  

> 问题：IBUS 安装和自动启动  
> 
> > 更新源之后，sudo apt-get install ibus-gtk ibus-pinyin ibus-pinyin-db-open-phrase  
> > 语言支持里面选IBUS即可，我装好后系统自动选了IBUS了  
> 
> 问题：ubuntu主题图标等  
> 
> > https://launchpad.net/  
> > 主题：  
> 
> > `sudo add-apt-repository ppa:ravefinity-project/ppa   
> > sudo apt-get install ambiance-colors radiance-colors  
> > `
> 
> > 图标：  
> > 
> > > deb http://ppa.launchpad.net/fs-icons-ubuntu/unstable/ubuntu precise main  
> > > deb-src http://ppa.launchpad.net/fs-icons-ubuntu/unstable/ubuntu precise main  
> 
> > sudo apt-get install fs-icons-ubuntu  
> 
>   
> 
> ![关于mate版本 - leaf - ------坚持雅操------](http://img7.ph.126.net/knbvxKqYlHs3TMbQX_Cbdw==/6598097810028118177.jpg "关于mate版本 - leaf - ------坚持雅操------")
> 
>  
> 
>   

参考：  
http://it-diary.com/linux/ubuntu-linux/install-mate-1-2-in-ubuntu-12-04-or-11-10/  
http://www.cnblogs.com/tnxk/archive/2012/08/30/2663146.html