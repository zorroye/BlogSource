---
title: thinkserver RD450 安装记录
tags:
  - 未分类
id: '358'
date: 2016-03-19 22:58:00
---

http://wenku.baidu.com/link?url=KYrrzw6uQxTetBy3\_dp6MgrrnYK00MFIztYcQeLN4ZIfS7Z4CAxe483AEFRAVVirZHmbfzk3JEy0P5FsR8byMRhvx03Ib-7i41P3LlPdw3u

  

  

  

0、配置清单

![thinkserver RD450 安装记录 - leaf - ------勤解万难------](http://img0.ph.126.net/sa62AD2PRykn8IiZKwxiPQ==/6598237448065851735.jpg "thinkserver RD450 安装记录 - leaf - ------勤解万难------")

 

1、设置RAID

> 按F10 进入deployment manager 
> 
> 选BIOS设置
> 
> 选boot manager
> 
> 选AVAGO MegaRAID
> 
> 选configure management
> 
> 选Create Virtual Drive
> 
> 选RAID1
> 
> 将2块硬盘Disabled状态改为Enabled
> 
> ![thinkserver RD450 安装记录 - leaf - ------勤解万难------](http://img0.ph.126.net/L43PO8dW3xPztbjQNS80Nw==/6598237448065851990.jpg "thinkserver RD450 安装记录 - leaf - ------勤解万难------")
> 
> 选Apply Changes
> 
> 选Save Configuration
> 
> 将Confirm \[Disabled\]状态改为\[Enabled\]
> 
> 按F10保存
> 
>   
> 
> 查看RAID信息
> 
> 选择Boot Manager  
> 
> 将Boot Mode \[Auto\]状态改成\[Legacy Only\] 
> 
> 选择Miscellaneous Boot Settings回车  
> 
> 将Storage OpROM Policy \[UEFI Only\]状态改为\[Legacy Only\]。  
> 
> 保存退出，重启服务器，即可看到RAID1
> 
> ![thinkserver RD450 安装记录 - leaf - ------勤解万难------](http://img0.ph.126.net/P3EA0FNh78MToomJWBRC4w==/4929752742210880728.jpg "thinkserver RD450 安装记录 - leaf - ------勤解万难------")
> 
>  
> 
> 安装win2012
> 
> 将Legacy Only 改为UEFI Only
> 
> 按F10 
> 
> 进入部署
> 
> ![thinkserver RD450 安装记录 - leaf - ------勤解万难------](http://img0.ph.126.net/Mdydw3_Idtcw27Ug6nBErA==/6598172576879816700.jpg "thinkserver RD450 安装记录 - leaf - ------勤解万难------")
> 
>