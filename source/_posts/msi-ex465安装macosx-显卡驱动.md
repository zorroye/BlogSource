---
title: msi EX465安装MACOSX 显卡驱动
tags:
  - 未分类
id: '246'
date: 2013-12-08 13:49:00
---

原理：

> dsdt让系统知道有这个显卡
> 
> FB告诉系统该显卡是如何处理信号的。

我是按这帖子做的：ATI 5系和6系显卡驱动&修改FB探讨

具体步骤：

1、查看显卡信息。

> GPU-Z可以查看
> 
>   

2、将ID加入到ATI5000Controller.kext和AMDRadeonAccelerator.kext中

> 5470m的ID里面有，所以不需要添加
> 
>   

3、提取rom，修改你的接口信息

> 1、rom提取用aida64提取
> 
> 2、用radeon\_bios\_decode和redsock\_bios\_decoder提取显卡信息
> 
> ./radeon\_bios\_decode < 1002\_68E0.rom

> > ATOM BIOS Rom:
> 
> >         SubsystemVendorID: 0x1462 SubsystemID: 0x1043       
> 
> >         IOBaseAddress: 0xd800                                            
> 
> >         Filename: BR35393.012
> 
> >         BIOS Bootup Message:
> 
> > MSI MS1455 PARK S3 LP DDR3 64Mx16 512MB                                    
> 
> > PCI ID: 1002:68e0
> 
> > Connector at index 0
> 
> >         Type \[@offset 44904\]: LVDS (7)
> 
> >         Encoder \[@offset 44908\]: INTERNAL\_UNIPHY (0x1e)
> 
> >         i2cid \[@offset 44960\]: 0x90, OSX senseid: 0x1
> 
> > Connector at index 1
> 
> >         Type \[@offset 44914\]: VGA (1)
> 
> >         Encoder \[@offset 44918\]: INTERNAL\_KLDSCP\_DAC1 (0x15)
> 
> >         i2cid \[@offset 44983\]: 0x97, OSX senseid: 0x8

> ./redsock\_bios\_decoder < 1002\_68E0.rom

> > BR35393.012 :
> 
> > MSI MS1455 PARK S3 LP DDR3 64Mx16 512MB                                    
> 
> > Subsystem Vendor ID: 1462
> 
> >        Subsystem ID: 1043
> 
> > Object Header Structure Size: 140
> 
> > Connector Object Table Offset: 2a
> 
> > Router Object Table Offset: 0
> 
> > Encoder Object Table Offset: 6c
> 
> > Display Path Table Offset: 12
> 
> > Connector Object Id \[14\] which is \[LVDS\]
> 
> >         encoder obj id \[0x1e\] which is \[INTERNAL\_UNIPHY (osx txmit 0x10 \[duallink 0x0\] enc 0x0)\] linkb: false
> 
> > Connector Object Id \[5\] which is \[VGA\]
> 
> >         encoder obj id \[0x15\] which is \[INTERNAL\_KLDSCP\_DAC1 (osx txmit 0x00 enc 0x10?)\] linkb: false
> 
> 提取的信息如下：

>          txmit       enc      senseid
> 
> LVDS      10          00        01
> 
> VGA       00          10        08
> 
> LVDS前面部分

> > 02 00 00 00 40 00 00 00 09 01 00 00

> VGA前面部分

> > 10 00 00 00 10 00 00 00 00 01 00 00

> 得到参数：

> > LVDS 02 00 00 00 40 00 00 00 09 01 00 00 10 00 00 01
> 
> > VGA  10 00 00 00 10 00 00 00 00 01 00 00 00 10 01 08

> > #紫色表示显示输出顺序，00表示最优先输出

> 整理得到最终参数

> > 0200000040000000090100001000000110000000100000000001000000100108

> 3、我们选用Zonalis参数

> > 我把5系列的参数基本上都试了一遍，最后才试到这个6接口的参数，坑爹啊！

> > 000400000406000000710000200106060004000004060000007100001000050500040000040600000071000021030204000400000406000000710000110201030004000004060000007100002205040200040000040600000071000012040301
> 
> > 我的只有2个接口，其他全部用0替代得到
> 
> > 020000004000000009010000100000011000000010000000000100000010010800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

> 4、我们更改ATI5000Contrller.kext>Contents>MacOS> ATI5000Contrller

> > 用0XED打开，选16进制，搜索Zonalis参数，替换为下面的参数，保存即可
> > 
> >   

4、笔记本A卡，且senseid为07

> 这一步就是改EDID，识别显示器用的，本LVDS接口是01，所以跳过  
> edid只是解决花屏或显示器识别问题，能正常进入桌面，说明edid暂时没什么问题。  
> 
>   

5、加载你修改的FB

> 这一步就是改dsdt.aml。用DSDTSE修改
> 
> 1、用IDSDT将dsdt和rom信息写在一起
> 
> 2、更改相关参数

> > ATY后面原参数是Motmot。然后搜索Motmot，替换为Zonalis 
> 
> > 再搜索ATY，往下拉，将@0,name，@1,name的ATY,Display-A、ATY,Display-B
> 
> > 之类的改为ATY,Zonalis。
> 
> > 将@0,name，@1,name，device\_type 的 Buffer（xxx）里面的数字删掉
> 
> > 备注：我只有两个接口，所以只到@1,name

> 3、点编译，生成新dsdt.aml。放入/Extra下面即可
> 
>   

6、重启查看已QE

> ![msi EX465安装MACOSX 显卡驱动 - leaf - ------坚持雅操------](http://img0.ph.126.net/9oQ4gEe614K_IX4ZZx3SAg==/1983835635956987556.jpg "msi EX465安装MACOSX 显卡驱动 - leaf - ------坚持雅操------")
> 
>   

> ![msi EX465安装MACOSX 显卡驱动 - leaf - ------坚持雅操------](http://img2.ph.126.net/ow1qdSInakYScXDN6dzkFg==/2074470578457543017.jpg "msi EX465安装MACOSX 显卡驱动 - leaf - ------坚持雅操------")
> 
>   
> 
>   

  

  

附：我改过的参数整理。

Aticonfig: Douc

ConnectorInfo count in decimal: 2

Disk offset in decimal 165856

    02  00  00  00  00  05  00  00  09  03  00  00  21  03  02  02

    00  04  00  00  04  02  00  00  00  03  00  00  11  02  01  01

  

0200000000050000090300002103020200040000040200000003000011020101

  

  

Aticonfig: Langur

ConnectorInfo count in decimal: 3

Disk offset in decimal 165904

    00  04  00  00  04  06  00  00  00  01  00  00  21  03  04  02

    00  04  00  00  04  06  00  00  00  01  00  00  11  02  01  01

    04  00  00  00  14  02  00  00  00  01  00  00  02  04  05  03

  

000400000406000000010000210304020004000004060000000100001102010104000000140200000001000002040503

  

  

Aticonfig: Hoolock

ConnectorInfo count in decimal: 3

Disk offset in decimal 166176

    00  04  00  00  04  06  00  00  00  01  00  00  21  03  05  01

    00  04  00  00  04  06  00  00  00  01  00  00  11  02  04  02

    04  00  00  00  14  02  00  00  00  01  00  00  02  04  01  03

  

000400000406000000010000210305010004000004060000000100001102040204000000140200000001000002040103

  

  

Aticonfig: Baboon

ConnectorInfo count in decimal: 3

Disk offset in decimal 166288

    04  00  00  00  14  00  00  00  00  01  00  00  01  02  01  03

    00  08  00  00  00  02  00  00  00  71  00  00  22  05  02  01

    10  00  00  00  10  00  00  00  00  01  00  00  00  10  00  02

  

040000001400000000010000010201030008000000020000007100002205020110000000100000000001000000100002

  

  

Aticonfig: Eulemur

ConnectorInfo count in decimal: 3

Disk offset in decimal 166336

    04  00  00  00  14  00  00  00  00  01  00  00  01  02  01  04

    00  08  00  00  00  02  00  00  00  71  00  00  12  04  04  02

    10  00  00  00  10  00  00  00  00  00  00  00  00  10  00  01

  

040000001400000000010000010201040008000000020000007100001204040210000000100000000000000000100001

  

  

Aticonfig: Galago

ConnectorInfo count in decimal: 2

Disk offset in decimal 166384

    02  00  00  00  00  01  00  00  09  03  00  00  21  03  02  02

    00  04  00  00  04  06  00  00  00  73  00  00  11  02  01  01

  

0200000000010000090300002103020200040000040600000073000011020101

  

  

Aticonfig: Colobus

ConnectorInfo count in decimal: 2

Disk offset in decimal 166432

    02  00  00  00  00  01  00  00  09  03  00  00  21  03  02  02

    00  04  00  00  04  06  00  00  00  73  00  00  11  02  01  01

  

0200000000010000090300002103020200040000040600000073000011020101

  

  

Aticonfig: Mangabey

ConnectorInfo count in decimal: 2

Disk offset in decimal 166480

    02  00  00  00  40  00  00  00  09  01  00  00  00  00  00  03

    00  04  00  00  04  06  00  00  00  73  00  00  11  02  01  01

  

0200000040000000090100000000000300040000040600000073000011020101

  

  

Aticonfig: Orangutan

ConnectorInfo count in decimal: 2

Disk offset in decimal 166608

    02  00  00  00  40  00  00  00  09  01  00  00  00  00  00  05

    00  04  00  00  04  06  00  00  00  73  00  00  11  02  01  01

  

0200000040000000090100000000000500040000040600000073000011020101

  

  

Personality: Nomascus

ConnectorInfo count in decimal: 4

Disk offset in decimal 169072

    02  00  00  00  40  00  00  00  09  01  00  00  00  00  00  05

    02  00  00  00  00  01  00  00  09  03  00  00  12  04  03  03

    00  04  00  00  04  06  00  00  00  73  00  00  11  02  01  01

    00  04  00  00  04  07  00  00  00  73  00  00  21  03  02  02

  

02000000400000000901000000000005020000000001000009030000120403030004000004060000007300001102010100040000040700000073000021030202

  

  

Personality: Vervet

ConnectorInfo count in decimal: 4

Disk offset in decimal 168752

    00  04  00  00  00  04  00  00  00  71  00  00  12  04  04  02

    04  00  00  00  14  00  00  00  00  71  00  00  01  12  01  04

    00  02  00  00  14  00  00  00  00  71  00  00  00  00  06  03

    00  08  00  00  00  02  00  00  00  71  00  00  22  05  05  01

  

00040000000400000071000012040402040000001400000000710000011201040002000014000000007100000000060300080000000200000071000022050501

  

  

Personality: Alouatta

ConnectorInfo count in decimal: 4

Disk offset in decimal 168640

    02  00  00  00  00  01  00  00  09  01  00  00  12  04  03  03

    00  04  00  00  04  06  00  00  00  71  00  00  11  02  01  01

    00  04  00  00  04  06  00  00  00  71  00  00  21  03  02  02

    00  04  00  00  04  06  00  00  00  71  00  00  22  05  04  04

  

02000000000100000901000012040303000400000406000000710000110201010004000004060000007100002103020200040000040600000071000022050404

  

  

Personality: Uakari

ConnectorInfo count in decimal: 4

Disk offset in decimal 168480

    00  04  00  00  00  04  00  00  00  71  00  00  12  04  04  01

    04  00  00  00  14  00  00  00  00  71  00  00  01  12  01  03

    00  02  00  00  14  00  00  00  00  71  00  00  00  00  06  05

    00  08  00  00  00  02  00  00  00  71  00  00  22  05  05  04

  

00040000000400000071000012040401040000001400000000710000011201030002000014000000007100000000060500080000000200000071000022050504