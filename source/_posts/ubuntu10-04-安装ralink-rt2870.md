---
title: ubuntu10.04 安装ralink rt2870
tags:
  - 未分类
id: '203'
date: 2010-11-23 23:07:00
---

用的笔记本是msi ex465 ，查无线驱动是rt2870(虽然标着是ms-3870，但看win的inf知道是rt2870)

  

第一部分：驱动能安装却不能上网

1、下载驱动  
       [http://www.ralinktech.com/support.php?s=2](http://www.ralinktech.com/support.php?s=2)    下载：RT2870USB(RT2870/RT2770)

  

2、安装  
     1、安装编译环境： sudo apt-get install build-essential linux-headers-generic  
     2、配置文件修改：

                tar -xvf 2010\_0709\_RT2870\_Linux\_STA\_v2.4.0.1.tar.bz2  
                cd  2010\_0709\_RT2870\_Linux\_STA\_v2.4.0.1  
                lsusb   

                      #显示：Bus 001 Device 003: ID 0db0:3870 MICRO STAR INTERNATIONAL

                      #记下代码号：0db0:3870  
                gedit common/rtusb\_dev\_id.c  
                     {USB\_DEVICE(0x0DB0,0x3870)},    

                      #添加在 #ifdef RT2870下面，就是有很多行{USB\_DEVIC 的地方  
                gedit os/linux/config.mk  
                      HAS\_WPA\_SUPPLICANT=y  
                      HAS\_NATIVE\_WPA\_SUPPLICANT\_SUPPORT=y  
        3、编译、安装

               sudo su

               make  
               make install  
               modprobe  rt2870sta  
               exit

  

         4、查看

               iwconfig

 ra0 Ralink STA ESSID:"11n-AP" Nickname:"RT2870STA"  
 Mode:Auto Frequency=2.412 GHz Access Point: Not-Associated   
 Bit Rate:1 Mb/s   
 RTS thr:off Fragment thr:off  
 Link Quality=10/100 Signal level:0 dBm Noise level:0 dBm  
 Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0  
 Tx excessive retries:0 Invalid misc:0 Missed beacon:0

  

      5、每次启动都开启无线

               sudo sh -c 'echo rt2870sta >> /etc/modules'  
        

以上安装好后，驱动已经安装了，但是连不了网，经过我一天的努力，终于找到好东西，分享以下 哈哈～～～

  

第二部分：终极解决方法：

1、在这个页面下下载软件:[compat-wireless](http://wireless.kernel.org/en/users/Download#Download_latest_Linux_wireless_drivers)

            或者 [http://linuxwireless.org/download/compat-wireless-2.6/](http://linuxwireless.org/download/compat-wireless-2.6/)

2、安装

sudo apt-get install build-essential linux-headers-generic

tar -xvf compat-wireless-2.6.tar.bz2

cd compat-wireless-2011-03-20                    #2011-03-20是会变的

sudo su

make

make install 

make unload

reboot

  

重启后，无线网卡即可工作，自动搜索无线信号 

  

总结：虽然现在能用无线了，可最终目的还是要解决第一部分遗留的问题，这样才能学到东西

  

哈哈，开心～～～

  

参考：

[http://ubuntuforums.org/showthread.php?t=1342593](http://ubuntuforums.org/showthread.php?t=1342593)

[http://linuxforums.org.uk/hardware-compatibility/ralink-rt2870-based-usb-wireless-n-adapters-(ubuntu)/](http://linuxforums.org.uk/hardware-compatibility/ralink-rt2870-based-usb-wireless-n-adapters-(ubuntu)/)

\---------------------------------------------------------------------------------------------------------------------------------------------

终极解决方法参考：

[http://thinklouder.cn/tag/compat-wireless-26/](http://thinklouder.cn/tag/compat-wireless-26/)

[http://wireless.kernel.org/en/users/Download](http://wireless.kernel.org/en/users/Download)