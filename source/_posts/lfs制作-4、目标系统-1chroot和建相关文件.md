---
title: LFS制作-4、目标系统-1chroot和建相关文件
tags:
  - 未分类
id: '229'
abbrlink: 3518050721
date: 2012-10-25 13:30:00
---

挂载相关系统

#export LFS=/mnt/lfs

#mkdir -pv $LFS

#mount -v -t ext3 /dev/hda1 $LFS  
#ln -sv $LFS/tools /  

mkdir -pv $LFS/{dev,proc,sys}

mknod -m 600 $LFS/dev/console c 5 1

mknod -m 666 $LFS/dev/null c 1 3

mount -v --bind /dev $LFS/dev

mount -vt devpts devpts $LFS/dev/pts

mount -vt tmpfs shm $LFS/dev/shm

mount -vt proc proc $LFS/proc

mount -vt sysfs sysfs $LFS/sys

chroot "$LFS" /tools/bin/env -i \\

    HOME=/root TERM="$TERM" PS1='\\u:\\w\\$ ' \\

    PATH=/bin:/usr/bin:/sbin:/usr/sbin:/tools/bin \\

    /tools/bin/bash --login +h

  

\-------------------------------------------------------------------------------------

  

1、建标准的目录树

mkdir -pv /{bin,boot,etc/opt,home,lib,mnt,opt}

mkdir -pv /{media/{floppy,cdrom},sbin,srv,var}

install -dv -m 0750 /root

install -dv -m 1777 /tmp /var/tmp

mkdir -pv /usr/{,local/}{bin,include,lib,sbin,src}

mkdir -pv /usr/{,local/}share/{doc,info,locale,man}

mkdir -v  /usr/{,local/}share/{misc,terminfo,zoneinfo}

mkdir -pv /usr/{,local/}share/man/man{1..8}

for dir in /usr /usr/local; do

  ln -sv share/{man,doc,info} $dir

done

mkdir -v /var/{lock,log,mail,run,spool}

mkdir -pv /var/{opt,cache,lib/{misc,locate},local}

  

2、建必要的符号连接

ln -sv /tools/bin/{bash,cat,echo,grep,pwd,stty} /bin

ln -sv /tools/bin/perl /usr/bin

ln -sv /tools/lib/libgcc\_s.so{,.1} /usr/lib

ln -sv /tools/lib/libstdc++.so{,.6} /usr/lib

ln -sv bash /bin/sh

> #安装软件包的时候相应的连接会被替代掉

  

3、建/etc/mtab  

touch /etc/mtab

  

4、建/etc/passwd

cat > /etc/passwd << "EOF"

root:x:0:0:root:/root:/bin/bash

nobody:x:99:99:Unprivileged User:/dev/null:/bin/false

EOF

  

5、建/etc/group

cat > /etc/group << "EOF"

root:x:0:

bin:x:1:

sys:x:2:

kmem:x:3:

tty:x:4:

tape:x:5:

daemon:x:6:

floppy:x:7:

disk:x:8:

lp:x:9:

dialout:x:10:

audio:x:11:

video:x:12:

utmp:x:13:

usb:x:14:

cdrom:x:15:

mail:x:34:

nogroup:x:99:

EOF

  

6、从新用bash登录，这样就有名字了

exec /tools/bin/bash --login +h

  

7、建日志文件

touch /var/run/utmp /var/log/{btmp,lastlog,wtmp}

chgrp -v utmp /var/run/utmp /var/log/lastlog

chmod -v 664 /var/run/utmp /var/log/lastlog