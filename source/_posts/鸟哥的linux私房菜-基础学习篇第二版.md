---
title: 鸟哥的linux私房菜-基础学习篇(第二版)
tags:
  - 未分类
id: '54'
abbrlink: 2598844820
date: 2010-06-09 20:30:00
---

2011-05-11更新

要深入学习及加强的有：

       1、vim多练习

       2、sed、awk、grep、cut、sort、uniq深入学习

       3、shell脚本深入学习

       4、PAM模块学习

       5、quota实践(和ldap、samba一起)

       6、at、crontab实践

       7、grub2学习

       8、make学习

       9、日志管理、系统备份实践

     10、logrotate实践

     11、xorg.conf 学习

     12、内核编译、驱动模块管理等联系

  

第一部分

一、  
    GNU、GPL、FSF、LSB、LHS、VFS(六)  
二、  
    多学、多练、多总结、多领悟

三、

    分区

    硬件设备号：/dev/lp0 /dev/st0 /dev/ht0

四、

    系统安装：

        utc：夏令时，没有用不要设置

        selinux：没什么用，关掉好了

    多重启动：

        dd if=dev/sda? of=/home/mbr bs=512 count=1 #?为linux安装的盘符

        然后复制到windows盘，安装windows并更改boot.ini

五、

     1、date +% 、cal 、bc scale 

     2、startx、exit、快捷键  
     3、man info  
     4、shutdown -t -h -r -c -k  -t 秒数  其他 +分钟

  

第二部分

六、

     1、u、g、o、a  421   
     2、chown、chgrp、chmod -R                                                                    注意 -R  
     3、- d l b c s p  
     4、LHS  
七、

    1、cd - ~ . .. 、 ls -a -l -i -d   
         mkdir -m -p  rmdir -p  
    2、cp mv rm   :cp -a -p -d -r -f -i -l -s -u                                                   注意 -u -r  
    3、cat tac nl more less head tail od  
    4、umask chattr lsattr  文件的安全属性 特殊权限  
          chattr +i +a

          --t--t--s  
    5、which whereis locate find  
         whereis  -m -b -s  
         find -time -user  -name -perm -exec                                                     要掌握  
八、  
     df、du、cfdisk、fsck、mount、mkfs、ln

     /etc/fstab  /etc/mtab

    1、扇区、物理存取原理  
    2、df du 

         df：系统目录 du：当前目录  
          fdisk mke2fs mkswap fsck  
    3、ln -s   
    4、mount  -t -o -L      -o rw,sync,auto,dev,suid,exec,user,defaults,remount  要掌握  
         将设备文件挂载到目录  
         ：e2lable 设备名 lable  
         dumpe2fs  
    5、/etc/fstab

    6、mkswap、swapon、swapoff   
九、

     tar、dd、cpio  
    1、tar -z -j -c -x -v -f -p -P --exclude  -N  
    2、dd if=dev/sda? of=/home/mbr bs=512 count=1 #?为linux安装的盘符  
    3、cpio -ocvB -icduv  
   
第三部分    
十、

     编辑模式：0、$、g、G、x、d、y、p、c、u、

     命令模式：w、q、e！、：w、ZZ、：set nu   
十一、

     cut、grep、sort、uniq、tee、split、xargs、alias、history、&& ||

     配置文件：bashrc、profile、inputrc、locale

十二、  
     sed、awk、grep、printf、字符  
十三、  
   1、if elif else fi  
   2、case $n in "") \*) esac  
   3、while \[\] do done  
      unil \[\] do done  
   4、for n in     do done  
  
第四部分  
十四、

   配置文件：passwd、shadow、securetty、nologin、sudoers

   groups、newgrp、useradd、passwd、userdel、who、mail

十五、  
   quota quotacheck edquota quotaon quotaoff 

   1、useradd、passwd

   2、vi /etc/fstab、mount -o remount 

   3、quotacheck -avug

   4、quotaon -avug

   5、edquota -u  edquota -p  edquota -t 

   6、/etc/rc.d/rc.local

   #   repquota -a 

十六、

   at.deny、cron.deny、crontab

   at、atq、atrm  
   crontab -l   
十七、

   &、jobs、fg % 、bg % 、kill

   ps aux、top、pstree -Aup

   free、rname -r -a 、uptime、dmesg、

   fuser、lsof、pidof        #不熟

  

第五部分  
十八、

    启动过程、inittab、rc.sysinit、sysconfig、rc.local、

    lsmod、modinfo、modprobe  -r、modprobe.conf 

    grub设置

十九、  
    configure   make   make clean   make install

    ldconfig、ldd    
二十、  
   rpm -ivh  
二一、  
    xinetd.conf、hosts.deny

    独立守护程序  
二二、

    syslog.conf  
    logrotate：

        monthly          #每个月轮替

        size=10M       #大于10M自动轮替

        rotate 5          #保存5份

        compress       #压缩

        sharedscripts  #？

        prerotate        #轮替前预处理

             /usr/bin/chattr -a /var/log/admin.log

        endscript

        sharedscripts

        postrotate      #轮替处理

            /usr/bin/killall -HUP syslogd

            /usr/bin/chattr +a /var/log/admin.log

        endscript

二三、  
        多种备份手段  
二四、  
        xorg.conf、inittab

          module         #加载模块

          inputdevice   #键盘鼠标设置

          files              #显示字体

          monitor         #水平、垂直刷新频率

          device           #显卡驱动

          screen          #屏幕分辨率

          serverlayout  #要用的设置

二五、  
       lspci、iostat

       LVM  
二六、  
   核心编译