---
title: ubuntu server 10.04 apache2：安装webalizer、awstats
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '153'
abbrlink: 3630694637
date: 2010-11-09 12:24:00
---

1、安装webalizer:  
     sudo apt-get install webalizer  
     sudo webalizer  
                    默认页面路径 /var/www/webalizer  
     webalizer 配置文件： /etc/webalizer/webalizer.conf  
                   logFile         更改要分析的log文件  
                   OutputDir    分析好的文件存放位置  
  
2、安装awstats  
    1、 sudo apt-get install awstats  
     2、让apache下所有站点都可使用awstats  
            sudo nano /etc/apache2/awstats.conf  
 Alias /awstatsclasses "/usr/share/awstats/lib"  
                    Alias /awstats-icon/  "/usr/share/awstats/icon/"  
                    Alias /awstatscss     "/usr/share/doc/awstats/examples/css"  
                    ScriptAlias /cgi-bin/  /usr/lib/cgi-bin/  
                    ScriptAlias /awstats/  /usr/lib/cgi-bin/  
                    Options ExecCGI -MultiViews +SymLinksIfOwnerMatch  
           将配置文件加入到apache2.conf中  
                    在apache2.conf中最后添加： Include /etc/apache2/awstats.conf  
           重新加载apache配置：  sudo /etc/init.d/apache2 reload  
     3、修改awstats配置文件 /etc/awstats/awstats.conf  
                    1、sudo cp -a awstats.conf awstats.192.168.1.10.conf  
                    2、sudo nano /etc/awstats/awstats.192.168.1.10.conf  
                             修改LogFile 和 SiteDomain  
     4、运行awstats来分析结果（非必须，可嫩cron运行后查看）  
                   sudo perl /usr/lib/cgi-bin/awstats.pl -update -config=192.168.1.10