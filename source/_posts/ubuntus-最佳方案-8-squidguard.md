---
title: ubuntus 最佳方案 -8 squidGuard
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '164'
abbrlink: 3846105662
date: 2012-05-29 15:04:00
---

安装  
sudo apt-get install squid  
sudo apt-get install squidguard  
  
正向代理：  
反向代理：对外表现为WEB服务器，但是数据不在代理服务器上，从而增加安全性  
透明代理：代理服务器做网关，从而不用去设置浏览器  
  
ACL规则、语法等该书没多少介绍，有机会最好专门读一下  
  
关于squidguard  
专门的访问控制插件，功能很强大  
  
建议这一章还是读专门的书比较好