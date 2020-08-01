---
title: 基础补充1：BIOS
tags:
  - 未分类
id: '82'
abbrlink: 3472081138
date: 2013-04-05 16:16:00
---

BIOS启动过程：  
开机  
\->cpu运行  
 ->CPU通过北桥找到bios程序  
  ->bios解压自身到内存中  
   ->bios检查个硬件信息并唤醒  
    ->bios读取南桥的cmos信息  
      ->bios把信息整合成smbios表  
       ->屏幕显示信息（按del键可进bios界面）  
        ->post自检  
         ->POST将临时硬件(USB)写入SMBIOS  
          ->BIOS将MBR中的stage1加载到内存中  

>   ->stage1读取stage1.5以识别文件系统  
>    ->stage1读取stage2  
>     ->stage2读取/boot/grub/grub.conf 并提供选择界面  
>      ->将kernel载入到内存中  
>       ->kernel在内存中建立rootfs空间，将initrd载入到rootfs中  
>        ->按intird里面的init执行相关操作（详谈）  
> 
> > \->kernel chroot到硬盘的文件系统中 （详谈）  
> >  ->执行/etc/inittab  
> >   ->显示登陆界面  

  
  
备注：其实黑苹果很重要的部分就是改SMBIOS信息。dsdt就有这个功能  
  
  
BIOS功能：  

> 自检所有芯片，并通知芯片启动  
> 记录设定值到CMOS中  
> 分配IRQ(中断处理)  
> 加载引导程序  
>   

其他：  

> linux下通过dmidecode导出SMBIOS  
> 
> > type 0：BIOS Information  
> > type 1：System Information 指机型  
> > type 2：Base Board Information  
> > type 3：Chassis Information  
> > type 4：Processor Information  
> > type 7：Cache Information   CPU高速缓存信息  
> > type 8：Port Connector Information  
> > type 9：System Slot Information  
> > type 13：BIOS Language Information  
> > type 15：System Event Log  
> > type 16：Physical Memory Array  
> > type 17：Memory Device  
> > type 19：Memory Array Mapped Address  
> >