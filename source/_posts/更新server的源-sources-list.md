---
title: 更新server的源 sources.list
tags:
  - ubuntu
categories:
  - Ubuntu
  - 基础
id: '271'
abbrlink: 3830180328
date: 2010-09-22 14:54:00
---

1、用sftp 上传sources.list  
      sftp server用户名@server主机名  
      输入 server用户名的密码  
  
    put /etc/apt/sources.list /etc/apt/.  
  
 (ssh 的使用查看上一篇： 从网络接手server：2、ssh到server)   
  
2、更新源  
     exit  
    ssh server用户名@server主机名  
   输入 server用户名的密码  
  
   sudo apt-get update