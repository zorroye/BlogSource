---
title: ubuntu14.04 链接iscsi
tags:
  - 未分类
id: '356'
date: 2016-02-06 17:56:00
---

  
一、安装  

> sudo apt-get install open-iscsi 然后重启  
>   

二、配置  

> sudo nano /etc/iscsi/iscsi.conf  
> #设置开机自动连接iscsi设备  
> 
> > node.startup = automatic   
> 
> #设置单向验证的账号密码  
> 
> > node.session.auth.authmethod = CHAP  
> > node.session.auth.username = username  
> > node.session.auth.password = password  
> > \----------双向验证再增加以下两行---------------  
> > node.session.auth.username\_in = username  
> > node.session.auth.password\_in = password

>   

三、连接  

> 查找iscsi设备  
> 运行该命令后在/etc/iscsi下面会多出nodes和send\_targets文件夹  
> 
> > sudo iscsiadm -m discovery -t sendtargets -p 192.168.3.12  
> 
> 连接  
> 
> > sudo iscsiadm -m node -T iqn.ubuntu -p 192.168.3.12 -l  
> > 
> > ![ubuntu14.04 链接iscsi - leaf - ------勤解万难------](http://img2.ph.126.net/MAwRwRK7yJjnuvmtUKIAaA==/6631214000750360321.png "ubuntu14.04 链接iscsi - leaf - ------勤解万难------")
> > 
> >  
> > 
> > ![ubuntu14.04 链接iscsi - leaf - ------勤解万难------](http://img0.ph.126.net/93IO30mUx6IiDu-2D2kXPg==/6598138492018427937.png "ubuntu14.04 链接iscsi - leaf - ------勤解万难------")
> > 
> >    
> 
> 格式化及挂载  
> 
> > fdisk /dev/sdd  
> > mkfs.ext4 /dev/sdd1  
> > mkdir /mnt/iscsi1  
> > mount /dev/sdd1 /mnt/iscsi1  
> 
>   

四、配置开机挂载  

> 设置网络为动态获取或者静态地址/etc/network/interface
> 
> > auto eth1  
> > iface eth1 inet dhcp  
> 
> 查看设备UUID  
> 
> > ls -l /dev/disk/by-uuid 可以看到刚挂载的设备的UUID  
> 
> 更改/etc/fstab  
> 
> > UUID=c017977c-a0d8-4e6b-9eee-38b6f5c17ebc    /mnt/iscsi1 ext4 \_netdev,relatime 0 2  
> >   
> 
>   

参考  
http://blog.csdn.net/sinchb/article/details/8433994  
http://blog.csdn.net/wbryfl/article/details/6702347  
其他  
http://www.server-world.info/en/note?os=Ubuntu\_14.04&p=iscsi&f=2  
http://manpages.ubuntu.com/manpages/hardy/man8/iscsiadm.8.html  

>   
>   
>