---
title: msi EX465安装MACOSX 网卡驱动
tags:
  - 未分类
id: '250'
abbrlink: 150377324
date: 2014-08-22 20:59:00
---

msi有线网卡是sis 191，无解

无线网卡是雷凌2870 usb的，可以安装雷凌驱动，其他都好，就是不能上app store

  

前几天网购了AR9380 （￥49元，还能接受）。直接免驱，但还是进不了app store。

原因：进app store的条件是有线网卡必须是en0，无线网卡必须是en1。

由于我的有线无解，导致装的无线变成en0了。下面就是解决这个问题的

  

解决思路是：1、虚拟一个有线网卡  2、把网卡名称对调一个

> 解决第一个问题

> 下载nullEthernet.kext并安装，然后dsdt打补丁或者加ssdt 。（这些下载里面都有）
> 
> http://bbs.pcbeta.com/viewthread-1505728-1-1.html
> 
> https://bitbucket.org/RehabMan/os-x-null-ethernet/downloads
> 
> 这样重启之后，无线变成en0，有线变成en1了。我们需要对调一个
> 
>   
> 
> 解决第二个问题
> 
> 删除：  
> /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist  
> /Library/Preferences/SystemConfiguration/preferences.plist  
> 重启搞定。
> 
>   
> 
> ![msi EX465安装MACOSX 网卡驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/pdp-y8SVeeJTqQ3kxlGDFA==/6608870824957417795.png "msi EX465安装MACOSX 网卡驱动 - leaf - ------坚持雅操------")
> 
>  
> 
>