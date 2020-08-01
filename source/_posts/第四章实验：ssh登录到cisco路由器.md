---
title: 第四章实验：SSH登录到cisco路由器
tags:
  - 未分类
id: '192'
date: 2012-05-04 16:23:00
---

  
R0开通SSH服务，R1进行连接

![第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------](http://img8.ph.126.net/Gp63yqNwYLeIJUti6lcHGQ==/2588162410871966418.jpg "第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------")

1、设置R0 IP，开启F1/0  

> enable  

> configure terminal  
> interface fastethernet 1/0  
> no shutdown  
> ip address 19.168.1.1 255.255.255.0  
> exit  

2、设置进特权密码  

> enable secret 123456  

3、设置ssh  

> hostname a123  
> 
> > #没设置hostname会出现  
> 
> > ![第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------](http://img2.ph.126.net/IWNmX8UoKl9HZAuRqK4t6A==/1005428616827936602.jpg "第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------")

> ip domain-name a.com  
> crypto key generate rsa general-keys modulus 1024  
> ip ssh time-out 60                      #会话空闲60秒  
> ip ssh authentication-retries 3   #错误尝试3次  
> line vty 0 4  
> transport input ssh  
> login  
> 
> > #出现提示  
> 
> > ![第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------](http://img8.ph.126.net/TCkphAtS62gI7HpEok2OWg==/3083276894906012538.jpg "第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------")

 4、设置vty登录账户及密码  

> exit  
> aaa new-model  
> aaa authentication login default local  

> username test password test  

5、设置进特权密码  

> enable secret 123456  
> end  
> copy running-config startup-config  
>   

\--------------------------------------------------------------------------------------------  
  
1、设置R1 IP，开启端口  

> enable  

> configure terminal  
> interface fastethernet 1/0  
> no shutdown  
> ip address 19.168.1.2 255.255.255.0  
> end  
>   

2、SSH到R0  

> ssh -l test 192.168.1.1  
> 然后输入密码test  
> enable  
> 然后输入密码 123456  
>   

\---------------------------------------------------------------------------------------------  
  
1、取消ssh服务  

> crypto key zeroize rsa  
>   
> 
> ![第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------](http://img9.ph.126.net/R1Wzt_IJThR0vOpbwoFozw==/2616591383519726509.jpg "第四章实验：SSH登录到cisco路由器 - leaf - ------坚持雅操------")
> 
>  
> 
>    

参考文章：http://wenku.baidu.com/view/2e81590bf78a6529647d537f.html