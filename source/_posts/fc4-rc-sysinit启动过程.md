---
title: FC4 rc.sysinit启动过程
tags:
  - 鸟哥的私房菜
categories:
  - Linux
  - 鸟哥的私房菜
id: '88'
abbrlink: 522471707
date: 2014-11-25 13:48:00
---

设置3个变量HOSTNAME,HOSTTYPE,unamer

运行. /etc/sysconfig/network

挂载/proc，加载usb模块，加载usb设备，挂载/sys

运行. /etc/init.d/functions

检查SELinux状态

显示欢迎字幕：welcome to red hat …

设置控制台的日志级别

设置codline #ro root=LABEL=/ rhgb quiet

初始化硬件，

加载ide，scsi，network，audio等模块

加载 /etc/sysconfig/modules/ 下的模块 #空

加载 /etc/rc.modules 下设置的模块 #空 

———开始图形化启动界面———

挂载/dev/pts

配置内核参数

设置系统时钟

设置hostname

加载acpi模块

设置zfcp

设置RAID

LVM2初始化

需要的话卸载initrd

需要的话更新quota

以读写模式从新挂载/

清理SELinux

清理mtab

删除mtab的临时文件

把加载的文件系统写入到/etc/mtab下 / /proc /sys /dev/pts /proc/bus/usb

挂载其他文件系统如smbfs等

启动磁盘配额

检查是否有必要设置SElinux？？？  Check to see if a full relabel is needed

开始图形化启动界面

初始化随机数

需要的话从新配置电脑，

从新读取/etc/sysconfig/network,hostname,

删除/目录下的隐藏文件

删除/var/lock/\* /var/run/\* 下的文件

删除/var/lib/rpm/\_\_db\*

删除/var/gdm/.gdmfifo

从新设置pam权限

清理utmp/wtmp

清理/tmp

新建/tmp/.ICE-unix

启用交换分区

挂载/proc/sys/fs/binfmt\_misc

运行/etc/rc.serial

需要的话加载ide-cd  ide-scsi模块

配置网络？？？ Boot time profiles. Yes, this should be somewhere else.

——-内核已可用，模块已加载完——

启动记录卸载/var/log/dmesg下

create the crash indicator flag to warn on crashes, offer fsck with timeout

结束rc.sysinit。