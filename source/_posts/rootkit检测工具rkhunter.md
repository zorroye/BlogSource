---
title: 'rootkit检测工具:rkhunter'
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '286'
abbrlink: 4003415816
date: 2013-01-04 09:15:00
---

rootkit：攻击者用来隐藏自己的踪迹和保留root访问权限的工具  
  
rkhunter：  
  
安装：sudo apt-get install rkhunter  
运行检测：sudo rkhunter --checkall  
日志文件：/var/log/rkhunter.log  
  
系统：Ubuntu10.04 X64  
检测结果：  

Checking system commands...  
 /sbin/chkconfig                                          \[ Warning \]  
\[08:15:09\] /sbin/chkconfig                                   \[ Warning \]  
\[08:15:10\] Warning: The command '/sbin/chkconfig' has been replaced by a script: /sbin/chkconfig: a /usr/bin/perl script text executable  
**#安装了chkconfig，但是不好用**  
  
Checking for rootkits...  
  Performing trojan specific checks  
    Checking for enabled inetd services                      \[ Warning \]  
\[08:17:49\] Performing trojan specific checks  
\[08:17:49\] Info: Starting test name 'trojans'  
\[08:17:49\] Info: Using inetd configuration file '/etc/inetd.conf'  
\[08:17:49\]   Checking for enabled inetd services             \[ Warning \]  
\[08:17:49\] Warning: Found enabled inetd service: swat  
**#我启动了网页管理samba的服务。**  
  
  Performing filesystem checks  
    Checking /dev for suspicious file types                  \[ Warning \]  
    Checking for hidden files and directories                \[ Warning \]  
\[08:21:52\] Performing filesystem checks  
\[08:21:52\] Info: Starting test name 'filesystem'  
\[08:21:52\] Info: SCAN\_MODE\_DEV set to 'THOROUGH'  
\[08:21:52\]   Checking /dev for suspicious file types         \[ Warning \]  
\[08:21:52\] Warning: Suspicious file types found in /dev:  
\[08:21:52\]          /dev/shm/pulse-shm-749119975: data  
\[08:21:52\]          /dev/shm/pulse-shm-1887985822: data  
\[08:21:52\]          /dev/shm/pulse-shm-1887045141: data  
\[08:21:52\]          /dev/shm/pulse-shm-125854523: data  
**#这几个文件不知道啥用的，求教**  
\[08:21:53\]   Checking for hidden files and directories       \[ Warning \]  
\[08:21:53\] Warning: Hidden directory found: /etc/.java  
**#我安装了yed graph editor所以有这个文件夹**  
\[08:21:53\] Warning: Hidden directory found: /dev/.udev  
\[08:21:53\] Warning: Hidden directory found: /dev/.initramfs  
**#这两个文件夹本来就有的，属于正常报错**  
  
服务器检测：  
Checking if SSH root access is allowed          \[ Warning \]  
**#把/etc/ssh/sshd\_config 里面的PermitRootLogin=no 然后重启ssh服务即可 。不影响sudo的使用。**