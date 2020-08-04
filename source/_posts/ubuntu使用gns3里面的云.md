---
title: ubuntu使用gns3里面的云
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '194'
abbrlink: 2281735761
date: 2012-05-09 15:46:00
---

![ubuntu使用gns3里面的云 - leaf - ------坚持雅操------](http://img3.ph.126.net/i9rtzE1JV_dBxKRttmg4KA==/2724677774576652283.jpg "ubuntu使用gns3里面的云 - leaf - ------坚持雅操------")

   
说明：只对vmet8 进行说明  
环境：  

> vmet8 ：172.16.43.0网段  

> vmware虚拟机IP：172.16.43.141  

> R3 IP：                  172.16.43.150  

注：linux需要用 sudo gns3 来启动  
  
  
1、云设置:  

> 双击云，然后添加vmet8 即可  
> 
> ![ubuntu使用gns3里面的云 - leaf - ------坚持雅操------](http://img6.ph.126.net/9P-rRwHWyfXioyqu2NWeeg==/3095098843927878076.jpg "ubuntu使用gns3里面的云 - leaf - ------坚持雅操------")
> 
>    

2、添加R3，连接云和R3，开启云和R3  
  
3、设置R3 IP地址，开启f1/0端口  
  
4、能相互ping通～～  

> ![ubuntu使用gns3里面的云 - leaf - ------坚持雅操------](http://img0.ph.126.net/ekc1qTjFfcN9oJd6Ws5r6g==/3093972944021031640.jpg "ubuntu使用gns3里面的云 - leaf - ------坚持雅操------")
> 
>  
> 
> ![ubuntu使用gns3里面的云 - leaf - ------坚持雅操------](http://img2.ph.126.net/YdHqigKX3OIgmqdo99ep4A==/109493765957949262.jpg "ubuntu使用gns3里面的云 - leaf - ------坚持雅操------")
> 
>