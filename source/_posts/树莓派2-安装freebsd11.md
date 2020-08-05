---
title: 树莓派2 安装freebsd11
tags:
  - 树莓派
categories:
  - Hardware
  - raspberrypi
id: '183'
abbrlink: 2900167838
date: 2015-10-24 19:54:00
---

1、下载镜像并安装  

> https://wiki.freebsd.org/FreeBSD/arm/Raspberry%20Pi  
> http://raspbsd.org/raspberrypi.html  

> 写入SD卡即可  
>   

2、freebsd基础配置  

> http://www.bigsea.com.cn/archives/1393/  
> 1、使用root账号ssh登陆  
> 
> > ee /etc/ssh/sshd\_config  
> > 加入  
> > PermitRootLogin yes  
> 
> 2、设置静态路由  
> 
> > ee /etc/rc.conf  
> > ifconfig\_ue0="inet 192.168.3.22 netmask 255.255.255.0"  
> > defaultrouter="192.168.3.1"  
> 
> 3、设置时间  
> 
> > cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
> > echo 'ntpd\_enable="YES"' >> /etc/rc.conf  
> > service ntpd start  
> 
> 4、设置swap分区  
> 
> > dd if=/dev/zero of=/usr/swap0 bs=1m count=128  
> > chmod 0600 /usr/swap0  
> > echo 'md99 none swap sw,file=/usr/swap0 0 0' >> /etc/fstab  
> > swapon -aq  

> 5、安装pkg install   (万年Operation timed out，没成功过T\_T)  
> 
> > 1\. First install pkg by pkg-static.  
> >     # fetch http://www.peach.ne.jp/archives/rpi/ports/rpi2/pkg-static  
> >     # chmod 755 pkg-static  
> >     # ./pkg-static add http://www.peach.ne.jp/archives/rpi/ports/rpi2/pkg.txz  
> >   
> > 2\. Disable default repo by FreeBSD.conf.  
> >     # mkdir -p /usr/local/etc/pkg/repos  
> >     # echo "FreeBSD: { enabled: no }" > /usr/local/etc/pkg/repos/FreeBSD.conf  
> >   
> > 3\. Install following rpi2.conf:  
> >     # fetch http://www.peach.ne.jp/archives/rpi/rpi2.conf  
> >     # mv rpi2.conf /usr/local/etc/pkg/repos  
> >     # pkg update  
> >   
> > 用host -t srv \_http.\_tcp.pkg.freebsd.org 得到的地址更新也是莫有用  
> >   

>