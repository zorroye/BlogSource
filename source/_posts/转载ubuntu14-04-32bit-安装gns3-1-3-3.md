---
title: '[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3'
tags:
  - 未分类
id: '368'
date: 2015-05-23 10:06:00
---

http://www.bearmr.com/index.php/gns3-1-0-for-linux/  
  
0、安装编译环境  

> sudo apt-get install build-essential libelf-dev uuid-dev libpcap-dev python3-dev python3-pyqt4  git  cmake  
>   

0、下载gns3 （仅用于编译插件，可不下）  

> https://github.com/GNS3/gns3-gui/releases/download/v1.3.3/GNS3-1.3.3.source.zip  

  
1、安装Dynamips (思科OS模拟器,下载的所有iou等都需要这个模拟器模拟)  

> git clone git://github.com/GNS3/dynamips.git  
> cd dynamips  
> mkdir build  
> cd build  
> cmake ..  
> make && sudo make install  
>   

> 测试Dynamips  
> dynamips -H 7200  

  
2、安装GNS3-server (gns3后台程序)  

> wget -Oez\_setup.py https://bootstrap.pypa.io/ez\_setup.py  
> sudo python3 ez\_setup.py  
> wget -O get-pip.py https://bootstrap.pypa.io/get-pip.py  
> sudo python3 get-pip.py  

> 用pip命令或apt-get命令安装pyzmq、 tornado 、netifaces这3个依赖的库  
> sudo pip3 install pyzmq  
> sudo pip3 install tornado  
> sudo pip3 install netifaces  

  

> git clone git://github.com/GNS3/gns3-server.git  
> cd gns3-server/  
> sudo python3 setup.py install  

  

> 测试GNS 3-Server  

> gns3server  

  
3、安装gns3-gui (gns3界面)  

> git clone git://github.com/GNS3/gns3-gui.git  
> cd gns3-gui.git/  
> sudo python3 setup.py install  

  
4、安装vpcs (虚拟pc机)  

> sh src/mk.sh i386 (第0步骤下载的程序目录)  
> 将编译的文件拷到gns3目录  

  
5、升级  

> pip3 install gns3-server==1.3.3     ==后面是版本号  

  
  
6、运行GNS3  

> gns3  

  
7、相关设置  

> 下载CiscoIOUKeygen.py和编译好的iouyap  
> 
> > iouyap 是用来在 IOU 和 UDP, TAP 和Ethernet.之间做桥接的。  

>   
> python3 CiscoIOUKeygen.py  

> 新建iourc.txt，复制license和下一行进去  

  

> 下载IOU/IOS 并安装  

> ![[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------](http://img1.ph.126.net/2r7FulZfj_7UBol-puv0OA==/643733271755249902.png "[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------")
> 
>   
> 
> ![[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------](http://img2.ph.126.net/1EAb_LGBwUUWHmZyRKadJA==/1172343278017882178.png "[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------")
> 
>   
> 
> ![[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------](http://img0.ph.126.net/VqehHsnYhAutTxCYl5Yaaw==/6619482211677763503.png "[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------")
> 
>  

8、安装相关工具  
sudo apt-get install roxterm wireshark  
![[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------](http://img0.ph.126.net/IKhsUkL3hVU3kSvSGpQqQw==/6630143076420477582.png "[转载]UBUNTU14.04 32bit 安装GNS3 1.3.3 - leaf - ------勤解万难------")  

  

9、错误提示

Server error from 127.0.0.1:8000: IOU2: The following shared library dependencies cannot be found for IOU image /home/ywz/5Soft/GNS3/images/IOU/i86bi-linux-l3-p-15.0a.bin: libcrypto.so.4

  

解决  sudo ln -s /lib/i386-linux-gnu/libcrypto.so.1.0.0 /lib/i386-linux-gnu/libcrypto.so.4