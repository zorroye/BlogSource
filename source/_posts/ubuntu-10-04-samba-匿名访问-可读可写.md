---
title: ubuntu 10.04    samba 匿名访问 可读可写
tags:
  - 未分类
id: '327'
abbrlink: 1833866432
date: 2010-07-14 11:27:00
---

基础知识：

SMB服务：services message block 是由微软开发的。

samba的进程：

> smbd：用于提供服务器中的共享资源。
> 
> nmbd：用于提供NETBIOS主机名称解析。(在域和工作组中可以找到，网上邻居可以找到)

  

0、开放防火墙  
安装 gufw， sudo apt-get install gufw  
在系统-系统管理-防火墙配置：勾选已启用，然后全部选允许进入好了，也可以把端口 137 138 139 445 加入  
1、安装samba  

> sudo apt-get install samba        #samba软件
> 
> sudo apt-get install smbfs         #samba文件系统
> 
> sudo apt-get install swat           #图形化samba管理

2、设置文件权限

> chmod 0755 3SHARE
> 
> chmod 1777 5TEMP

3、配置文件

其中#后面的都是说明文档，而；后面的都是实例文档

 \[global\]  
    workgroup = WORKGROUP     #设置工作组  
    netbios name = 信息中心          #网上邻居上用的名字  
    server string = it001                    #对主机的描述说明  
  
    display charset = utf-8  
    dos charset = cp936  
  
    log file = /var/log/samba/%m.log   #对每个访客建独立日志记录。

> > > > > > #%m.log表示按登陆名称建目录  
> > > > > > 
> > > > > > #由于是匿名的，所有访客都记录在nobody.log下面(未验证)

    max log size = 50                          #日志最大50KB  
  
    security = share                             #安全级别：share user server domain

> > > > > > #server：让另一台主机提供验证服务
> > > > > > 
> > > > > > #domain：让域控制器来提供验证服务
> > > > 
> > > > #2014.08.12  补充  
> > > > 
> > > > > 在samba4中 share 和 server 已被弃用（ubuntu14.04）  
> > > > > 改为  
> > > > >  security = user  
> > > > > 
> > > > >     map to guest = Bad User
> > > > > 
> > > > > 参考：http://blog.chinaunix.net/uid-74892-id-4232517.html

  
  
    socket options = TCP\_NODELAY SO\_RCVBUF=8192 SO\_SNDBUF=8192  
    dns proxy = no  
    template shell = /bin/false  
    winbind use default domain = no  
  
#\[homes\] 表示登陆用户自己的家目录。就是每个登陆linux的用户都有各自的家目录是一样的。  
  
\[share\]  
    comment = read only  
    path = /home/it001/3SHARE  
    read only = yes  
    public = yes                     #共享的意思，所有人都可见。  
  
\[temp\]  
    comment = read write  
    path = /home/it001/5TEMP  
    writeable = yes  
    public = yes  
    create mode = 0666  
    directory mode = 1777  
  
\[printers\]  
    comment = All Printers  
    path = /var/spool/samba  
    printable = Yes  
    browseable = yes  

  
  
关于swat   (2012.11.20添加)  

> 由xinet负责进程的管理  
> 配置文件：/etc/inetd.conf  
> 配置内容：swat        stream    tcp    nowait.400    root    /usr/sbin/tcpd    /usr/sbin/swat  
> 
> > > > > 流                                               使用TCP wrapper  

> 端口:901  
> 端口设置:/etc/services  
>   
> 参考：http://yuanbin.blog.51cto.com/363003/117105  
> 浏览器访问：127.0.0.1:901  
> 
> ![ubuntu 10.04    samba 匿名访问 可读可写 - leaf - ------坚持雅操------](http://img1.ph.126.net/zWPbEpo0nYIscHXNqQs9-A==/6598068123214412271.jpg "ubuntu 10.04    samba 匿名访问 可读可写 - leaf - ------坚持雅操------")
> 
>  
> 
>    
>   

注释2013.10.09更新。其他说明在另一篇有写。