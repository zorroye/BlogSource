---
title: ubuntus 最佳方案  3-基于端口的多虚拟主机
tags:
  - 未分类
id: '160'
abbrlink: 2458785665
date: 2012-04-19 12:16:00
---

1、建虚拟目录  
      /var/www/www.a.com  
      /var/www/www.b.com  
  
2、修改/etc/apache2/ports.conf  
      加入Listen 8080  
  
3、建配置文件  
     cd /etc/apache2/sites-available  
     sudo cp default www.a.com  
     sudo cp default www.b.com  
  
4、修改www.a.com 和 www.b.com 的配置文件  
     www.a.com配置如下  

> NameVirtualHost \*  
> <VirtualHost \*>  
>         ServerAdmin webmaster@localhost  
>         DocumentRoot /var/www/www.a.com  
>         ServerName  www.a.com  
>         <Directory />  
>                 Options FollowSymLinks  
>                 AllowOverride None  
>         </Directory>  
>         <Directory /var/www/www.a.com/>  
>                 Options Indexes FollowSymLinks MultiViews  
>                 AllowOverride None  
>                 Order allow,deny  
>                 allow from all  
>         </Directory>  

> 后面略。。。。  
>   

       www.b.com配置如下  

> <VirtualHost 172.16.43.140:8080>  

>         ServerAdmin webmaster@localhost  
>          
>         DocumentRoot /var/www/www.b.com  
>          
>         ServerName www.b.com  
>   
>         <Directory />  
>                 Options FollowSymLinks  
>                 AllowOverride None  
>         </Directory>  
>         <Directory /var/www/www.b.com/>  
>                 Options Indexes FollowSymLinks MultiViews  
>                 AllowOverride None  
>                 Order allow,deny  
>                 allow from all  
>         </Directory>  

> 后面略。。。  

  
5、重启apache2  
      sudo a2dissite default  
      sudo a2ensite www.a.com  
      sudo a2ensite www.b.com  
      sudo /etc/init.d/apache2 restart  
  
  
  
然后访问www.a.com 就输入 172.16.43.140  
       访问www.b.com 就输入 172.16.43.140:8080  
  
  
参考：  
http://wenku.baidu.com/view/c61a0dd6b9f3f90f76c61b18.html  
http://httpd.apache.org/docs/2.2/vhosts/examples.html