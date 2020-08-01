---
title: ubuntu server 10.04 安装PHP强化模块
tags:
  - 未分类
id: '150'
abbrlink: 2665123118
date: 2010-09-30 10:01:00
---

1、安装eaccelerator  
 wget http://bart.eaccelerator.net/source/0.9.6.1/eaccelerator-0.9.6.1.tar.bz2  
 tar -jxvf eaccelerator-0.9.6.1.tar.bz2  
 cd ./eaccelerator-0.9.6.1  
 phpize5 #这个要安装的 sudo apt-get install php-dev  
 ./configure --enable-eaccelerator=shared --with-php-config=/usr/bin/php-config  
 make  
 make install  
  
2、配置相关文件  
 sudo nano /etc/ld.so.conf  
       加入 /usr/lib/php5  
 sudo ldconfig  
 sudo nano /etc/php5/apache2/php.ini  
          加入  
 ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;  
;http://eaccelerator.net;  
;2010.09.29 ywz;  
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;  
extension="eaccelerator.so"  
eaccelerator.shm\_size="16"  
eaccelerator.cache\_dir="/tmp/eaccelerator"  
eaccelerator.enable="1"  
eaccelerator.optimizer="1"  
eaccelerator.check\_mtime="1"  
eaccelerator.debug="0"  
eaccelerator.filter=""  
eaccelerator.shm\_max="0"  
eaccelerator.shm\_ttl="0"  
eaccelerator.shm\_prune\_period="0"  
eaccelerator.shm\_only="0"  
eaccelerator.compress="1"  
eaccelerator.compress\_level="9"  
  
3、建暂存数据目录  
mkdir /tmp/eaccelerator  
chmod 777 /tmp/eaccelerator  
sudo apache2ctl restart  
  
4、测试  
ab -dSk -c100 -n100 http://127.0.0.1/index.php     #index.php  是自己建立的 内容为 <? phpinfo(); ?>