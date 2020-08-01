---
title: ACL设置网段不能互访
tags:
  - 未分类
id: '322'
abbrlink: 760246906
date: 2016-09-28 17:32:00
---

vlan21

acl name acl-vlan21 3010

rule deny ip source 10.1.21.0 0.0.0.255 destination 10.1.22.0 0.0.0.255

rule deny ip source 10.1.21.0 0.0.0.255 destination 10.1.31.0 0.0.0.15

rule deny ip source 10.1.21.0 0.0.0.255 destination 10.1.32.0 0.0.0.15

rule deny ip source 10.1.21.0 0.0.0.255 destination 10.1.252.0 0.0.0.63

traffic-filter vlan 21 inbound acl name acl-vlan21

  

  

  

vlan22

acl name acl-vlan22 3015

rule deny ip source 10.1.22.0 0.0.0.255 destination 192.168.1.0 0.0.0.255

rule deny ip source 10.1.22.0 0.0.0.255 destination 10.1.31.0   0.0.0.15

rule deny ip source 10.1.22.0 0.0.0.255 destination 10.1.32.0   0.0.0.15

rule deny ip source 10.1.22.0 0.0.0.255 destination 10.1.128.0  0.0.0.63

rule deny ip source 10.1.22.0 0.0.0.255 destination 10.1.252.0  0.0.0.63

traffic-filter vlan 22 inbound acl name acl-vlan22

  

  

  

vlan31

acl name acl-vlan31 3020

rule deny ip source 10.1.31.0 0.0.0.15 destination 10.1.32.0   0.0.0.15

rule deny ip source 10.1.31.0 0.0.0.15 destination 10.1.128.0  0.0.0.63

rule deny ip source 10.1.31.0 0.0.0.15 destination 10.1.252.0  0.0.0.63

traffic-filter vlan 31 inbound acl name acl-vlan31

  

  

  

vlan32

acl name acl-vlan32 3025

rule deny ip source 10.1.32.0 0.0.0.15 destination 10.1.128.0  0.0.0.63

rule deny ip source 10.1.32.0 0.0.0.15 destination 10.1.252.0  0.0.0.63

traffic-filter vlan 32 inbound acl name acl-vlan32

  

  

  

vlan128

acl name acl-vlan128 3030

rule deny ip source 10.1.128.0 0.0.0.63 destination 10.1.252.0  0.0.0.63

traffic-filter vlan 128 inbound acl name acl-vlan128

  

  

  

vlan252

无