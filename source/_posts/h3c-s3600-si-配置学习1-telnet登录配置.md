---
title: H3C S3600-SI 配置学习1---telnet登录配置
tags:
  - 未分类
id: '189'
abbrlink: 1399434713
date: 2011-11-22 10:55:00
---

system-view  
  interface vlan-interface 3                 #创建vlan-interface 3 接口用于登录所使用的IP地址  
  ip address 192.168.0.72 24             #24为子网掩码  
  quit  
  
user-interface vty 0 4                         #0-4 共5个接口  
  user privilege level 3                        #可使用所有命令