---
title: gpg使用说明
tags:
  - 未分类
id: '206'
abbrlink: 841776280
date: 2011-03-19 14:46:00
---

转载自：[http://www.alexgao.com/2009/01/24/gpg/](http://www.alexgao.com/2009/01/24/gpg/)  
  

**第一部分：生成、传播、作废**

**1、生成密钥对：**

 **gpg --gen-key**

 **信息：solar (solar000)  solar123@solar.com**

 **密钥ID：538E9DA1** 

**2、上传下载公钥：(给别人用)**

 **gpg --keyserver hkp://keys.gnupg.net --send-keys 538E9DA1   #上传**

  ****gpg --keyserver** hkp://keys.gnupg.net --recv** **538E9DA1              #下载**

**3、生成公钥回收证书： (用于作废密钥)**

 **1、生成回收证书：    gpg --output revoke.asc --gen-revoke 538E9DA1**

 **2、上传到服务器上：gpg --keyserver hkp://keys.gnupg.net --send-keys 538E9DA1** 

**第二部分：导入导出**

**1、导出公钥：gpg -o solar-pubkey --export 538E9DA1**

**2、导出私钥：gpg -o solar-subkey --export-secret-keys 538E9DA1**

**3、使用人导入公钥：gpg --import solar-pubkey**

**4、查看是否已经导入公钥：gpg --list-keys**

**第三部分：加密解密**

**1、加密： gpg -o test.gpg -er solar test**

**2、解密：gpg -o test -d test.gpg**

**3、签名+加密：gpg -o test.sig -ser solar test**

**4、待续。。**

**对称加解密：**

**加密：gpg -o test.gpg -c test**

**解密：gpg -o test -d test.gpg**

**第四部分：删除密钥**

**0、作废公钥：gpg --keyserver hkp://keys.gnupg.net --send-keys** **538E9DA1**

**1、删除私钥：gpg --delete-secret-keys solar123@solar.com**

**2、删除公钥：gpg --delete-keys solar123@solar.com**