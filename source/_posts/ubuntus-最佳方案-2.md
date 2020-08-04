---
title: ubuntus 最佳方案 -2
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '276'
abbrlink: 387816121
date: 2012-04-17 15:17:00
---

系统使用：ubuntu-8.04.4-server-i386.iso  
  
1、文件目录  
/sys：用于存放系统信息  

![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img5.ph.126.net/cXj5mkGxWJmsMc7bmwVVKg==/2583095861291110315.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")

   
2、/etc/fstab  
      sudo blkid  查看分区uuid  
  
3、lvm  逻辑卷管理器  
     硬盘上面建lvm，lvm上面建分区。易于扩容和备份等  
  
4、tasksel  用于快速安装服务套件  

     ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img9.ph.126.net/STWB9322u2SY1-r6MX3cOQ==/634163122546532059.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")

 

 5、更改语系  
       查看当前语言设置：locale  
       语言设置文件：/etc/default/locale  

       ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img8.ph.126.net/WNWkGw6u0Doq-dfdelmgPQ==/3084684269789498848.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")

   
6、nano使用方法  
      ctrl+o ：保存  
      ctrl+x ：退出  
      ctrl+w：查找  
      ctrl+k： 剪切  
      ctrl+u：撤销  

      ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img2.ph.126.net/99RlVjpIJA2LoTEI86bCtw==/2601954684730730712.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")

   
7、mc 图形化资源管理器   
  
8、包管理软件  
     ----apt工具  
     apt相关文件  
        /etc/apt/sources.list          软件包资源列表  
        /etc/apt/apt.conf.d            apt零碎配置文件  
        /var/cache/apt/archives    存放已经下载的软件包  
    apt软件仓库分类  
        main           自由软件，ubuntu完全支持  
        restricted    不完全自由软件，但被广泛使用，ubuntu也提供支持  
        universe     依赖社区提供支持，ubuntu不提供安全补丁等支持  
        multiverse   非自由软件，完全没有支持  
     apt-get命令  
        update         更新软件包列表  
        upgrade       升级所有软件包  
        purge           彻底删除软件包  
        source          下载源码包  
        dist-upgrade  升级整个发行版  
      apt-cache命令  
         search          搜索软件包在ubuntu下的名字  
      aptitude命令  
         图形界面安装软件  
      dpkg命令  
         dpkg -l         查找软件包是否已经安装  
         dpkg -L        查找软件包包含哪些文件  
         dpkg -C        查找哪些软件未完成安装  
         dpkg-reconfigure     自动配置已安装的软件包  
  
9、服务的启动和停止  
 update-rc.d  apache defaults    设置默认启动  
         update-rc.d  apache purge        不自动启动  
  
10、网络配置  
                /etc/network/interfaces   网卡及IP地址配置文件  
                ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img2.ph.126.net/1WnTuBHmsufWHtDGPaKQ3w==/1299569967490523612.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")  
      重启网络  
                 /etc/init.d/networking restart         
      DNS配置文件  
                 /etc/resolv.conf  
                 ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img2.ph.126.net/dp58g5iEd6j07JkpRHcuQQ==/2759580671688692722.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")  
       hosts文件  
                 /etc/hosts   
  
11、时间同步（每天同步一次）  
       sudo nano /etc/cron.daily/timeupdate  
          添加： ntpdate ntp.ubuntu.com  
                     关于ntp servers，访问：http://tf.nist.gov/tf-cgi/servers.cgi  
       sudo chmod 755 /etc/cron.daily/timeupdate  
  
12、远程管理ubuntus  
       ---服务器上安装ssh-s  
           sudo apt-get install openssh-server  
                 ssh配置文件：/etc/ssh/sshd\_config  
       ---客户端远程登录服务器  
           ssh xxx@172.16.43.140    然后输入xxx的密码(xxx为服务器的用户名)  

        ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img8.ph.126.net/XNEalyrGgPBGQtUW3fdrig==/1275081644516690278.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")

 

        查看那些人登录到本机：who  
        踢出用户：  
               ps -ef | grep pts/0  
               kill -9 5593  
        ![ubuntus 最佳方案 -2 - leaf - ------坚持雅操------](http://img0.ph.126.net/HeI2Igi3XztxiaNamKlQYQ==/2655434930305746040.jpg "ubuntus 最佳方案 -2 - leaf - ------坚持雅操------")