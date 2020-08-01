---
title: 'BLFS-1:补充软件'
tags:
  - 未分类
id: '233'
abbrlink: 768145412
date: 2012-10-26 12:55:00
---

  
没有wget，下载很不方便，没有openssh，所有代码都要自己输很不方便，所以安装  
1、wget  

> cd /root/sources  
> ftp ftp.gnu.org  
> 
> > 用户名：anonymous  
> 
> > cd gnu  
> > cd wget  
> > get wget-1.11.1.tar.bz2  
> 
> bye  
> cd ../build  
> tar -xvf ../sources/wget-1.11.1.tar.bz2  
> cd wget-1.11.1  
> 
> > ./configure --prefix=/usr --sysconfdir=/etc  
> > make && make install  
> 
> cd ..  
>   

2、gdbm  

> 按孙海勇的书装了这个。  

> wget ftp://ftp.gnu.org/gnu/gdbm/gdbm-1.8.3.tar.gz  
> vi /etc/passwd  
> 
> > bin:x:2:2:bin:/bin:/bin/sh  
> 
> ./configure --prefix=/usr  
> make && make install  
> make install-compat  
>   

3、openssl  

> wget http://www.openssl.org/source/openssl-0.9.8l.tar.gz  
> wget http://www.linuxfromscratch.org/patches/downloads/openssl/openssl-0.9.8l-fix\_manpages-1.patch  

> ./config --prefix=/usr \\  
> 
> > \--openssldir=/etc/ssl shared zlib-dynamic  
> 
> make  
> make test  
> make MANDIR=/usr/share/man install  
> install -v -d -m755 /usr/share/doc/openssl-0.9.8l  
> cp -v -r doc/{HOWTO,README,\*.{txt,html,gif}} /usr/share/doc/openssl-0.9.8l  
>   

4、openssh  

> 安装  
> openssh需要openssl和  

> wget http://ftp.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh-5.3p1.tar.gz    #要大写  
> install -v -m700 -d /var/lib/sshd  
> chown -v root:sys /var/lib/sshd  
> groupadd -g 50 sshd  
> useradd -c ‘sshd PrivSep’ -d /var/lib/sshd -g sshd \\  
> 
> > \-s /bin/false -u 50 sshd  
> 
> sed -i.orig 's@-lcrypto@/usr/lib/libcrypto.a -ldl@' configure  
> ./configure --prefix=/usr --sysconfdir=/etc/ssh \\  
> 
> > \--datadir=/usr/share/sshd \\  
> > \--libexecdir=/usr/lib/openssh --with-md5-passwords \\  
> > \--with-privsep-path=/var/lib/sshd  
> 
> make  
> make install  
> install -v -m755 -d /usr/share/doc/openssh-5.3p1  
> install -v -m644 INSTALL LICENCE OVERVIEW README\* WARNING.RNG /usr/share/doc/openssh-5.3p1  
> 配置  
> 从livedcd里面拷过来就好了  
> 从livedcd启动，位置：/etc/rc.d/init.d/sshd  
> 添加系统启动自启动  
> cd /etc/rc.d/init.d &&  
> ln -sf ../init.d/sshd ../rc0.d/K30sshd &&  
> ln -sf ../init.d/sshd ../rc1.d/K30sshd &&  
> ln -sf ../init.d/sshd ../rc2.d/K30sshd &&  
> ln -sf ../init.d/sshd ../rc3.d/S30sshd &&  
> ln -sf ../init.d/sshd ../rc4.d/S30sshd &&  
> ln -sf ../init.d/sshd ../rc5.d/S30sshd &&  
> ln -sf ../init.d/sshd ../rc6.d/K30sshd  

  

![BLFS-1:安装wget、ssh等软件 - leaf - ------坚持雅操------](http://img9.ph.126.net/3LjXwKiwwVW1LWjdc4IFZg==/1647754513681411459.jpg "BLFS-1:安装wget、ssh等软件 - leaf - ------坚持雅操------")