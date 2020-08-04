---
title: '[转载]linux系统挂载光盘镜像ISO的方法'
tags:
  - mount
categories:
  - Linux
  - 鸟哥的私房菜
id: '213'
abbrlink: 3868300778
date: 2012-12-04 12:01:00
---

  
http://www.jb51.net/os/RedHat/1050.html  
  
ISO：  
iso 格式的光盘镜像可以说是最普遍和通用的了，处理起来非常方便，挂载命令：  
( 假设镜像文件名为 download，挂载点为 /mount-point ，下同)  
mount -t iso9660 -o loop,user download.iso  /mount-point  
  
MDF：  
mdf 是 Win 下的虚拟光驱软件 Alcohol 120% 的专有格式，你可以用 mdf2iso 把 mdf  文件转换成 iso 格式再挂载，或者尝试用下面的命令挂载：  
mount download.mdf /mount-point -o loop=/dev/loop0  
不过遗憾的是，有些分轨的 mdf 文件，这样还是无能为力。  
  
BIN (or  BIN + CUE )：  
可以用 cdemu 挂载，也可以用 bin2iso 转换成 iso 再挂载，也可以 bchunk 转换 bin+cue 到 iso 。  
  
NRG：  
nrg 格式的镜像文件是 Nero 的专有格式，你可以用 nrg2iso 转换成 iso 再挂载，或者尝试下面的命令：  
mount -o loop,offset=307200 download.nrg /mount-point  
  
CCD：  
ccd 是 CloneCD 的专有格式，你可以用 ccd2iso 转换成 iso 再挂载。