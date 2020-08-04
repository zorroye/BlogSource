---
title: msi EX465安装MACOSX 声卡驱动
tags:
  - ex465
categories:
  - Hackintosh
  - ex465
id: '248'
abbrlink: 3100805840
date: 2013-12-09 14:16:00
---

本篇没有成功，只记录过程。

[http://bbs.pcbeta.com/viewthread.php?tid=623626&highlight=%2B%D7%CF%C3%D7](http://bbs.pcbeta.com/viewthread.php?tid=623626&highlight=%2B%D7%CF%C3%D7)

[http://bbs.pcbeta.com/viewthread-1017396-1-1.html](http://bbs.pcbeta.com/viewthread-1017396-1-1.html)

  

步骤如下：

1、提取声卡原始信息

2、摘取相关信息

3、得出 pin config，pathmap等数据

4、更改相关文件，对applehda打补丁

5、dsdt.aml文件更改

  

一、提取声卡信息

> 进ubuntu，使用root权限
> 
> cat /proc/asound/card0/codec#？ > Codec.txt
> 
>   

  
二、摘取 Address、Node、Pin Default 这三个数值

Codec: Realtek ALC662 rev1

Address: 0

Vendor Id: 0x10ec0662

0x14  0x0121141f: \[Jack\] HP Out at Ext Rear    Black          0x0c         OUT HP                 耳麦接口

0x18  0x01a11c20: \[Jack\] Mic at Ext Rear          Black         0x0e         IN VREF\_80            麦克风接口

0x19  0x99a3092f: \[Fixed\] Mic at Int ATAPI         Unknown   0X0c\* 0x0e   IN VREF\_80        电脑麦克风

0x1b  0x99130110: \[Fixed\] Speaker at Int ATAPI Unknown   0x0c 0X0e\*   OUT VREF\_HIZ   电脑扬声器

> 按下图更换位置

> ![msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------](http://img2.ph.126.net/GqH0lWiPCpSwkKmbW0yy7Q==/1837750123043916662.jpg "msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------")

0x14 1f 14 21 01 \[Jack\] HP Out at Ext Rear Black    0x0c OUT HP 耳麦接口

0x18 20 1c a1 01 \[Jack\] Mic at Ext Rear Black    0x0e IN VREF\_80 麦克风接口

0x19 2f 09 a3 99 \[Fixed\] Mic at Int ATAPI Unknown 0X0c\* 0x0e IN VREF\_80 电脑麦克风

0x1b 10 01 13 99 \[Fixed\] Speaker at Int ATAPI Unknown 0x0c 0X0e\* OUT VREF\_HIZ 电脑扬声器

备注：其他接口由于是N/A，所以全部加屏蔽即可

  

三-一、ConfigData

> 第一位代表关联的设备(仅针对多声道)

> > HP是5
> 
> > 外置麦克风按line in设置： 2
> 
> > 内置麦克风按mic设置：1
> 
> > 扬声器按intspeaker设置：4
> 
> 第二位设置声道有关
> 
> 这边全部设置为0

第三位代表接口颜色

black 1 unknown 0

1

1

0

0

> 第四位设置是否侦测插口

侦测 0  不侦测 1

0

0

1

1

第五位表示设备类型

HP2

line in8

mica

扬声器1

第六位表示连接类型

笔记本保持原样

1

1

3

3

第七位表示是否有插孔和插孔位置

外接 0 内置 9

0

0

9

9

第八位表示插口所在位置

内置和屏蔽 0 其余为1

1

1

0

0

得出

1450 10 21 01

1820 10 81 01

 1910 01 a3 90

1b40 01 13 90

屏蔽代码 f0 00 00 40

  

按下图整理出最终数据。因有EAPD，加入代码01470c02

> ![msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/4_V10ARmiHyjLIlgcun-YA==/1994531685072004159.jpg "msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------")

  

01471c50 01471d10 01471e21 01471f01 01571cf0 01571d00 01571e00 01571f40 01671cf0 01671d00 01671e00 01671f40 01871c20 01871d10 01871e81 01871f01 01971c10 01971d01 01971ea3 01971f90 01a71cf0 01a71d00 01a71e00 01a71f40 01b71c40 01b71d01 01b71e13 01b71f90 01c71cf0 01c71d00 01c71e00 01c71f40 01d71cf0 01d71d00 01d71e00 01d71f40 01e71cf0 01e71d00 01e71e00 01e71f40 01470c02  
 备注：需要一行写完，不能有回车

  

  

三-二、PathMap

> http://bbs.pcbeta.com/viewthread-613358-1-1.html

> ![msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/l06WX7v8qTr75TuNKC2P_w==/6597629418076920580.jpg "msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------")
> 
> 原则：输入是从后往前推断节点，输出是从前往后推
> 
>   
> 
> 下载工具graphviz，codecgraph
> 
> 运行命令   ./codecgraph codec.txt ，然后用AI导出png图片
> 
> ![msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------](http://img1.ph.126.net/uJcIWiNYKGMqIpSjIOuF2w==/3016848800485121575.png "msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------")
> 
>  可以很清楚的看出节点图，按codec图找也是差不多的。
> 
> 140c02
> 
> 092218
> 
> 082319
> 
> 1b0e04
> 
>   

四、更改相关文件

更改的文件包括AppleHDAHardwareConfigDriver.kext/Contents下面的Info.plist、layout86.xml、Platforms.xml、applehda打补丁。

其中applehda打补丁

可以下载PATCHHDA打，或者用0XDE将885改成662即可

sudo perl -pi -e 's|\\x85\\x08\\xec\\x10|\\x62\\x06\\xec\\x10|g' /System/Library/Extensions/AppleHDA.kext/Contents/MacOS/AppleHDA

>   

五、dsdt.aml文件修改

用voodoohda，然后查看在哪个节点，我的是HDA，

然后改HDA这个节点，将HDA改成HDEF(有2处)

用IDSDT生成dsdt代码，然后再改

dsdt代码如下：method部分

            Device (HDEF)            {                Name (\_ADR, 0x000F0000)                Method (\_DSM, 4, NotSerialized)                {                    Store (Package (0x08)                        {                            "codec-id",                             Buffer (0x04)                            {                                0x62, 0x06, 0xEC, 0x10                            },                             "layout-id",                             Buffer (0x04)                            {                                0x96, 0x02, 0x00, 0x00                            },                             "device-type",                             Buffer (0x0F)                            {                                "Realtek ALC662"                            },                             "PinConfigurations",                             Buffer (Zero) {}                        }, Local0)                    DTGP (Arg0, Arg1, Arg2, Arg3, RefOf (Local0))                    Return (Local0)                }

>   

六、关于pinconfigurations

dsdt 改pinconfigurations 可以在系统信息里面显示声卡信息。具体更改如下

         "PinConfigurations", 

 Buffer (0x28) 

 {0x50, 0x10, 0x21, 0x01, 0xF0, 0x00, 0x00, 0x40, 

0xF0, 0x00, 0x00, 0x40, 0x20, 0x10, 0x81, 0x01, 

0x10, 0x01, 0xA3, 0x90, 0xF0, 0x00, 0x00, 0x40, 

0x40, 0x01, 0x13, 0x90, 0xF0, 0x00, 0x00, 0x40, 

0xF0, 0x00, 0x00, 0x40, 0xF0, 0x00, 0x00, 0x40 }

备注：代码就是上面得出的代码

显示如下

![msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------](http://img0.ph.126.net/K64uUlyS4T_yY8_kyZFrWw==/860750478881228391.jpg "msi EX465安装MACOSX 声卡驱动 - leaf - ------坚持雅操------")