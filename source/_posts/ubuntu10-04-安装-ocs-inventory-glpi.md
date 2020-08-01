---
title: ubuntu10.04 安装 OCS Inventory + GLPI
tags:
  - 未分类
id: '281'
date: 2011-05-03 12:00:00
---

1、ocs ：IT设备**配置**管理

2、glpi ：IT设备**资产**管理

\-----------------------------------------------------------------------------------------------------------------------------------

方法一：编译安装

安装服务端

1、sudo apt-get install apache2 apache2-doc 

     sudo su -c ' echo ServerName 127.0.1.1 >> /etc/apache2/apache2.conf'

     sudo /etc/init.d/apache2 reload

2、sudo apt-get install mysql-server

3、sudo apt-get install php5 php5-cgi php5-cli php5-dev php5-gd php5-mysql libapache2-mod-php5 

4、sudo apt-get install \\

     dmidecode nmap perl libapache-dbi-perl libapache2-mod-perl2 libcompress-zlib-perl       \\

     libcrypt-ssleay-perl libdbd-mysql-perl libdbi-perl libdigest-md5-perl libmodule-install-perl  \\

     libnet-cups-perl libnet-ip-perl libnet-snmp-perl libnet-ssleay-perl libnmap-parser-perl        \\

     libphp-pclzip libproc-daemon-perl libproc-pid-file-perl libsoap-lite-perl libwww-perl            \\

     libxml-simple-perl

       #安装perl相关，另外nmblookup已经有了

5、安装zip

     sudo apt-get install libpcre3 libpcre3-dev

     [下载zip](http://pecl.php.net/package/zip) 

     tar -xvf zip-1.10.2.tgz

     cd zip-1.10.2

     phpize

     ./configure

     make

     sudo make install 

6、安装 XML-Entities

     wget http://mirror.osqdu.org/CPAN/authors/id/S/SI/SIXTEASE/XML-Entities-1.0000.tar.gz

      tar -xvf XML-Entities-1.0000.tar.gz

      cd XML-Entities

      perl Makefile.PL

      make

      sudo make install

      或者

       cpan -i XML:Entities

7、安装OCS

      wget \\

      http://launchpad.net/ocsinventory-server/stable-2.0/2.0rc4/+download/OCSNG\_UNIX\_SERVER-2.0rc4.tar.gz

      tar -xvf OCSNG\_UNIX\_SERVER-2.0rc4.tar.gz

      cd OCSNG\_UNIX\_SERVER-2.0rc4

      sudo sh ./setup.sh  #默认到底

8、sudo /etc/init.d/apache2 restart

9、浏览器打开：

     http://127.0.0.1/ocsreports

     login MYSQL:                root

     Mot de passe MYSQL:   密码

     Nom de la base donnée: 要创建的数据库名，默认即可

     MYSQL HostName:        localhost

     http://127.0.0.1/ocsreports/index.php

     admin：admin

10、sudo rm /usr/share/ocsinventory-reports/ocsreports/install.php

     重设admin密码

     重设ocs数据库的连接密码

           1、改ocs的密码

           2、改/usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php里面的代码

\-----------------------------------------------------

安装客户端

wget \\

      http://launchpad.net/ocsinventory-unix-agent/stable-2.0/2.0rc4/+download/Ocsinventory-Agent-2.0rc4.tar.gz

      tar -xvf Ocsinventory-Agent-2.0rc4.tar.gz

      cd Ocsinventory-Agent-2.0rc4

      perl Makefile.PL

      make

      sudo make install   #要设置server的计算机名，其他默认即可

\------------------------------------------------------------------------------------------------------------------------------------

方法二：apt-get安装

1、安装ampp，同方法一：1、2、3

2、安装perl插件，同方法一：4、5、6

3、sudo apt-get install ocsinventory-server  ocsinventory-reports  

 #设置mysql的密码，设置ocs数据库的密码

4、sudo apt-get install ocsinventory-agent

5、sudo  dpkg-reconfigure ocsinventory-agent 

6、sudo ocsinventory-agent

\------------------------------------------------------------------------------------------------------------------------------------  
中文化：  
暂无  
\------------------------------------------------------------------------------------------------------------------------------------  

GLPI安装：

tar -xvf glpi-0.78.4.tar.gz

sudo mv glpi /var/www

cd /var/www

sudo chown -R www-data:www-data glpi

http://localhost/glpi 设置

\-------------------------------------------------------------------------------------------------------------------------------------

参考：

1、扩展阅读：[开源IT资产管理](http://ossbox.net/open-source-IT-Asset-Mgmt)

\------------------------------------------------------

1、[OCS Inventory](http://doc.ubuntu-fr.org/ocs_inventory%7C#installation_du_client_linux)

[](http://doc.ubuntu-fr.org/ocs_inventory%7C#installation_du_client_linux)2、[OCS Inventory NG 2.x Documentation](http://wiki.ocsinventory-ng.org/index.php/Documentation:Main)  

2、[IT Inventory and Resource Management with OCS Inventory NG 1.02.pdf](http://www.itpub.net/thread-1321323-1-1.html)

3、[Ubuntu下安装 OCS Inventory 电脑资产管理系统](http://zhjack.blog.163.com/blog/static/143149200810702324478/)

4、[(三)开源IT资产管理系统-->OCS（unix）客户端代理安装](http://viong.blog.51cto.com/844766/503694)

5、[这几天在装ocs inventory](http://hi.baidu.com/kan_jian/blog/item/ae5c5a3411e64e3c5bb5f59f.html)

\-----------------------------------------------------

1、[GLPI Administration Manual](http://www.glpi-project.org/wiki/doku.php?id=en:manual:admin:0_index)  
2、[(四)开源IT资产管理系统-->部署GLPI与OCS数据同步](http://viong.blog.51cto.com/844766/503735)