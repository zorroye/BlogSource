---
title: '学习ldap:2安装openldap'
tags:
  - 未分类
id: '350'
date: 2013-02-25 16:40:00
---

安装：openssl+berkeleydb+sasl+mit kerberos+openldap  
参考：http://www.linuxfromscratch.org/blfs/view/svn/index.html  
  
1、openssl  
http://www.openssl.org/source/openssl-1.0.1c.tar.gz  
http://www.linuxfromscratch.org/patches/blfs/svn/openssl-1.0.1c-fix\_manpages-1.patch  

>   
> patch -Np1 -i ../openssl-1.0.1c-fix\_manpages-1.patch  
> ./config  shared  
> make  
> make  install  
>   
>   

2、BerkeleyDB  
http://download.oracle.com/berkeley-db/db-5.3.21.tar.gz  

> cd build\_unix                        ../dist/configure  
> make  
> make  install  
> ln -v -sf  /usr/local/BerkeleyDB.5.3/include/\* /usr/include  
> ln -v -sf  /usr/local/BerkeleyDB.5.3/lib/\*     /usr/lib  

  
3、Cyrus SASL  
http://ftp.andrew.cmu.edu/pub/cyrus-mail/cyrus-sasl-2.1.25.tar.gz  
http://www.linuxfromscratch.org/patches/blfs/svn/cyrus-sasl-2.1.25-fixes-1.patch  

>   
> patch -Np1 -i ../cyrus-sasl-2.1.25-fixes-1.patch  
> ./configure  
> make  
> make install  
> ln -s /usr/local/lib/sasl2 /usr/lib/sasl2  
>   
>   

4、mit kerberos  
http://web.mit.edu/kerberos/www/dist/krb5/1.11/krb5-1.11-signed.tar  
  

> cd src  

> ./configure  --prefix=/usr  --localstatedir=/var/lib    --enable-dns-for-realm  
> make  
> make install  
> for LIBRARY in gssapi\_krb5 gssrpc k5crypto kadm5clnt\_mit kadm5srv\_mit \\  
>                kdb5 krb5 krb5support verto ; do  
>     chmod -v 755 /usr/lib/lib$LIBRARY.so.\*.\*  
> done &&  
> mv -v /usr/lib/libkrb5.so.3\*        /lib &&  
> mv -v /usr/lib/libk5crypto.so.3\*    /lib &&  
> mv -v /usr/lib/libkrb5support.so.0\* /lib &&  
> ln -v -sf ../../lib/libkrb5.so.3.3        /usr/lib/libkrb5.so        &&  
> ln -v -sf ../../lib/libk5crypto.so.3.1    /usr/lib/libk5crypto.so    &&  
> ln -v -sf ../../lib/libkrb5support.so.0.1 /usr/lib/libkrb5support.so &&  
> mv -v /usr/bin/ksu /bin &&  
> chmod -v 755 /bin/ksu   &&  
> install -v -dm755 /usr/share/doc/krb5-1.11 &&  
> cp -vfr ../doc/\*  /usr/share/doc/krb5-1.11 &&  
> unset LIBRARY  

  
  
5、openldap  
ftp://ftp.openldap.org/pub/OpenLDAP/openldap-release/openldap-2.4.33.tgz  
http://www.linuxfromscratch.org/patches/blfs/svn/openldap-2.4.33-blfs\_paths-1.patch  
http://www.linuxfromscratch.org/patches/blfs/svn/openldap-2.4.33-symbol\_versions-1.patch  
http://www.linuxfromscratch.org/patches/blfs/svn/openldap-2.4.33-ntlm-1.patch  

>   
> patch -Np1 -i ../openldap-2.4.33-ntlm-1.patch  
> patch -Np1 -i ../openldap-2.4.33-blfs\_paths-1.patch  
> patch -Np1 -i ../openldap-2.4.33-symbol\_versions-1.patch  
> autoconf  
> ./configure \\  
> 
> > \--with-tls=openssl \\  
> > \--enable-spasswd \\  
> > \--disable-static \\  
> > \--disable-debug \\  
> > \--enable-dynamic \\  
> > \--enable-crypt \\  
> > \--enable-modules \\  
> > \--enable-rlookups \\  
> > \--enable-backends=mod \\  
> > \--enable-overlays=mod \\  
> > \--disable-ndb \\  
> > \--disable-sql  
> 
> make depend    #config结束后会提示这一步操作  
> make test          #全部通过  
> make  
> make install  
>   
>