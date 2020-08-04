---
title: CCNA第四章 CISCO IOS
tags:
  - ccna
categories:
  - Network
  - cisco
id: '199'
abbrlink: 529402642
date: 2012-08-28 16:17:00
---

本章主要介绍怎么进cisco  
  
cisco安全层次  

> 普通模式-特权模式-编辑模式。  
> 跟vim有点像，  
> 
> > 普通模式就相当于进入vim的时候你可以浏览文档  
> > 特权模式就相当于vim可以操作dd，wq之类的  
> > 编辑模式就相当于按下insert之类的命令之后可以开始编辑  

  
cisco的配置文档结构  

> 结构就是全局+各个具体项  
> 设置用户名，设置路由协议，acl之类的就是全局配置  
> 进入各个接口，进入各个line就是具体项配置。  

  
  
  
  
  
  
主要内容：  

> 设置密码  
> 设置SSH  
> 其他常用命令  

  
1、设置口令  

> 登录口令：包括aux、console、vty等口令，就是连接路由器的时候要输入的口令  
> 
> > (config)#line vty 0 4  
> > (config-line)#password 123  
> > (config-line)#login  
> 
> 特权口令：就是输入 routrer>enable 后要输入的口令  
> 
> > (config)#enable password 123  / enable secret 123  

> 其他：  
> 
> > 不设置登录口令  
> > 
> > > (config)#line vty 0 4  
> > > (config-line)#no login  
> > 
> > 控制台的相关设置  
> > 
> > > (config-line)#logging synchronous   阻止控制台信息的显示  
> > > (config-line)#exec-timeout 0 0         设置无操作时的退出时间  
> > 
> > 加密配置中的密码  
> > 
> > > (config)#service password-encryption  
> > 
> > 对接口进行描述  
> > 
> > > (config-if)#description \*\*\*\*\*\*  
> > >   

2、SSH加密通信  

> (config)#hostname rt                         先设置主机名  
> (config)#ip domain-name rt.com       再设置域名  
> (config)#crypto key generate rsa general-keys modulus 1024   这里用rsa加密，密钥位数1024  
> (config)#ip ssh time-out 60                        自动断开时间60秒  
> (config)#ip ssh authentication-retries 3      密码错误重试3次  
> (config)#transport input ssh telnet              应用到ssh和telnet  

  
3、开启路由器的http/https服务  

> 略 p185  

  
4、其他  

> 登录特权模式 router>enable                          当前用户模式：查看统计信息等  
> 
> > #show history                                       查看历史命令  
> > #show terminal                                     查看终端设置  
> > 
> > > #terminal history size 25              修改历史命令行数  
> > 
> > #show version                                      查看ios版本  
> >   
> > show interface f0/1                               查看接口配置  
> > show ip interface                                  查看接口的IP配置  
> > show ip interface brief                          查看接口的详细状态      
> > show protocols                                     查看1、2层状态  
> > show controllers                                   查看接口DCE、DTE      
> >   
> > #erase startup-config                           删除启动配置  
> > #copy running-config startup-config     保存  
> > #reload  (重启)                                     重新加载配置  
> >   
> 
> 登录全局模式router#configure terminal         当前特权模式：可查看/修改配置，查询路由表等  
> 
> > (config)#hostname rt                             更改主机名  
> > (config)#banner motd ! \*\*\*\*\*\*\*\*\*\*\* !         banner 横幅 ，就是登录或者离开系统时的提示  
> >   
> 
> 登录功能模式router(config)#interface fastEthernet 0/0     当前全局模式，可改主机名、时钟等

> > (config-if)#ip address 192.168.1.2 255.255.255.0  
> > (config-if)#ip address 192.168.2.2 255.255.255.0 secondary  
> >                                                               一般不会用到，同一个端口设置第二个子网地址  

  

> interface s0/0  
> 
> > (config-if)#clock rate 1000000  
> > (config-if)#bandwidth 100000
> 
>   

5、除错  

> serial0/0 is up,line protocol is down   
> 正常的话物理层和数据链路层都应该是up，如果数据链路层down的话考虑时钟等，这种问题一般出现在串口上  

  

> 错误提示  

> > %incomplete command                            一行命令没输完整  
> > %invalid input detected at '^' marker        输入错误  
> > %ambiguous command                            产生歧义，命令不唯一