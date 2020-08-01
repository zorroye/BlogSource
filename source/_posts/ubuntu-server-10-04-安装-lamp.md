---
title: ubuntu server 10.04 安装 LAMP
tags:
  - 未分类
id: '148'
abbrlink: 3097134107
date: 2010-09-28 17:37:00
---

1、安装软件：apt-get install apache2 mysql-server mysql-client php5 php5-gd php5-mysql  
            1> 可以打开http://127.0.0.1/     说明apache已启动  
            2> 设置mysql root 密码             mysql亦已启动  
2、设置www权限：`sudo chmod 777 /var/www  
3、启用 mod_rewrite 模块  
   终端命令：sudo a2enmod rewrite  
   重启Apache服务器：sudo /etc/init.d/apache2 restart  
       1> php 设置成功  
  
4、安装phpmyadmin (非必须，就是设置mysql比较容易点)` sudo apt-get install phpmyadmin     另外输入上面设置的mysql密码  
        sudo ln -s /usr/share/phpmyadmin /var/www    (非必须，好像不连接也能用的)  
`  
  
  
**在/var/www内新建网页用于测试**  
1、``<?php phpinfo(); ?>  用来测试PHP是否好用  
2、  
`<?php  
$link = mysql\_connect("localhost","root","添入刚才设置的密码");  
if (!$link)  
{  
die('Could not connect: ' . mysql\_error());  
}  
else echo "Mysql Is Working";  
mysql\_close($link);  
?>  
`测试mysql是否可用  
  
**其他测试：**  
netstat -tunl  
查看 80端口和 3306端口即可知道 apache2 和 mysql 是否启动  
  
**相关配置文件：**  
1、apache2 相关文件：  
   /etc/apache2/apache2.conf    apache配置文件  
   /etc/apache2/conf.d          自定义配置文件  
   /var/www                     网页存放区  
   /usr/sbin/apache2ctl         apache的执行文件  
   /usr/bin/htpasswd            apache密码保护  
`2、mysql 相关文件：  
      /etc/mysql/my.cnf                              mysql配置文件  
3、mysql相关文件：  
     /etc/php5/apache2/php.ini                 php配置文件  
     /etc/php5/conf.d/mysql.ini                  php支持mysql接口  
  
  
  
参考：  
[http://blog.myspace.cn/e/407367767.htm](http://blog.myspace.cn/e/407367767.htm)  
[http://farlee.info/archives/ubuntu-server-install-lamp-phpmyadmin-vsftpd-zend-framework.html](http://farlee.info/archives/ubuntu-server-install-lamp-phpmyadmin-vsftpd-zend-framework.html)    (内有乱码解决方案，挺好)