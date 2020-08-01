---
title: LFS制作-5、完成制作
tags:
  - 未分类
id: '232'
date: 2012-10-25 16:40:00
---

1、chroot

chroot "$LFS" /usr/bin/env -i \\

    HOME=/root TERM="$TERM" PS1='\\u:\\w\\$ ' \\

    PATH=/bin:/usr/bin:/sbin:/usr/sbin \\

    /bin/bash --login

  

2、配置系统脚本

LFS-Bootscripts-6.3 

> 包含一套在 LFS 系统启动和关闭时的启动和停止脚本
> 
> 脚本：halt、reboot、ifup、ifdown、udev、

  

cat > /etc/sysconfig/clock << "EOF"

> UTC=0

EOF

  

cat > /etc/inputrc << "EOF"

  

cat > /etc/profile << "EOF"

> export LANG=en\_US.UTF-8
> 
> export INPUTRC=/etc/inputrc  
> alias ls="ls --color"  
> 
> export PS1='\\u:\\w\\$'

EOF

  

echo "HOSTNAME=leaf" > /etc/sysconfig/network

  

cat > /etc/hosts << "EOF"

> 127.0.0.1 leaf localhost

EOF

  

cd /etc/sysconfig/network-devices

mkdir -v ifconfig.eth0

cat > ifconfig.eth0/ipv4 << "EOF"

> ONBOOT=yes
> 
> SERVICE=ipv4-static
> 
> IP=172.16.43.100
> 
> GATEWAY=172.16.43.2
> 
> PREFIX=24
> 
> BROADCAST=172.16.43.255

EOF

  

cat > /etc/resolv.conf << "EOF"

> nameserver 172.16.43.2 

EOF

  

cat > /etc/fstab << "EOF"

  

3、安装核心

Linux-2.6.22.5 

make mrproper

make menuconfig  #参考孙海勇的设置

make

make modules\_install

cp -v arch/i386/boot/bzImage /boot/lfskernel-2.6.22.5

cp -v System.map /boot/System.map-2.6.22.5

cp -v .config /boot/config-2.6.22.5

install -d /usr/share/doc/linux-2.6.22.5

cp -r Documentation/\* /usr/share/doc/linux-2.6.22.5

  

  

4、stage写入MBR

配置了软驱

dd if=/boot/grub/stage1 of=/dev/fd0 bs=512 count=1

dd if=/boot/grub/stage2 of=/dev/fd0 bs=512 seek=1

  

grub

> root (hd0,0)
> 
> setup (hd0)

quit

  

cat > /boot/grub/menu.lst << "EOF"

  

mkdir -v /etc/grub

ln -sv /boot/grub/menu.lst /etc/grub

  

5、完成制作

echo 6.3 > /etc/lfs-release

  

sync

reboot

  

制作完毕！：-)

  

![LFS制作-5、完成制作 - leaf - ------坚持雅操------](http://img2.ph.126.net/aXVFRIrHp03lrh9b3NOsRQ==/6597672299028385782.jpg "LFS制作-5、完成制作 - leaf - ------坚持雅操------")