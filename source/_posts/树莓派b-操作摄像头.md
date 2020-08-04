---
title: 树莓派B+ 操作摄像头
tags:
  - 树莓派
categories:
  - Hardware
  - 树莓派
id: '177'
abbrlink: 2348587197
date: 2015-03-16 10:47:00
---

1、开启树莓派的摄像头功能

> sudo raspi-config

> 重启

2、安装相关软件

> sudo apt-get install luvcview

> sudo apt-get install python-opencv python-scipy python-numpy python-pip

> sudo pip install https://github.com/ingenuitas/SimpleCV/zipball/master

>   

3、测试SimpleCV库

> python

> Python 2.7.3 (default, Mar 18 2014, 05:13:23)
> 
> \[GCC 4.6.3\] on linux2
> 
> Type "help", "copyright", "credits" or "license" for more information.
> 
> \>>>import SimpleCV
> 
> \>>>

  

4、用摄像头保存一张图片

> from SimpleCV import Camera,Display  
> from time import sleep  
>   
> myCamera = Camera(prop\_set={"width":320,"height":240})  
>   
> frame = myCamera.getImage()  
> frame.save("camera-output.jpg")
> 
>   
> 
>   

> ![树莓派B+ 操作摄像头 - leaf - ------坚持雅操------](http://img2.ph.126.net/M95LVRZPOdHpdmovl9kuyg==/6608866426911394034.jpg "树莓派B+ 操作摄像头 - leaf - ------坚持雅操------")
> 
>  

5、人脸检测

> from SimpleCV import Camera,Display  
> from time import sleep  
>   
> myCamera = Camera(prop\_set={"width":320,"height":240})  
>   
> myDisplay = Display(resolution=(320,240))  
>   
> while not myDisplay.isDone():  
> frame = myCamera.getImage()  
> faces = frame.findHaarFeatures('face')  
> if faces:  
> for face in faces:  
> print "Face at: " + str(face.coordinates())  
> else:  
> print "No faces detected."  
> frame.save(myDisplay)  
> sleep(.1)  
>   
> 
> ![树莓派B+ 操作摄像头 - leaf - ------坚持雅操------](http://img2.ph.126.net/IaHfSsP6KyeRAZZHRoJBSw==/2453335897027967291.png "树莓派B+ 操作摄像头 - leaf - ------坚持雅操------")
> 
>  

6、监控

> 1、安装抓图软件sudo apt-get install fswebcam
> 
> 2、Yeelink注册，并添加设备和传感器。（不交钱是公开的）
> 
> 3、linux新建脚本
> 
> sudo fswebcam -d /dev/video0 -r 320x240 --bottom-banner --title "RaspberryPi @ Yeelink" --no-timestamp /home/pi/yeelink.jpg  
> curl --request POST --data-binary @"/home/pi/yeelink.jpg" --header "U-ApiKey:\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" http://api.yeelink.net/v1.0/device/\*\*\*\*\*/sensor/\*\*\*\*\*/photos  
>   

> > u-apikey：在yeelink的用户的账户这里找
> 
> > 后面的地址在传感器这里找
> 
>   
> 
> 4、加入到crontab

> > crontab -e

> > \*/1 \* \* \* \* /home/pi/yeelink.sh
> 
>   

> ![树莓派B+ 操作摄像头 - leaf - ------坚持雅操------](http://img0.ph.126.net/x3SH3AJYpeb967AyqmO8Mw==/3363063021841550211.png "树莓派B+ 操作摄像头 - leaf - ------坚持雅操------")
> 
>