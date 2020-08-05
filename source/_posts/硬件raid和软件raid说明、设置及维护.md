---
title: 硬件raid和软件raid说明、设置及维护
tags:
  - raid
categories:
  - Hardware
  - storage
id: '274'
abbrlink: 582936588
date: 2010-11-20 08:31:00
---

说明：  
硬件raid一定要用raid卡或者板载raid功能，用raid卡的硬盘接在raid卡上，用板载raid的硬盘接在硬盘上  
软件raid不需要raid卡或者板载raid，只要硬盘插在主板上即可  
   
      关于硬盘：  
              sas硬盘：串行scsi硬盘  
              sata硬盘：普通硬盘，串行ata硬盘  
   
     关于网络存储：  
              nas：相当于片上系统+硬盘。能独立运行，独立提供存储服务  
              san：存储网络，通过服务器对外提供存储服务  
              相关知识：  
                          [NAS与SAN存储解决方案优劣比较](http://tech.sina.com.cn/roll/2008-12-15/0913914313.shtml)  
                          [家用NAS选购经验谈](http://news.sanhaostreet.com/NewsData/2009/6/2009625164357166.shtml)  
                          [家用NAS常见处理器全解析](http://storage.it168.com/a2009/0603/582/000000582556.shtml)  
  
设置：  
硬件raid设置：  
       1、开机自检时按ctrl+R进入配置界面：  
       2、在VD Mgmt中，按F2创建VD  
       3、 选RAID模式，选物理硬盘，选容量(就像硬盘分区一样)。这样就创建好一个VD  
       4、选初始化VD(就像格式化分区一样)  
       5、在选容量、初始化等00000000  
   --------------------------------------------------  
       6、配置热备：  
             全局热备：  
            1、按ctrl+R切换到PD Mgmt  
            2、选空盘，按F2，选make global hs，按确定即可  
             某磁盘组热备：  
            1、VD Mgmt界面，选磁盘组，按F2，选manage ded.HS，选硬盘即可  
硬件raid--系统安装  
       [   在主板RAID上(俗称的FakeRAID)安装UBUNTU10.04](http://forum.ubuntu.org.cn/viewtopic.php?t=274182)  
  
软件raid设置：(ubuntu)  
         1、先对每个硬盘进行分区：建空分区表，分区(选择用于：raid物理卷)，备份分区表到其他硬盘  
               alt+f2   sudo sfdisk -d /dev/sda | sudo sfdisk  --force /dev/sdb  
          2、建raid阵列  
                sudo mdadm --create /dev/md0 --auto=yes --force -R --level=raid1 --raid-devices=2 /dev/sd\[a-b\]1   
   ---------------------------------------------------  
lvm设置：  
        1、 对md0进行创建lvm物理卷  
        2、创建lvm卷组  
        3、想对新硬盘分区一样创建lvm逻辑卷并分区  
系统安装：  
         跟单硬盘一样安装即可  
  
\-----------------------------------------------------------  
安装操作系统  
         ^  
对逻辑卷进行文件系统选择和挂在目录  
         ^  
创建lvm逻辑卷                          lv  
         ^  
创建lvm卷组                             vg  
         ^  
对RAID进行创建LVM物理卷     pv  
         ^  
根据分区数，创建RAID           md  
         ^  
N个硬盘,各自分区                    sd  
\------------------------------------------------------------  
  
硬盘容量不够的话，先硬盘分区，建raid，建lvm物理卷，扩lvm卷组，扩某个lvm逻辑卷，扩容xfs分区  
linux系统下操作：     cfdisk          mdadm   pvcreate        vgextend     lvextend                xfs\_growfs