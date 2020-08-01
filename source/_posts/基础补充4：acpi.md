---
title: 基础补充4：ACPI
tags:
  - 未分类
id: '85'
date: 2013-04-11 09:31:00
---

ACPI:由BIOS、硬件、操作系统共同支持来实现的  

> ![基础补充4：ACPI - leaf - ------坚持雅操------](http://img2.ph.126.net/Gpm_QaMIKP4DnkJXZW3caA==/3032611399098946130.jpg "基础补充4：ACPI - leaf - ------坚持雅操------")
> 
>    

ACPI的功能：略  

> IRQ的数目是通过ACPI来实现扩充的。  
>   

ACPI的各个状态  

> G0(正常)-----------------G1(睡眠)----------------G2(可网络唤醒等关机状态)---------G3(关机)  
> |S0                              |S1-S4                        |S5  
> |C/D/P State

  

> S State：  
> 
> > cat /proc/acpi/sleep  
> > 
> > > S0 S3 S4 S5  
> > 
> > \-------------------------  
> 
> > S0：正常状态  
> > S3：待机状态：STR：当前状态存储到内存，未关机  
> > S4：休眠状态：STD：当前状态存储到硬盘并关机，从新开机后回到关机前的状态  
> > S5：关机状态：包含G2、G3  
> 
>   
> C State：调CPU的状态，如CPU的电压，暂停CPU执行的指令  
> 
> > cat /proc/acpi/processor/CPU0/power  
> 
>   
> D State：调设备的用电量：屏幕亮度，空闲时关闭网卡等  
>   
> P State：调CPU的频率  
> 
> > cat /sys/devices/system/cpu/cpu0/cpufreq/scaling\_available\_frequencies  
> > 
> > > 2900000 2200000 1700000 800000  
> > 
> >   
> 
>