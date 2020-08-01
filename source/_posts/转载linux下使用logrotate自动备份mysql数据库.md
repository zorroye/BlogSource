---
title: '[转载]linux下使用logrotate自动备份mysql数据库'
tags:
  - 未分类
id: '285'
date: 2012-11-23 10:12:00
---

原文：http://islandlinux.org/howto/automated-mysql-backups  
参考：http://www.cslog.cn/Content/logrotate-mysql-automated-backu/  
  
1、建备份账户  

> mysql -u root -p  
> 
> > GRANT SELECT, LOCK TABLES ON \*.\* TO backup@localhost IDENTIFIED BY 'bkup123';  
> > FLUSH PRIVILEGES;  
> > EXIT；  
> > #账户名：backup   密码：bkup123  

  
2、建密码文件用于登录  

> touch .mysql.backup  
> 
> > \[client\]  
> > user="backup"  
> > password="bkup123"  
> 
> chmod 400 .mysql.backup  
>   

3、建备份脚本  

> cd /usr/local/sbin  

> sudo touch  backup\_mysql.sh  
> sudo vi backup\_mysql.sh  

#!/bin/sh  
#  
\# written by Dallas Vogels 2008-10-01  
#  
export PATH=/bin:/usr/bin:/sbin:/usr/sbin  
  
#将数据库备份到 /var/backups/mysql  
OUTPUTDIR="/var/backups/mysql"  
OPTIONS="--all --complete-insert --add-drop-table --extended-insert --quote-names"  
#密码文件所在位置  
CONFIG\_FILE="/home/solarit001/.mysql.backup"  
  
\# check that backup dir exists  
if \[ ! -d $OUTPUTDIR \]; then  
        mkdir $OUTPUTDIR  
fi  
  
\# get list of databases  
DATABASES=\`echo "SHOW DATABASES" | mysql --defaults-file="$CONFIG\_FILE" mysql\`  
#我这里的结果如下  
#Database  
#information\_schema  
#mysql  
#wordpress  
  
 for DATABASE in $DATABASES; do  
  
#备份名字为\*.sql  
  if \[ "$DATABASE" != "Database" -a "$DATABASE" != "information\_schema" \]; then  
    # backup database  
    mysqldump --defaults-file="$CONFIG\_FILE" $OPTIONS $DATABASE > $OUTPUTDIR/$DATABASE.sql  
  fi  
  
done  
  
exit 0  

> sudo chmod 500 backup\_mysql.sh  
>   

4、创建logrotate文件  

> cd /etc/logrotate.d  
> sudo touch mysql-backups  
> sudo vi mysql-backups  

/var/backups/mysql/\*.sql {  
  daily  
  copy  
  missingok  
  rotate 30  
  compress  
  notifempty  
  create 640 root adm  
  sharedscripts  
  prerotate  
    /usr/local/sbin/backup\_mysql.sh  #备份之前先运行backup\_mysql.sh  
  endscript  
}

  

>   
> 5、测试  

  

> sudo backup\_mysql.sh  
> sudo logrotate -f /etc/logrotate.d/mysql-backups

>   
>   

问题：  
mysqldump: Got error: 1044: Access denied for user 'backup'@'localhost' to database 'information\_schema'  
when using LOCK TABLES  
  
解决：  

> 1、加参数：--skip-lock-tables  
> 2、不备份被锁定的数据库：  
> 
> > if \[ "$DATABASE" != "Database" -a "$DATABASE" != "information\_schema" \]; then  
> 
> 3、用root账户备份  
>   
>