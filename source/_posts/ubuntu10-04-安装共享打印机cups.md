---
title: ubuntu10.04 安装共享打印机(CUPS)
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '328'
abbrlink: 1042151429
date: 2010-07-16 08:38:00
---

1、安装打印机驱动  
      系统-系统管理-打印 添加 选canon-ix5000  
2、安装cups  
      sudo apt-get install cupsys  
3、调试  
      http://127.0.0.1:631/printers 打开管理页面  

![ubuntu10.04 安装共享打印机(CUPS) - leaf - ------坚持雅操------](http://img.ph.126.net/vurHjkaPT9r7AV-W0gDY3w==/3280309378587648520.jpg "ubuntu10.04 安装共享打印机(CUPS) - leaf - ------坚持雅操------")

   
4、在其他电脑上添加网络打印机  
     http://192.168.2.188:631/printers/canon-ix5000  
  

  

5、关于不能添加打印机：(由于选了 Use Kerberos authentication(FAQ))

提示：

请输入您的用户名称和密码或者 root 用户的用户名称和密码来访问此页面。如果您正在使用 Kerberos 鉴定，请确定您拥有的 Kerberos 票据是有效的。

解决方法：

修改/etc/cups/cupsd.conf文件下的

<Policy default>

<Policy authenticated>

全部改为 

  Order allow,deny

  Allow all

即可

添加好了再改回去好了

  

20140809补充：/etc/group 里面lp这一行添加用户，用来管理cups服务

  
安装PDF打印机  http://www.oschina.net/p/cups-pdf   
1、sudo aptitude install cups-pdf  
2、更改  /usr/lib/cups/backend/ cups-pdf权限(加上SUID权限)

sudo chmod u+s cups-pdf

可以看到打印里已经加了一台PDF打印机

试验结果：能打印，但总是提示错误