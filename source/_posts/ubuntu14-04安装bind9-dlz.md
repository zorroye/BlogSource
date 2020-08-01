---
title: UBUNTU14.04安装BIND9_DLZ
tags:
  - 未分类
id: '334'
date: 2015-09-13 19:16:00
---

参考：  

> http://ubuntuforums.org/showthread.php?t=823578  
> http://ubuntuforums.org/showthread.php?p=11380598  
> http://bind-dlz.sourceforge.net/  

  
环境  

> 服务器OS：UBUNTU14.04  
> 服务器主机名：bind9  
> 域：leaf.org  
> 完整名字：bind9.leaf.org  
> mysql密码：123456  
> db名字：bind9dlz  
> 服务器IP：192.168.122.41  
> 网关：192.168.122.1  
>   

服务器名称及IP地址设置  

> cat /etc/hostname  
> 
> > bind9.leaf.org  
> 
> cat /etc/hosts  
> 
> > 127.0.0.1    bind9.leaf.org   bind9  
> 
> cat /etc/network/interfaces  
> 
> > \# The loopback network interface  
> > auto lo  
> > iface lo inet loopback  
> >   
> > \# The primary network interface  
> > auto eth0  
> > iface eth0 inet static  
> >     address 192.168.122.41  
> >     netmask 255.255.255.0  
> >     gateway 192.168.122.1  
> >     dns-nameservers 192.168.122.41 192.168.122.1  
> >     dns-search leaf.org  
> 
> sudo reboot  

  
1、安装带dlz功能的bind9  

> sudo su  
> apt-get install bind9  
> apt-get install bind9utils  
> apt-get remove bind9  
> apt-get build-dep bind9  
> apt-get install fakeroot  
> mkdir /home/ywz/bind9  
> cd /home/ywz/bind9  
> apt-get source bind9  
> apt-get install libpq-dev  
> apt-get install libmysqlclient-dev  
> apt-get install unixodbc unixodbc-dev  
> apt-get install mysql-server mysql-client  
>   
> nano /home/ywz/bind9/bind9-9.9.5.dfsg/debian/rules  
> 
> > 在configure-stamp:下面加入    --with-dlz-mysql \\  
> 
> 然后制作软件包 dpkg-buildpackage -rfakeroot -b  
> 
> ![UBUNTU14.04安装BIND9_DLZ - leaf - ------勤解万难------](http://img2.ph.126.net/dZv-i8qbHFlbF3c5bOJeOQ==/6631405315769279714.png "UBUNTU14.04安装BIND9_DLZ - leaf - ------勤解万难------")
> 
> 然后安装：dpkg -i \*.deb  

  
bind9配置  

> nano /etc/bind/named.conf.options  
> 加入  
> 
> > forwarders {  
> > 
> > > 192.168.122.41；  
> > > 192.168.122.1；  
> > 
> > };  

> nano /etc/bind/named.conf.local  
> 加入  
> dlz "Mysql zone" {  
>   database "mysql  
>    {host=127.0.0.1 dbname=bind9dlz user=root pass=123456}  
>    {select zone from dns\_records where zone = '$zone$'}  
>    {select ttl, type, mx\_priority, case when lower(type)='txt' then concat('\\"', data, '\\"') when lower(type) = 'soa' then concat\_ws(' ', data, resp\_person, serial, refresh, retry, expire, minimum) else data end from dns\_records where zone = '$zone$' and host = '$record$'}";  
> };  
> 或者  
> dlz "Mysql zone" {  
>    database "mysql  
>    {host=127.0.0.1 dbname=bind9dlz user=root pass=123456}  
>    {select zone from dns\_records where zone = '$zone$'}  
>    {select ttl, type, mx\_priority, case when lower(type)='txt' then concat('\\"', data, '\\"')  
>         when lower(type) = 'soa' then concat\_ws(' ', data, resp\_person, serial, refresh, retry, expire, minimum)  
>         else data end from dns\_records where zone = '$zone$' and host = '$record$'}  
>    {}  
>    {select ttl, type, host, mx\_priority, case when lower(type)='txt' then  
>         concat('\\"', data, '\\"') else data end, resp\_person, serial, refresh, retry, expire,  
>         minimum from dns\_records where zone = '$zone$'}  
>    {select zone from xfr\_table where zone = '$zone$' and client = '$client$'}";  
> };  
>   

  
mysql配置  

> mysql -u root -p  
> #建数据库  
> create database bind9dlz;  
> grant all privileges on bind9dlz.\* to root@localhost identified by '123456';  
> #建表  
> use bind9dlz;  
> 
> > CREATE TABLE \`dns\_records\` (  
> >   \`id\` int(11) NOT NULL auto\_increment,  
> >   \`zone\` varchar(64) default NULL,  
> >   \`host\` varchar(64) default NULL,  
> >   \`type\` varchar(8) default NULL,  
> >   \`data\` varchar(64) default NULL,  
> >   \`ttl\` int(11) NOT NULL default '3600',  
> >   \`mx\_priority\` int(11) default NULL,  
> >   \`refresh\` int(11) NOT NULL default '3600',  
> >   \`retry\` int(11) NOT NULL default '3600',  
> >   \`expire\` int(11) NOT NULL default '86400',  
> >   \`minimum\` int(11) NOT NULL default '3600',  
> >   \`serial\` bigint(20) NOT NULL default '2008082700',  
> >   \`resp\_person\` varchar(64) NOT NULL default 'ywz@163.com',  
> >   \`primary\_ns\` varchar(64) NOT NULL default 'bind9.leaf.org',  
> >   \`data\_count\` int(11) NOT NULL default '0',  
> >   PRIMARY KEY  (\`id\`),  
> >   KEY \`host\` (\`host\`),  
> >   KEY \`zone\` (\`zone\`),  
> >   KEY \`type\` (\`type\`)  
> > ) ENGINE=MyISAM DEFAULT CHARSET=latin1;  
> 
> #写入DNS记录 insert开头这四句  
> // for www.leaf.org to resolve to 192.168.122.41  
> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', 'www', 'A', '192.168.122.41', null);  
>   
> // for leaf.org to resolve to 192.168.122.41  
> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', '@', 'A', '192.168.122.41', null);  
>   
> // for bind9.leaf.org to alias to www.leaf.org  
> // note the trailing period in the data field  
> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', 'bing9', 'CNAME', 'www.leaf.org.', null);  
>   
> // for mail for leaf.org to go to leaf.org  
> // note the trailing period in the data field  
> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', '@', 'MX', 'leaf.org.', '0');  

  

> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', '@', 'SOA', '192.168.122.41', 10800);  
> insert into dns\_records (zone, host, type, data, mx\_priority) values ('leaf.org', '@', 'NS', '192.168.122.41', null);  

  

> quit  

  
验证  

> sudo /etc/init.d/bind9 start  
>   

> dig @192.168.122.41 leaf.org  
> 
> ![UBUNTU14.04安装BIND9_DLZ - leaf - ------勤解万难------](http://img2.ph.126.net/j_E32s1s-kz3vAm_aRaiNg==/6630455337723668096.png "UBUNTU14.04安装BIND9_DLZ - leaf - ------勤解万难------")
> 
>