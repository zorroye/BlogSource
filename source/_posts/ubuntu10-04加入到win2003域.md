---
title: ubuntu10.04加入到win2003域
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '204'
abbrlink: 1311692127
date: 2011-02-07 00:28:00
---

2014.08.13 ubuntu14.04加域

> 1、下载PBIS
> 
> 2、安装 sudo ./pbis-open-8.0.1.2029.linux.x86\_64.deb.sh
> 
> 3、加域命令

> > sudo su
> > 
> > cd /opt/pbis/bin
> > 
> > domainjoin-cli join --disable ssh hy.com.cn  257769@hy.com.cn

> > ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img2.ph.126.net/tgZoU6lfDmZSnb1ld2UIWg==/6608853232771323788.png "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")

> 4、重启 即可

> > ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img2.ph.126.net/X38cPQXr7whP9jh3vl9cvw==/6608444214445793399.png "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")
> > 
> >  
> 
>  参考：[Join Ubuntu 14.04LTS to a Windows Domain using PBIS Open](http://community.spiceworks.com/how_to/show/80336-join-ubuntu-14-04lts-to-a-windows-domain-using-pbis-open)

>   

  

  

  

virtualbox下试验成功，用的就是likewise-open-gui  
  
win2003:192.168.56.10  
ubuntu：192.168.56.101  
  
0、设置dns  

> sudo nano /etc/resolv.conf  
> nameserver 192.168.56.10     #nameserver就这么写就好了  

  
1、安装samba smbfs  

> sudo apt-get install samba smbfs  

  
2、安装likewise  

> sudo aptitude install likewise-open-gui   #默认即可  

  
3、加域  

> sudo domainjoin-cli join leaf.com domain    #leaf.com为域  domain为域管理员  
> 要求输入域管理员的密码  

  

> 之后会跳出secceeded，然后提示重启  
> 你也可以用图形方式，最后会出现，#退出域点 leave domain  
> 
> ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img618.ph.126.net/q8IJGyBPJu10aV67kTrpKw==/1969761887022951153.jpg "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")  
>   
> 
> win2003下的电脑信息  
> 
> ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img2.ph.126.net/Dfync5Z1O0_o-lEaWSpo-Q==/2871044762548721789.png "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")

   
4、登陆  

> 要填leaf\\ywz      #leaf域的netbios名 ywz为win2003给的账户名。win2003里面先建账户  
> 
> ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img396.ph.126.net/H9Cf2t6M5Qd6kfeux0F0RA==/3065262496380234663.jpg "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")

   

> 登陆后账号信息会显示：  
> 
> ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img854.ph.126.net/PYjlPUmuniVCBwRlncRTyw==/2748040197627127591.jpg "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")

   
  
5、允许AD管理员为ubuntu管理  

> 有两种方法，都是在/etc/sudoers里面改：  

> 1、添加用户组  

> > %leaf\\\\domain^users ALL=(ALL) ALL  
> > %admin ：表示用户组  
> 
> 2、添加用户  
> 
> > leaf\\\\ywz ALL=(ALL) ALL  
> > 第一个\\表示转意  

  

> ![ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------](http://img2.ph.126.net/B9d8j1IB2RqoltMnP84LVw==/1442559255742305386.png "ubuntu10.04加入到win2003域 - leaf - ------坚持雅操------")

   
相关命令：  
1、sudo domainjoin-cli join leaf.com domain  
2、sudo domainjoin-cli leave  
  
#2013.10.02更新，解决全部加域问题。  
  
参考：  
[1、把ubuntu desktop10.4 加入windows 域](http://hi.baidu.com/mihuo19/blog/item/08feafdeada40c4494ee378f.html)  
2、[How to add Ubuntu 8.04 to win server 2003 Active Directory Domain](http://www.ubuntugeek.com/how-to-add-ubuntu-804-to-win-server-2003-active-directory-domain.html#comment-148131)  
3、[UbuntuHelp:ActiveDirectoryWinbindHowto/zh](http://wiki.ubuntu.org.cn/UbuntuHelp:ActiveDirectoryWinbindHowto/zh#.E6.9C.80.E5.BE.8C.E4.B8.80.E4.BB.B6.E4.BA.8B)  
4、[Ubuntu 13.04 登录Windows域](http://www.linuxidc.com/Linux/2013-09/89578.htm)