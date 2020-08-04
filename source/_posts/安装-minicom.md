---
title: 安装 minicom
tags:
  - ubuntu
categories：
  - Ubuntu
  - 基础
id: '186'
abbrlink: 2051443138
date: 2011-02-25 13:56:00
---

公司有台h3c s3600 闲置，刚好拿来练习用  
1、安装  
sudo apt-get install minicom  
  
2、配置  
sudo minicom -s  
选择Serial port setup。设置A,B,E等为如下所示，并保存。 A -    Serial Device      : /dev/ttyUSB0    #直接插com口就用/dev/ttyS0,com转usb接口就用/dev/ttyUSB0 B - Lockfile Location     : /var/lock                                   
     C -   Callin Program      :                                            
     D -  Callout Program      :                                            
     E -    Bps/Par/Bits       : 9600 8N1                                   
     F - Hardware Flow Control : Yes                                         
     G - Software Flow Control : No   
设置“Modem and dialing”，将A,B,K这三项的值去掉。  
  
3、相关命令及快捷键  
\-、保存屏幕的所有显示 minicom -C 文件名  
     或者 minicom 登录后再快捷键 CTRL+a 再输入l 会提示输入要保存的文件名，保存位置为当前文件夹  
\-、  
ctrl+a +z 显示帮助文件  
ctrl+a +o 配置串口  
ctrl+a +x 退出  
ctrl+a +c 清屏  
ctrl+a +k 刷新屏幕  
ctrl+a +j 挂起minicom  
  
  
参考：  
1、[linux超级终端](http://blog.csdn.net/olive10000/archive/2009/03/01/3946891.aspx)  
2、[minicom使用介绍](http://apps.hi.baidu.com/share/detail/17380252)