---
title: 8、修改FakeSMC
tags:
  - hackintosh
categories:
  - Hackintosh
  - 安装
id: '244'
abbrlink: 1736323804
date: 2013-03-20 22:50:00
---

  
  
FakeSMC文件设置的机型必须与smbios.plist相对应  

![8、修改FakeSMC - leaf - ------坚持雅操------](http://img1.ph.126.net/F37VbXMBZhbqtXX_AOEqSw==/6598098909540862129.png "8、修改FakeSMC - leaf - ------坚持雅操------")

   
REV值设定：  
        MacPro3,1                1.25f4        ASUPAAAE  
        MacPro4,1                1.39f5        ATkPAAAF  
        MacPro5,1                1.39f11        ATkPAAAR  
        iMac8,1                1.30f1        ATAPAAAB  
        iMac9,1                1.45f0        AUUPAAAA  
        iMac10,1                1.53f13        AVMPAAAT  
        iMac11,1                1.54f36        AVQPAAA2  
        iMac12,1                1.72f5        AXIPAAAF     
        MacBookPro5,1        1.33f8        ATMPAAAI  
        MacBookPro5,1        1.33f8        ATMPAAAI  
        MacBookPro6,1        1.58f16        AVgPAAAW  
        MacBookPro7,1        1.62f6        AWIPAAAG  
        MacBookPro8,1        1.68f96        AWgPAACW  
  
smc-compatible值设定：  
        MacPro3,1                smc-napa  
        MacPro4,1                smc-thurley  
        MacPro5,1                smc-thurley  
        iMac9,1                smc-napa  
        iMac10,1                smc-mcp  
        iMac11,1                smc-piketon  
        iMac12,1                smc-huronriver     
        MacBookPro5,1        smc-mcp  
        MacBookPro5,5        smc-mcp  
        MacBookPro6,1        smc-piketon  
        MacBookPro7,1        smc-mcp  
        MacBookPro8,1        smc-huronriver  
  
tjmax值设定：  

> 通过aida64extreme查看，CPU最高工作温度  
>   

参考：  

> http://bbs.pcbeta.com/viewthread-799385-1-1.html  
> http://bbs.pcbeta.com/viewthread-973896-1-1.html