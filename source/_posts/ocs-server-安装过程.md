---
title: ocs-server 安装过程
tags:
  - 未分类
id: '282'
abbrlink: 342914756
date: 2011-05-04 10:07:00
---

desktop:~/XML-Entities/OCSNG\_UNIX\_SERVER-2.0rc4$ sudo sh ./setup.sh 

  

+----------------------------------------------------------+

|                                                          |

| Welcome to OCS Inventory NG Management server setup !    |

|                                                          |

+----------------------------------------------------------+

  

Trying to determine whitch OS or Linux distribution you use

+----------------------------------------------------------+

| Checking for Apache web server binaries !                |

+----------------------------------------------------------+

  

CAUTION: If upgrading Communication server from OCS Inventory NG 1.0 RC2 and

previous, please remove any Apache configuration for Communication Server!

  

Do you wish to continue (\[y\]/n)?y

Assuming Communication server 1.0 RC2 or previous is not installed

on this computer.

  

Starting OCS Inventory NG Management server setup from folder /home/ywz/XML-Entities/OCSNG\_UNIX\_SERVER-2.0rc4

Storing log in file /home/ywz/XML-Entities/OCSNG\_UNIX\_SERVER-2.0rc4/ocs\_server\_setup.log

#1、做安装前的准备，包括数据库等

+----------------------------------------------------------+

| Checking for database server properties...               |

+----------------------------------------------------------+

  

Your MySQL client seems to be part of MySQL version 5.1.

Your computer seems to be running MySQL 4.1 or higher, good ;-)

#要安装mysql5.1

Which host is running database server \[localhost\] ?

OK, database server is running on host localhost ;-)

#因为是本机安装，所以就写localhost

On which port is running database server \[3306\] ?

OK, database server is running on port 3306 ;-)

#mysql服务端口：3306

  

+----------------------------------------------------------+

| Checking for Apache web server daemon...                 |

+----------------------------------------------------------+

  

Where is Apache daemon binary \[/usr/sbin/apache2\] ?

OK, using Apache daemon /usr/sbin/apache2 ;-)

#要安装aphche2

  

+----------------------------------------------------------+

| Checking for Apache main configuration file...           |

+----------------------------------------------------------+

  

Where is Apache main configuration file \[/etc/apache2/apache2.conf\] ?

OK, using Apache main configuration file /etc/apache2/apache2.conf ;-)

#apache2的配置文件在/etc/apache2/apache2.conf

  

+----------------------------------------------------------+

| Checking for Apache user account...                      |

+----------------------------------------------------------+

  

Which user account is running Apache web server \[www-data\] ?

OK, Apache is running under user account www-data ;-)

#apache的用户名为：www-data

  

+----------------------------------------------------------+

| Checking for Apache group...                             |

+----------------------------------------------------------+

  

Which user group is running Apache web server \[www-data\] ?

OK, Apache is running under users group www-data ;-)

#apache的用户组为：www-data

  

+----------------------------------------------------------+

| Checking for Apache Include configuration directory...   |

+----------------------------------------------------------+

  

Setup found Apache Include configuration directory in

//etc/apache2/conf.d/.

Setup will put OCS Inventory NG Apache configuration in this directory.

Where is Apache Include configuration directory \[//etc/apache2/conf.d/\] ?

OK, Apache Include configuration directory //etc/apache2/conf.d/ found ;-)

#apache的配置文件还包括/etc/apache2/conf.d/

  

+----------------------------------------------------------+

| Checking for PERL Interpreter...                         |

+----------------------------------------------------------+

  

Found PERL Intrepreter at </usr/bin/perl> ;-)

Where is PERL Intrepreter binary \[/usr/bin/perl\] ?

OK, using PERL Intrepreter /usr/bin/perl ;-)

#要安装perl

  

Do you wish to setup Communication server on this computer (\[y\]/n)?y

#2、OCS Inventory NG Communication server安装

  

+----------------------------------------------------------+

| Checking for Make utility...                             |

+----------------------------------------------------------+

  

OK, Make utility found at </usr/bin/make> ;-)

#要安装make

+----------------------------------------------------------+

| Checking for Apache mod\_perl version...                  |

+----------------------------------------------------------+

  

Checking for Apache mod\_perl version 1.99\_22 or higher

Found that mod\_perl version 1.99\_22 or higher is available.

OK, Apache is using mod\_perl version 1.99\_22 or higher ;-)

#要安装libapache2-mod-perl2

+----------------------------------------------------------+

| Checking for Communication server log directory...       |

+----------------------------------------------------------+

  

Communication server can create detailled logs. This logs can be enabled

by setting interger value of LOGLEVEL to 1 in Administration console

menu Configuration.

Where to put Communication server log directory \[/var/log/ocsinventory-server\] ?

OK, Communication server will put logs into directory /var/log/ocsinventory-server ;-)

#Communication server的log放在/var/log/ocsinventory-server

  

+----------------------------------------------------------+

| Checking for required Perl Modules...                    |

+----------------------------------------------------------+

  

Checking for DBI PERL module...                              #要安装libdbi-perl

Found that PERL module DBI is available. 

Checking for Apache::DBI PERL module...                 #要安装libapache-dbi-perl

Found that PERL module Apache::DBI is available.

Checking for DBD::mysql PERL module...                  #要安装libdbd-mysql-perl

Found that PERL module DBD::mysql is available.

Checking for Compress::Zlib PERL module...             #要安装libcompress-zlib-perl

Found that PERL module Compress::Zlib is available.

Checking for XML::Simple PERL module...                #要安装libxml-simple-perl

Found that PERL module XML::Simple is available.

Checking for Net::IP PERL module...                         #要安装libnet-ip-perl

Found that PERL module Net::IP is available.

  

+----------------------------------------------------------+

| Checking for optional Perl Modules...                    |

+----------------------------------------------------------+

  

Checking for SOAP::Lite PERL module...                  #要安装libsoap-lite-perl

Found that PERL module SOAP::Lite is available.

Checking for XML::Entities PERL module...               #要安装XML-Entities

Found that PERL module XML::Entities is available.

  

  

+----------------------------------------------------------+

| OK, looks good ;-)                                       |

|                                                          |

| Configuring Communication server Perl modules...         |

+----------------------------------------------------------+

  

Checking if your kit is complete...

Looks good

Writing Makefile for Apache::Ocsinventory

  

+----------------------------------------------------------+

| OK, looks good ;-)                                       |

|                                                          |

| Preparing Communication server Perl modules...           |

+----------------------------------------------------------+

  

  

+----------------------------------------------------------+

| OK, prepare finshed ;-)                                  |

|                                                          |

| Installing Communication server Perl modules...          |

+----------------------------------------------------------+

  

  

+----------------------------------------------------------+

| OK, Communication server Perl modules install finished;-)|

|                                                          |

| Creating Communication server log directory...           |

+----------------------------------------------------------+

  

Creating Communication server log directory /var/log/ocsinventory-server.

  

Fixing Communication server log directory files permissions.

Configuring logrotate for Communication server.

Removing old communication server logrotate file /etc/logrotate.d/ocsinventory-NG

Writing communication server logrotate to file /etc/logrotate.d/ocsinventory-server

#做communication server的轮替 /etc/logrotate.d/ocsinventory-server

  

+----------------------------------------------------------+

| OK, Communication server log directory created ;-)       |

|                                                          |

| Now configuring Apache web server...                     |

+----------------------------------------------------------+

  

To ensure Apache loads mod\_perl before OCS Inventory NG Communication Server,

Setup can name Communication Server Apache configuration file

'z-ocsinventory-server.conf' instead of 'ocsinventory-server.conf'.

Do you allow Setup renaming Communication Server Apache configuration file

to 'z-ocsinventory-server.conf' (\[y\]/n) ?y

OK, using 'z-ocsinventory-server.conf' as Communication Server Apache configuration file

Removing old communication server configuration to file //etc/apache2/conf.d//ocsinventory.conf

Writing communication server configuration to file //etc/apache2/conf.d//z-ocsinventory-server.conf

#communication server的配置文件/etc/apache2/conf.d/ocsinventory.conf

  

+----------------------------------------------------------+

| OK, Communication server setup sucessfully finished ;-)  |

|                                                          |

| Please, review //etc/apache2/conf.d//z-ocsinventory-server.conf

| to ensure all is good. Then restart Apache daemon.       |

+----------------------------------------------------------+

  

  

Do you wish to setup Administration Server (Web Administration Console)

on this computer (\[y\]/n)?y

#3、安装Administration Server

+----------------------------------------------------------+

| Checking for Administration Server directories...        |

+----------------------------------------------------------+

  

CAUTION: Setup now install files in accordance with Filesystem Hierarchy

Standard. So, no file is installed under Apache root document directory

(Refer to Apache configuration files to locate it). 

#文件不放在/var/www下，放在/usr/share/ocsinventory-reports

#具体查看apache2的配置文件在/etc/apache2/apache2.conf和/etc/apache2/conf.d/

If you're upgrading from OCS Inventory NG Server 1.01 and previous, YOU

MUST REMOVE (or move) directories 'ocsreports' and 'download' from Apache

root document directory.

If you choose to move directory, YOU MUST MOVE 'download' directory to

Administration Server writable/cache directory (by default

/var/lib/ocsinventory-reports), especialy if you use deployement feature.

#download文件夹要放在/var/lib/ocsinventory-reports下以做部署用

Do you wish to continue (\[y\]/n)?y

Assuming directories 'ocsreports' and 'download' removed from

Apache root document directory.

  

Where to copy Administration Server static files for PHP Web Console

\[/usr/share/ocsinventory-reports\] ?

#ocsinventory的控制端放在/usr/share/ocsinventory-reports

OK, using directory /usr/share/ocsinventory-reports to install static files ;-)

Where to create writable/cache directories for deployement packages,

IPDiscover and SNMP \[/var/lib/ocsinventory-reports\] ?

OK, writable/cache directory is /var/lib/ocsinventory-reports ;-)

#部署文件,IPDiscover and SNMP的相关文件放在/var/lib/ocsinventory-reports

  

+----------------------------------------------------------+

| Checking for required Perl Modules...                    |

+----------------------------------------------------------+

  

Checking for DBI PERL module...

Found that PERL module DBI is available.

Checking for DBD::mysql PERL module...

Found that PERL module DBD::mysql is available.

Checking for XML::Simple PERL module...

Found that PERL module XML::Simple is available.

Checking for Net::IP PERL module...

Found that PERL module Net::IP is available.

  

+----------------------------------------------------------+

| Installing files for Administration server...            |

+----------------------------------------------------------+

  

Creating PHP directory /usr/share/ocsinventory-reports/ocsreports.

Copying PHP files to /usr/share/ocsinventory-reports/ocsreports.

Fixing permissions on directory /usr/share/ocsinventory-reports/ocsreports.

#php文件放在/usr/share/ocsinventory-reports/ocsreports

Creating database configuration file /usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php.

#数据库配置文件放在/usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php

Creating IPDiscover directory /var/lib/ocsinventory-reports/ipd.

Fixing permissions on directory /var/lib/ocsinventory-reports/ipd.

#ipd文件夹放在/var/lib/ocsinventory-reports/ipd

Creating packages directory /var/lib/ocsinventory-reports/download.

Fixing permissions on directory /var/lib/ocsinventory-reports/download.

#部署文件放在/var/lib/ocsinventory-reports/download

Creating packages directory /var/lib/ocsinventory-reports/snmp.

Fixing permissions on directory /var/lib/ocsinventory-reports/snmp.

#snmp文件放在/var/lib/ocsinventory-reports/snmp

Configuring snmp\_com.txt file

Configuring IPDISCOVER-UTIL Perl script.

Installing IPDISCOVER-UTIL Perl script.

Fixing permissions on IPDISCOVER-UTIL Perl script.

Writing Administration server configuration to file //etc/apache2/conf.d//ocsinventory-reports.conf

#控制端配置文件放在/etc/apache2/conf.d//ocsinventory-reports.conf

+----------------------------------------------------------+

| OK, Administration server installation finished ;-)      |

|                                                          |

| Please, review //etc/apache2/conf.d//ocsinventory-reports.conf

| to ensure all is good and restart Apache daemon.         |

|                                                          |

| Then, point your browser to http://server//ocsreports

| to configure database server and create/update schema.   |

+----------------------------------------------------------+

#网页打开http://server//ocsreports 来配置数据库和架构

  

Setup has created a log file /home/ywz/XML-Entities/OCSNG\_UNIX\_SERVER-2.0rc4/ocs\_server\_setup.log. Please, save this file.    \# 安装记录放在ocs\_server\_setup.log

If you encounter error while running OCS Inventory NG Management server,

we can ask you to show us his content !

  

DON'T FORGET TO RESTART APACHE DAEMON !

#重启apache服务

Enjoy OCS Inventory NG ;-)

  

总结：

1、要安装的软件

      make、mysql5、apache2、php

      perl、libapache2-mod-perl2、libdbi-perl、libapache-dbi-perl、libdbd-mysql-perl、

      libcompress-zlib-perl、libxml-simple-perl、libnet-ip-perl、libsoap-lite-perl、XML-Entities

2、apache的配置文件

      /etc/apache2/apache2.conf和/etc/apache2/conf.d/

3、communication server

     communication server的配置文件/etc/apache2/conf.d/ocsinventory.conf

     Communication server的log放在/var/log/ocsinventory-server

     communication server的轮替 /etc/logrotate.d/ocsinventory-server

4、Administration Server 

     控制端配置文件放在/etc/apache2/conf.d/ocsinventory-reports.conf

     数据库配置文件放在/usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php

     文件放在/usr/share/ocsinventory-reports

      php文件放在/usr/share/ocsinventory-reports/ocsreports

      部署文件放在/var/lib/ocsinventory-reports/download

      ipd文件夹放在/var/lib/ocsinventory-reports/ipd

      snmp文件放在/var/lib/ocsinventory-reports/snmp