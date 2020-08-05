---
title: '[安装记录]2、(补充) 在内核升级后自动安装nvdia驱动'
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '12'
abbrlink: 2270031191
date: 2010-01-24 23:16:00
---

[http://forum.ubuntu.org.cn/viewtopic.php?f=42&t=141431&start=0](http://forum.ubuntu.org.cn/viewtopic.php?f=42&t=141431&start=0)  
  
如果你使用的是在nv的官方网站下载的驱动，  
每当内核升级后，你必须重新手动安装nv驱动。  
本指南目标是当内核升级后自动进行安装驱动的过程，而不需要手工干预。  
  
第一步，把你使用的驱动放到/usr/src下，并生成链接。例如：  
sudo mv NVIDIA-Linux-x86-173.14.05-pkg1.run /usr/src  
sudo ln -s /usr/src/NVIDIA-Linux-x86-173.14.05-pkg1.run /usr/src/nvidia-driver  
  
这样做的目的是当你更换所用的驱动时，只需要删除原来的链接后再指定新的链接即可，  
不需要改变我们将使用的脚本(     script      )。  
  
自动安装nv驱动的脚本如下：  

**代码:**

#!/bin/bash  
#  
  
\# Set this to the exact path of the nvidia driver you plan to use  
\# It is recommended to use a symlink here so that this       script       doesn't  
\# have to be modified when you change driver versions.  
  
DRIVER=/usr/src/nvidia-driver  
  
\# Build new driver if it doesn't exist  
  
if \[ -e /lib/modules/$1/kernel/drivers/video/nvidia.ko \] ; then  
  
    echo "NVIDIA driver already exists for this kernel." >&2  
  
else  
  
    echo "Building NVIDIA driver for kernel $1" >&2  
  
    sh $DRIVER -K -k $1 -s -n 2>1 > /dev/null  
  
    if \[ -e /lib/modules/$1/kernel/drivers/video/nvidia.ko \] ; then  
  
        echo "   SUCCESS: Driver installed for kernel $1" >&2  
  
    else  
  
        echo "   FAILURE: See /var/log/nvidia-installer.log" >&2  
  
    fi  
fi  
  
  
exit 0

  
  
基本上，原理是检查新安装的内核是否安装了正确的nv驱动，  
如果没有，脚本将自动为新内核安装驱动模块。  
  
把上面的脚本命名为update-nvidia，并通过如下命令安装：  
  
sudo mkdir -p /etc/kernel/postinst.d  
sudo install update-nvidia /etc/kernel/postinst.d