---
title: ubuntu10.04 squid配置
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '157'
abbrlink: 492604514
date: 2011-03-11 11:11:00
---

1、开放防火墙端口

  

2、配置squid.conf

  

acl all src all

acl manager proto cache\_object

acl localhost src 127.0.0.1/32

acl to\_localhost dst 127.0.0.0/8 0.0.0.0/32

acl localnet src 10.0.0.0/8 \# RFC1918 possible internal network

acl localnet src 172.16.0.0/12 \# RFC1918 possible internal network

acl localnet src 192.168.0.0/16 \# RFC1918 possible internal network

acl SSL\_ports port 443 \# https

acl SSL\_ports port 563 \# snews

acl SSL\_ports port 873 \# rsync

acl Safe\_ports port 80 \# http

acl Safe\_ports port 21 \# ftp

acl Safe\_ports port 443 \# https

acl Safe\_ports port 70 \# gopher

acl Safe\_ports port 210 \# wais

acl Safe\_ports port 1025-65535 \# unregistered ports

acl Safe\_ports port 280 \# http-mgmt

acl Safe\_ports port 488 \# gss-http

acl Safe\_ports port 591 \# filemaker

acl Safe\_ports port 777 \# multiling http

acl Safe\_ports port 631 \# cups

acl Safe\_ports port 873 \# rsync

acl Safe\_ports port 901 \# SWAT

acl purge method PURGE

acl CONNECT method CONNECT

  

#abcgc persons-------------------------------

acl jcx arp 00:24:1D:88:58:28

acl brw arp 00:1E:8C:AE:05:77

acl lxx arp 6C:F0:49:A0:0E:89

acl yy  arp 6C:F0:49:78:36:AF

acl hwt arp 00:22:19:06:B8:8B

acl hhb arp 00:24:1D:DE:04:12

acl jzd arp 00:22:19:06:B8:4D

acl js  arp 6C:F0:49:08:92:1C

acl lw  arp 00:07:E9:D9:17:AA

acl pjc arp 00:1A:A0:8F:71:BE

acl zjm arp 6C:F0:49:81:B3:FB

acl chh arp 00:24:1D:88:64:7E

#acl lwm arp

#acl slm arp

acl abc arp 00:1B:FC:2B:F7:C0

  

  

#active ----------------------------------------

acl worktime time M T W H F 7:30-9:30 13:00-15:00

  

#control-------------------------------------------

http\_access allow jcx

http\_access allow hwt

http\_access allow js

http\_access allow lw

http\_access allow zjm

http\_access allow abc

  

http\_access deny !worktime

  

http\_access allow brw

http\_access allow lxx

##http\_access allow yy 

##http\_access allow hhb

http\_access allow jzd

http\_access allow pjc

http\_access allow chh

##http\_access allow lwm

##http\_access allow slm

#http\_access allow abc 

#---------------------------------------------------

  

  

http\_access allow manager localhost

http\_access deny manager

http\_access allow purge localhost

http\_access deny purge

http\_access deny !Safe\_ports

http\_access deny CONNECT !SSL\_ports

http\_access allow localhost

http\_access deny all

icp\_access allow localnet

icp\_access deny all

http\_port 3128

  

#---------------------------------------------

cache\_mem 64 MB

cache\_swap\_low 80

cache\_swap\_high 85

maximum\_object\_size 32768 KB

#maxium\_object\_size\_in\_memory 8KB

cache\_dir ufs /var/spool/squid 4096 64 1024

cache\_effective\_user proxy

cache\_effective\_group proxy

cache\_mgr abc@163.com

#---------------------------------------------

  

hierarchy\_stoplist cgi-bin ?

access\_log /var/log/squid/access.log squid

refresh\_pattern ^ftp: 1440 20% 10080

refresh\_pattern ^gopher: 1440 0% 1440

refresh\_pattern -i (/cgi-bin/|\\?) 0 0% 0

refresh\_pattern (Release|Package(.gz)\*)$ 0 20% 2880

refresh\_pattern . 0 20% 4320

acl shoutcast rep\_header X-HTTP09-First-Line ^ICY.\[0-9\]

upgrade\_http0.9 deny shoutcast

acl apache rep\_header Server ^Apache

broken\_vary\_encoding allow apache

extension\_methods REPORT MERGE MKACTIVITY CHECKOUT

hosts\_file /etc/hosts

coredump\_dir /var/spool/squid

visible\_hostname abcproxy

  

3、改/var/spool/squid的用户名、用户组为proxy