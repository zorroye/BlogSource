---
title: ubuntus 最佳方案 -4 LAMP
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '162'
abbrlink: 2177598682
date: 2012-04-27 11:01:00
---

1、安装lamp套装  

> sudo apt-get install apache2 libapache2-mod-php5 php5-mysql mysql-server php5-memcache php5-gd  
> 说明：  
> php5-gd用于处理图片格式  
> php5-memcache 用于把内存做缓存用  
>   

2、创建数据库、建用户等  

> nano mydb.sql  

> > DROP TABLE IF EXISTS \`users\`;  
> > CREATE TABLE \`users\`(  
> >   \`uid\` int(10) unsigned NOT NULL default '0',  
> >   \`name\` varchar(60) NOT NULL default '',  
> >   \`pass\` varchar(32) NOT NULL default '',  
> >   \`mail\` varchar(64) default '',  
> >   PRIMARY KEY (\`uid\`),  
> >   UNIQUE KEY \`name\` (\`name\`)  
> > );  
> >   
> > INSERT INTO \`users\` (\`uid\`, \`name\`, \`pass\`, \`mail\`) VALUES  
> > (1, 'Hiweed', MD5('passwdHiweed'), 'hiweed@test.com'),  
> > (2, 'Ning', MD5('passwdNing'), 'ning@test.com'),  
> > (3, 'Guoce', MD5('passwdGuoce'), 'guoce@test.com')  
> 
> mysqladmin -uroot -p create mydb  
> mysql mydb -uroot -p < mydb.sql  
> 检查导入的数据是否正确  
> mysql mydb -uroot -p 然后输入密码  
> mysql> select \* from users;  
> 
> ![ubuntus 最佳方案 -4 - leaf - ------坚持雅操------](http://img1.ph.126.net/_YJiklBfcPvLaHGWFYHlsA==/2493586818696969731.jpg "ubuntus 最佳方案 -4 - leaf - ------坚持雅操------")
> 
>  建用户并设置权限  
> mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, INDEX, ALTER ON mydb.\* TO 'abc'@'localhost' IDENTIFIED BY '123456';  
> Query OK, 0 rows affected (0.00 sec)  
>   
> mysql> flush privileges;    #刷新使之生效  
> Query OK, 0 rows affected (0.00 sec)  
>   
> mysql> exit  
> Bye  

  
3、测试PHP  

> echo "<?php phpinfo(); ?>"  | sudo tee /var/www/www.a.com/phpinfo.php  

>   
> 装phpmyadmin  
> sudo apt-get install phpmyadmin  
> sudo ln -s /usr/share/phpmyadmin /var/www/www.a.com/phpmyadmin  
>   

4、建站实例drupal  

> 1、下载drupal  
> 
> > http://drupal.org/node/3060/release?api\_version\[\]=87  
> > 按书上的，我下载的也是6.6版本  
> > tar xvf drupal-6.6.tar.gz  
> > sudo mv drupal-6.6/{\*,.htaccess} /var/www/www.a.com  
> 
> 2、建drupal数据库和用户  
> 
> > mysqladmin -uroot -p create drupal6  
> 
> > mysql -uroot -p  
> 
> > mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal6.\* TO 'drupaluser'@'localhost' IDENTIFIED BY '123456';  
> > Query OK, 0 rows affected (0.01 sec)  
> >   
> > mysql> FLUSH PRIVILEGES;  
> > Query OK, 0 rows affected (0.01 sec)  
> >   
> > mysql> \\q  
> > Bye  
> 
> 3、开启clean url功能  
> 
> > sudo nano /etc/apache2/sites-available/www.a.com  
> > 把<Direectory /var/www/www.a.com/> 下面的  
> > allowoverride none  改为allowoverride all  
> >   
> 
> 4、配置drupal  
> 
> > 第二步 要更改权限  
> > sudo chmod o+w /var/www/www.a.com/sites/default  
> > sudo chmod o+w /var/www/www.a.com/sites/default/settings.php  
> > 第五步 再把权限改回来  
> > sudo chmod o-w /var/www/www.a.com/sites/default  
> > sudo chmod o-w /var/www/www.a.com/sites/default/settings.php  
> >   
> > 下载中文模块  
> > http://drupal.org/node/265348  
> 
>   

  
5、建wordpress  

> 1、建wordpress数据库和用户  
> 
> > mysqladmin -uroot -p create wordpress  
> 
> > mysql -uroot -p  
> 
> mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON wordpress.\* TO 'wordpress'@'localhost' IDENTIFIED BY '123456';  
> Query OK, 0 rows affected (0.01 sec)  
>   
> mysql> FLUSH PRIVILEGES;  
> Query OK, 0 rows affected (0.01 sec)  
>   
> mysql> \\q  
> Bye  
>   
> 2、改所有者  
> sudo chown -R www-data:www-data /var/www/wordpress  
>   
> 3、然后下一步下一步即可  
>   
>   
>   
> 附、更改上传文件的大小限制  
> sudo gedit /etc/php5/apache2/php.ini  
> 更改  
> 
> > post\_max\_size=200M  
> > file\_uploads=On  
> > upload\_max\_filesize=100M  
> 
>   
> 
> ![ubuntus 最佳方案 -4 LAMP - leaf - ------坚持雅操------](http://img2.ph.126.net/b-5dciHZHxuNErJeRiLVHw==/1074952936075702232.jpg "ubuntus 最佳方案 -4 LAMP - leaf - ------坚持雅操------")
> 
>