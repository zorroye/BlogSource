---
title: ubuntu14.04 server 安装keepalived
tags:
  - 未分类
id: '287'
date: 2015-05-25 20:10:00
---

keepalived功能就是实现VRRP协议，解决单点故障问题。

  

参考：  
keepalived权威指南  
ubuntu server最佳方案2  
  
设备：  

> 树莓派2-1：Yrpi2-cryst，192.168.3.17，当MASTER  
> 树莓派2-2：Yrpi2-black，192.168.3.18，当BACKUP  
> IP地址：192.168.3.16

  
树莓派2-1 配置  

> /etc/hosts：192.168.3.17    Yrpi2-cryst

>   

> /etc/sysctl.conf  

> > net.ipv4.ip\_forward=1
> 
> > net.ipv4.ip\_nonlocal\_bind=1
> 
> > net.ipv4.tcp\_fin\_timeout=30
> 
> > net.ipv4.tcp\_syncookies=1

> sudo sysctl -p

>   

> /etc/keepalived/keepalived.conf  
> global\_defs  {

> > notification\_email {
> 
> > ywz@leaf.com

> > }

> notification\_email\_from 306@leaf.com  
> smtp\_server 127.0.0.1  
> smtp\_connect\_timeout 20  
> router\_id Yrpi2-cryst       #机器标识  
> }  
>   
> vrrp\_script chk\_haproxy {

> > script  "killall -0 haproxy"
> 
> > interval  2
> 
> > weight    2

> }  
>   
> #一个虚拟路由器包含多个物理的VRRP路由器  
> vrrp\_instance VI\_1 {        #VRRP路由器

> > state BACKUP
> 
> > smtp\_alert               #启用email通知
> 
> > nopreempt               #设置非抢占式，只有设置为BKUP才能设置这个选项
> 
> > interface eth0           #要绑定的网卡
> 
> > virtual\_router\_id 51  #所属虚拟路由器
> 
> > priority 150              #通过优先级来设置MASTER，跟BACKUP相差要50以上
> 
> > advert\_int 1             #每隔1s进行检测

>   
> #设置认证方式和密码  
> authentication {

> > auth\_type PASS
> 
> > auth\_pass Amitabha
> 
> > }

>   
> #设置共享的虚拟IP地址  
> virtual\_ipaddress {

> > 192.168.3.16
> 
> > }

>   
> #haproxy相关设置：故障检测  
> track\_script {

> > chk\_haproxy
> 
> > }

> }

>   

树莓派2-2 配置  

> /etc/hosts：192.168.3.18    Yrpi2-black

>   
> /etc/sysctl.conf  

> > net.ipv4.ip\_forward=1
> 
> > net.ipv4.ip\_nonlocal\_bind=1
> 
> > net.ipv4.tcp\_fin\_timeout=30
> 
> > net.ipv4.tcp\_syncookies=1

> sudo sysctl -p

>   
> /etc/keepalived/keepalived.conf

> global\_defs  {  
>     notification\_email {  
>         ywz@leaf.com  
>     }  
>     notification\_email\_from 306@leaf.com  
>     smtp\_server 127.0.0.1  
>     smtp\_connect\_timeout 20  
>     router\_id Yrpi2-black  
> }  
>   
> vrrp\_script chk\_haproxy {  
>     script  "killall -0 haproxy"  
>     interval  2  
>     weight    2  
> }  
>   
> vrrp\_instance VI\_1 {  
>     state BACKUP  
>     smtp\_alert  
>     interface eth0  
>     virtual\_router\_id 51  
>     priority 100  
>     advert\_int 1  
>     authentication {  
>         auth\_type PASS  
>         auth\_pass Amitabha  
>     }  
>     virtual\_ipaddress {  
>         192.168.3.20  
>     }  
>     track\_script {  
>         chk\_haproxy  
>     }  
> }

  
  
效果  

![ubuntu14.04 server 安装keepalived - leaf - ------勤解万难------](http://img1.ph.126.net/jlfVjqg5EpRMYPOHRDgg1Q==/6630387168001870027.png "ubuntu14.04 server 安装keepalived - leaf - ------勤解万难------")

 

![ubuntu14.04 server 安装keepalived - leaf - ------勤解万难------](http://img2.ph.126.net/wLB5cRdbZZnQ8PuVnowjgw==/6630474029420464148.png "ubuntu14.04 server 安装keepalived - leaf - ------勤解万难------")