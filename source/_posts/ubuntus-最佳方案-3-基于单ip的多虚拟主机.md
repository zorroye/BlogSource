---
title: ubuntus 最佳方案 3-基于单IP的多虚拟主机
tags:
  - 未分类
id: '163'
date: 2012-04-27 15:45:00
---

  
环境：  

> 本机：ubuntu10.04.4  
> vmware：ubuntu8.04.4  
>   

说明：  

> 由于没有建DNS服务器，所以在本机上修改了hosts文件  
> sudo nano /etc/hosts  添加  
> 172.16.43.140   www.a.com  
> 172.16.43.140   www.b.com  

  
  
1、建虚拟目录  
      /var/www/www.a.com  
      /var/www/www.b.com  
  
2、建配置文件  
     cd /etc/apache2/sites-available  
     sudo cp default www.a.com  
     sudo cp default www.b.com  
  
3、修改www.a.com 和 www.b.com 的配置文件  
     www.a.com配置如下  

> NameVirtualHost 172.16.43.140  
> <VirtualHost 172.16.43.140>  
>         ServerAdmin webmaster@localhost  
>         DocumentRoot /var/www/www.a.com  
>         ServerName www.a.com  
>         <Directory />  
>                 Options FollowSymLinks  
>                 AllowOverride None  
>         </Directory>  
>         <Directory /var/www/www.a.com/>  
>                 Options Indexes FollowSymLinks MultiViews  
>                 AllowOverride all  
>                 Order allow,deny  
>                 allow from all  
>         </Directory>  

> 后面略。。。。  
>   

       www.b.com配置如下  

> #NameVirtualHost \*  
> <VirtualHost 172.16.43.140>  
>     ServerAdmin webmaster@localhost  
>  DocumentRoot /var/www/www.b.com  
>     ServerName www.b.com  
>     <Directory />  
>         Options FollowSymLinks  
>         AllowOverride None  
>     </Directory>  
>  <Directory /var/www/www.b.com/>  
>         Options Indexes FollowSymLinks MultiViews  
>         AllowOverride None  
>         Order allow,deny  
>         allow from all  
>     </Directory>  

> 后面略。。。  

  
4、重启apache2  
      sudo a2dissite default  
      sudo a2ensite www.a.com  
      sudo a2ensite www.b.com  
      sudo /etc/init.d/apache2 restart  
  
5、访问网站  

> http://www.a.com  
> http://www.b.com