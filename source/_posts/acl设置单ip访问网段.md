---
title: ACL设置单IP访问网段
tags:
  - 未分类
id: '321'
abbrlink: 884278273
date: 2016-09-28 17:31:00
---

acl 3005

rule permit ip source 10.1.11.0 0.0.0.255 destination 10.1.21.0 0.0.0.255

rule permit ip source 10.1.11.0 0.0.0.255 destination 10.1.22.0 0.0.0.255

rule permit ip source 10.1.11.0 0.0.0.255 destination 10.1.31.0 0.0.0.15

rule permit ip source 10.1.11.0 0.0.0.255 destination 10.1.32.0 0.0.0.15

rule permit ip source 10.1.11.0 0.0.0.255 destination 10.1.252.0 0.0.0.63

  

  

acl 3006

rule permit ip source 10.1.11.21 0 destination 10.1.21.0 0.0.0.255

rule permit ip source 10.1.11.21 0 destination 10.1.22.0 0.0.0.255

rule permit ip source 10.1.11.21 0 destination 10.1.31.0 0.0.0.15

rule permit ip source 10.1.11.21 0 destination 10.1.32.0 0.0.0.15

rule permit ip source 10.1.11.21 0 destination 10.1.252.0 0.0.0.63

  

  

traffic classifier vlan11c1 

if-match acl 3005

  

traffic classifier vlan11c2 

if-match acl 3006

  

  

  

traffic behavior vlan11b1

deny

  

traffic behavior vlan11b2

permit

  

  

  

traffic policy vlan11p1

classifier vlan11c2 behavior vlan11b2

classifier vlan11c1 behavior vlan11b1

  

vlan 11

traffic-policy vlan11p1 inbound