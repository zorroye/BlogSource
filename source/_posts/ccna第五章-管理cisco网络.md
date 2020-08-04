---
title: CCNA第五章 管理cisco网络
tags:
  - ccna
categories:
  - Network
  - cisco
id: '200'
abbrlink: 3113480854
date: 2012-08-30 15:45:00
---

本章主要介绍怎么用cisco  
  
cisco存储介质  
  

> ROM：  
> 
> > 存放POST自检程序 (相当于BIOS)  
> > 存放bootstrap          (相当于linux的grub，一个启动程序)
> 
> > ROM监控程序，微型IOS(相当于WINPE)  
> 
> NVRAM：  
> 
> > 16位软件寄存器(相当于设置启动顺序)  
> > 存放配置文件  
> 
> 闪存：  
> 
> > 保存CISCO IOS (相当于电脑硬盘)  
> 
> RAM：  
> 
> > 内存(相当于电脑内存)  

  
cisco的启动顺序  

> \->POST自检  
> \->启动bootstrap  
> \->bootstrap调用16位寄存器设置  
> \->bootstrap载入闪存中的IOS/TFTP的IOS/ROM上的微型IOS  

> \->cisco ios 调用NVRAM上的配置文件  
>   

CDP cisco发现协议  

> 只能看到直连cisco设备  
> 绘制拓扑图非常方便  
> 不用啥设置，基本上show一下啥都清楚了  
>   

  
恢复口令  
  

>   

debug命令  

> 检查全面，但是消耗巨大，严重降低性能。  
> #debug all  
> #no debug all  
>   

>   
>   
>   

  
主要内容：  

> 启动过程  

> 恢复口令  
> CDP  
> hosts/DNS名称解析设置  

  
1、路由器启动详细过程  

> 思科路由器的启动过程和电脑类似  
> 首先，开机自检，开机自检程序存在ROM中。  
> 
> > ROM存了  |post自检程序  
> > 
> > > > |ROM监控程序  
> > > > |bootstrap，用于加载IOS，IOS相当于linux的内核；bootstrap相当于grub  
> > > > |微型IOS，相当于WINPE  
> 
> 第二，由bootstrap加载IOS到RAM中  
> 
> > IOS存放在flash中，flash相当于硬盘  
> > RAM就是内存，这个过程和加载linux内核是一样的  
> 
> 第三，加载配置文件  
> 
> > 加载配置文件就相当于linux中的init程序的操作  
> > 配置文件存放在NVRAM中，NVRAM中还存放配置寄存器  
> > 
> > > 配置寄存器的作用和linux下的inittab差不多  
> > > inittab可以使linux启动命令行界面或图形界面  
> > > 而配置寄存器可以使IOS加载配置或不加载配置  

  

> 补充：  
> CISCO IFS就是对flash的操作，flash就相当于硬盘  

> 而路由协议啥的就是应用程序  
>   
>   

2、恢复口令  

> 1、开路由器后马上按ctrl+pause|break键，进入ROM监控模式  
> 2、设置寄存器>confreg 0x2142  
> 3、重启路由器>reset  
> 4、修改密码  
> 
> > copy startup-config running-config  
> > config terminal  
> > enable secret 123  
> > copy running-config startup-config  
> > config-register 0x2102  
> >   

3、思科CDP  

> 就是查看直连设备IP、端口、IOS版本等  
> cdp有2个参数  
> 
> > #show cdp  
> 
> > (config)#cdp holdtime 180  
> > (config)#cdp timer 60  
> 
> cdp相关命令  
> 
> > (config)#no cdp run 完全关闭cdp  
> > (config-if)#no cdp enable 关闭某个端口的cdp  
> >   
> > #show cdp neighbor  
> > #show cdp neighbor detail  
> > #show cdp entry \* protocols  
> > #show cdp entry \* version  
> > #show cdp traffic  
> > #show cdp interface (显示接口的CDP状态)  

  
4、利用dns解析主机表  

> 前提是网络上有DNS服务器  
> ip domain-lookup  
> ip name-server 192.168.1.1  
> ip domain-name 123.com  
>   
> 直接自己输入：  
> ip host R1 10.2.2.2  相当于在hosts文件里面写主机表  

  
5、对远程连接的操作  

> telnet 10.1.1.1  
> 本地的操作  
> 
> > show sessions  
> > disconnect 2  
> >   
> 
> 远程设备上的操作  
> 
> > show users  
> > exit  /  chlar line 2  

  
  
其他摘录  

> boot system flash rom ftp tftp  
>   
> show processes 相当于进程管理器  
>   
> debug all  
>   
>