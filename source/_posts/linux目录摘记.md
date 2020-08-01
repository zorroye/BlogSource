---
title: linux目录摘记
tags:
  - 未分类
id: '40'
date: 2013-02-27 16:37:00
---

查看书名：系统架构和目录解析\_邱世华  
  
/lib：存放函数库和内核模块  

> /lib/modules：存放内核模块ko  
> 内核模块加载顺序：  
> 
> > /lib/modules/\`uname -r\`/initrd/----->  
> > /lib/modules/\`uname -r\`/updates/---->  
> > /lib/modules/\`uname -r\`/kernel/drivers/  

> /lib/security：存放PAM库文件so  
> 
> > 用于PAM机制认证  
> 
>   

/etc/default：存放系统软件默认值的目录  

> 如/etc/default/useradd：就设置了添加账户时的默认参数信息。  
>   

/dev：设备文件目录  

> 操作系统Ring概念：  
> 
> > 用户使用应用程序操作硬件--->  
> > 应用程序调用模块--->  
> > 模块使用虚拟文件系统中对应的文件---->  
> > 虚拟文件系统请求内核对硬件进行操作。  

>   

/proc：程序信息和系统设置目录  

> 查看cpu信息：cat /proc/cpuinfo  
>   

/sys：系统分类信息  

> 以分类的方式列出系统信息。