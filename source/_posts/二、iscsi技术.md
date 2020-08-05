---
title: 二、ISCSI技术
tags:
  - iscsi
categories:
  - Hardware
  - storage
id: '352'
abbrlink: 4220424958
date: 2016-02-05 18:12:00
---

IP-SAN里面最重要的就是ISCSI技术

就是讲SCSI协议封装到以太网里面，在以太网上实现scsi存储技术。  
  
ISCSI结构  

![二、ISCSI技术 - leaf - ------勤解万难------](http://img1.ph.126.net/KE8AO1mSgBDxDXOhSLVyuw==/6631304160703828771.jpg "二、ISCSI技术 - leaf - ------勤解万难------")

ISCSI initiator就是客户电脑  
ISCSI target 就是服务器或者说就是一块硬盘  
ISCSI lun 就是硬盘的盘片，你可以增加一个盘片的容量，也可以给一块硬盘加入多个盘片。  
  
  

![二、ISCSI技术 - leaf - ------勤解万难------](http://img0.ph.126.net/TpI-mnMqD-2FfxDpDiD4Ng==/6631288767541027428.png "二、ISCSI技术 - leaf - ------勤解万难------")

![二、ISCSI技术 - leaf - ------勤解万难------](http://img0.ph.126.net/ZsOBVWkTLQeokVhg8LiE0A==/6631254682680568695.png "二、ISCSI技术 - leaf - ------勤解万难------")

  

 相关的安全技术：

> ![二、ISCSI技术 - leaf - ------勤解万难------](http://img0.ph.126.net/S-GxGmK4674YKBOiY5eAiA==/6598103307646317621.png "二、ISCSI技术 - leaf - ------勤解万难------")
> 
>  

实验主要实现CHAP和IPSec等设置。