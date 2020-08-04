---
title: ubuntu server 10.04  .htaccess认证
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '149'
abbrlink: 3451413846
date: 2010-09-30 09:44:00
---

浏览权限设置  
1、针对IP、主机名称  
      /etc/apache2/sites-available/default 里面设置  
  
2、输入帐号密码  
    1> 建一个要保护的目录  
         mkdir /var/www/protect  
    2>确定下面是存在的(本来就在的)  
        /etc/apache2/apache2.conf  
 # The following lines prevent .htaccess and .htpasswd files from being  
 # viewed by Web clients.  
 #  
 <Files ~ "^\\.ht">  
 Order allow,deny  
 Deny from all  
 Satisfy all  
 </Files>  
  
        /etc/apache2/sites-available/default 加入  
 <Directory /var/www/protect>  
 AllowOverride AuthConfig  
 Order allow,deny  
 allow from all  
 </Directory>  
    
     3>在/var/www/protect 建 .htaccess 文件 并加入  
 AuthName        "Protect test by .htaccess"     #出现对话框  
 Authtype           Basic                                      #认证的类型  
 AuthUserFile    /var/apache2.passwd             #密码文件地址  
 Require            valid-user                               #允许的用户，valid-user表示apache2.passwd里的帐号都可登录  
  
    4>建密码文件 apache2.passwd  
                sudo htpasswd -c /var/apache2.passwd test020    #新建并添加帐号  
                sudo htpasswd -c /var/apache2.passwd test021    #追加帐号  
   
   5> 重启apache    ：sudo apache2ctl restart  
    
3> SSL 认证  
    待续