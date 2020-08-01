---
title: LFS中使用rpm有关问题
tags:
  - 未分类
id: '223'
date: 2012-10-07 10:13:00
---

转载：  
http://www.linuxfromscratch.org/hints/downloads/files/rpm.txt  
http://hi.baidu.com/manbuzhe2009/item/94ba0f2af1bff4c6ee10f139  
[百度知道](http://zhidao.baidu.com/question/101700893.html&__bd_tkn__=6ea61a343c69dc25571ba779eca42cf6bd1388fd8078338d51fed8133ea5c69d362ad36bb4bcda3b39bb3949f6bbe47087ac3af56e60b1f4e7eb6015795cfc359d67a1f15d0f03de01252778dc32be0a4a739e7e0a2fba88a03f37087d2e372ecf6f7f323cb5a8a8e97d89accbdc8d02ce3226fe4faa)  
  
LFS虽然能安装rpm之类的包管理软件，但是由于建LFS是源码建的，所以rpm数据库中就不包含这些源码建的包，  
这就导致用软件包管理系统在安装软件包的时候，会因为依赖关系不足而无法安装。  
  
做好临时系统后直接勇rpm或者deb进行制作目标系统不知道是不是可以做出含包管理软件的目标系统