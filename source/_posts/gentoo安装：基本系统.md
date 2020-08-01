---
title: gentoo安装：基本系统
tags:
  - 未分类
id: '234'
date: 2012-11-28 12:20:00
---

环境：  
宿主：              CPU：amd 4核         内存：DDR3 8G           显卡GT8500  
vmware 9 ：    CPU：2核                  内存：1G                     硬盘：30G  
参考：http://www.gentoo.org/doc/en/handbook/handbook-x86.xml  
下载：http://distfiles.gentoo.org/releases/x86/autobuilds/current-iso/install-x86-minimal-20120710.iso  
  
1、进光盘系统  

> 光盘启动  
> 15秒内按F1，然后输入gentoo进系统  

  
2、安装网卡驱动  

> ifconfig 只找到lo，没有eth0  
> 查看设备：lspci  
> 
> > 02:01.0 Ethernet controller: Advanced Micro Devices \[AMD\] 79c970 \[PCnet32 LANCE\] (rev 10)  
> 
> 查看模块：lsmod | grep net  
> 
> > pcnet32                23142  0  
> 
> 显然模块是有的，就是没加载  
> 安装显卡驱动  
> 
> > net-setup eth0  
> > 按照提示选择即可  

  
3、开启ssh  

> /etc/init.d/sshd start  
> passwd root  
>   

4、宿主开终端，用ssh连接进光盘系统  

> ssh root@172.16.43.142  
> #dhcp获取的IP地址是172.16.43.142  
>   

5、分区、格式化、挂载  

> 分区  
> 
> > cfdisk  
> > /dev/sda1     ext2           128M               Boot partition  
> > /dev/sda2     (swap)     1024M               Swap partition  
> > /dev/sda3     ext3     Rest of the disk      Root partition  

>   
> 建文件系统  
> 
> > mkfs.ext2 /dev/sda1  
> > mkfs.ext3 /dev/sda3  
> > mkswap /dev/sda2  
> > swapon /dev/sda2  
> 
>   
> 挂载文件系统  
> 
> > mount /dev/sda3 /mnt/gentoo                 #/mnt/gentoo文件夹本身就有  
> > mkdir /mnt/gentoo/boot  
> > mount /dev/sda1 /mnt/gentoo/boot  
> 
>   

6、下载stage3和portage包  

> stage3已经将目标系统的环境全部建好了，就剩下一些软件、linux内核、grub没装了。  

> 0、cd /mnt/gentoo  
> 1、links http://www.gentoo.org/main/en/mirrors.xml  
> 
> > #Enter：进入，按键D：下载    按键Q：退出  
> 
> 2、下载stage3  
> 
> > downloads-mirrors-6、Asia-China-sohu.inc(http)-releases/x86/autobuilds/20121016/stage3-i686-20121016.tar.bz2  
> > #实际地址  
> > http://mirrors.sohu.com/gentoo/releases/x86/autobuilds/20121016/stage3-i686-20121016.tar.bz2  
> 
> 3、下载portage包  
> 
> > downloads-mirrors-6、Asia-China-sohu.inc(http)-snapshots/portage-latest.tar.bz2  
> 
> > #实际地址  
> 
> > http://mirrors.sohu.com/gentoo/snapshots/portage-latest.tar.bz2  
> 
> 4、解压  
> 
> > tar xvjpf stage3-i686-20121016.tar.bz2  
> > tar xvjf /mnt/gentoo/portage-latest.tar.bz2 -C /mnt/gentoo/usr  
> 
> > #这里tar参数p：表示按原地址解压  
> >   
> 
> 这里，可以配置/mnt/gentoo/etc/portage/make.conf 来用多核一起编译软件  
> 
> > nano -w /mnt/gentoo/etc/portage/make.conf  
> > MAKEOPTS="-j2"  
> 
>   

7、选源、选同步  

> 选源  
> mirrorselect -i -o >> /mnt/gentoo/etc/portage/make.conf  
> 
> > #这里我选了3个  

> > GENTOO\_MIRRORS="http://mirrors.163.com/gentoo/  
> > 
> > > > > >   ftp://mirrors.sohu.com/gentoo/  
> > > > > >   http://mirrors.sohu.com/gentoo/"  

> 选同步  
> mirrorselect -i -r -o >> /mnt/gentoo/etc/portage/make.conf  

> >     SYNC="rsync://rsync.cn.gentoo.org/gentoo-portage"  

  
8、chroot  

> 复制dns信息  

> > cp -L /etc/resolv.conf /mnt/gentoo/etc/  

  

> 加载必需的文件系统  
> 
> > mount -t proc none /mnt/gentoo/proc  
> > mount --rbind /sys /mnt/gentoo/sys  
> > mount --rbind /dev /mnt/gentoo/dev  

  

> chroot操作  
> 
> > chroot /mnt/gentoo /bin/bash  
> > env-update  
> > source /etc/profile  
> > export PS1="(chroot) $PS1"  

  
9、更新portage树，保持安装软件的最新版  

> emerge --sync  

> 如果有些软件包已经更新，则再运行emerge --oneshot portage 更新  

>   
>   

10、自定义安装模式  

> eselect profile list  
> 
> > Available profile symlink targets:  
> >   \[1\]   default/linux/x86/10.0 \*  
> >   \[2\]   default/linux/x86/10.0/selinux  
> >   \[3\]   default/linux/x86/10.0/desktop  
> >   \[4\]   default/linux/x86/10.0/desktop/gnome  
> >   \[5\]   default/linux/x86/10.0/desktop/kde  
> >   \[6\]   default/linux/x86/10.0/developer  
> >   \[7\]   default/linux/x86/10.0/server  
> >   \[8\]   hardened/linux/x86  
> >   \[9\]   hardened/linux/x86/selinux  
> >   \[10\]  hardened/linux/uclibc/x86  
> 
> eselect profile set 4  
> nano -w /etc/portage/make.conf  
> 
> > USE="gtk gnome -qt4 -kde dvd alsa cdr"
> 
> > USE参数很重要，这里是自定义要安装的软件。  
> 
> > USE参数中文说明：  
> > http://linux.chinaunix.net/techdoc/desktop/2007/10/20/970341.shtml  
> 
>   
>   

11、安装内核  

> 设置时区  
> 
> > cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
> > echo "Asia/Shanghai" > /etc/timezone  

> 安装内核源码  
> 
> > emerge gentoo-sources  
> > 安装好后查看ls -l /usr/src/linux  
> > 会有内核源代码 Linux-->Kernel 3.5.7-gentoo  
> 
> 自动安装内核  
> 
> > emerge genkernel                          #安装genkernel软件包  
> > genkernel all  
> > ls /boot/kernel\* /boot/initramfs\*       #查看是否已经有内核文件  
> 
> 手动添加内核模块  
> 
> > 列：nano -w /etc/conf.d/modules  
> >        modules\_2\_6="3c59x"  
> 
>   
>   

12、设置配置文件  

> nano -w /etc/fstab  
> 
> > 注释掉全部内容，然后添加  
> > /dev/sda1   /boot        ext2    defaults,noatime     0 2  
> > /dev/sda2   none         swap    sw                   0 0  
> > /dev/sda3   /            ext3    noatime              0 1  
> > /dev/cdrom  /mnt/cdrom   auto    noauto,user          0 0  

>   
>   
> #设置主机名  
> nano -w /etc/conf.d/hostname          
> 
> > hostname="leaf"  
> 
>   
> #设置域里的计算机名和网络  
> nano -w /etc/conf.d/net  
> 
> > dns\_domain\_lo="leafnet"  
> > config\_eth0="dhcp"  
> >   
> 
> #设置网络接口开机启动  
> cd /etc/init.d  
> 
> > ln -s net.lo net.eth0  
> > rc-update add net.eth0 default   
> 
>   
> #设置hosts  
> nano -w /etc/hosts  
> 
> > 127.0.0.1     leaf localhost  
> 
>   
> #设置root密码  
> passwd  
>   
> #设置时钟  
> nano -w /etc/conf.d/hwclock  
> 
> > clock="local"  
> 
>   
> #设置语言  
> locale -a  
> nano -w /etc/locale.gen  
> 
> > en\_US.UTF-8 UTF-8  
> 
>   
> nano -w /etc/env.d/02locale  
> 
> > LANG="en\_US.UTF-8 UTF-8"  
> > LC\_COLLATE="C"  
> 
>   
>   

13、安装系统工具  

> #log工具  

> emerge syslog-ng  
> rc-update add syslog-ng default  

  

> #cron  

> emerge vixie-cron  
> rc-update add vixie-cron default  
>   
> #安装mlocate  
> emerge mlocate  
>   
> #设置sshd服务开启启动  
> rc-update add sshd default  
> nano -w /etc/inittab  
> 
> > s0:12345:respawn:/sbin/agetty 9600 ttyS0 vt100  
> > s1:12345:respawn:/sbin/agetty 9600 ttyS1 vt100  
> 
>   
> #安装dhcp客户端  
> emerge dhcpcd  
>   

  
14、安装GRUB  

> emerge grub

> nano -w /boot/grub/grub.conf  
> 
> > default 0  
> > timeout 30  
> > splashimage=(hd0,0)/boot/grub/splash.xpm.gz  
> >   
> > title Gentoo Linux 3.3.7  
> > root (hd0,0)  
> > kernel /boot/kernel-genkernel-x86-3.5.7-gentoo root=/dev/sda3  
> > initrd /boot/initramfs-genkernel-x86-3.5.7-gentoo  
> 
>   
> grep -v rootfs /proc/mounts > /etc/mtab  
> grub-install --no-floppy /dev/sda  
> grub --no-floppy  
> 
> > root (hd0,0)  
> > setup (hd0)  
> > quit   
> 
>   

15、重启，至此安装完成  

> exit  
> umount -l /mnt/gentoo/dev{/shm,/pts,}  
> umount -l /mnt/gentoo{/boot,/proc,}  
> reboot  

>   

16、建普通账户和清理文件  

> 建账户  
> useradd -m -G users,wheel,audio -s /bin/bash leaf  
> passwd leaf  

>   
> 清理文件  
> rm /stage3-i686-20121016.tar.bz2\*  
> rm /portage-latest.tar.bz2\*  

  
  
备注：以上是gentoo基本系统，X window 等都没有安装。  
  

![vmware安装gentoo - leaf - ------坚持雅操------](http://img3.ph.126.net/2zpvk_RktRS-X3t2soSQ4w==/6598189069493526073.jpg "vmware安装gentoo - leaf - ------坚持雅操------")