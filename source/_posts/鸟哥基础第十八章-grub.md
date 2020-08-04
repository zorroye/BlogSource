---
title: 鸟哥基础第十八章-grub
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '73'
abbrlink: 3244904808
date: 2012-10-01 07:34:00
---

  
硬盘分区表结构：  

> 主引导记录MBR  
> 
> > bootlader：446B  
> > DPT：64B  
> > magic number：2B \_\_\_\_\_\_ 以上共512B  
> 
> stage1.5：32K  

> 分区1  
> 分区2  
> 分区3  
> 分区4  
>   

  
  
GRUB  

> /boot/grub里面包含  
> 
> > 引导程序：stage1、stage2
> 
> > 启动设备信息：device.map  
> 
> > 文件系统：iso9660、ufs、xfs、fat、jfs、e2fs等  
> > 启动选项：menu.lst 。menu.lst是指向grub.conf的  
> > 启动选项背景：splash.xpm.gz  
> >   
> 
> grub.conf  
> 
> > cat grub.conf | egrep -v '^#|^$'  
> > default=0                                                               #按菜单第一行启动：就是2.6...FC4smp  
> > timeout=5                                                              #等待时间：5秒  
> > splashimage=(hd0,0)/boot/grub/splash.xpm.gz    #背景图片  
> > hiddenmenu                                                          #隐藏菜单  
> > title Fedora Core (2.6.11-1.1369\_FC4smp)  
> >         root (hd0,0)                                                    
> >         kernel /boot/vmlinuz-2.6.11-1.1369\_FC4smp ro root=LABEL=/ rhgb quiet  
> >         initrd /boot/initrd-2.6.11-1.1369\_FC4smp.img  
> > title Fedora Core-up (2.6.11-1.1369\_FC4)  
> >         root (hd0,0)  
> >         kernel /boot/vmlinuz-2.6.11-1.1369\_FC4 ro root=LABEL=/ rhgb quiet  
> >         initrd /boot/initrd-2.6.11-1.1369\_FC4.img  
> >   
> > 
> > > 说明：  
> > > root (hd0,0)                                                   
> > > 
> > > > #这里的root表示核心在哪个位置。也就是/boot在哪个位置  
> > > 
> > > kernel /boot/vmlinuz-2.6.11-1.1369\_FC4smp ro root=LABEL=/ rhgb quiet  
> > > 
> > > > #这里的root表示/分区在哪个位置。可以用root=/dev/sda1代替  
> > 
> > >   
> > 
> > 其他选项;  
> > 
> > > unhide (hd0,1)            #显示/dev/hda2  
> > > hide (hd0,4)                #隐藏/dev/hda5  
> > > rootnoverify (hd0,0)    #不检查/dev/hda1  
> > > chainloader +1            #表示打开/dev/hda2的第一个扇区  
> > 
> > > makeactive                  #设置为活动分区  
> > 
> >   
> >   
> 
> grub shell  
> 
> > grub 进入grub shell  
> > help查看所有命令  
> > root (hd0,0)：                 查找含有/boot的分区  
> > find /boot/grub/stage1**+\[tab\]** ：查找是否存在stage1文件  
> > setup (hd0) ：                 安装到MBR中  
> > setup (hd0,0)：               安装到第一个分区的第一个扇区中