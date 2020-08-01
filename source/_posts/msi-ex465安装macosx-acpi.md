---
title: msi EX465安装MACOSX ACPI
tags:
  - 未分类
id: '247'
abbrlink: 2873657863
date: 2013-12-08 18:02:00
---

http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1098975

http://bbs.pcbeta.com/viewthread-594984-1-5.html

  

一、原生电源管理

1、加载AppleHPET

> 搜索PNP0103
> 
> 我的代码

                Device (HPET)

                {

                    Name (\_HID, EisaId ("PNP0103"))

                    Name (ATT3, ResourceTemplate ()

                    {

                        IRQNoFlags ()

                            {0}

                        IRQNoFlags ()

                            {8}

                        Memory32Fixed (ReadOnly,

                            0xFED00000,         // Address Base

                            0x00000400,         // Address Length

                            )

                    })

                    Name (ATT4, ResourceTemplate ()

                    {

                    })

                    Method (\_CRS, 0, NotSerialized)

                    {

                        If (LEqual (HPFL (), One))

                        {

                            Return (ATT4)

                        }

                        Else

                        {

                            Return (ATT3)

                        }

                    }

                    Method (\_STA, 0, NotSerialized)

                    {

                        If (LEqual (HPFL (), One))

                        {

                            Return (0x0A)

                        }

                        Else

                        {

                            Return (0x0F)

                        }

                    }

                }

> 改为

                Device (HPET)

                {

                    Name (\_HID, EisaId ("PNP0103"))

                    Name (ATT3, ResourceTemplate ()

                    {

                        IRQNoFlags ()

                            {0}

                        IRQNoFlags ()

                            {8}

                        Memory32Fixed (ReadOnly,

                            0xFED00000,         // Address Base

                            0x00000400,         // Address Length

                            )

                    })

                    Method (\_CRS, 0, NotSerialized)

                    {

                        Return (ATT3)

                    }

                    Method (\_STA, 0, NotSerialized)

                    {

                        Return (0x0F)

                    }

                }

> 重启后应该已加载AppleHPET
> 
>   

2、加载AppleLPC

> 搜索：Name (\_ADR, 0x00020000)
> 
> 一、在Device前加入以下代码

                Method (\_DSM, 4, NotSerialized)

                {

                    Store (Package (0x08)

                        {

                            "device-id",

                            Buffer (0x04)

                            {

                                 0xAC, 0x0A, 0x00, 0x00

                            },

> > >  "vendor-id", 

                            Buffer (0x04)

                            {

                                0xDE, 0x10, 0x00, 0x00

                            }, 

                            "IOName", 

                            Buffer (0x0D)

                            {

                                "pci10de,aac"

                            }, 

                            "name", 

                            Buffer (0x0D)

                            {

                                "pci10de,aac"

                            }

                        }, Local0)

                    DTGP (Arg0, Arg1, Arg2, Arg3, RefOf (Local0))

                    Return (Local0)

> 二、在dsdt头部的method模块前面加入以下代码
> 
> 备注：不加会出现DTGP错误

>     Method (DTGP, 5, NotSerialized)
> 
>     {
> 
>         If (LEqual (Arg0, Buffer (0x10)
> 
>                 {
> 
>                     /\* 0000 \*/   0xC6, 0xB7, 0xB5, 0xA0, 0x18, 0x13, 0x1C, 0x44,
> 
>                     /\* 0008 \*/   0xB0, 0xC9, 0xFE, 0x69, 0x5E, 0xAF, 0x94, 0x9B
> 
>                 }))
> 
>         {
> 
>             If (LEqual (Arg1, One))
> 
>             {
> 
>                 If (LEqual (Arg2, Zero))
> 
>                 {
> 
>                     Store (Buffer (One)
> 
>                         {
> 
>                              0x03
> 
>                         }, Arg4)
> 
>                     Return (One)
> 
>                 }
> 
>                 If (LEqual (Arg2, One))
> 
>                 {
> 
>                     Return (One)
> 
>                 }
> 
>             }
> 
>         }
> 
>         Store (Buffer (One)
> 
>             {
> 
>                  0x00
> 
>             }, Arg4)
> 
>         Return (Zero)
> 
>     }
> 
>   
> 
> 重启应该已加载AppleLPC.kext 
> 
> 仿冒的是10de;nVidia Corporation;0aac;MCP79 LPC Bridge;Bridge;ISA bridge
> 
>   

3、更改相关kext

> 打开最新fakesmc，

> > 修改相关参数

> > Contents下新建文件夹PlugIns，放入相关kext。然后把fakesmc加入/S/L/E下

> 删除Nullintercpumanagement.kext 
> 
> 重启 即可加载原生驱动了。

  

![msi EX465安装MACOSX ACPI - leaf - ------坚持雅操------](http://img1.ph.126.net/CUsEg0mdRS_8A1hiuHBwJQ==/6608250700398870511.jpg "msi EX465安装MACOSX ACPI - leaf - ------坚持雅操------")

 

  

 二、CPU降频

> http://bbs.pcbeta.com/viewthread-1071634-1-1.html

> 我不添加SSDT也有2档降频。所以我直接加档位即可。

> 1、提取SSDT，并放入/Extra下面

> 2、变色龙勾选Drop SSDT

> 3、安装相关kext和工具查看CPU能变的频率

> > 安装VoodooMonitor.kext、VoodooPState.kext
> 
> > 打开Voodoomonitor.app 来查看所有的频率
> 
> > 记录如下：
> 
> > 十进制16进制control值
> 
> > 2546  >09F2491F
> 
> > 2412096C091E
> 
> > 227808E6481D
> 
> > 21440860081C
> 
> > 201007DA471B
> 
> > 18760754071A
> 
> > 174206CE4619
> 
> > 160806480617
> 
> 4、按电压和频率倍数算出大致的使用电量

> > 十六进制算出电量电压外频倍数

> > 88b8   <35000  =1100  X31
> 
> > 76E430436108728
> 
> > 6D2E27950107526
> 
> > 639025488106224
> 
> > 5A3C23100105022
> 
> > 510420740103720
> 
> > 481218450102518
> 
> > 3E8016000100016
> 
> >   
> 
> 5、改有PSS代码的那个SSDT文件，我的是SSDT-1.aml

> > > Name (\_PSS, Package (0x08)
> > 
> > >         {
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x000009F2, 
> > 
> > >                 0x000088B8, 
> > 
> > >                 0x0000000A, 
> > 
> > >                 0x0000000A, 
> > 
> > >                 0x0000491F,
> > 
> > >                 0x0000491F
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x0000096C, 
> > 
> > >                 0x000076E4,
> > 
> > >                 0x0000000A, 
> > 
> > >                 0x0000000A, 
> > 
> > >                 0x0000091E, 
> > 
> > >                 0x0000091E
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x000008E6,
> > 
> > >                 0x00006D2E,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000481D,
> > 
> > >                 0x0000481D
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x00000860,
> > 
> > >                 0x00006390,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000081C,
> > 
> > >                 0x0000081C
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x000007DA,
> > 
> > >                 0x00005A3C,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000471B,
> > 
> > >                 0x0000471B
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x00000754,
> > 
> > >                 0x00005104,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000071A,
> > 
> > >                 0x0000071A
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x000006CE,
> > 
> > >                 0x00004812,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x00004619,
> > 
> > >                 0x00004619
> > 
> > >             }, 
> > 
> > >             Package (0x06)
> > 
> > >             {
> > 
> > >                 0x00000648,
> > 
> > >                 0x00003E80,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x0000000A,
> > 
> > >                 0x00000617,
> > 
> > >                 0x00000617
> > 
> > >             }
> > 
> > >         })
> > 
> >   

> 备注：

> 1、有中间频率，但是不会稳在中间频率。你动几下就能看到中间频率。

> 2、也可以直接在DSDT里面添加代码即可。参见[第一个地址](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1098975)

>   

三、关机断电

> http://bbs.pcbeta.com/viewthread-900017-1-1.html
> 
> 搜索Method (\_PTS, 1, NotSerialized) 只要在里面添加Else和一对｛｝即可
> 
>     Method (\_PTS, 1, NotSerialized)
> 
>     {
> 
>         If (LEqual (Arg0, 0x05))
> 
>         {
> 
>             Store (Zero, SLPE)
> 
>             Sleep (0x10)
> 
>         }
> 
>         Else
> 
>  {
> 
>             Store (Arg0, DBG8)
> 
>             PTS (Arg0)
> 
>             Store (Zero, Index (WAKP, Zero))
> 
>             Store (Zero, Index (WAKP, One))
> 
>             If (LAnd (LEqual (Arg0, 0x04), LEqual (OSFL (), 0x02)))
> 
>             {
> 
>                 Sleep (0x0BB8)
> 
>             }
> 
>   
> 
>             Store (ASSB, WSSB)
> 
>             Store (AOTB, WOTB)
> 
>             Store (AAXB, WAXB)
> 
>             Store (Arg0, ASSB)
> 
>             Store (OSFL (), AOTB)
> 
>             Store (Zero, AAXB)
> 
>         }
> 
>     }
> 
>   
> 
> 备注：因USB问题导致无法重启和睡眠，正在解决中。。。
> 
>   

四、睡眠

>