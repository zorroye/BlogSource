---
title: 系统备份工具---ucloner
tags:
  - 未分类
id: '36'
date: 2012-12-06 23:02:00
---

  
ucloner适用于ubuntu12.04，http://forum.ubuntu.org.cn/viewtopic.php?t=372432  
软件下载地址：http://code.google.com/p/ucloner/  
  
  
用软件之前先安装如下软件：  

> sudo apt-get install squashfs-tools  
> sudo apt-get install python-gtk2 zenity python-vte  

  
备份：  

> 打开./ucloner\_gui.py  

> 设置保存目录，设置要排除的目录即可。生成squashfs文件  
>   

还原  

> 将squashfs文件和Ucloner复制到U盘  

> 用同版本的光盘或U盘启动，ubuntu10.04-x86的系统用ubuntu10.04-x86的盘  
> 设置存放目录，设置分区和grub等即可还原。  
> #目标系统可以不格式化，选current  
> #不格式化可以保护原先在盘里面的资料  

>   

  

> 还原的时候如果原先分区有多个盘，可以用命令行来设置还原  
> 如分区如下  
> /                /dev/sda1  
> /home       /dev/sda5  
> /usr          /dev/sda6  
> /var          /dev/sda7  
> swap        /dev/sda8  
>   
> 则还原命令如下  

> sudo  ./ucloner\_cmd.py  mode=restore  lang=cn   restore\_from=/media/disk-1/ubuntu-10.04.squashfs   /=/dev/sda1  /\_fs=ext4   /home=/dev/sda5  /home\_fs=current    /usr=/dev/sda6  /usrl\_fs=ext4   /var=/dev/sda7  /var\_fs=ext4   grubdev=/dev/sda   swap=/dev/sda8  

  
   
克隆  

> 主要用于在多台配置相同的电脑中快速安装系统。  
> 接上其他电脑的硬盘，然后分好区， 然后就可以克隆了。  
> 克隆好后把硬盘接回其他电脑上就可以用了。  
>   

  
制作lived系统  

> 不会  

  
  
Ucloner和ghost的区别是：硬盘间操作，ucloner要先分区再还原。  
分区最好用Gparted