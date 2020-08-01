---
title: 无线ap端口需要配置access模式
tags:
  - 未分类
id: '317'
abbrlink: 2171983291
date: 2016-09-12 00:31:00
---

interface gigabitethernet 0/0/46  
port link-type access  
port default vlan 22  
  
  
  
  
  
trunk模式配置  
interface gigabitethernet 0/0/46  
port link-type trunk  
port trunk allow vlan all  
undo port trunk allow vlan 1