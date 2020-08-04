---
title: ubuntu10.04 安装 itdb 1.1
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '207'
abbrlink: 2125441215
date: 2011-04-28 15:07:00
---

itdb:IT资产库存管理软件 [http://www.sivann.gr/software/itdb/](http://www.sivann.gr/software/itdb/)

可以全部导出为xls格式，亦可导出数据库等，除了英文，其他多挺好用的

  

0、sudo apt-get install apache2 libapache2-mod-php5 php5-sqlite sqlite3

1、 tar -xvf itdb-1.1.tar.gz

 sudo mv itdb /var/www

2、cd /var/www/itdb

 sudo mv pure.db itdb.db

3、sudo cp /etc/apache2/sites-available/default /etc/apache2/sites-available/itdb

 sudo nano /etc/apache2/sites-available/itdb

 1>修改DocumentRoot /var/www             为 DocumentRoot /var/www/itdb

 2>修改<DocumentRoot /var/www>         为 <DocumentRoot /var/www/itdb>

 3>修改Error /var/log/apache2/error.log 为 Error /var/log/apache2/error-itdb.log

 4> 修改CustomLog /var/log/apache2/access.log combined 为

 CustomLog /var/log/apache2/access-itdb.log combined

 sudo a2dissite default && sudo a2ensite itdb

 sudo /etc/init.d/apache2 restart

4、cd /var/www/itdb

 sudo chown www-data itdb.db 

 sudo chmod u+w itdb.db 

5、cd /var/www

 sudo chown www-data itdb

 sudo chmod u+w itdb

 sudo chown www-data /var/www/itdb/files/

 sudo chmod u+w /var/www/itdb/files/

6、sudo nano conf.php 修改公司名、公司logo等

  

访问：http://localhost