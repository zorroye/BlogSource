---
title: UBUNTU14.04安装SAMBA4.1.6作AD，DNS，ldap
tags:
  - 未分类
id: '332'
date: 2015-09-10 00:00:00
---

  
参考  

> https://wiki.samba.org/index.php/Samba\_AD\_DC\_HOWTO  
> http://www.jadota.com/2013/01/installing-samba4-on-ubuntu-12-04/  

  
环境：  

> 服务器OS：UBUNTU14.04  
> 
> > 服务器主机名：sambadc  
> > 域：ye.org  
> > 完整名字：sambadc.ye.org  
> > NETBIOS名：YE  
> > 域控管理员密码：Password0  
> > 服务器IP：192.168.122.30  
> > 网关：192.168.122.1  
> 
> 客户端OS：winxp  
> 
> > 192.168.122.110  
> > 255.255.255.0  
> > 192.168.122.1  
> > \-------------------------  
> > 192.168.122.30  
> 
> 管理端OS：win2003，win7  
>   

服务器名称及IP地址设置  

> cat /etc/hostname  
> 
> > sambadc.ye.org  
> 
> cat /etc/hosts  
> 
> > 127.0.0.1    sambadc.ye.org    sambadc  
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
> >     address 192.168.122.30  
> >     netmask 255.255.255.0  
> >     gateway 192.168.122.1  
> >     dns-nameservers 192.168.122.30 192.168.122.1  
> >     dns-search ye.org  
> 
> sudo reboot  
>   

安装OPENSSH  

> sudo apt-get update  
> sudo apt-get install openssh-server  

> sudo reboot  
>   

安装NTP

> [http://chenpeng.info/html/241](http://chenpeng.info/html/241)

> sudo apt-get install ntp

>   

安装SAMBA  

> sudo apt-get install build-essential libacl1-dev python-dev libldap2-dev pkg-config gdb libgnutls-dev libblkid-dev libreadline-dev libattr1-dev python-dnspython libpopt-dev libbsd-dev attr docbook-xsl libcups2-dev git      #只需要安装python-dev就可以，方便期间全部安装  
> sudo apt-get instajll samba  
> samba -V  
> 
> > Version 4.1.6-Ubuntu #查询samba版本号  
> 
> sudo reboot  
>   

配置SAMBA  

> sudo mv /etc/samba/smb.conf    /etc/samba/smb.conf-orig  

> sudo su  

> samba-tool domain provision --use-rfc2307 --interactive  

**Realm: YE.ORG**  
 **Domain \[YE\]: YE**  
 **Server Role (dc, member, standalone) \[dc\]: dc**  
 **DNS backend (SAMBA\_INTERNAL, BIND9\_FLATFILE, BIND9\_DLZ, NONE) \[SAMBA\_INTERNAL\]:**  
 **DNS forwarder IP address (write 'none' to disable forwarding) \[192.168.122.30\]: 192.168.122.1**  
**Administrator password:**  
**Retype password:**  
**Looking up IPv4 addresses**  
**Looking up IPv6 addresses**  
**No IPv6 address will be assigned**  
**Setting up share.ldb**  
**Setting up secrets.ldb**  
**Setting up the registry**  
**Setting up the privileges database**  
**Setting up idmap db**  
**Setting up SAM db**  
**Setting up sam.ldb partitions and settings**  
**Setting up sam.ldb rootDSE**  
**Pre-loading the Samba 4 and AD schema**  
**Adding DomainDN: DC=ye,DC=org**  
**Adding configuration container**  
**Setting up sam.ldb schema**  
**Setting up sam.ldb configuration data**  
**Setting up display specifiers**  
**Modifying display specifiers**  
**Adding users container**  
**Modifying users container**  
**Adding computers container**  
**Modifying computers container**  
**Setting up sam.ldb data**  
**Setting up well known security principals**  
**Setting up sam.ldb users and groups**  
**Setting up self join**  
**Adding DNS accounts**  
**Creating CN=MicrosoftDNS,CN=System,DC=ye,DC=org**  
**Creating DomainDnsZones and ForestDnsZones partitions**  
**Populating DomainDnsZones and ForestDnsZones partitions**  
**Setting up sam.ldb rootDSE marking as synchronized**  
**Fixing provision GUIDs**  
**A Kerberos configuration suitable for Samba 4 has been generated at /var/lib/samba/private/krb5.conf**  
**Setting up fake yp server settings**  
**Once the above files are installed, your Samba4 server will be ready to use**  
**Server Role:           active directory domain controller**  
**Hostname:              sambadc**  
**NetBIOS Domain:        YE**  
**DNS Domain:            ye.org**  
**DOMAIN SID:            S-1-5-21-3720594679-4085702030-3410277671**  

> sudo nano  /etc/network/interfaces  
> 
> > \# The loopback network interface  
> > auto lo  
> > iface lo inet loopback  
> >   
> > \# The primary network interface  
> > auto eth0  
> > iface eth0 inet static  
> >     address 192.168.122.30  
> >     netmask 255.255.255.0  
> >     gateway 192.168.122.1  
> >     dns-nameservers 192.168.122.30  
> >     dns-search ye.org  
> 
> sudo reboot  
>   

验证SAMBA  

> sudo apt-get install smbclient  
> smbclient -L localhost -U%  
> 
> > Domain=\[YE\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> >   
> >     Sharename       Type      Comment  
> >     ---------       ----      -------  
> >     netlogon        Disk       
> >     sysvol          Disk       
> >     IPC$            IPC       IPC Service (Samba 4.1.6-Ubuntu)  
> > Domain=\[YE\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> >   
> >     Server               Comment  
> >     ---------            -------  
> >   
> >     Workgroup            Master  
> >     ---------            -------  
> >     WORKGROUP            SAMBA  
> 
> smbclient //localhost/netlogon -U 'administrator'  
> 
> > Enter administrator's password:  
> > Domain=\[YE\] OS=\[Unix\] Server=\[Samba 4.1.6-Ubuntu\]  
> > smb: \\> ls  
> >   .                                   D        0  Wed Sep  9 21:29:19 2015  
> >   ..                                  D        0  Wed Sep  9 21:29:27 2015  
> >   
> >         60333 blocks of size 131072. 46075 blocks available  

测试DNS  

> host -t SRV \_ldap.\_tcp.ye.org.  
> 
> > \_ldap.\_tcp.ye.org has SRV record 0 100 389 sambadc.ye.org.  
> 
> host -t SRV \_kerberos.\_udp.ye.org.  
> 
> > \_kerberos.\_udp.ye.org has SRV record 0 100 88 sambadc.ye.org.  
> 
> host -t A sambadc.ye.org.  
> 
> > sambadc.ye.org has address 192.168.122.30  
> 
>   

安装Kerberos  

> sudo apt-get install krb5-user  
> kinit administrator  
>     Password for administrator@YE.ORG:  
>     Warning: Your password will expire in 41 days on Wed 21 Oct 2015 09:29:26 PM CST  
> klist  
>     Ticket cache: FILE:/tmp/krb5cc\_1000  
>     Default principal: administrator@YE.ORG  
>   
>     Valid starting       Expires              Service principal  
>     09/09/2015 23:44:49  09/10/2015 09:44:49  krbtgt/YE.ORG@YE.ORG  
>         renew until 09/10/2015 23:44:44  

  
查看SAMBA配置文件  

> samba -b  
> Samba version: 4.1.6-Ubuntu  
> Build environment:  
>    Build host:  Linux lgw01-45 3.19.0-25-generic #26~14.04.1-Ubuntu SMP Fri Jul 24 21:16:20 UTC 2015 i686 i686 i686 GNU/Linux  
> Paths:  
>    BINDIR: /usr/bin  
>    SBINDIR: /usr/sbin  
>    CONFIGFILE: /etc/samba/smb.conf  
>    NCALRPCDIR: /var/run/samba/ncalrpc  
>    LOGFILEBASE: /var/log/samba  
>    LMHOSTSFILE: /etc/samba/lmhosts  
>    DATADIR: /usr/share  
>    MODULESDIR: /usr/lib/i386-linux-gnu/samba  
>    LOCKDIR: /var/run/samba  
>    STATEDIR: /var/lib/samba  
>    CACHEDIR: /var/cache/samba  
>    PIDDIR: /var/run/samba  
>  PRIVATE\_DIR: /var/lib/samba/private  
>    CODEPAGEDIR: /usr/share/samba/codepages  
>    SETUPDIR: /usr/share/samba/setup  
>    WINBINDD\_SOCKET\_DIR: /var/run/samba/winbindd  
>    WINBINDD\_PRIVILEGED\_SOCKET\_DIR: /var/lib/samba/winbindd\_privileged  
>    NTP\_SIGND\_SOCKET\_DIR: /var/lib/samba/ntp\_signd  

  
XP加域  
win2003安装管理工具包  

> http://www.microsoft.com/zh-CN/download/details.aspx?id=6315  

win7安装管理工具包  

> http://www.microsoft.com/zh-CN/download/details.aspx?id=7887  
> https://wiki.samba.org/index.php/Installing\_RSAT  

>