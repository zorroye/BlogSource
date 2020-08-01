---
title: openldap实际操作问题
tags:
  - 未分类
id: '347'
abbrlink: 2816354876
date: 2012-02-26 19:14:00
---

1、 <rootpw> can only be set when rootdn is under suffix  
解决：配置文件slapd.conf里面的：suffix行和rootdn行：里面的dc值    和要导入的ldif里面的dc值对应不起来  
  
参考：[http://apfelboymchen.homeunix.net/gnu/notes/openldap%20config%20backend.html](http://apfelboymchen.homeunix.net/gnu/notes/openldap%20config%20backend.html)  
  
2、ldap\_add: Server is unwilling to perform (53)  
    additional info: no global superior knowledge  
解决：ldif书写错误  
正确格式：  
dn: dc=solar,dc=com  
objectClass: dcObject  
objectClass: organization  
dc: solar  
o: Example Company  
书上是 ou: Example Company，我按书上的来，导致一直出现这种错误  
  
参考：[http://wenku.baidu.com/view/8de4de22482fb4daa58d4bba.html](http://wenku.baidu.com/view/8de4de22482fb4daa58d4bba.html)  
  
3、ldap\_sasl\_bind(SIMPLE): Can't contact LDAP server (-1)  
解决：服务没有开起来：sudo /usr/local/openldap/libexec/slapd start  
  
  
其他参考资料：  
[http://crablfs.sourceforge.net/sysadm\_zh\_CN.html](http://crablfs.sourceforge.net/sysadm_zh_CN.html)  
[http://www.openldap.org/faq/data/cache/1322.html](http://www.openldap.org/faq/data/cache/1322.html)  
[http://apfelboymchen.homeunix.net/gnu/notes/openldap%20config%20backend.html](http://apfelboymchen.homeunix.net/gnu/notes/openldap%20config%20backend.html)  
  
  
继续内容：  
1、objectclass的作用，  
2、ldapadd的命令的熟悉  
3、ldif的格式