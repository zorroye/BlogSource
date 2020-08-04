---
title: 安装 VCSA 6
tags:
  - vmware
categories:
  - Virtualization
  - vmware
id: '297'
abbrlink: 998840505
date: 2016-01-31 02:32:00
---

一、我部署的是嵌入式模式。  

> 所谓的vcsa部署，就是在esxi上面装一个虚拟机而已。  

二、对该虚拟机的要求是：最小是双核，8G内存。  

> 该要求不是针对安装VMware-ClientIntegrationPlugin-6.0.0.exe的windows系统的。  

三、我下载的是vcsa的linux版本。  
  
1、连接esxi  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img1.ph.126.net/5-VQd2EL9vflWP86Z0xHaA==/6608500289539539973.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
2、新建虚拟机，设置的密码为登陆虚拟机的密码  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img1.ph.126.net/AHDbx0ZCPY5j_W3XMtBa2w==/6598274831460123562.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
3、我安装的是嵌入式的  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img0.ph.126.net/-8GOhPIwFVy0vkY6w-Iozg==/6630719220515633301.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
4、设置域，该域提示说不能和AD一样  

> 这里的密码是登陆 web client的密码，账号就是administrator@域名  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img2.ph.126.net/I_wRJVoK_7tb9R5JGvk0GQ==/2487957319163734031.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
5、这里说明了虚拟机的配置要求  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img2.ph.126.net/eqkgkiTGDmgHlVSSMzbXzw==/6631308558750196301.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
6、虚拟机存放位置  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img0.ph.126.net/5ipcgGKpIazPKUIAhISOqw==/6631306359726940788.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
7、安装了嵌入式的数据库  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img0.ph.126.net/YB-xSeVqTlkG4t5tFI8r-A==/6597170921728686795.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
8、设置虚拟机网络  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img1.ph.126.net/6wm5JB9WA5QrBqgrrDFuHg==/6598275930971751355.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
9、安装完毕  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img1.ph.126.net/at0Q2Nof1tBsLBxYc_3hCg==/6619251314236185709.png "安装 VCSA 6 - leaf - ------勤解万难------")

   
10、虚拟机的界面。  

![安装 VCSA 6 - leaf - ------勤解万难------](http://img1.ph.126.net/oJRzII8jAhr_z5SOaoqSDg==/6630616965934467178.png "安装 VCSA 6 - leaf - ------勤解万难------")