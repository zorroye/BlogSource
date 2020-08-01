---
title: ubuntuserver10.04 安装LAMP：PHP及配置drupal
tags:
  - 未分类
id: '154'
abbrlink: 3835034022
date: 2010-11-10 18:01:00
---

1、安装lamp环境  
     sudo apt-get install apache2 libapache2-mod-php5 php5-mysql mysql-server php5-memcache  
  
1、配置apache2 及awstats 日志分析文件  
  
2、配置mysql  
     1、设置root密码  
     2、为drupal创建数据库 和用户  
  
3、配置php  
      用phpinfo()才测试php是否被apache2支持  
  
4、安装phpmyadmin，并将phpmyadmin链接到自己的网站目录下  
  
5、安装及配置drupal  
      软件下载 http://drupal.org/download  
      语言包     http://localize.drupal.org/  
          将./sites/default 权限设置为 646  
          复制./sites/default/default.settings.php 到./sites/default/settings.php 并将settings.php 权限设置为646  
     一步一步设置即可～