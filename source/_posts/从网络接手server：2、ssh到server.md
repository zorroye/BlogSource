---
title: 从网络接手server：2、ssh到server
tags:
  - ubuntu
categories:
  - Ubuntu
  - 基础
id: '270'
abbrlink: 3778847342
date: 2010-09-22 14:35:00
---

1、防火墙开放22端口  
      sudo ufw allow 22    （开放22端口）  
      sudo ufw status        （查看ufw状态）  
  
2、连接到server  
      ssh server的用户名@server主机名     (server主机名我连不了，我用IP才连上去)  
      sftp server的用户名@server主机名  
  
  
其他：

> 查看日志 grep sshd /var/log/auth.log
> 
> 设置ssh不允许用root用户
> 
> nano /etc/ssh/sshd\_config

> > 更改PermitRootLogin no 即可

>   

3、端口敲门：

> 服务器端：

> >  sudo apt-get install knockd

> > 配置knockd.conf
> > 
> >   

\[options\]

UseSyslog

      #使用/var/log/syslog

\[openSSH\]

sequence    = 7000,8000,9000

      #敲门端口号

seq\_timeout = 5

      #敲门需在5秒内完成

command     = /sbin/iptables -I INPUT 1 -s %IP% -p tcp --dport 22 -j ACCEPT

      #-I INPUT 1：插入到iptable第一行

      #-s %IP%   ：目标IP地址

      #-p tcp    ：对应tcp协议

      #--dport 22  ：要连接的22端口

      #-j ACCEPT   ：允许通过

      #合起来就是： 在第一行插入一条规则：允许该IP通过tcp为22的端口

tcpflags    = syn

      制定tcp数据包标记

\[closeSSH\]

seq\_timeout = 5

        #等待5秒再执行关闭命令

command     = /sbin/iptables -D INPUT -s %IP% -p tcp --dport 22 -j ACCEPT

tcpflags    = syn

  

> >   

> 客户端：

> > sudo apt-get install knockd
> > 
> > knock IP 7000 8000 9000； ssh user@IP
> > 
> >   

http://www.ibm.com/developerworks/cn/aix/library/au-sshlocks/index.html  
  
附：  
1、第一次连接会提示是否连接点是  
2、提示输入密码，要输入server用户名的密码