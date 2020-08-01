---
title: Ubuntu Server 14.04 安装nagios，nrpe
tags:
  - 未分类
id: '288'
abbrlink: 3633964971
date: 2015-06-17 21:07:00
---

0、安装软件

1、设置主机及相关关系

2、设置主机组

3、设置监控的服务

4、nrpe设置

  

0、安装软件及初始化

> sudo apt-get install apache2 -y

> sudo apt-get install nagios3 nagios-plugins nagios-images -y

> 更改管理员账户

> sudo sed -i 's/nagiosadmin/ywz/g' /etc/nagios3/cgi.cfg 

> sudo htpasswd /etc/nagios3/htpasswd.users ywz

> 添加用户

> sudo htpasswd /etc/nagios3/htpasswd.users user1

> 联系人设置

> > define contact{
> 
> >         contact\_name                    ywz
> 
> >         alias                           ywz
> 
> >         service\_notification\_period     24x7
> 
> >         host\_notification\_period        24x7
> 
> >         service\_notification\_options    w,u,c,r
> 
> >         host\_notification\_options       d,r
> 
> >         service\_notification\_commands   notify-service-by-email
> 
> >         host\_notification\_commands      notify-host-by-email
> 
> >         email                           ywz\_306@163.com
> 
> >         }

> > define contactgroup{
> 
> >         contactgroup\_name       admins
> 
> >         alias                   Nagios Administrators
> 
> >         members                 ywz
> 
> >         }

> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img1.ph.126.net/mkDjilPJUD95PABtOkq2QA==/6630544398164876428.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>  

1、设置主机及用户组

> 设置名称，地址，及相互连接方式

> sudo nano /etc/nagios3/conf.d/hosts.cfg

> > define host{
> 
> >         host\_name Baidu
> 
> >         alias   IC
> 
> >         address www.baidu.coom
> 
> >         use     generic-host
> 
> > }
> 
> >   
> 
> > define host{
> 
> >         host\_name WAN
> 
> >         alias   pppoe
> 
> >         address  172.24.214.44
> 
> >         parents Baidu
> 
> >         use     generic-host
> 
> > }
> 
> >   
> 
> >   
> 
> > define host{
> 
> >         host\_name Lan
> 
> >         alias   route
> 
> >         address 192.168.3.1
> 
> >         parents WAN
> 
> >         use     generic-host
> 
> > }
> 
> >   
> 
> > define host{
> 
> >         host\_name haproxy1
> 
> >         alias   haproxy1
> 
> >         address 192.168.3.17
> 
> >         parents Lan
> 
> >         use     generic-host
> 
> > }
> 
> >   
> 
> > define host{
> 
> >         host\_name haproxy2
> 
> >         alias   haproxy2
> 
> >         address 192.168.3.18
> 
> >         parents Lan
> 
> >         use     generic-host
> 
> > }
> 
> >   
> 
> > define host{
> 
> >         host\_name www1
> 
> >         alias   www1
> 
> >         address 192.168.3.33
> 
> >         parents Lan
> 
> >         use     generic-host
> 
> > }
> 
> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img0.ph.126.net/uc9XHREN4TrO5B_baEmJ7g==/6630876450676878426.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>  

2、设置主机组

> sudo nano /etc/nagios3/conf.d/hostgroups\_nagios2.cfg

> > \# Some generic hostgroup definitions
> 
> > \# A simple wildcard hostgroup
> 
> > define hostgroup {
> 
> >         hostgroup\_name  all
> 
> > alias           All Servers
> 
> > members         \*
> 
> >         }
> 
> >   
> 
> > \# A list of your Debian GNU/Linux servers
> 
> > define hostgroup {
> 
> >         hostgroup\_name  debian-servers
> 
> > alias           Debian GNU/Linux Servers
> 
> > members         localhost,haproxy1,haproxy2,www1
> 
> >         }
> 
> >   
> 
> > \# A list of your web servers
> 
> > define hostgroup {
> 
> >         hostgroup\_name  http-servers
> 
> > alias           HTTP servers
> 
> > members         localhost,www1
> 
> >         }
> 
> >   
> 
> > \# A list of your ssh-accessible servers
> 
> > define hostgroup {
> 
> >         hostgroup\_name  ssh-servers
> 
> > alias           SSH servers
> 
> > members         localhost, haproxy1, haproxy2,www1
> 
> >         }
> 
> >   
> 
> > define hostgroup {
> 
> > hostgroup\_name all-gateways
> 
> > aliasAll Gateways
> 
> > membersLan, WAN
> 
> > }
> 
> >   
> 
> > define hostgroup {
> 
> > hostgroup\_name ubuntu-servers
> 
> > aliasUbuntu servers
> 
> > members localhost, haproxy1, haproxy2, www1
> 
> > }
> 
> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img1.ph.126.net/8LDGl8VTCyukhUv18UrBwA==/6630272818792815316.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>  
> 
>   

2.1设置设备图标

> sudo nano /etc/nagios3/conf.d/extinfo\_nagios2.cfg

> ##
> 
> \## Extended Host and Service Information
> 
> ##
> 
>   
> 
> define hostextinfo{
> 
>         hostgroup\_name   debian-servers
> 
>         notes            Debian GNU/Linux servers
> 
> \#       notes\_url        http://webserver.localhost.localdomain/hostinfo.pl?host=netware1
> 
>         icon\_image       base/debian.png
> 
>         icon\_image\_alt   Debian GNU/Linux
> 
>         vrml\_image       debian.png
> 
>         statusmap\_image  base/debian.gd2
> 
>         }
> 
>   
> 
> define hostextinfo{
> 
> hostgroup\_name all-gateways
> 
> icon\_image base/ng-switch40.png
> 
> statusmap\_image base/ng-switch40.png
> 
> }
> 
>   
> 
> define hostextinfo{
> 
> hostgroup\_name ubuntu-servers
> 
> icon\_image base/ubuntu.png
> 
> statusmap\_image base/ubuntu.png
> 
> }
> 
>   
> 
>   

3、设置需要监控服务

> sudo nano /etc/nagios3/conf.d/services\_nagios2.cfg

> > \# check that web services are running
> 
> > define service {
> 
> >         hostgroup\_name                  http-servers
> 
> >         service\_description             HTTP
> 
> >  check\_command                   check\_http
> 
> >         use                             generic-service
> 
> > notification\_interval           0 ; set > 0 if you want to be renotified
> 
> > }
> 
> >   
> 
> > \# check that ssh services are running
> 
> > define service {
> 
> >         hostgroup\_name                  ssh-servers
> 
> >         service\_description             SSH
> 
> > check\_command                   check\_ssh
> 
> >         use                             generic-service
> 
> > notification\_interval           0 ; set > 0 if you want to be renotified
> 
> > }
> 
> >   
> 
> > define service {
> 
> > hostgroup\_nameall-gateways
> 
> > service\_descriptionPING
> 
> > check\_commandcheck\_ping!100.0,20%!500.0,60%
> 
> > usegeneric-service
> 
> > notification\_interval0
> 
> > }
> 
> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img2.ph.126.net/980I-29uNSfLr03RIM8r4A==/6630603771793179824.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>  

3.1 nagios-plugins 安装

> http://nagios-plugins.org/
> 
> https://www.nagios.org/download/plugins/

  

4、nrpe相关设置

> 被控端

> > sudo apt-get install nagios-nrpe-server -y
> 
> > 更改配置文件
> 
> > sudo nano /etc/nagios/nrpe.cfg

> > > allowed\_hosts=192.168.1.50  
> > > 
> > > command\[check\_all\_disks\]=/usr/lib/nagios/plugins/check\_disk -w 20% -c 10% -e
> > 
> > sudo service nagios-nrpe-server restart
> 
> 主控端

> > 新建单独的配置文件
> 
> > sudo nano /etc/nagios3/conf.d/www1.cfg

> > > define service{  
> > > usegeneric-service  
> > > host\_name www1  
> > > service\_descriptionDisk space  
> > > check\_commandcheck\_nrpe\_1arg!check\_all\_disks  
> > > }  
> > >   
> > > define service{   
> > >         use     generic-service  
> > >         host\_name       www1         
> > >         service\_description     Current Users  
> > >         check\_command   check\_nrpe\_1arg!check\_users  
> > > }  
> > >   
> > > define service{   
> > >         use     generic-service  
> > >         host\_name       www1         
> > >         service\_description     Total Processes  
> > >         check\_command   check\_nrpe\_1arg!check\_total\_procs  
> > > }  
> > >   
> > > define service{   
> > >         use     generic-service  
> > >         host\_name       www1         
> > >         service\_description     Current Load  
> > >         check\_command   check\_nrpe\_1arg!check\_load  
> > > }
> > 
> > >   

> >   
> 
> 说明

> 1、插件的命令全部放在/usr/lib/nagios/plugins/下面

> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img0.ph.126.net/qHQS3yZeIwfewi25KrBj_A==/6630728016607132347.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>  

> 2、check\_nrpe\_1arg 命令定义在/etc/nagios-plugins/config/check\_nrpe.cfg
> 
> ![Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------](http://img0.ph.126.net/tngLW9gV9Z7bndmk7TSHsQ==/6630640055676909957.png "Ubuntu Server 14.04 安装nagios，nrpe - leaf - ------勤解万难------")
> 
>