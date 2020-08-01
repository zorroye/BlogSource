---
title: CCNA第六章 静态路由、默认路由、RIPv2
tags:
  - 未分类
id: '201'
date: 2012-09-10 11:08:00
---

  
路由详细过程

静态路由

> (config)#ip route 目标网段 子网掩码 下一路由接口 管理距离AD
> 
> (config)#ip route 10.0.0.0 255.0.0.0 192.168.1.10 150
> 
> \--------\[R1\]-192.168.1.1-----------192.168.1.10-\[R2\]-----10.0.0.0-------- 
> 
> AD越小越好越可信，直连为0

  

默认路由

> 只有1条出去的道路才能用默认路由
> 
> (config)#ip route     0.0.0.0    0.0.0.0             10.1.11.1

> > > > > 所有的IP，所有的子网掩码 下一路由接口地址

  
RIP

> 对相同开销的链路直接实现负载均衡，最多6条
> 
> RIPv2组播整个路由表到相邻路由器上
> 
> 防路由回路：

> > 最大跳计数15，
> 
> > 水平分割(不像接收方向发送网段信息)，
> 
> > 路由中毒(对故障网段设置最大跳为16)，
> 
> > 保持关闭(设置定时，一段时间内不能恢复)
> 
> (config)#router rip
> 
> (config-router)#network 10.0.0.0
> 
> (config-router)#version 2
> 
>   

  
  
  
  
  
  
  
  
  
  
  
  
一个星期没看了。。。唉，三天打鱼，两天撒网  
  
摘录  

> 发送destination unreachable 只可能是出故障(接口被关闭)的那个路由器。这可以判断哪个位置出故障  
>   
> show ip route  
> 
> > C:直接连接  
> > S：静态路由  
> > R：rip  
> > O：ospf  
> 
>   
> 防止路由环路  
> 
> > 最大跳数限制  
> > 水平分割          发来的信息不能发回原路  
> > 路由中毒          一旦设置为16，将通告所有这条路由信息  
> > 保持关闭         设置定时器，一定时间内改不了  

  
  
无线路由配置  

> (config)#int dot11radio 0/3/0  
> (config-if)#ip address 10.1.8.1 255.255.255.0  
> (config-if)#ssid test  
> (config-if-ssid)#guest-mode                       指此接口将广播这个ssid，若要隐藏就不要设置  
> (config-if-ssid)#authentication open  
> (config-if-ssid)#infrastructure-ssid             指此接口可以与其他接入点进行通信  
> (config-if-ssid)#no shutdown  
> (config-if-ssid)#exit  
> (config-if)#exit  
> 
> (config)#ip dhcp pool test  
> 
> (dhcp-config)#network 10.1.8.0 255.255.255.0
> 
> (dhcp-config)#default-router 10.1.8.1
> 
> (dhcp-config)#exit
> 
> (config)#ip dhcp excluded-address 10.1.8.1
> 
>   
> 扩展，如设置无线密码等查看 [多vlan的AP配置](http://wan118.sinaapp.com/?p=115)  
>   

无线AP配置  

> (config)#int bvi 1  
> (config-if)#ip address 10.1.1.2 255.255.255.0  
> (config-if)#no shutdown  
> (config-if)#exit  
> (config)#ip default-gateway 10.1.1.1  
> 
> (config)#ip dhcp pool test2  
> 
> (dhcp-config)#network 10.1.1.0 255.255.255.0
> 
> (dhcp-config)#default-router 10.1.1.1
> 
> (dhcp-config)#exit
> 
> (config)#ip dhcp excluded-address 10.1.1.1
> 
> (config)#ip dhcp excluded-address 10.1.1.2

  
静态路由命令  

> (config)#ip route 172.16.3.0       255.255.255.0           192.168.2.4                               150  

>              下一个网段         子网掩码         通往下一网段的接口IP地址        管理距离，可有可无  

  
默认路由命令  

> (config)#ip route 0.0.0.0 0.0.0.0 217.124.6.1  
> 或者       ip default-network 217.124.6.0  
>   

RIP  

> (config)#router rip  
> (config-router)#network 10.0.0.0  
> (config-router)#passive-interface s0/0    s0/0不能向外发送rip信息，但是能接收  
> (config-router)#version 2  
>   

查看、验证、出错命令  

> show ip route  
> show ip protocols  
>   
> debug ip rip  
> 
> > debug查看的时候就看进来有哪些信息，出去有哪些信息，就能画出网络图，然后再除错  
> > 另外一般多是远程连路由器的，所以要输入命令 #terminal monitor 不然看不到debug信息的  

>