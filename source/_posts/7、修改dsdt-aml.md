---
title: 7、修改DSDT.aml
tags:
  - 未分类
id: '243'
date: 2013-03-20 22:40:00
---

  
\-------------------------------------------------------------------------  
DSDT.aml其实就是BIOS的SMBIOS文件。非SMBIOS.plist  
\-------------------------------------------------------------------------  
  
一、导出DSDT、rom、SSDT等文件  

> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img0.ph.126.net/Hkeiwfr8E2D2xJrDqtVT9Q==/6597780051168992133.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")  
> 
>  ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img0.ph.126.net/tmoDqi_-R75xXbrSFGmAFQ==/6597540357634133052.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")  
> 1、ACPI tool 可以导出DSDT.bin 和多个SSDT.bin。我们直接把后缀改位aml即可  
> 2、video debug可以调出：显卡.rom  

  
  
二、修改DSDT.aml  

> 我一般直接用这个软件修复，也可以使用DSDTFixer先修复，再用DSDT\_editor修复  
> 1、点open打开DSDT.aml文件  
> 
> > 备注：DSDT\_editor也可以直接导出DSDT的原始文件。  
> 
> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img2.ph.126.net/bReZkoDf67zj1mwdF2AXDA==/6597947176936422335.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
>  打开后显示如下：  

> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img2.ph.126.net/CdLWiuHPi2jp10c3b4S3FA==/6597929584750368650.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
> 2、 先自动修复,点fixerrors  
> 
> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img0.ph.126.net/qDKCGKFcOn21ltMW0v7mAA==/6597716279494574346.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
>  3、我碰到了3种警告  
> 
> > 1> 把 \_T\_0  替换为T\_0即可  
> > 2>Possible operator timeout is ignored  
> 
> > > 将 Acquire (MUTE, 0x03E8)改为Acquire (MUTE, 0xFFFF)
> 
> > 3>not all control paths return a value (SIOS)  
> > 
> > > 最下面的}之前插入一行，添加 Return (Zero)
> 
>     错误修复参考：http://roderickvincent.com/post/2012-03-11/40031714899  
>   
> 4、打补丁，DSDT\_editor里面包含很多补丁了。
> 
> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img2.ph.126.net/kQqqjra1PrQ6IowItxIRIw==/6597538158610877708.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
>    
> 
> 5、手动添加修改信息  
> 通过IORegisryExplorer看接口信息，然后在DSDT\_editor里面找到位置进行更改  
> 
> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img1.ph.126.net/9kwWBagc4x_BMCE_AQNNpQ==/6597754762401552568.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
> 参考：http://bbs.pcbeta.com/viewthread-1020621-1-1.html  
>   
> 6、导出aml文件即完成DSDT.aml  

  
  
三、添加显卡信息、声卡信息  

> 用iDSDT导入DSDT.aml 和显卡.rom文件，声卡coder信息  
> iDSDT会自动帮我们导出aml文件。  
> 
> ![7、修改DSDT.aml - leaf - ------坚持雅操------](http://img1.ph.126.net/AdfJVcEiujL8f2M1158a2Q==/6597292967517383413.jpg "7、修改DSDT.aml - leaf - ------坚持雅操------")
> 
> 注意：iDSDT导出来的文件是放在桌面上的，若名字相同导出来的aml文件就没用了  
>   
> 推荐：  
> http://bbs.pcbeta.com/viewthread.php?tid=832974  
> http://bbs.pcbeta.com/viewthread-826965-1-1.html  

  
  
四、修改SSDT.aml  

> 用DSDT\_editor文件修复好即可。导出aml文件  
>   
>   

五、将这些文件放入/Extra文件夹下，配置变色龙添加文件地址即可。