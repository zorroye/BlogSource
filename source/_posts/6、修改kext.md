---
title: 6、修改KEXT
tags:
  - hackintosh
categories:
  - Hackintosh
  - ex465
id: '242'
abbrlink: 2385987775
date: 2013-03-20 22:40:00
---

驱动ATI显卡的一般步骤  

> 1、确认你的显卡ID，可以通过win下的GPU-Z确定  

> 2、添加ID到相关kext里的Info.plist里面  
> 3、提取rom修改你的接口信息  
> 4、修改ATIx000Contrller.kext>Contents>MacOS> ATIx000Contrller文件 (解决输出问题)  
> 5、加载你修改的FB

>   

  
第2步说明：  

> ATI显卡必备驱动  
> 　　ATI4600Controller.kext （加入ID）  
> 　　ATIFramebuffer.kext  
> 　　ATISupport.kext  
> 　　ATIRadeonX2000.kext （确认有ID）  
> 　　ATIRadeonX2000GA.plugin  
> 　　ATIRadeonX2000GLDriver.bundle  
> 　　ATIRadeonX2000VADriver.bundle  

  

> 参考：  
> [Thinkpad E40 ML 完善过程分享](http://bbs.pcbeta.com/viewthread-1017396-1-1.html)  
> [ThinkPad E40黑苹果折腾大结局](http://bbs.pcbeta.com/viewthread-1196057-1-1.html)  

>   
>   

第4步说明：  

> 各接口代码前端：  

> > LVDS：02 00 00 00 40 00 00 00 09 01 00 00  
> > HDMI：00 08 00 00 04 02 00 00 00 71 00 00  
> > VGA： 10 00 00 00 10 00 00 00 00 01 00 00  
> > DVI：   04 00 00 00 14 02 00 00 00 01 00 00  
> > DP：    00 04 00 00 04 06 00 00 00 71 00 00  
> 
> 后端：  
> 
> > txmit enc hotplugin senseid 还有8位  

> 代码生成器：  
> 
> > BuildFramebuffer.app  
> 
>   
> 参考：  

> [ATI 5系和6系显卡驱动&修改FB探讨](http://bbs.pcbeta.com/viewthread-1060313-1-1.html)  
> [从零开始完美玩转苹果ATI驱动+QE/CI+多屏](http://bbs.pcbeta.com/viewthread-991835-1-1.html) ：这篇讲原理，不懂可以看下面  
> [可以驱动所有ATI 4330](http://bbs.pcbeta.com/viewthread-937823-1-1.html)  
>