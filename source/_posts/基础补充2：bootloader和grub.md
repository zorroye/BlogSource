---
title: 基础补充2：bootloader和GRUB
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '83'
abbrlink: 1588026503
date: 2013-04-09 10:49:00
---

磁道结构：  
bootloader-partition table-magic number ---stage1.5---分区(boot sector(512B)+存储区域)  
|<---------------MBR------------------------->|  
  
bootloader功能：stage1  

> 加载扇区：各扇区之间切换  
> 加载核心：通过stage1.5---读取stage2---配置文件---核心  

  
GRUB：  

> MBR和stage1的区别  
> 
> ![基础补充2：bootloader和GRUB - leaf - ------坚持雅操------](http://img1.ph.126.net/GQptpHNR7E4qcoZgLTaSaA==/6597161026123611847.png "基础补充2：bootloader和GRUB - leaf - ------坚持雅操------")  
>   
> 配置文件-核心加载方式  
> 链接加载  
> 
> > rootnoverify (hd0,0)   指定bootloader所在分区  
> > chainloader +1           指定为第一个扇区  
> 
>