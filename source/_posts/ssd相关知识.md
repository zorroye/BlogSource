---
title: SSD相关知识
tags:
  - ssd
categories:
  - Hardware
  - storage
id: '44'
abbrlink: 3884163245
date: 2013-08-01 17:30:00
---

SSD的组成：主控芯片，缓存，闪存

  

1、主控芯片

> ![SSD相关知识 - leaf - ------坚持雅操------](http://img1.ph.126.net/PBRdzfUehbZ9lET3Tgr-cw==/6597671199518593636.jpg "SSD相关知识 - leaf - ------坚持雅操------")

>   

> sandforce：

> > 使用压缩算法。
> 
> > 特点是兼容性好，次品闪存也兼容，所以就导致质量参差不齐。

> > 一般金士顿、威刚啥的都用它。sf2281

> marvell：

> > 使用非压缩算法。
> > 
> > 特点：性能突出且稳定，在NADA出现问题后能够恢复数据
> > 
> > 一般浦科特、闪迪、美光都用他。9187、9175

> 参考：

> > [http://ssd.zol.com.cn/368/3683027.html](http://ssd.zol.com.cn/368/3683027.html)
> 
> > [http://www.pcpop.com/doc/0/674/674480\_all.shtml](http://www.pcpop.com/doc/0/674/674480_all.shtml)
> > 
> >   
> > 
> >   

2、缓存

> 缓存一般就是DDR2的和DDR3的。容量一般64m及以上。
> 
> 缓存能有效提高速度。

  

  

3、闪存

> ![SSD相关知识 - leaf - ------坚持雅操------](http://img2.ph.126.net/CGfP5pKJrW-gPi3kRTTDPQ==/1915155741639394541.png "SSD相关知识 - leaf - ------坚持雅操------")
> 
>  

> > onfi标准：

> > > 这个标准里面的2.0有个异步模式，是掉速的一个原因。
> > > 
> > > 使用异步模式是为了保护缺陷闪存，使得其能用的更久。但其速度50MB/S不如机械硬盘快

> > toggle标准：

> >   

> 参考：[http://ssd.zol.com.cn/350/3507628.html](http://ssd.zol.com.cn/350/3507628.html)

  

  

其他参数：

> 1、4K对齐

> > 现在硬盘的扇区都是4096B了，所以格式化的最小单位也设置为4096B。这样就算对齐了。

> 2、AHCI模式
> 
> 3、SATA3.0

  

  

本人笔记本SISM672DX+SIS968：

> 1、不支持双通道,已加了2G内存
> 
> 2、不支持AHCI模式
> 
> 3、支持FSB800MHZ以上的CPU：我已升级至P8700

坑爹啊！想升级SSD都升不了