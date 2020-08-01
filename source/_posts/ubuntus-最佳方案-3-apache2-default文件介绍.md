---
title: ubuntus 最佳方案 3-apache2 default文件介绍
tags:
  - 未分类
id: '159'
abbrlink: 3499039072
date: 2012-04-18 22:18:00
---

文件位置：/etc/apache2/sites-available/default

文档分2部分：NameVirtualHost 和<VirtualHost></VirtualHost>

  

NameVirtualHost \*         指定服务器的网卡，开通线路等  
<VirtualHost \*>               指定虚拟主机的IP地址。  
        ServerAdmin webmaster@localhost         指定站长EMAIL  
          
        DocumentRoot /var/www/                          指定网站根目录     

 1>更改为网站存放的位置：如/var/www/blog.test.com  
        <Directory />                                        ？？全部虚拟主机的设置？？  
                Options FollowSymLinks                     网站根目录的特性，允许使用符号链接  
                AllowOverride None                            网站根目录的特性，忽略.htaccess文件的作用  
        </Directory>  
        <Directory /var/www/>                      2>更改为网站存放的位置：如/var/www/blog.test.com  
                Options Indexes FollowSymLinks MultiViews  
                AllowOverride None  
                Order allow,deny          acl设置，符合下一行allow规则的都能访问，不符合allow规则的不能访问

               # Order deny,allow        acl设置，符合下一行deny规则的都不能访问，不符合deny规则的能访问  
                allow from all                控制哪些主机可以访问，默认所有主机都可以访问  
        </Directory>  
  
        ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/  
        <Directory "/usr/lib/cgi-bin">  
                AllowOverride None  
                Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch  
                Order allow,deny  
                Allow from all  
        </Directory>  
  
        ErrorLog /var/log/apache2/error.log    3>log存放的文档位置  
  
        # Possible values include: debug, info, notice, warn, error, crit,  
        # alert, emerg.  
        LogLevel warn                                     4>设置log信息的等级  
  
        CustomLog /var/log/apache2/access.log combined  
        ServerSignature On  
  
    Alias /doc/ "/usr/share/doc/"    设置别名，访问/var/www/blog.test.com/doc 其实就是访问/usr/share/doc  
    <Directory "/usr/share/doc/">  
        Options Indexes MultiViews FollowSymLinks  
        AllowOverride None  
        Order deny,allow  
        Deny from all  
        Allow from 127.0.0.0/255.0.0.0 ::1/128  
    </Directory>  
  
</VirtualHost>