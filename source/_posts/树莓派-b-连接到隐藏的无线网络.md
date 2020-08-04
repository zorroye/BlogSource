---
title: 树莓派 B+ 连接到隐藏的无线网络
tags:
  - 树莓派
categories:
  - Hardware
  - 树莓派
id: '176'
abbrlink: 4154792531
date: 2015-03-07 11:24:00
---

pi@YRPI ~ $ cat /etc/network/interfaces

auto lo

iface lo inet loopback

  

iface eth0 inet static

address 192.168.1.16

netmask 255.255.255.0

gateway 192.168.1.1

  

auto wlan0

allow-hotplug wlan0

iface wlan0 inet static

address 192.168.1.17

netmask 255.255.255.0

gateway 192.168.1.1

wpa-scan-ssid 1                #这个设置成1 可以连接到隐藏的网络

wpa-ap-scan 1                  #这个设置成1 可以连接到隐藏的网络

wpa-ssid "HELLO"

wpa-psk "123456"

#wpa-roam /etc/wpa\_supplicant/wpa\_supplicant.conf

  

iface default inet dhcp

  

auto wlan0  
allow-hotplug wlan0  
iface wlan0 inet dhcp  
   wpa-scan-ssid 1  
   wpa-ap-scan 1  
   wpa-key-mgmt WPA-PSK  
   wpa-proto RSN WPA  
   wpa-pairwise CCMP TKIP  
   wpa-group CCMP TKIP  
   wpa-ssid "My Secret SSID"  
   wpa-psk "My SSID PSK"

  

修复断线问题。设置无线网卡不节能。

> lsmod
> 
> > 8192cu                550797  0
> 
> >   
> 
> 创建sudo nano /etc/modprobe.d/8192cu.conf
> 
> \# Disable power saving
> 
> options 8192cu rtw\_power\_mgnt=0 rtw\_enusbss=1 rtw\_ips\_mode=1

  

相关命令

> iwconfig wlan0    查看无线接口状态
> 
> iwlist wlan0 scan    扫描无线网络

  

  

http://www.geekfan.net/8776/

http://www.dafinga.net/2013/01/how-to-setup-raspberry-pi-with-hidden.html     需要翻墙