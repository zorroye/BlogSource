---
title: ubuntu10.04加入到win2003域 相关配置文件
tags:
  - 未分类
id: '208'
date: 2011-05-17 10:06:00
---

/etc/hosts:127.0.0.1 ywz.leaf.com ywz localhost

  

/etc/krb5.conf

\[libdefaults\]

default\_realm = LEAF.COM

  

\# The following krb5.conf variables are only for MIT Kerberos.

krb4\_config = /etc/krb.conf

krb4\_realms = /etc/krb.realms

kdc\_timesync = 1

ccache\_type = 4

forwardable = true

proxiable = true

  

\# The following encryption type specification will be used by MIT Kerberos

\# if uncommented.  In general, the defaults in the MIT Kerberos code are

\# correct and overriding these specifications only serves to disable new

\# encryption types as they are added, creating interoperability problems.

#

\# Thie only time when you might need to uncomment these lines and change

\# the enctypes is if you have local software that will break on ticket

\# caches containing ticket encryption types it doesn't know about (such as

\# old versions of Sun Java).

  

# default\_tgs\_enctypes = des3-hmac-sha1

# default\_tkt\_enctypes = des3-hmac-sha1

# permitted\_enctypes = des3-hmac-sha1

  

\# The following libdefaults parameters are only for Heimdal Kerberos.

v4\_instance\_resolve = false

v4\_name\_convert = {

host = {

rcmd = host

ftp = ftp

}

plain = {

something = something-else

}

}

fcc-mit-ticketflags = true

default\_tgs\_enctypes = RC4-HMAC DES-CBC-MD5 DES-CBC-CRC

default\_tkt\_enctypes = RC4-HMAC DES-CBC-MD5 DES-CBC-CRC

preferred\_enctypes = RC4-HMAC DES-CBC-MD5 DES-CBC-CRC

dns\_lookup\_kdc = true

  

\[realms\]

ATHENA.MIT.EDU = {

kdc = kerberos.mit.edu:88

kdc = kerberos-1.mit.edu:88

kdc = kerberos-2.mit.edu:88

admin\_server = kerberos.mit.edu

default\_domain = mit.edu

}

MEDIA-LAB.MIT.EDU = {

kdc = kerberos.media.mit.edu

admin\_server = kerberos.media.mit.edu

}

ZONE.MIT.EDU = {

kdc = casio.mit.edu

kdc = seiko.mit.edu

admin\_server = casio.mit.edu

}

MOOF.MIT.EDU = {

kdc = three-headed-dogcow.mit.edu:88

kdc = three-headed-dogcow-1.mit.edu:88

admin\_server = three-headed-dogcow.mit.edu

}

CSAIL.MIT.EDU = {

kdc = kerberos-1.csail.mit.edu

kdc = kerberos-2.csail.mit.edu

admin\_server = kerberos.csail.mit.edu

default\_domain = csail.mit.edu

krb524\_server = krb524.csail.mit.edu

}

IHTFP.ORG = {

kdc = kerberos.ihtfp.org

admin\_server = kerberos.ihtfp.org

}

GNU.ORG = {

kdc = kerberos.gnu.org

kdc = kerberos-2.gnu.org

kdc = kerberos-3.gnu.org

admin\_server = kerberos.gnu.org

}

1TS.ORG = {

kdc = kerberos.1ts.org

admin\_server = kerberos.1ts.org

}

GRATUITOUS.ORG = {

kdc = kerberos.gratuitous.org

admin\_server = kerberos.gratuitous.org

}

DOOMCOM.ORG = {

kdc = kerberos.doomcom.org

admin\_server = kerberos.doomcom.org

}

ANDREW.CMU.EDU = {

kdc = vice28.fs.andrew.cmu.edu

kdc = vice2.fs.andrew.cmu.edu

kdc = vice11.fs.andrew.cmu.edu

kdc = vice12.fs.andrew.cmu.edu

admin\_server = vice28.fs.andrew.cmu.edu

default\_domain = andrew.cmu.edu

}

CS.CMU.EDU = {

kdc = kerberos.cs.cmu.edu

kdc = kerberos-2.srv.cs.cmu.edu

admin\_server = kerberos.cs.cmu.edu

}

DEMENTIA.ORG = {

kdc = kerberos.dementia.org

kdc = kerberos2.dementia.org

admin\_server = kerberos.dementia.org

}

stanford.edu = {

kdc = krb5auth1.stanford.edu

kdc = krb5auth2.stanford.edu

kdc = krb5auth3.stanford.edu

master\_kdc = krb5auth1.stanford.edu

admin\_server = krb5-admin.stanford.edu

default\_domain = stanford.edu

}

LEAF.COM = {

auth\_to\_local = RULE:\[1:$0\\$1\](^LEAF\\.COM\\\\.\*)s/^LEAF\\.COM/LEAF/

auth\_to\_local = RULE:\[1:$0\\$1\](^LEAF\\.COM\\\\.\*)s/^LEAF\\.COM/LEAF/

auth\_to\_local = DEFAULT

}

  

\[domain\_realm\]

.mit.edu = ATHENA.MIT.EDU

mit.edu = ATHENA.MIT.EDU

.media.mit.edu = MEDIA-LAB.MIT.EDU

media.mit.edu = MEDIA-LAB.MIT.EDU

.csail.mit.edu = CSAIL.MIT.EDU

csail.mit.edu = CSAIL.MIT.EDU

.whoi.edu = ATHENA.MIT.EDU

whoi.edu = ATHENA.MIT.EDU

.stanford.edu = stanford.edu

.slac.stanford.edu = SLAC.STANFORD.EDU

.LEAF.com = LEAF.COM

  

\[login\]

krb4\_convert = true

krb4\_get\_tickets = false

\[appdefaults\]

pam = {

   mappings = LEAF\\\\(.\*) $1@LEAF.COM

   forwardable = true

   validate = true

}

httpd = {

   mappings = LEAF\\\\(.\*) $1@LEAF.COM

   reverse\_mappings = (.\*)@LEAF\\.COM LEAF\\$1

}