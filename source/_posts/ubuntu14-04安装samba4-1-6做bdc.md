---
title: UBUNTU14.04安装SAMBA4.1.6做BDC
tags:
  - 未分类
id: '333'
date: 2015-09-11 14:01:00
---

参考：  
https://wiki.samba.org/index.php/Samba4/HOWTO/Join\_a\_domain\_as\_a\_DC  
https://wiki.samba.org/index.php/Check\_and\_fix\_DNS\_entries\_on\_DC\_joins  
  
环境：  

> 服务器OS1：UBUNTU14.04  
> 服务器主机名：sambadc  
> 域：ye.org  
> 完整名字：sambadc.ye.org  
> NETBIOS名：YE  
> 域控管理员密码：Password0  
> 服务器IP：192.168.122.30  
> 网关：192.168.122.1  
>   
> 服务器OS2：UBUNTU14.04  
> 服务器主机名：sambabdc  
> 域：ye.org  
> 完整名字：sambabdc.ye.org  
> NETBIOS名：YE  
> 域控管理员密码：Password0  
> 服务器IP：192.168.122.31  
> 网关：192.168.122.1  
>   

服务器OS2及IP地址设置  

> cat /etc/hostname  
> 
> > sambabdc.ye.org  
> 
> cat /etc/hosts  
> 
> > 127.0.0.1       localhost.localdomain    localhost  
> > 192.168.122.31    sambabdc.ye.org    sambabdc  
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
> 
> >     address 192.168.122.31  
> 
> >     netmask 255.255.255.0  
> >     gateway 192.168.122.1  
> >     dns-nameservers 192.168.122.30  
> >     dns-search ye.org  
> 
> sudo reboot  

> 测试dns设置：host -t -A sambadc.ye.org  

  
安装samba  

> sudo apt-get install samba smbclient python-dev  
>   

安装Kerberos  

> sudo apt-get install krb5-user  
> sudo nano /etc/krb5.conf  
> 
> > \[libdefaults\]  
> >     dns\_lookup\_realm = false  
> >     dns\_lookup\_kdc = true  
> >     default\_realm = YE.ORG  
> 
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

>   

加入域  

> sudo su  
> mv /etc/samba/smb.conf /etc/samba/smb.conf-orig  
> samba-tool domain join ye.org DC -Uadministrator --realm=ye.org --dns-backend=SAMBA\_INTERNAL  

>   

检查DNS条目  

> 加host记录  
> 测试：  
> host -t -A sambabdc.ye.org.  
> 
> > 会出现 Host sambabdc.ye.org. not found: 3(NXDOMAIN) 之类的提示  

> 加入：  
> samba-tool dns add SAMBADC ye.org SAMBABDC A 192.168.122.31 -Uadministrator  
> 
> > Password for \[SAMDOM\\administrator\]: Password0  
> > Record added successfully  
> 
>   
> 加CNAME记录  
> sudo su  
> ldbsearch -H /var/lib/samba/private/sam.ldb '(invocationId=\*)' --cross-ncs objectguid  
> 
> > \# record 1  
> > dn: CN=NTDS Settings,CN=SAMBABDC,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=ye,DC=org  
> > objectGUID: 619eabd6-9d28-42d1-8a2f-d11ffacfa948  
> >   
> > \# record 2  
> > dn: CN=NTDS Settings,CN=SAMBADC,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=ye,DC=org  
> > objectGUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
> >   
> > \# returned 2 records  
> > \# 2 entries  
> > \# 0 referrals  
> >   
> 
> 测试：  
> host -t CNAME 619eabd6-9d28-42d1-8a2f-d11ffacfa948.\_msdcs.ye.org.  
> 
> > Host 619eabd6-9d28-42d1-8a2f-d11ffacfa948.\_msdcs.ye.org. not found: 3(NXDOMAIN)  
> 
> 加入：  
> samba-tool dns add SAMBADC \_msdcs.ye.org 619eabd6-9d28-42d1-8a2f-d11ffacfa948 CNAME SAMBABDC.ye.org -Uadministrator  
> 
> > Password for \[SAMDOM\\administrator\]: passw0rd  
> > Record added successfully  
> 
>   

目录复制  
samba-tool drs showrepl  

> Default-First-Site-Name\\SAMBABDC  
> DSA Options: 0x00000001  
> DSA object GUID: 619eabd6-9d28-42d1-8a2f-d11ffacfa948  
> DSA invocationId: 5d417388-c68d-4784-8aa4-167c9a40a5b4  
>   
> \==== INBOUND NEIGHBORS ====  
>   
> DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ Fri Sep 11 11:41:05 2015 CST was successful  
>         0 consecutive failure(s).  
>         Last success @ Fri Sep 11 11:41:05 2015 CST  
>   
> CN=Configuration,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ Fri Sep 11 11:41:06 2015 CST was successful  
>         0 consecutive failure(s).  
>         Last success @ Fri Sep 11 11:41:06 2015 CST  
>   
> DC=ForestDnsZones,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ Fri Sep 11 11:41:05 2015 CST was successful  
>         0 consecutive failure(s).  
>         Last success @ Fri Sep 11 11:41:05 2015 CST  
>   
> CN=Schema,CN=Configuration,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ Fri Sep 11 11:41:06 2015 CST was successful  
>         0 consecutive failure(s).  
>         Last success @ Fri Sep 11 11:41:06 2015 CST  
>   
> DC=DomainDnsZones,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ Fri Sep 11 11:41:05 2015 CST was successful  
>         0 consecutive failure(s).  
>         Last success @ Fri Sep 11 11:41:05 2015 CST  
>   
> \==== OUTBOUND NEIGHBORS ====  
>   
> DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ NTTIME(0) was successful  
>         0 consecutive failure(s).  
>         Last success @ NTTIME(0)  
>   
> CN=Configuration,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ NTTIME(0) was successful  
>         0 consecutive failure(s).  
>         Last success @ NTTIME(0)  
>   
> DC=ForestDnsZones,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ NTTIME(0) was successful  
>         0 consecutive failure(s).  
>         Last success @ NTTIME(0)  
>   
> CN=Schema,CN=Configuration,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ NTTIME(0) was successful  
>         0 consecutive failure(s).  
>         Last success @ NTTIME(0)  
>   
> DC=DomainDnsZones,DC=ye,DC=org  
>     Default-First-Site-Name\\SAMBADC via RPC  
>         DSA object GUID: f2de8425-5a1d-4e27-92ea-705b1039bbe6  
>         Last attempt @ NTTIME(0) was successful  
>         0 consecutive failure(s).  
>         Last success @ NTTIME(0)  
>   
> \==== KCC CONNECTION OBJECTS ====  
>   
> Connection --  
>     Connection name: 435389c9-22f8-4ae0-aa1b-046cc684cb40  
>     Enabled        : TRUE  
>     Server DNS name : sambadc.ye.org  
>     Server DN name  : CN=NTDS Settings,CN=SAMBADC,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=ye,DC=org  
>         TransportType: RPC  
>         options: 0x00000001  
> Warning: No NC replicated for Connection!  
>   

更新DNS设置  

> /etc/network/interfaces on SAMBABDC  
> nameserver 192.168.122.30  
> nameserver 127.0.0.1  
> search ye.org  
>    
> /etc/network/interfaces on SAMBADC  
> nameserver 192.168.122.31  
> nameserver 127.0.0.1  
> search ye.org  
>   

域控管理  

> ![UBUNTU14.04安装SAMBA4.1.6做BDC - leaf - ------勤解万难------](http://img0.ph.126.net/T_xbdZhdBzvw-2Axls3mqw==/6630082603281836382.png "UBUNTU14.04安装SAMBA4.1.6做BDC - leaf - ------勤解万难------")
> 
>    
> 
> ![UBUNTU14.04安装SAMBA4.1.6做BDC - leaf - ------勤解万难------](http://img1.ph.126.net/DYmimScDudNxu-HMHgLnzA==/6619451425352315557.png "UBUNTU14.04安装SAMBA4.1.6做BDC - leaf - ------勤解万难------")
> 
>