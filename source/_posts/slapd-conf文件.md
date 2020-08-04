---
title: slapd.conf文件
tags:
  - ldap
categories:
  - Services
  - ldap
id: '346'
abbrlink: 3091646095
date: 2012-02-25 08:40:00
---

#  
\# See slapd.conf(5) for details on configuration options.  
\# This file should NOT be world readable.  
#  
include        /usr/local/etc/openldap/schema/core.schema   
#属性类型多放着这个文件下，包括类型定义，OID，等等  
  
\# Define global ACLs to disable default read access.  
  
\# Do not enable referrals until AFTER you have a working directory  
\# service AND an understanding of referrals.  
#referral    ldap://root.openldap.org  
  
pidfile        /usr/local/var/run/slapd.pid      #记录正在执行的slapd进程ID  
argsfile    /usr/local/var/run/slapd.args      #记录正在执行的slapd命令行参数  
  
\# Load dynamic backend modules:  
\# modulepath    /usr/local/libexec/openldap  
\# moduleload    back\_bdb.la  
\# moduleload    back\_hdb.la  
\# moduleload    back\_ldap.la  
  
#---------------------SASL选线--------------------------#  
#sasl-host              认证dn  
#sasl-realm            认证domain  
#sasl-secprops      设置安全性  
  
  
#--------------------SSL/TLS选项----------------------#  
#TLSCipherSuite            定义接受哪些加密法  
#TLSCertficateFile         存放公钥地址  
#TLSCertificateKeyFile  存放密钥地址  
  
  
\# Sample security restrictions  
#    Require integrity protection (prevent hijacking)  
#    Require 112-bit (3DES or better) encryption for updates  
#    Require 63-bit encryption for simple bind  
\# security ssf=1 update\_ssf=112 simple\_bind=64  
  
\# Sample access control policy:  
#    Root DSE: allow anyone to read it  
#    Subschema (sub)entry DSE: allow anyone to read it  
#    Other DSEs:  
#        Allow self write access  
#        Allow authenticated users read access  
#        Allow anonymous users to authenticate  
#    Directives needed to implement policy:  
\# access to dn.base="" by \* read  
\# access to dn.base="cn=Subschema" by \* read  
\# access to \*  
#    by self write  
#    by users read  
#    by anonymous auth  
  
#-----------------ACL设定------------------------  
#access to dn.base="cn=Subschema" by \* read   一个access一个设定  
#dn.base="cn=Subschema"                                  针对的项目  
#by \* read                                                             设置存取权限。\* 表示所有人，read是权限  
#                                                                           以上表示对某个项目，所有人多有读取权限  
#注意access的先后次序  
  
#  
\# if no access controls are present, the default policy  
\# allows anyone and everyone to read anything but restricts  
\# updates to rootdn.  (e.g., "access to \* by \* read")  
#  
\# rootdn can always read and write EVERYTHING!  
  
#######################################################################  
\# BDB database definitions  
#######################################################################  
  
database    bdb                                          #定义使用的数据库  
suffix        "dc=my-domain,dc=com"                              #定义根DN名称  
rootdn        "cn=Manager,dc=my-domain,dc=com"       #定义ldap的root账户，当前账户为：Manager  
\# Cleartext passwords, especially for the rootdn, should  
\# be avoid.  See slappasswd(8) and slapd.conf(5) for details.  
\# Use of strong authentication encouraged.  
  
rootpw       {SSHA}VkcVbrkqa6jqf7GiaQD8bXNglap2qy4a  
#rootpw的默认密码为secret  
#此处用{SSHA}进行了加密  
\# 加密方法： sudo slappasswd -h {SSHA}        然后把编码复制到配置文件中即可  
#此处参考：[http://www.php-oa.com/2007/10/17/openldap.html](http://www.php-oa.com/2007/10/17/openldap.html)   
                
 #定义ldap的root账户的密码：当前密码为明文 secret  
#密文的话密码前面会有提示：{MD5}wenwjker  
#rootpw可以不设置，使用全局设置(上面的)的认证方法来认证  
#rootdn则要改为：rootdn "uid=xxxxx,cn=xxxx,cn=auth"  
  
  
\# The database directory MUST exist prior to running slapd AND  
\# should only be accessible by the slapd and slap tools.  
\# Mode 700 recommended.  
  
directory    /usr/local/var/openldap-data               #定义leap数据的存放地点  
#mode 0600                                                         #定义数据存取权限  
\# Indices to maintain  
index    objectClass    eq                                      #定义索引，eq表示搜索内容要完全一直才能搜索到  
#cachesize  2000                                                 #定义存放在内存中的项目数