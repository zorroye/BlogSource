---
title: Eth-trunk 配置
tags:
  - 未分类
id: '320'
date: 2016-09-24 14:56:00
---

二层eth-trunk配置

#switchA

#建eth-trunk端口  
interface Eth-Trunk11  

>  description GE19 GE20 s5720-S5700S48P
> 
>  port link-type trunk
> 
>  port trunk allow-pass vlan 2 to 4094
> 
> #eth-trunk设置
> 
>  mode lacp
> 
>  max active-linknumber 2
> 
> #arp保护
> 
>  arp anti-attack rate-limit enable
> 
>  arp-miss anti-attack rate-limit enable

interface GigabitEthernet0/0/19  

>  eth-trunk 11
> 
>  lacp priority 100

interface GigabitEthernet0/0/20  

>  eth-trunk 11
> 
>  lacp priority 100

  

#switchB

#建eth-trunk端口

interface Eth-Trunk11  

>  port link-type trunk
> 
>  port trunk allow-pass vlan 2 to 4094
> 
> #eth-trunk设置
> 
>  mode lacp
> 
>  max active-linknumber 2

interface GigabitEthernet0/0/47  

>  eth-trunk 11

interface GigabitEthernet0/0/48  

>  eth-trunk 11

  

\--------------------------------------------------------------------------------------------------

  

三层eth-trunk配置

routeA

interface Eth-Trunk1

>  undo portswitch
> 
>  ip address 10.1.1.1 255.255.255.252
> 
>  mode lacp-static
> 
>  max active-linknumber 2

interface GigabitEthernet0/0/0

>  undo portswitch
> 
>  eth-trunk 1

interface GigabitEthernet0/0/1

>  undo portswitch
> 
>  eth-trunk 1

  

switchB

interface Eth-Trunk1

>  undo portswitch
> 
>  ip address 10.1.1.2 255.255.255.252
> 
>  mode lacp
> 
>  max active-linknumber 2

interface GigabitEthernet0/0/21

>  eth-trunk 1
> 
>  lacp priority 100

interface GigabitEthernet0/0/22

>  eth-trunk 1
> 
>  lacp priority 100