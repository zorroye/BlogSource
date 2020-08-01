---
title: 通过PXE安装系统
tags:
  - 未分类
id: '165'
date: 2014-02-18 15:28:00
---

PXE整个安装的过程是这样的：

PXE网卡启动 => 

DHCP获得IP地址 => 

从TFTP上下载 pxelinux.0、vmlinuz、initr.img 等 => 

引导系统进入安装步骤 => 

通过PEX linux 下载ks.cfg文件并跟据ks.cfg自动化安装系统 => 完成。

  

  

  

windows下软件有

> TFTPD32

> 深度网吧GHOST辅助工具服务端

>   

>   

linux下详细配置

> 需要的文件有
> 
> isolinux：安装光盘里有

> > vmlinuz
> 
> > initrd.img
> 
> > isolinux.cfg
> > 
> > vesamenu.c32
> 
> > splash.jpg

>   
> 
> syslinux：http://www.syslinux.org/wiki/index.php/Download

> > pxelinux.0
> > 
> > vesamenu.c32 (可选用，二选一)

> 系统安装盘

  

  

  

http://zhumeng8337797.blog.163.com/blog/static/100768914201121383022804/

http://www.ipcpu.com/2010/12/linux-pxe/

www.kernel.org/pub/linux/utils/boot/syslinux/