---
title: '[转载]ubuntu10.04 x64 安装PacketTracer5.3'
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '367'
abbrlink: 3345977369
date: 2012-12-03 18:29:00
---

  
转自：  
http://kaslnetwork.com/articles/installing-cisco-packettracer-5-3-2-on-64-bit-ubuntu-or-debian/?doing\_wp\_cron=1354528617.3749530315399169921875  
  
PacketTracer5.3只有32位的，而且提供的软件是bin文件。以下提供如何在ubuntu 64位下安装  
方法是：  
安装的时候提取出packettracer的deb文件，然后装好32位库文件，再强制安装packettracer即可  
  
1、下载packettracer5.3  

> 下载地址我忘了，有需要的可以留言。  
>   

2、建sh脚本：PacketTracerx64Hack.sh

#!/bin/bash  
  
\# PacketTracer Installer Hack  
\# Written by K. Law @ http://kaslit.com  
\# PacketTracer is a program by Cisco Systems  
#  
\# The purpose of this script is to install PacketTracer on  
\# the unsupported 64-bit Ubuntu or Debian Linux platforms  
  
echo "Installing Required Libraries"  
apt-get -y install ia32-libs-gtk  
echo "ia32-libs-gtk is the key to the installation. Without it, PacketTracer will not work."  
echo ".deb file exists in /tmp"  
echo " "  
echo "copying installer to ./"  
echo " "  
cp -v /tmp/selfextract.\*/Packet\* ./  
echo "Copy Successful"  
echo " "  
echo "Installing Libraries"  
wget -c http://content.kaslit.com/downloads/getlibs-all.deb  
dpkg -i getlibs-all.deb  
echo " "  
echo "Running dpkg -i --force-architecture Packet\*.deb"  
dpkg -i --force-architecture Packet\*.deb  
echo " "  
echo "PacketTracer is installed"  
echo " "  
echo "Applying libs"  
getlibs /usr/local/PacketTracer5/bin/PacketTracer5  
echo " "  
echo "PacketTracer should now be installed - However, this script is light and does not detect errors."  
echo " "  
echo "Running PacketTracer"  
echo " "  
echo "Did PacketTracer Not Install? If not, look for the ia32-libs-gtk file in the Debian/Ubuntu repositories. It is the key to the successful install." > ~/PacketTracer\_README\_IF\_IT\_FAILED.txt  
/usr/local/PacketTracer5/packettracer

  
3、安装  

> sudo sh PacketTracer53\*  
> 点<enter>阅读说明，阅读到90%的时候，另开一个终端  
> sudo sh PacketTracerx64Hack.sh  
> 该脚本会自动复制packettracer的deb文件，并自动安装