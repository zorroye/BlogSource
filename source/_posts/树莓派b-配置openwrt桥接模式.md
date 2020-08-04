---
title: 树莓派B+ 配置openwrt桥接模式
tags:
  - 树莓派
categories:
  - Hardware
  - 树莓派
id: '174'
abbrlink: 690818048
date: 2015-02-11 13:49:00
---

实现：桥接模式，无线AP，迅雷远程

硬件：树莓派B+，8188cus无线网卡，AX88772A有线网卡，其他

  

1、下载并刷入tf卡，远程连接等

> http://downloads.openwrt.org/snapshots/trunk/brcm2708/generic/openwrt-brcm2708-sdcard-vfat-ext4.img

  

2、安装驱动

> opkg update
> 
> opkg install kmod-rtl8192cu                               #无线网卡驱动
> 
> opkg install kmod-usb-net kmod-usb-net-asix  #有线网卡驱动
> 
>   

3、安装软件

> opkg update
> 
> opkg install luci luci-i18n-base-zh-cn
> 
> opkg install usbutils ip 
> 
> opkg install kmod-usb-core kmod-usb-uhci kmod-usb-ohci kmod-usb2
> 
> opkg install hostapd wireless-tools                #无线AP必备
> 
>   
> 
>   

4、配置

> 无线
> 
> wifi detect > /etc/config/wireless
> 
> vi /etc/config/wireless
> 
> config wifi-device 'radio0'
> 
>         option type 'mac80211'
> 
>         option channel '11'
> 
>         option hwmode '11g'
> 
>         option path 'platform/bcm2708\_usb/usb1/1-1/1-1.2/1-1.2:1.0'
> 
>         option htmode 'HT20'
> 
>   
> 
> config wifi-iface
> 
>         option device 'radio0'
> 
>         option network 'lan'
> 
>         option mode 'ap' 
> 
>         option ssid 'OpenWrt'
> 
>         option disabled '0'                #是否广播ssid
> 
>         option encryption 'none'#加密模式
> 
>   

> 网络
> 
> config interface 'loopback'
> 
>         option ifname 'lo'
> 
>         option proto 'static'
> 
>         option ipaddr '127.0.0.1'
> 
>         option netmask '255.0.0.0'
> 
>   
> 
> config interface 'lan'
> 
>         option proto 'dhcp'                #可设置为其他，设置IP是为了树莓派能上网
> 
>         option type 'bridge'
> 
>         option ifname 'eth0 eth1'
> 
>   
> 
> config alias                                   #设置树莓派管理地址，找了好久终于搞定管理地址
> 
>         option interface 'lan'
> 
>         option proto 'static'
> 
>         option ipaddr '192.168.1.3'
> 
>         option netmask '255.255.255.0'
> 
>   
> 
> config globals 'globals'
> 
>         option ula\_prefix 'fd40:132b:9a10::/48'
> 
>   

![树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------](http://img0.ph.126.net/ekuUkBkj24IdK_dB6e-pcQ==/6619470117049688565.png "树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------")

![树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------](http://img1.ph.126.net/QQYYOx2xnTewZQZCYaS-jQ==/3113394717414550858.png "树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------") 

![树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------](http://img0.ph.126.net/S21VuiewLa6mZVfTyIPm1g==/3113676192391261497.png "树莓派B+ 配置openwrt桥接模式 - leaf - ------坚持雅操------")

 

  

5、安装迅雷远程

>   

>   

参考

[http://www.leiphone.com/news/201406/diy-a-smart-router-topic-openwrt.html](http://www.leiphone.com/news/201406/diy-a-smart-router-topic-openwrt.html)

[http://blog.sina.com.cn/s/blog\_40983e5e0102v6qt.html](http://blog.sina.com.cn/s/blog_40983e5e0102v6qt.html)

[http://www.shuyz.com/install-openwrt-on-raspberry-as-a-wireless-router.html](http://www.shuyz.com/install-openwrt-on-raspberry-as-a-wireless-router.html)

[http://www.tuicool.com/articles/rmmemif](http://www.tuicool.com/articles/rmmemif)