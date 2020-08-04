---
title: ubuntu16.04安装NVIDIA GT710驱动
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '219'
abbrlink: 1460166489
date: 2016-07-21 10:36:00
---

1、将nouveau模块移除

mv /lib/modules/3-???-generic/kernel/drivers/gpu/drm/nouveau/nouveau.ko ./

2、更新initramfs

update-initramfs -u

3、重启后关闭lightdm

/etc/init.d/lightdm stop

4、安装nvidia驱动

./Nvidia....run 

  

  

  

搞定