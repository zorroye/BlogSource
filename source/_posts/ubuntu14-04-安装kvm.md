---
title: ubuntu14.04 安装kvm
tags:
  - 未分类
id: '216'
abbrlink: 2372106058
date: 2015-05-19 23:50:00
---

0、检查是否有kvm模块

> ls /dev 看看是否有kvm

  

1、安装时遇到的问题

> http://my.oschina.net/lhplj/blog/336313

> sudo apt-get install openssh-server
> 
> > 提示openssh-server : 依赖: openssh-client (= 1:6.6p1-2ubuntu1)
> 
> 安装 sudo apt-get install openssh-client=1:6.6p1-2ubuntu1
> 
> sudo apt-get install openssh-server

  

2、安装

> sudo apt-get install ubuntu-virt-server
> 
> sudo apt-get install virtinst
> 
> sudo apt-get install virt-manager (图形界面)