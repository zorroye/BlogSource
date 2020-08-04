---
title: UBUNTU14.04 server安装AWStats
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '166'
abbrlink: 201714586
date: 2015-05-08 11:11:00
---

0、设置网站的log存放地址  

> cd /etc/apache2/sites-available

> sudo cp 000-default.conf blog.mytest.com.conf
> 
> sudo nano blog.mytest.com.conf

> > DocumentRoot /var/www/blog.mytest.com
> > 
> > ErrorLog ${APACHE\_LOG\_DIR}/error-blog.mytest.com.log
> > 
> > CustomLog ${APACHE\_LOG\_DIR}/access-blog.mytest.com.log combined

> sudo mkdir /var/www/blog.mytest.com
> 
> echo "<h1>Amitabha</h1>" | sudo tee /var/www/blog.mytest.com/index.html
> 
> sudo a2dissite 000-default && sudo a2ensite blog.mytest.com
> 
> sudo service apache2 restart

  

1、安装配置awstats

> sudo apt-get install awstats -y

  

> 新建apache配置文件local-awstats.conf

> > sudo nano /etc/apache2/conf-available/local-awstats.conf

> > > Alias /awstatsclasses "/usr/share/awstats/lib/"
> 
> > > Alias /awstats-icon/ "/usr/share/awstats/icon/"
> 
> > > Alias /awstatscss "/usr/share/doc/awstats/examples/css"
> 
> > > ScriptAlias /awstats/ /usr/lib/cgi-bin/

> 启用配置文件

> > sudo a2enconf local-awstats

> 启用cgi模块

> > sudo  a2enmod cgi
> 
> > sudo service apache2 reload

>   
> 
>   
> 
> 为网站建立awstats配置文件，主要是指定网站的log地址
> 
> cd /etc/awstats
> 
> sudo cp awstats.conf     awstats.blog.mytest.com.conf
> 
> sudo nano awstats.blog.mytest.com.conf

> > LogFile="/var/log/apache2/access-blog.mytest.com.log"  
> > 
> > SiteDomain="blog.mytest.com"  
> > 
> > HostAliases="localhost 127.0.0.1 blog.mytest.com"

  
  
3、运行awstats分析

> sudo chmod a+r /var/log/apache2/access-blog.mytest.com.log\*

> sudo perl /usr/lib/cgi-bin/awstats.pl -update -config=blog.mytest.com

>   

> 打开网页查看

> http://blog.mytest.com/awstats/awstats.pl?config=blog.mytest.com

> ![UBUNTU SERVER14.04 安装AWStats - leaf - ------勤解万难------](http://img0.ph.126.net/zr0X7GYYlTWwGucgI-YRiw==/6630260724164504700.png "UBUNTU SERVER14.04 安装AWStats - leaf - ------勤解万难------")

4、awstats的cron任务

> MAILTO=root
> 
> \*/10 \* \* \* \* www-data \[ -x /usr/share/awstats/tools/update.sh \] && /usr/share/awstats/tools/update.sh
> 
> \# Generate static reports:
> 
> 10 03 \* \* \* www-data \[ -x /usr/share/awstats/tools/buildstatic.sh \] && /usr/share/awstats/tools/buildstatic.sh
> 
>   

> >