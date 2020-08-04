---
title: 基础补充3：initrd.img里的init和/etc/rc.sysinit
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '84'
abbrlink: 695420585
date: 2013-04-09 15:52:00
---

  
了解这两个文件对以后制作LFS很有帮助。  
  
1、调出initrd.img 里的init文件  

> mv initrd.img initrd.gz  
> gunzip initrd.gz  
> cpio -id < initrd 就能看到了  
> 
> ![基础补充3：initrd.img里的init和/etc/rc.sysinit - leaf - ------坚持雅操------](http://img2.ph.126.net/m66GHfFX_CgNhzDRGsQc0Q==/2232096565415793248.png "基础补充3：initrd.img里的init和/etc/rc.sysinit - leaf - ------坚持雅操------")
> 
>    
> \---------------------------FC4 init内容-----------------------------  
> #---------开启nash用于执行以下内容，nash同bash，比较小巧。#!是固定格式。-----
> 
> > #!/bin/nash        
> 
>   
> #------加载3目录。initrd里面已经有这3个“空”目录了，加载到内存中供kernel使用 --------  
> #------这3个目录里的文件将由kernel产生  
> #-----需要注意的是/目录是由kernel产生的，而不是initrd提供的。  
> #-----procfs和sysfs是内核层的文件，除了内核，其他都改不了。用于存储硬件和进程相关信息。  
> #-----/dev文件 以tmpfs文件系统来存储  
> #-----tmpfs是建立在内存中的，刚开机由于没有实体设备被加载，所有产生的信息都存在内存中。  
> 
> > mount -t proc /proc /proc  
> > setquiet  
> > echo Mounted /proc filesystem  
> > echo Mounting sysfs  
> > mount -t sysfs /sys /sys  
> > echo Creating /dev  
> > mount -o mode=0755 -t tmpfs /dev /dev  
> 
>   
> #---------建立设备文件，console用于显示，null和zero起到垃圾桶的作用 -------------  
> #------mknod 主要是建b c  
> 
> > mknod /dev/console c 5 1  
> > mknod /dev/null c 1 3  
> > mknod /dev/zero c 1 5  
> 
>   
> #---------------------建立伪终端目录、临时暂存-----------------------------  
> #-----/dev/pts 给ssh和xterm用。  
> #----/dev/shm 用于提供暂存  
> #----udev用于动态的管理设备文件，特别是热插拔的设备。改善/dev的问题  
> #----udev配合/sysfs使用。  
> 
> > mkdir /dev/pts  
> > mkdir /dev/shm  
> > echo Starting udev  
> > /sbin/udevstart          #自动从/sys中找到热插拔设备  
> > echo -n "/sbin/hotplug" > /proc/sys/kernel/hotplug  
> 
>   
> #--------加载模块-------  
> 
> > echo "Loading jbd.ko module"  
> > insmod /lib/jbd.ko  
> > echo "Loading ext3.ko module"  
> > insmod /lib/ext3.ko  
> 
>   
> #-----mkrootdev 主要是把grub.conf里面的 root (hd0,0) 的路径先建立好。  
> #-----将找到的root路径：/dev/root  挂载到initrd的/sysroot下  
> #------然后用switchroot到该目录。正式切到硬盘操作系统的环境中。switchroot同chroot  
> 
> > /sbin/udevstart  
> > echo Creating root device  
> > mkrootdev /dev/root  
> > echo Mounting root filesystem  
> > mount -o defaults --ro -t ext3 /dev/root /sysroot  
> > echo Switching to new root  
> > switchroot --movedev /sysroot  
> 
>   

2、/etc/rc.sysinit  

> 设置3个变量    HOSTNAME,HOSTTYPE,unamer  

> /etc/sysconfig/network                   设置网络状态  
> HOSTNAME=localhost                  HOSTNAME变量设值  
> mount -n -t proc /proc /proc            挂载/proc  
> /proc/bus/usb                                   检查USB设备文件所需的目录  
> mount -n -t sysfs /sys /sys >/dev/null 2>&1    挂载/sys  
> . /etc/init.d/functions                         设置环境变量  
> 设置SELINUX  
> 打印welcome to  
> /bin/dmesg                                         设置系统能够记录的等级，当前设置值是1  
> /sbin/start\_udev                                 开启udev机制，/etc/udev下所有规则可套用  
> cat /proc/cmdline                              读取grub.conf vmlinuz这一行  
> /proc/sys/kernel/modprobe             加载各硬件模块  
> mount -n /dev/pts                             产生一个tty接口  
> sysctl -e -p /etc/sysctl.conf >/dev/null 2>&1    加载sysctl.conf 设置值  
> /etc/sysconfig/clock                         设置时间种类，如UTC  
> /sbin/hwclock                                   设置系统时间  
> 设置hostname  
> /proc/acpi                                          开启ACPI功能  
> /sbin/zfcpconf.sh                               scsi相关  
> /etc/mdadm.conf                               raid相关  
> /sbin/lvm.static                                  LVM相关  
> . /etc/sysconfig/readonly-root           以只读方式挂载文件系统  
> mount -n -o remount,rw /                  以可读可写方式挂载根目录  
> 清空SElinux表  
> (> /etc/mtab) &> /dev/null                 清空/etc/mtab  
> 从新挂载系统目录  
> /usr/bin/rhgb                                       加载图形开机画面背景，并显示开机进度条  
> 进行系统初始设置  
> 清除相关文件  
> mkdir -m 1777 -p /tmp/.ICE-unix >/dev/null 2>&1 设定X window所要使用的目录  
> swapon -a -e                                       开启swap交换空间  
> /usr/sbin/system-config-network-cmd        设置网络  
> dmesg -s 131072 > /var/log/dmesg        写入dmesg信息  
> touch /.autofsck &> /dev/null                    建立.autofsck文件，判断是否正常启动还是非正常断电  
> /usr/bin/rhgb-client --sysinit                      告知系统要离开这个脚本了，继续则转到inittab脚本     

>