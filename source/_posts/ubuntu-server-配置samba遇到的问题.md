---
title: ubuntu server 配置samba遇到的问题
tags:
  - samba
categories:
  - Services
  - samba
id: '330'
abbrlink: 4091169391
date: 2010-09-24 17:16:00
---

1、开放了防火墙  
2、samba服务开着的  
3、smb.conf都对的，放到桌面上能用  
4、文件夹权限也都对的  
  
百思不得其解，最后还是权限出了问题  
  
安装ubuntu server的时候选择了“加密用户目录“，导致用户目录里的资料都不能共享，即使共享了别人也访问不了