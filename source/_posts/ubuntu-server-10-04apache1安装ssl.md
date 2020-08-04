---
title: 'ubuntu server 10.04:apache1:安装ssl'
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '152'
abbrlink: 1720998562
date: 2010-11-09 09:51:00
---

1、安装apache： sudo apt-get install apache2  
2、创建虚拟主机：  
      cd /etc/apache2/sites-available  
      sudo cp -a default blog.test.com  
     sudo mkdir /var/www/blog.test.com  
     更改blog.test.com配置：略  
3、开启虚拟主机：  
     sudo a2dissite default  
     sudo a2ensite blog.test.com  
     sudo /etc/init.d/apache2 restart  
4、设置ssl  
     1、启动模块 sudo a2enmod ssl  
     2、创建key openssl genrsa -des3 -out server.key 1024  
           创建csr证书 openssl req -new -key server.key -out server.csr  
           创建crt自己认证的证书  openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt  
     3、安装证书  
            sudo cp server.crt /etc/ssl/certs  
            sudo cp server.key /etc/ssl/private  
     4、修改配置 blog.test.com  
          DocumentRoot一行的下方加入内容：  
          SSLEngine on  
          SSLOptions +StrictRequire  
         SSLCertificateFile /etc/ssl/certs/server.crt  
         SSLCertificateKeyFile /etc/ssl/private/server.key  
      5、重启apache  
            sudo /etc/init.d/apache2 restart