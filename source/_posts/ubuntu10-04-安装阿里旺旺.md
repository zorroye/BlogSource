---
title: Ubuntu10.04 安装阿里旺旺
tags:
  - 未分类
id: '39'
abbrlink: 3112032052
date: 2013-01-31 02:23:00
---

阿里旺旺下载地址：http://ge.tt/8sPpGIA  
#地址能打开，但是很慢。  
附下载地址：[http://pan.baidu.com/share/link?shareid=260186&uk=336411764](http://pan.baidu.com/share/link?shareid=260186&uk=336411764)  
  
1、下载相应的库文件  

> 直接安装会提示：错误： 依赖关系没有满足：libqtcore4 (>= 4:4.7.0~beta1)  
> 
> ![Ubuntu10.04 X64 安装阿里旺旺方法 - leaf - ------坚持雅操------](http://img0.ph.126.net/hhGY_S7U2FPMVyidhi2R7w==/6597222598774607540.jpg "Ubuntu10.04 X64 安装阿里旺旺方法 - leaf - ------坚持雅操------")

下载相应库文件：  

> libqtcore4\_4.7.4-0ubuntu8.2\_amd64.deb  
> libqt4-dbus\_4.7.4-0ubuntu8.2\_amd64.deb  
> libqt4-xmlpatterns\_4.7.4-0ubuntu8.2\_amd64.deb  
> libqt4-network\_4.7.4-0ubuntu8.2\_amd64.deb  
> libqtgui4\_4.7.4-0ubuntu8.2\_amd64.deb  
> libqt4-sql\_4.7.4-0ubuntu8.2\_amd64.deb  

下载地址：http://packages.ubuntu.com/  
  
  
2、安装库文件  
一、将库文件一个一个解压，再解压里面的data.tar.lzma，将相应的库文件放到相应的文件夹下  
如：sudo cp -a ～/libqtcore4\_4.7.4-0ubuntu8.2\_amd64/usr/lib/x86\_64-linux-gnu/\*  /usr/lib/x86\_64-linux-gnu/  
       #这里我没有复制其中的文件夹，只复制和文件包名字相同在的库文件  
二、sudo ldconfig  
  
3、安装阿里旺旺  
解压阿里旺旺，把对应的文件放到对应的目录下面即可  

> 把其中的AiWangWang AliWWAutoUpdate 放到/usr/bin下面  
> 把其中的AiWangWang文件夹    放到/usr/share下面  
> 把其中的aliwangwang.desktop 放到/usr/share/applications 下面  
> 把其中的doc/aliwangwang        放到/usr/share/doc/ 下面  
> 把其中的AliWangWang.png       放到/usr/share/pixmaps 下面  
>   
>   

运行效果  

![Ubuntu10.04 X64 安装阿里旺旺方法 - leaf - ------坚持雅操------](http://img0.ph.126.net/ki1l8xMeD43XCvKSWu3QLg==/6598123098796218750.jpg "Ubuntu10.04 X64 安装阿里旺旺方法 - leaf - ------坚持雅操------")

http://pan.baidu.com/share/link?shareid=260186&uk=336411764