---
title: ubuntus 最佳方案  3-apache.conf
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '161'
abbrlink: 2254503815
date: 2012-04-19 15:30:00
---

apache2.conf默认配置如下

> ServerRoot "/etc/apache2"

> LockFile /var/lock/apache2/accept.lock

> PidFile ${APACHE\_PID\_FILE}
> 
> \# Timeout: The number of seconds before receives and sends time out.
> 
> Timeout 300
> 
>   
> 
> \# KeepAlive: Whether or not to allow persistent connections (more than
> 
> \# one request per connection). Set to "Off" to deactivate.
> 
> KeepAlive On
> 
>   
> 
> \# MaxKeepAliveRequests: The maximum number of requests to allow
> 
> \# during a persistent connection. Set to 0 to allow an unlimited amount.
> 
> \# We recommend you leave this number high, for maximum performance.
> 
> MaxKeepAliveRequests 100
> 
>   
> 
> \# KeepAliveTimeout: Number of seconds to wait for the next request from the
> 
> \# same client on the same connection.
> 
> KeepAliveTimeout 15    #保持连接15秒不断开
> 
>   
> 
> \# prefork MPM
> 
> <IfModule mpm\_prefork\_module>
> 
>     StartServers          5
> 
>     MinSpareServers       5
> 
>     MaxSpareServers      10
> 
>     MaxClients          150
> 
>     MaxRequestsPerChild   0
> 
> </IfModule>
> 
>   
> 
> \# worker MPM
> 
> <IfModule mpm\_worker\_module>
> 
>     StartServers          2
> 
>     MaxClients          150       #最大连接数
> 
>     MinSpareThreads      25
> 
>     MaxSpareThreads      75 
> 
>     ThreadsPerChild      25
> 
>     MaxRequestsPerChild   0
> 
> </IfModule>
> 
>   
> 
> \# These need to be set in /etc/apache2/envvars
> 
> User ${APACHE\_RUN\_USER}
> 
> Group ${APACHE\_RUN\_GROUP}
> 
>   
> 
> AccessFileName .htaccess
> 
>   
> 
> \# The following lines prevent .htaccess and .htpasswd files from being 
> 
> \# viewed by Web clients. 
> 
> <Files ~ "^\\.ht">
> 
>     Order allow,deny
> 
>     Deny from all
> 
> </Files>
> 
>   
> 
> DefaultType text/plain
> 
>   
> 
> HostnameLookups Off   #off只获取客户的IP地址，on则获取客户的DNS
> 
>   
> 
> ErrorLog /var/log/apache2/error.log
> 
>   
> 
> LogLevel warn
> 
>   
> 
> \# Include module configuration:
> 
> Include /etc/apache2/mods-enabled/\*.load
> 
> Include /etc/apache2/mods-enabled/\*.conf
> 
>   
> 
> \# Include all the user configurations:
> 
> Include /etc/apache2/httpd.conf
> 
>   
> 
> \# Include ports listing
> 
> Include /etc/apache2/ports.conf
> 
>   
> 
> LogFormat "%h %l %u %t \\"%r\\" %>s %b \\"%{Referer}i\\" \\"%{User-Agent}i\\"" combined
> 
> LogFormat "%h %l %u %t \\"%r\\" %>s %b" common
> 
> LogFormat "%{Referer}i -> %U" referer
> 
> LogFormat "%{User-agent}i" agent
> 
>   
> 
> ServerTokens Full            #显示HTTP响应头的信息 
> 
>   
> 
> ServerSignature On
> 
>   
> 
> Include /etc/apache2/sites-enabled/