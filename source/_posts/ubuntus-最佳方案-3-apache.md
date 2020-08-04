---
title: ubuntus 最佳方案 -3 apache
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '158'
abbrlink: 2706917480
date: 2012-04-18 22:14:00
---

安装apache2-mpm-worker  

> sudo apt-get install apache2

  
配置文件说明![ubuntus 最佳方案 -3 - leaf - ------坚持雅操------](http://img2.ph.126.net/rjDrEcnNpCK8qcSGcrkM1A==/2500060743161473472.jpg "ubuntus 最佳方案 -3 - leaf - ------坚持雅操------")  

> apache2.conf:全局配置文件，如允许的进程数、日志等级、ServerTokens等多在这边设置  
> envvars:环境变量，运行apache的用户名和组就在这边设置  
> httpd.conf:用户配置文件，默认空  
> ports.conf:SSL的端口号  
> conf.d:好像是跟编码有关的配置，不是很清楚  
> mods-available:  可用的模块  
> mods-enabled：已在用的模块  
> sites-available:   存在的虚拟主机(网站)  
> sites-enabled:    已经对外服务的虚拟主机

  
查看模块  

> 查看可用模块：sudo a2enmod  
> 查看已用模块：sudo a2dismod  
> 查找要安装的模块名称：apt-cache search xxx

  
虚拟主机  

> 虚拟主机有两种：基于IP和基于域名  
> 虚拟主机(网站)存放位置：一般为 /var/www/ 下  
> 虚拟主机的配置文件放在：/etc/apache2/sites-available/   注:对每个虚拟主机单独建配置文件比较好  
> 已用的虚拟主机配置文件：/etc/apache2/sites-enable/   通过a2dissite 和a2ensite 来关闭/开启虚拟主机  
> 注：用a2ensite和a2dissite后，sites-enable下会自动创建符号链接  
> 详见：ubuntus 最佳方案  3-基于端口的多虚拟主机

  
虚拟主机配置详解  

> 详见：ubuntus 最佳方案  3-apache2 default文件介绍

  

HTTPS的实现  

> sudo a2enmod ssl  
> sudo /etc/init.d/apache2 reload  
> sudo apt-get install openssl  
> \--------------------------------------  
> openssl genrsa -des3 -out server.key 1024    #然后输入密码  
> openssl req -new -key server.key -out server.csr    #先输入密码，再输信息  
> openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt  
> sudo cp server.crt /etc/ssl/certs   #公钥  
> sudo cp server.key /etc/ssl/private   #私钥  
> \-------------------------------------  
> 更改虚拟主机配置  
> 添加：  
> SSLEngine on  
> SSLOptions +StrictRequire  
> SSLCertificateFile /etc/ssl/certs/server.crt  
> SSLCertificateKeyFile /etc/ssl/private/server.key  
> 
> ![ubuntus 最佳方案 -3 - leaf - ------坚持雅操------](http://img1.ph.126.net/EWKDYD0fPBHsN0y_3ZXbLA==/2824601391308859841.jpg "ubuntus 最佳方案 -3 - leaf - ------坚持雅操------")  
> \------------------------------------------  
> 
> sudo /etc/init.d/apache2 restart  
> https://172.16.43.140  
> 
> ![ubuntus 最佳方案 -3 - leaf - ------坚持雅操------](http://img2.ph.126.net/vcjije7yiPpC1kYykPBB0w==/110619665864714502.jpg "ubuntus 最佳方案 -3 - leaf - ------坚持雅操------")

 Apache 性能优化

> 详见 ubuntus 最佳方案  3-apache.conf
> 
>   
> 
> 启用压缩

> > sudo a2enmod deflate
> 
> > sudo /etc/init.d/apache2 force-reload
> 
> > 配置文件为：/etc/apache2/mods-enabled/deflate.conf
> 
> > <IfModule mod\_deflate.c>
> 
> >           AddOutputFilterByType DEFLATE text/html text/plain text/xml
> 
> > </IfModule>

>   
> 
> 使用缓存
> 
> sudo a2enmod disk\_cache           (sudo a2enmod mem\_cache)
> 
> 配置文件/etc/apache2/sites-available/www.a.com
> 
> 在最后添加：
> 
>     <IfModule mod\_disk\_cache.c>
> 
>         CacheEnable disk /               #缓存类型为硬盘   /为网站的根目录，即对整个网站启用缓存
> 
>         CacheRoot /var/www/www.a.com/cache
> 
>         CacheDefaultExpire 7200    #失效周期，7200s
> 
>         CacheMaxExpire 604800    #最大失效周期，604800s
> 
>     </IfModule>
> 
> 创建cache文件夹

> > sudo mkdir /var/www/www.a.com/cache
> 
> > sudo chown www-data:www-data /var/www/www.a.com/cache
> 
> > sudo /etc/init.d/apache2 restart

>   
> 
> 压力测试

> > ab -n 20000 -c 200 http://localhost/

> > ab apache benchmarking
> 
> > \-n 发送总数
> 
> > \-c 一次发送
> 
> >   

Apache安全相关  

> 查看http文件头

> > telnet 172.16.43.140 80 
> 
> > 然后输入HEAD / HTTP/1.0 
> 
> > 然后可以看到

> ![ubuntus 最佳方案 -3 - leaf - ------坚持雅操------](http://img6.ph.126.net/MA9PPoapzN4loDA5xqZ5_A==/605452674922044526.jpg "ubuntus 最佳方案 -3 - leaf - ------坚持雅操------")

> >  更改方法：更改/etc/apache2/apache2.conf 里面的ServerTokens：prod 

>   
> 
> DDOS防范

> > 略

>   

Apache 日志分析  

>   
> 
>   
> 
>