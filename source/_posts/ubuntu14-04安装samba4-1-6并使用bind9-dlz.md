---
title: UBUNTU14.04安装SAMBA4.1.6并使用BIND9_DLZ
tags:
  - samba
categories:
  - Services
  - samba
id: '335'
abbrlink: 1528754021
date: 2015-09-16 10:46:00
---

  
参考：  

> http://blogging.dragon.org.uk/samba4-ad-dc-on-ubuntu-14-04/  
> https://wiki.samba.org/index.php/DNS\_Backend\_BIND  
> http://blog.163.com/ywz\_306/blog/static/1325771120158137124386/  

  
思路：  

> 首先把bind\_dlz，ntp，(openldap)等都设置好，  
> 然后安装samba，  
> 最后配置samba的时候把bind\_dlz,openldap都带上即可  

  
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
> >     dns-nameservers 192.168.122.41 192.168.122.1 #bind配置完后把122.1去掉  
> >     dns-search leaf.org  
> 
> sudo reboot  

  
一、BIND9\_DLZ  

> http://blog.163.com/ywz\_306/blog/static/1325771120158137124386/

  
二、安装NTP服务  

> sudo apt-get install ntp  
>   

三、安装samba4  

> 安装软件包  
> sudo apt-get install samba smbclient build-essential libacl1-dev libattr1-dev \\ libblkid-dev libgnutls-dev libreadline-dev python-dev libpam0g-dev \\ python-dnspython gdb pkg-config libpopt-dev libldap2-dev \\ dnsutils libbsd-dev krb5-user docbook-xsl libcups2-dev ldb-tools

> Kerberos设置的时候会跳出设置，依次是  
> 
> > Configuring Kerberos Authentication: LEAF.ORG  
> > hostname of Kerberos servers in the BLACK.DRAGON.LAB: bind9  
> > hostname of the Administrative (password changing) servers: bind9  
> 
>   
> 配置  
> 1、先移除原有smb.conf  
> sudo mv /etc/samba/smb.conf{,-orig}  
> sudo samba-tool domain provision --use-rfc2307 --interactive  
> 
> > Realm: LEAF.ORG  
> > Domain: LEAF  
> > Server Role: dc  
> > DNS Backend: BIND\_DLZ  
> 
>   
> 配置/etc/samba/smb.conf  
> 
> > \[global\]里面加入  
> 
> > allow dns updates = nonsecure and secure  
> > dns forwarder = 192.168.122.41  
> 
>   
> 配置/var/lib/samba/private/named.conf  
> 
> > named -V  
> > 可以看到bind版本号为 BIND 9.9.5-3ubuntu0.5-Ubuntu  
> >   
> > 然后更改/var/lib/samba/private/named.conf  
> > 把9.8注销掉，启用9.9  
> 
> > dlz "AD DNS Zone" {  
> >     # For BIND 9.8.0  
> >    # database "dlopen /usr/lib/i386-linux-gnu/samba/bind9/dlz\_bind9.so";  
> >   
> >     # For BIND 9.9.0  
> >      database "dlopen /usr/lib/i386-linux-gnu/samba/bind9/dlz\_bind9\_9.so";  
> > };  
> 
>   
> 配置/etc/bind/named.conf.options  
> 
> > options{}里面加入  
> > tkey-gssapi-keytab "/var/lib/samba/private/dns.keytab";  
> 
>   
> 配置/etc/bind/named.conf  
> 
> > 第二行加入include "/var/lib/samba/private/named.conf";  
> 
>   
> 
> > 配置权限sudo nano /etc/apparmor.d/usr.sbin.named  
> > 
> > > /usr/lib/i386-linux-gnu/ldb/\*\* rwmk,  
> > > /usr/lib/i386-linux-gnu/samba/\*\* rwmk,  
> > > /var/lib/samba/private/dns/\*\* rwmk,  
> > > /var/lib/samba/private/named.conf r,  
> > > /var/lib/samba/private/dns.keytab r,  
> > > /var/tmp/\* rw,  
> > > /dev/urandom rw,  
> > 
> > sudo service apparmor reload  
> 
>   
> 
> > 更改dns.keytab权限  
> > sudo chgrp bind /var/lib/samba/private/dns.keytab  
> > sudo chmod g+r /var/lib/samba/private/dns.keytab  
> 
>   
> 删除/etc/bind/named.conf.local下的dlz全部内容。  
>   

sudo reboot。  
至此，全部配完。  

>   

三、碰到的问题  

> 检查bind问题  
> 
> > named -d 3 -f -g  
> > named-checkconf  

>   
> 问题1：  

> open /var/lib/samba/private/named.conf permission denied  
> 
> > 在/etc/apparmor.d/usr.sbin.named 加入以下内容  
> > 或者/etc/apparmor.d/local/usr.sbin.named加入以下内容  
> > 
> > > /usr/lib/i386-linux-gnu/ldb/\*\* rwmk,  
> > > /usr/lib/i386-linux-gnu/samba/\*\* rwmk,  
> > > /var/lib/samba/private/dns/\*\* rwmk,  
> > > /var/lib/samba/private/named.conf r,  
> > > /var/lib/samba/private/dns.keytab r,  
> > > /var/tmp/\* rw,  
> > > /dev/urandom rw,  
> > >   
> > 
> > sudo service apparmor reload  
> 
>   
> 问题2：  
> 'dlz' redefined near 'dlz'  
> 
> > 把原先加在nano /etc/bind/named.conf.local下的dlz全部删除即可

  
四、测试  

>  smbclient -L localhost -U%  
> 
> > Domain=\[LEAF\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> >   
> >     Sharename       Type      Comment  
> >     ---------       ----      -------  
> >     netlogon        Disk       
> >     sysvol          Disk       
> >     IPC$            IPC       IPC Service (Samba 4.1.6-Ubuntu)  
> > Domain=\[LEAF\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> >   
> >     Server               Comment  
> >     ---------            -------  
> >   
> >     Workgroup            Master  
> >     ---------            -------  
> >     WORKGROUP            BIND9  
> 
> ywz@bind9:/var/log$ smbclient //localhost/netlogon -UAdministrator -c 'ls'  
> 
> > Enter Administrator's password:  
> > Domain=\[LEAF\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> >   .                                   D        0  Tue Sep 15 17:42:22 2015  
> >   ..                                  D        0  Tue Sep 15 17:42:31 2015  
> >   
> >         60333 blocks of size 131072. 43559 blocks available  
> 
> ywz@bind9:/var/log$ host -t SRV \_ldap.\_tcp.leaf.org.  
> 
> > \_ldap.\_tcp.leaf.org has SRV record 0 100 389 bind9.leaf.org.  
> 
> ywz@bind9:/var/log$ host -t SRV \_kerberos.\_udp.leaf.org.  
> 
> > \_kerberos.\_udp.leaf.org has SRV record 0 100 88 bind9.leaf.org.  
> 
> ywz@bind9:/var/log$ host -t A bind9.leaf.org.  
> 
> > bind9.leaf.org has address 192.168.122.41  
> 
> ywz@bind9:/var/log$ kinit administrator  
> 
> > Password for administrator@LEAF.ORG:  
> > Warning: Your password will expire in 41 days on Tue 27 Oct 2015 05:42:29 PM CST  
> 
> ywz@bind9:/var/log$ klist  
> 
> > Ticket cache: FILE:/tmp/krb5cc\_1000  
> > Default principal: administrator@LEAF.ORG  
> >   
> > Valid starting       Expires              Service principal  
> > 09/16/2015 10:02:07  09/16/2015 20:02:07  krbtgt/LEAF.ORG@LEAF.ORG  
> >     renew until 09/17/2015 10:02:03  
> 
> ywz@bind9:/var/log$ samba-tool dns query bind9 LEAF.ORG @ ALL  
> 
> >   Name=, Records=3, Children=0  
> >     SOA: serial=1, refresh=900, retry=600, expire=86400, minttl=0, ns=bind9.leaf.org., email=hostmaster.leaf.org. (flags=600000f0, serial=1, ttl=3600)  
> >     NS: bind9.leaf.org. (flags=600000f0, serial=1, ttl=900)  
> >     A: 192.168.122.41 (flags=600000f0, serial=1, ttl=900)  
> >   Name=\_msdcs, Records=0, Children=0  
> >   Name=\_sites, Records=0, Children=1  
> >   Name=\_tcp, Records=0, Children=4  
> >   Name=\_udp, Records=0, Children=2  
> >   Name=bind9, Records=1, Children=0  
> >     A: 192.168.122.41 (flags=f0, serial=1, ttl=900)  
> >   Name=DomainDnsZones, Records=0, Children=2  
> >   Name=ForestDnsZones, Records=0, Children=2  
> 
> ywz@bind9:/var/log$ ping www.baidu.com  
> 
> > PING www.a.shifen.com (103.235.46.39) 56(84) bytes of data.  
> > ^C64 bytes from 103.235.46.39: icmp\_seq=1 ttl=49 time=420 ms  
> >   
> > \--- www.a.shifen.com ping statistics ---  
> > 1 packets transmitted, 1 received, 0% packet loss, time 0ms  
> > rtt min/avg/max/mdev = 420.071/420.071/420.071/0.000 ms