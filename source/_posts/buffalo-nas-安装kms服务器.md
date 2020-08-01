---
title: buffalo nas 安装kms服务器
tags:
  - 未分类
id: '184'
abbrlink: 942033720
date: 2016-11-08 09:29:00
---

buffalo必须先root

  

下载vlmcsd

> vlmcsd-svn796-2015-07-18-Hotbird64.7z

> http://rgho.st/8jnLk5tst
> 
>   

使用的是arm5el-glibc

vlmcsd-svn796-2015-07-18-Hotbird64\\binaries\\Linux\\arm\\little-endian\\glibc\\vlmcs-armv5el-glibc

  

我放的目录是/usr/local/vlmcsd下

  

ssh进去 ./vlmcsd 即可

备注：1688端口不能被占用

  

开机启动

echo '/usr/local/vlmcsd/vlmcsd -l /var/log/vlmcsd.log > /dev/null 2>&1 ' >/etc/init.d/vlmcsd.sh

chmod 755 /etc/init.d/vlmcsd.sh

ln -s /etc/init.d/vlmcsd.sh  /etc/rc.d/sysinit.d/S99vlmcsd.sh 

chmod 777 /etc/rc.d/sysinit.d/S99vlmcsd.sh

  

  

  

  

  

  

  

  

>