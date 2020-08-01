---
title: ubuntu10.04安装openldap
tags:
  - 未分类
id: '345'
abbrlink: 2209076749
date: 2012-02-24 20:40:00
---

软件：  
1、openssl-1.0.0g.tar.gz  
2、db-4.7.25.tar.gz  (下载了5.2 但又换成4.7了。4.7也折腾了不少时间)  
3、cyrus-sasl-2.1.25.tar.gz  
4、openldap-stable-20100719.tgz  
  
  
安装  
1、安装openssl ：用于SSL/TLS连接  
        ./config shared --openssldir=/usr/local  
        make  
        sudo make install  
     #安装没出现什么问题  
  
2、安装Berkeley DB  
         cd db-4.7.25/build\_unix  
         ../dist/configure  
         make  
         sudo make install  
         sudo  < - page margin cm p margin-bottom cm --> --&lt;cp /usr/local/BerkeleyDB.4.7/include/\* /usr/include  
         sudo cp /usr/local/BerkeleyDB.4.7/lib/\* /usr/lib  
         sudo mv db-4.7.25 /usr/local/src/  
  
3、安装cyrus-sasl ：用于和其他软件整合时认证用(Kerberos)  
      ./configure  
      make  
      sudo make install  
      sudo ln -s /usr/local/lib/sasl2 /usr/lib/sasl2  
  
    make出现问题：  
        make\[2\]: Leaving directory \`/root/postfix/cyrus-sasl-2.1.25/sasldb'  
        make\[1\]: \*\*\* \[all-recursive\] 错误 1  
        make\[1\]: Leaving directory \`/root/postfix/cyrus-sasl-2.1.25'  
  
   解决：  
    在sasldb和utils各添加一个NULL即可  
    参考：  
    [http://www.irbs.net/internet/cyrus-sasl/0301/0042.html](http://www.irbs.net/internet/cyrus-sasl/0301/0042.html)  
    [http://lidiantian.blog.51cto.com/456473/366144](http://lidiantian.blog.51cto.com/456473/366144)  
  
  
4、安装openldap  
       ./configure  
       make depend  
       make  
       make test  
       sudo  make install  
  
     configure就出现问题：  
        configure: error: BDB/HDB: BerkeleyDB not available  
  
     解决：  
      1、sudo su  
           输入一下3个环境变量  
            export LDFLAGS="-L/usr/local/lib -L/usr/local/BerkeleyDB.4.7/lib -R/usr/local/BerkeleyDB.4.7/lib"  
            export CPPFLAGS="-I/usr/local/BerkeleyDB.4.7/include/"  
            export LD\_LIBRARY\_PATH="/usr/local/BerkeleyDB.4.7/lib"  
     2、输入env查看是不是输入的多能看到，多能看到的情况下就可以./configure了  
  
  make depend  和 make 正常  
  make test 检查58个项目，第58个项目错误3个，不知道有没有影响  
  make install 正常  
  
slapd.conf 文件放置在/usr/local/etc/openldap文件夹下  
  
  
实验等，待续。。。  
  
  
参考：  
1、ldap系统管理书 (书不详细)  
2、[源代码方式安装openldap](http://www.linuxso.com/sql/18619.html)  
3、[openldap (1) 基本安装](http://blog.chinaunix.net/space.php?uid=24799710&do=blog&id=3014278)  
4、[http://www.irbs.net/internet/cyrus-sasl/0301/0042.html](http://www.irbs.net/internet/cyrus-sasl/0301/0042.html)  
5、[http://lidiantian.blog.51cto.com/456473/366144](http://lidiantian.blog.51cto.com/456473/366144)