---
title: ubuntu server 10.04 samba 需要用户名和密码访问
tags:
  - 未分类
id: '329'
date: 2010-09-24 11:00:00
---

1、防火墙开启相关端口

> sudo ufw enable               #开启ufw
> 
> sudo ufw default deny      #关闭外部对本机的所有访问
> 
> sudo ufw allow 137
> 
> sudo ufw allow 138
> 
> sudo ufw allow 139
> 
> sudo ufw allow 445
> 
>   
> 
> ufw相关操作请查看 http://wiki.ubuntu.org.cn/UFW防火墙简单设置

> ufw补充：sudo ufw allow from 192.168.2.0/24 to any port 21   #允许某个IP访问某个端口

  

2、设置要共享的文件夹权限

> chmod 0777 TEMP

  

3、写配置

\[global\]

> workgroup = WORKGROUP
> 
> netbios name = IT-TEST
> 
> server string = it-test
> 
> display charset = utf-8
> 
> dos charset = cp936
> 
> socket options = TCP\_NODELAY SO\_RCVBUF=8192 SO\_SNDBUF=8192
> 
> dns proxy = no
> 
> template shell = /bin/false
> 
> winbind use default domain = no
> 
> security = user
> 
> encrypt passwords = yes
> 
> smb passwd file = /etc/samba/smbpasswd
> 
> name resolve order = lmhosts bcast host
> 
> #hosts allow 表示允许哪些网段可以访问

  

\[homes\]                              #\[homes\]表示家目录，不是共享文件夹名称

> comment = user home directories
> 
> browseable=no        #不允许别人查看
> 
> writable = yes           #允许登陆用户读写

  

\[temp\]

> comment = read write
> 
> path = /media/TEMP
> 
> writeable = yes
> 
> public = yes
> 
> write list=@test1                                       #表示组成员可访问
> 
> #valid users = test001，test0022            #设置某些用户可访问
> 
> #only guest=yes 表示采用nobody也就是guest的权限登陆。
> 
> create mode = 0666
> 
> directory mode = 0777

  

4、新建 smbpasswd文件

> smbpasswd默认是没有的，通过smbpasswd -a等添加用户后就有了。
> 
> samba的用户首先必须是系统用户，也就是/etc/passwd里面有的，然后才能成为samba用户
> 
> 备注：是系统用户不一定就能登陆系统。
> 
> smbpasswd的操作就4个命令
> 
> smbpasswd -a 添加用户
> 
> smbpasswd -x 删除用户
> 
> smbpasswd -e 启用用户
> 
> smbpasswd -d 禁用用户

  

5、添加系统账户、群组

> 1>添加群组 ：sudo groupadd  test1
> 
> 2>添加账户：

> sudo useradd -M -s /sbin/nologin -d /dev/null -g test1  test001    

> > #加入群组，只用于登陆samba，不登陆系统，不建家目录，

  

6、给samba添加用户

> sudo smbpasswd -a test001              #这个用户名必须和上面的对应起来。要输入两遍密码

  

7、smb相关命令

> smbstatus：服务端查看连接到本服务器的连接状态

> smbclient -L //IP ：查看资源列表
> 
> smbclient //IP -U user ：使用用户身份登陆到samba服务器，然后使用ftp命令上传下载文件
> 
> smbmount //IP /mnt/share -o username=user    挂在共享文件夹到本地 。参数同mount
> 
> mount -t smbfs //IP /mnt/share -o username=user

  

以上2013.10.09更改，接下去学习smb.conf配置文件。