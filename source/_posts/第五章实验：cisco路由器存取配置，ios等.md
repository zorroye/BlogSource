---
title: 第五章实验：cisco路由器存取配置，ios等
tags:
  - 未分类
id: '195'
date: 2012-05-09 17:22:00
---

环境：  

> gns3，vmware做tftp服务器  
> R0 F0/0 ：172.16.43.150  
> vmware：172.16.43.141  
> 
> ![第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------](http://img4.ph.126.net/PZ83qiwlo5aNsQA26bgQFA==/1552897446530188234.jpg "第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------")

   
1、组建tftp服务器：  

> cisco-tftp-server 下载：http://www.onlinedown.net/soft/33433.htm  

> 开启后测试一下：tftp -i 172.16.43.141 get 1.txt  

> tftp内存放有 c3660-i-mz.122-40a.bin  
>   

2、gns3设置  

> 云设置在上一篇已经介绍过了  
> 对R0的设置：  
> 
> > en  
> > configure terminal  
> > interface f0/0  
> > no shutdown  
> > ip address 172.16.43.150 255.255.255.0  
> > end  
> > copy running-config startup-config  
> > erase flash:  
> > 
> > ![第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------](http://img3.ph.126.net/AG9aehE4lTwLKiu2mF9TGQ==/617274623943966983.jpg "第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------")
> > 
> >    

3、验证是否连通  
  
4、开始存取命令  

> copy tftp flash：  
> 
> ![第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------](http://img7.ph.126.net/jKEJfSX8GpJcMOTLa9zGsA==/3099883918531950267.jpg "第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------")
> 
>    
> copy startup-config tftp  
> 
> ![第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------](http://img5.ph.126.net/wy-hxzpcuSbh_6Gnv_KSZQ==/2568177687525529385.jpg "第五章实验：cisco路由器存取配置，ios等 - leaf - ------坚持雅操------")
> 
>    
>   
>