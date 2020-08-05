---
title: 3、相关工具、kext说明
tags:
  - hackintosh
categories:
  - Hackintosh
  - base
id: '239'
abbrlink: 3969467101
date: 2013-03-20 21:30:00
---

  
下载地址：http://pan.baidu.com/share/link?shareid=436698&uk=336411764  
按照制作过程列出  
\---------------------------  
1、制作启动盘工具  

> DiskGenius：用于分区、格式化  
> BOOTICE：制作引导盘，用来引导mac镜像  
> 硬盘安装助手：制作镜像盘，用来将mac镜像写入U盘，使U盘成为安装盘  
> Mac Drive：windows下读写HFS分区，用于修改镜像盘。  
> HFSExploer：也是windows下读写HFS分区，用于修改镜像盘。

  
2、修改镜像  

> NullCPUPowerManagement.kext  关闭ACPI电源管理的驱动  
> AppleACPIPS2Nub.kext                用于支持PS2的鼠标键盘  
> ApplePS2Controller.kext               用于支持PS2的鼠标键盘  
> FakeSMC.kext（2.5版）  
> \-------  
> myfix：用于修复文件权限  
> \---------------  
> 安装过程要增删kext，在win下操作的话win下的读写工具就用上了。  
>   

  
3、第一次进系统  

> Chameleon\_2.2svn\_r2187\_trunk.pkg 变色龙引导工具，使硬盘自己引导启动  
> 把/E/E下的kext拷到/S/L/E下  
>   

4、安装驱动工具  

> 一般工具  
> 
> > MultiBeast ：一些工具和驱动集合  
> > System Info.app 检查系统驱动了那些硬件，加载了那些kext  
> > ShowAllFiles.app：查看隐藏文件  
> > Chameleon Wizard ：创建org.apple.Boot.plist、SMBIOS等  
> 
>   
> Kext工具  
> 
> > Kext Wizard ：安装kext驱动工具  
> > ATI Tools ：导出端口参数的工具  
> > HexEdit ：修改端口参数的工具  
> > PlistEditPro：修改plist文件的工具  
> 
>   
> DSDT相关工具  
> 
> > aida64extreme：导出主板和gpu的SMBIOS工具  
> > IORegistryExplorer：查看系统加载的kext工具  
> > DSDTFixer.app ：修复原始aml文件  
> 
> > DSDT\_Editor：编辑、修复、导出DSDT.AML工具  
> > iDSDT：添加显卡、声卡信息到aml文件。(亦可手动添加)  
> >   
> 
>   

5、查看日志  

> bdmesg：查看变色龙的运行日志  
> Chameleon Wizard：也内置了bdmesg，也可以很方便的查看  
> dmesg：查看mac启动记录  
> 控制台：点kernel.log

  
  
  
KEXT说明  
\-------------------  

> FakeSMC.kext：                              黑苹果必要kext，模拟苹果设备  
> NullCPUPowerManagement.kext     禁用电源管理的kext  
> AppleACPIPS2Nub.kext                   PS2键盘鼠标驱动  
> ApplePS2Controller.kext                   PS2键盘鼠标驱动  
> \----------------------------  
> AppleIntelPIIXATA.kext　　　Intel免AHCI专用kext  
> AppleATIATA.kext　　　　　AMD芯片组专用kext(2009.12.30)  
> AppleATIPATA.kext　　　　  AMD芯片组专用kext  
> AppleNForceATA.kext　　　 NForce芯片组专用kext  
> AppleVIAATA.kext　　　　　VIA芯片组专用kext  
> JMicronATA.kext　　　　　  JMicron芯片组专用kext  
> AppleVIAATA.kext.for.sis　　SIS芯片组专用kext  
> \---------------------------  
> ElliottForceLegacyRTC.kext或者LegacyAppleRTC.kext   防止主板BIOS的CMOS重置（2选1，不可共用）  
> OpenHaltRestart.kext或者EvOreboot.kext              解决重启/关机时遇到无法断电问题（2选1，不可共用）  
> PlatformUUID.kext　　　　　解决Unable to determine UUID for host. Error : 35的问题  
> AppleACPIPlatform.kext         据说能解决：DSMOS has arrived错误  
> 待续。。。。  

  
  
  
推荐网站  

> http://www.osx86.net/  
>