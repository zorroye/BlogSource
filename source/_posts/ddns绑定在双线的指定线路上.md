---
title: ddns绑定在双线的指定线路上
tags:
  - huawei
categories:
  - Network
  - huawei
id: '324'
abbrlink: 2104355930
date: 2017-01-20 09:06:00
---

需求：

1、拉了一根电信20M pppoe拨号宽带和一根移动50M 静态IP。  

      双线接入后DDNS自动绑定在了移动IP上了，需要将DDNS解析到电信IP上面

2、用的DDNS是3322的，DNS服务器IP是members.3322.org和www.3322.org

  

华为路由策略

acl name acl-dxddns 3500

rule permit ip destination  118.184.176.13 0

rule permit ip destination  118.184.176.15 0

  

policy-based-route dxddns permit node 10

if-match acl 3500

apply output-interface Dialer 1

quit

  

ip local policy-based-route dxddns