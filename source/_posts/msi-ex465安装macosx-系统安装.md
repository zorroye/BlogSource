---
title: msi EX465安装MACOSX 系统安装
tags:
  - ex465
categories:
  - Hackintosh
  - ex465
id: '245'
abbrlink: 1858804712
date: 2013-12-08 13:35:00
---

备注：显卡方法适用10.9.5以下，不适合10.10。

  

电脑配置如下：

> 处理器英特尔 酷睿2 双核 P8700 @ 2.53GHz 笔记本处理器
> 
> 主板微星 MS-1455 (矽统 672DX)+ SIS968
> 
> 内存4 GB ( 海力士 DDR2 800MHz / 金泰克 DDR2 800MHz )
> 
> 硬盘希捷 ST500LT012-9WS142 ( 500 GB / 5400 转/分 )
> 
> 硬盘西数 WDC WD3200BEVT-22A23T0 ( 320 GB / 5400 转/分 )
> 
> 硬盘日立 ( 500 GB / 5400 转/分 )
> 
> 显卡ATI Mobility Radeon HD 5470  ( 1 GB / 微星 )
> 
> 显示器三星 SEC3050 ( 14.7 英寸 )
> 
> 声卡瑞昱 ALC662 @ 矽统 Azalia Audio Controller
> 
> 网卡矽统 191 100/10 Ethernet Adapter / 微星
> 
> 无线网卡雷凌 RT2870
> 
> 蓝牙motolola
> 
> USBPNY 8G
> 
>   

0、硬件准备工作：

> 1、因BIOS无法设置AHCI，导致无法U盘安装，只能硬盘安装
> 
> 2、我准备了3个硬盘，分别用来安装winxp，macosx，ubuntu。

> > 2.1、win盘分出10G的FAT32盘，制作安装盘。后用DiskGenius将FAT32的OC改为AF

> 3、笔记本我把光驱位拆了，装了一块用于安装macosx的硬盘
> 
> 4、我要安装的是单系统，所以安装盘做在winxp这块硬盘的第二个主分区上
> 
> 5、U盘和winxp安装变色龙都可以引导
> 
>   

1、软件准备工作：  

> SIS芯片需要专用KEXT，AppleVIAATA.kext.for.sis.SATA 就这一个即可
> 
> 无法U盘安装，会提示still waiting for root device错误。只能硬盘分出一个区做安装盘。
> 
> win版变色龙启动有时候会提示：NullCPUPowerManagement.kext::start。重启重引导即可。
> 
> 需要使用参数npci=0x2000 -v ,不然会卡在PCI configure begin
> 
> 做WIN+MAC的话需要将MAC分区设置为逻辑分区，做主分区会导致无法选取分区。
> 
> 将BIOS的Legacy USB support设置为Disable。不然会提示
> 
> Echi controller unable to take control from bios (这个在新版已不需要设置)
> 
> 准备的kext有这些：
> 
> NullCPUPowerManagement.kext
> 
> OpenHaltRestart.kext
> 
> ElliottForceLegacyRTC.kext
> 
> PlatformUUID.kext
> 
> AppleVIAATA.kext.for.sis.SATA
> 
> FakeSMC.kext
> 
> AppleACPIPS2Nub.kext
> 
> ApplePS2Controller.kext
> 
> 放入安装盘的/Extra/Extensions下。另/Extra下不需要smbios和com文件
> 
> 不需要删除CPUPowerManagement.kext
> 
>   

2、系统安装：  

> 1、U盘引导或win版变色龙引导，输入npci=0x2000 -v -x -f启动。
> 
> 2、系统安装非常顺利，20多分钟搞定。
> 
> 3、然后进windows，
> 
> 将上面的KEXT放入MAC系统的/System/Library/Extensions
> 
> 将myfix放入/usr/sbin/下
> 
> 4、重启，输入npci=0x2000 -v -x -f -s进单用户模式
> 
> 用myfix修复权限，重启，输入npci=0x2000 -v 即可进入系统。

这时电脑的状态是显卡，声卡，网卡都没驱动。  

>   

3、安装变色龙实现自启动

> 由于硬盘是4K的，重启后有这个提示：boot0 ERROR

> 安装ubuntu盘，进ubuntu

> 下载boot1h文件：http://bbs.pcbeta.com/viewthread-971434-1-1.html
> 
> 切换到root权限：sudo su
> 
> 输入
> 
> dd if=/media/MACOSX/Extra/boot1h of=/dev/sdb2 bs=4096
> 
> \#                    mac分区卷标                               安装在第二个分区

> ![msi EX465安装MACOSX 系统安装 - leaf - ------坚持雅操------](http://img2.ph.126.net/gbQbtznL-OLI296DJFiclA==/1956251088239247869.png "msi EX465安装MACOSX 系统安装 - leaf - ------坚持雅操------")

  

4、安装驱动

> 网卡：
> 
> 将BIOS的Legacy USB support设置为Disable。
> 
> 安装雷凌原版驱动即可
> 
> 建议购买原装无线网卡，AR9380。

>   
> 
> 声卡：

> 移除APPLEHDA，加入VoodooHDA即可。仿冒驱动还在研究中。。。。

>   
> 
> 显卡驱动见后篇。
> 
>   

5、DSDT提取和修改

> win、linux、MAC下导出的DSDT文件应该都是一样的。
> 
> 使用DSDTEditor导出和除错。
> 
> ubuntu下:
> 
> sudo apt-get install acpidump iasl
> 
> sudo acpidump -t DSDT -b > dsdt.aml
> 
> http://bbs.pcbeta.com/viewthread-1133482-1-1.html
> 
>   
> 
> 修改方面，我碰到3个方面的错误
> 
> Not all control paths return a value (XXX)
> 
> 解决：Return (Zero)
> 
> Possible operator timeout is ignored
> 
> 解决：将 Acquire (MUT0, 0x0FFF)或者Acquire (MUTE, 0x03E8) 的参数修改为 0xFFFF
> 
> 还个就是删除 \_  即可
> 
> 然后保存为dsdt.aml，放入/Extra下，然后编辑org，加入dsdt.aml的路径即可
> 
>   

本篇到此结束，下篇就是显卡驱动。