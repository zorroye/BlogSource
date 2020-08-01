---
title: ubuntu10.04 调整屏幕亮度
tags:
  - 未分类
id: '42'
abbrlink: 3839016931
date: 2013-03-12 19:37:00
---

  
参考：http://www.linuxidc.com/Linux/2012-06/63727.htm  
  
1、安装软件：sudo apt-get install laptop-mode-tools  
  
2、配置文件：  
文章提到2个配置文件，但我笔记本上配置一个就可以了  
sudo nano  /etc/laptop-mode/conf.d/lcd-brightness.conf  

> CONTROL\_BRIGHTNESS=1  
> BATT\_BRIGHTNESS\_COMMAND="echo 70"  
> LM\_AC\_BRIGHTNESS\_COMMAND="echo 70"  
> NOLM\_AC\_BRIGHTNESS\_COMMAND="echo 70"  
> BRIGHTNESS\_OUTPUT="/proc/acpi/video/AVGA/LCD/brightness  
>   
> 备注：  
> 首先调整亮度，  
> 然后 cat /proc/acpi/video/AVGA/LCD/brightness 会限制当前亮度  
> 然后替代上面的70参数即可  
>   
> 变量说明  
> BATT\_BRIGHTNESS\_COMMAND          使用电池时亮度  
> LM\_AC\_BRIGHTNESS\_COMMAND       使用交流电时亮度  
> NOLM\_AC\_BRIGHTNESS\_COMMAND  ？？  

>   

2、好像系统管理里面的电源管理也可以调的。绕弯了。。。