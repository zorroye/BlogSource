---
title: 树莓派B+ 安装archlinux做下载机
tags:
  - 树莓派
categories:
  - Hardware
  - 树莓派
id: '181'
abbrlink: 102964102
date: 2015-10-13 10:21:00
---

2016.02.16  
已改用OpenMediaVault。其他还有nas4free。这两个都可以在树莓派1代上运行，很不错。  
xware自动启动  

> 新建脚本(下面有)  
> sudo update-rc.d xunlei.sh defaults  

  
  
选用archlinux是因为它支持树莓派B+。而且是字符界面也比较适合树莓派B+

  

1、安装

> [http://archlinuxarm.org/platforms/armv6/raspberry-pi](http://archlinuxarm.org/platforms/armv6/raspberry-pi)

> 分2个区，一个作boot目录，一个作root目录，然后下载解压就算制作好了
> 
> > fat32  100M
> 
> > ext4    其余
> > 
> > wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-latest.tar.gz
> > 
> > bsdtar -xpf ArchLinuxARM-rpi-latest.tar.gz -C root
> > 
> > sync
> > 
> > mv root/boot/\* boot

> 默认账号有2个，root和alarm

>   

2、基础设置

> [http://hugozhu.myalert.info/2013/03/09/setup-archliunx-on-raspberry-pi.html](http://hugozhu.myalert.info/2013/03/09/setup-archliunx-on-raspberry-pi.html)

> https://wiki.archlinux.org/index.php/Systemd-networkd  
> 更改时区  
> 
> > cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
> 
> 设置静态地址  
> /etc/systemd/network/_eth0_.network  
> 
> > \[Match\]  
> > Name=eth0  
> >   
> > \[Network\]  
> > #DHCP=yes  
> > Address = 192.168.3.13/24  
> > Gateway = 192.168.3.1  
> 
>   
> 添加源

> nano /etc/pacman.d/mirrorlist  
> 
> > Server = https://mirrors.ustc.edu.cn/archlinuxarm/$arch/$repo

> > 更新源 pacman -Syy

>   

> 添加用户

> > useradd ywz
> 
> > passwd ywz
> 
> > mkdir /home/ywz
> 
> > chown ywz:ywz /home/ywz  
> 
> > pacman -S sudo
> 
> > visudo
> 
> > ywz ALL=(ALL) NOPASSWD: ALL

>   
> 设置无线网络  
> http://hugozhu.myalert.info/2013/03/09/setup-archliunx-on-raspberry-pi.html  
> https://wiki.archlinux.org/index.php/Wireless\_network\_configuration\_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29  
> 
> > 查看设备状况  
> > dmesg | grep usbcore  
> > 
> > > registered new interface driver rtl8192cu  
> > 
> > 查看设备名  
> > ls /sys/class/net  
> > 
> > > eth0  lo  wlan0  
> > 
> > 启用无线设备  
> > 
> > > ip link set wlan0 up  
> > 
> > 由于我用的是免驱的8188cus，所以不用安装驱动了。  
> > 其他网卡可以这么操作 如：pacman -S dkms-8188eu  
> > 连接无线网络  
> > 
> > > pacman -S wireless\_tools   
> > > 
> > > > 会提示你安装其他相关插件，一起装了  
> > > 
> > > wifi-menu  
> > > 
> > > > 会产生一个配置文件(我的命名为Leaf)，放在/etc/netctl下面  
> > 
> > > 编辑配置文件  
> > 
> > > Description='A simple WPA encrypted wireless connection using a static IP'  
> > > Interface=wlan0  
> > > Connection=wireless  
> > > Security=wpa  
> > > ESSID='Leaf'  
> > > Key='zane1984#'  
> > > IP=static  
> > > Address='192.168.3.22/24'  
> > > Gateway='192.168.3.1'  
> > > DNS=('192.168.3.1')  
> > > \# Uncomment this if your ssid is hidden  
> > > Hidden=yes  
> > 
> > > 配置文件是从/etc/netctl/examples/wireless-wpa-static 复制过来的  
> > > 设置自启动  
> > 
> > > > netctl enable Leaf  
> 
>   
> 
> 挂在移动硬盘
> 
> lsblk -o name,kname,uuid

> ![树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------](http://img0.ph.126.net/etAFT6nSEwKNs8xECfgOOg==/2587317985942457601.png "树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------") 

> mkdir /home/ywz/download  
> mount /dev/sdc /home/ywz/download  
> 
> nano /etc/fstab

> > UUID=2db5ecf6-c374-4724-a27b-662b304f82a6       /home/ywz/download        ext4    defaults,noatime  0       0

>   

3、安装samba，ntp

> pacman -S samba ntp
> 
> mv /etc/samba/smb.conf{,-orig}
> 
> nano /etc/samba/smb.conf

> > \[global\]
> 
> >     workgroup = WORKGROUP
> 
> >     security = user
> 
> >     guest account = ywz
> 
> >     map to guest = bad user
> 
> >     wins support = yes
> 
> >     log level = 1
> 
> >     max log size = 1000
> 
> >   
> 
> > \[download\]
> 
> >     path = /home/ywz/download
> 
> >     read only = no
> 
> >     force user = ywz
> 
> >     force group = ywz
> 
> >     guest ok = yes

> 开机启动              systemctl enable smbd.service
> 
> 添加samba用户  smbpasswd -a ywz

  

4、安装迅雷远程

> [http://dl.lazyzhu.com/file/Thunder/Xware/1.0.31/](http://dl.lazyzhu.com/file/Thunder/Xware/1.0.31/)

> [http://lilin.hn.cn/2014102710272.html](http://lilin.hn.cn/2014102710272.html)
> 
> [http://www.linuxidc.com/Linux/2013-05/84748.htm](http://www.linuxidc.com/Linux/2013-05/84748.htm)
> 
>   
> 
> wget http://dl.lazyzhu.com/file/Thunder/Xware/1.0.31/Xware1.0.31\_armel\_v5te\_glibc.zip
> 
> pacman -S zip unzip
> 
> unzip Xware1.0.31\_armel\_v5te\_glibc.zip -d xware
> 
> mv xware /opt/xware
> 
> ./opt/xware/portal   会出来一个代码
> 
> 打开 http://yuancheng.xunlei.com/ 后点添加，输入激活码即可
> 
>   
> 
> 开机启动
> 
> nano /opt/xware/xunlei

> > #!/bin/sh
> > 
> > #
> > 
> > \# Xunlei initscript
> > 
> > #
> > 
> > \### BEGIN INIT INFO
> > 
> > \# Provides:          xunlei
> > 
> > \# Required-Start:    $network $local\_fs $remote\_fs
> > 
> > \# Required-Stop::    $network $local\_fs $remote\_fs
> > 
> > \# Should-Start:      $all
> > 
> > \# Should-Stop:       $all
> > 
> > \# Default-Start:     2 3 4 5
> > 
> > \# Default-Stop:      0 1 6
> > 
> > \# Short-Description: Start xunlei at boot time
> > 
> > \# Description:       A downloader
> > 
> > \### END INIT INFO
> > 
> > do\_start()
> > 
> > {
> > 
> >         ./opt/xware/portal
> > 
> > }
> > 
> > do\_stop()
> > 
> > {
> > 
> >         ./opt/xware/portal -s
> > 
> > }
> > 
> > case "$1" in
> > 
> >   start)
> > 
> >     do\_start
> > 
> >     ;;
> > 
> >   stop)
> > 
> >     do\_stop
> > 
> >     ;;
> > 
> > esac
> > 
> >   
> 
> nano /usr/lib/systemd/system/xunlei.service

> > \[Unit\]
> 
> > Description=xunlei
> 
> > ConditionPathExists=/opt/xware/xunlei
> 
> >   
> 
> > \[Service\]
> 
> > Type=forking
> 
> > ExecStart=/opt/xware/xunlei start
> 
> > TimeoutSec=0
> 
> > StandardOutput=tty
> 
> > RemainAfterExit=yes
> 
> > SysVStartPriority=99

> >   

> > \[Install\]  
> > WantedBy=multi-user.target
> 
> >   
> 
> systemctl enable xunlei.service  添加开机启动命令

> systemctl status xunlei.service   可查看运行状况

>   

  

5、aria2

> [https://wiki.archlinux.org/index.php/Aria2](https://wiki.archlinux.org/index.php/Aria2)
> 
> [http://aria2c.com/usage.html](http://aria2c.com/usage.html)
> 
> [http://www.eeboard.com/bbs/thread-22086-1-1.html](http://www.eeboard.com/bbs/thread-22086-1-1.html)
> 
> [http://godloong.com/RaspberryPi/raspberrypi-nas-samba-baiduyun.html](http://godloong.com/RaspberryPi/raspberrypi-nas-samba-baiduyun.html)
> 
> [http://blog.binux.me/2012/12/aria2-examples/](http://blog.binux.me/2012/12/aria2-examples/)
> 
> [https://www.librehat.com/aria2-camouflage-utorrent-pt-download/](https://www.librehat.com/aria2-camouflage-utorrent-pt-download/)  
> http://phpquan.com/arm/raspberry-pi-aria2-yaaw-downloader/  
> 
> pacman -S aria2 nginx git
> 
> 开机启动 systemctl enabel nginx    
> 
>   
> 
> 安装Yaaw

> cd /usr/share/nginx          
> 
> rm -rf html
> 
> git clone https://github.com/binux/yaaw.git     /usr/share/nginx/html/

>   
> 
> 配置aria2

> mkdir /home/ywz/.aria2  
> cd /home/ywz/.aria2  
> touch aria2.conf    aria2.session    log.log  
> nano aria2.conf

> > ####http://aria2c.com/usage.html####  
> > enable-rpc=true  
> > rpc-allow-origin-all=true  
> > rpc-listen-all=true  
> > rpc-secret=secret  
> >   
> > bt-max-peers=96  
> > listen-port=25236  
> > enable-dht=false  
> > enable-dht6=false  
> > bt-enable-lpd=false  
> > enable-peer-exchange=false  
> > user-agent=uTorrent/341(109279400)(30888)  
> > peer-id-prefix=-UT341-  
> > seed-ratio=1.0  
> > force-save=true  
> > bt-hash-check-seed=true  
> > bt-seed-unverified=true  
> > bt-save-metadata=true  
> >   
> > dir=/home/ywz/download  
> > file-allocation=none  
> > continue=true  
> >   
> > max-concurrent-downloads=3  
> > max-connection-per-server=5  
> > split=5  
> > disable-ipv6=true  
> >   
> > input-file=/home/ywz/.aria2/aria2.session  
> > save-session=/home/ywz/.aria2/aria2.session  
> > log=/home/ywz/.aria2/log.log  
> > log-level=warn  
> > 
> > >   

> 验证配置文件

> aria2c --conf-path=/home/ywz/.aria2/aria2.conf

>   
> 
> 开机启动

> [https://github.com/GutenYe/systemd-units/tree/master/aria2  
> ](https://github.com/GutenYe/systemd-units/tree/master/aria2)sudo nano /usr/lib/systemd/system/aria2.service
> 
> > \[Unit\]  
> > Description=Aria2 User Service by %u  
> > After=network.target  
> >   
> > \[Service\]  
> > ExecStart=/usr/bin/aria2c --enable-rpc --rpc-listen-all --rpc-allow-origin-all --save-session /home/ywz/.aria2/aria2.session --input-file /home/ywz/.aria2/aria2.session --conf-path=/home/ywz/.aria2/aria2.conf  
> >   
> > \[Install\]  
> > WantedBy=default.target

> sudo systemctl enable aria2.service

>   

> 其他还支持百度网盘，旋风离线，迅雷离线。  
>   

http://token:secret@192.168.3.101:6800/jsonrpc  
  

![树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------](http://img2.ph.126.net/e7gspMPED-AHBEXtDEFMbg==/6631360235792953016.png "树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------")

 

  
安装yaourt  

> https://wiki.archlinux.org/index.php/Yaourt\_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29  
> pacman -S base-devel fakeroot sudo  
> 安装 package-query  
> 
> > wget https://aur.archlinux.org/cgit/aur.git/snapshot/package-query.tar.gz  
> > tar zxvf package-query.tar.gz  
> > cd package-query  
> > 
> > ![树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------](http://img1.ph.126.net/8Nn5vsChGC1TwjZesC8f5w==/6630354182654129188.png "树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------")
> > 
> > makepkg -si  
> 
> 安装 yaourt  

> > wget https://aur.archlinux.org/cgit/aur.git/snapshot/yaourt.tar.gz  
> > tar zxvf yaourt.tar.gz  
> > cd yaourt  
> > makepkg -si  

  
安装monitorix  

> https://wiki.archlinux.org/index.php/Monitorix  
> https://linux.cn/article-3171-1.html  
> http://www.monitorix.org/documentation.html#3  
>   

> yaourt monitorix    
> 或者  

> wget https://aur.archlinux.org/cgit/aur.git/snapshot/monitorix.tar.gz  
> tar zxvf monitorix.tar.gz  
> cd monitorix  
> makepkg -si  
>   
> 配置  
> /etc/monitorix/monitorix.conf  
> 
> > <httpd\_builtin>  
> > enabled = y  
> 
>   
> /etc/nginx/nginx.conf  
> 
> > server {  
> >     listen       80;  
> >     server\_name  your.domain.com;  
> >   
> >     location / {  
> >        proxy\_pass http://127.0.0.1:8080/;  
> >        proxy\_buffering off;  
> >     }  
> >   
> >     location ~ ^/monitorix/(.+\\.png)$ {  
> >         alias /srv/http/monitorix/$1;  
> >     }  
> > }  
> 
>   
> 添加自启动  
> sudo su  
> systemctl enable monitorix.service  
>   

> http://192.168.3.13:8080/monitorix  

> ![树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------](http://img0.ph.126.net/pyBeUgAOH_-_3TfPBAEI9w==/6630616965933875370.png "树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------")
> 
>    

  

DLNA

> pacman -S minidlna

> nano /etc/minidlna

> > media\_dir=/home/ywz/download
> 
> > media\_dir=A,/home/ywz/download
> 
> > media\_dir=P,/home/ywz/download
> 
> > media\_dir=V,/home/ywz/download

>   

  
alsi  

> yaourt alsi  
> 
> ![树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------](http://img2.ph.126.net/CJkVLDdWLKIMJMu_nZ5aZQ==/6630453138700746482.png "树莓派B+ 安装archlinux做下载机 - leaf - ------勤解万难------")
> 
>