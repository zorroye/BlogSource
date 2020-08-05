---
title: 从网络接手server：1、网络启动server
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '268'
abbrlink: 461935396
date: 2010-09-17 10:42:00
---

1、BIOS设置：  
         power manager setup ---> wake-up by LAN/Ring ---> enable

  
2、系统开启远程唤醒功能：  
         1> 安装ethtool

> > sudo apt-get install ethtool

          2>开启唤醒功能

> > 查看：sudo ethtool eth0

> > > wake-on 为g时已开启，d表示禁用

> > 设置：sudo ethtool -s eth0 wol g

> > > 在rc.local里加入一句     ethtool -s eth0 wol g (这样每次启动就不用重新设置了)

          3>记录MAC地址：ifconfig 

  
 3、从本机网络启动server  
            1>安装wakeonlan  sudo apt-get install wakeonlan  
            2>开启命令 wakeonlan MAC  
  
参考：[http://hi.baidu.com/liuweigang525/blog/item/d0ccf902c4ec83e208fa93eb.html](http://hi.baidu.com/liuweigang525/blog/item/d0ccf902c4ec83e208fa93eb.html)