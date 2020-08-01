---
title: 【转载】win2012安装sql server 2005
tags:
  - 未分类
id: '359'
abbrlink: 946913595
date: 2016-03-20 18:38:00
---

http://wenku.baidu.com/link?url=vKN0NLKyKOFX9R-di\_Co\_ilHg1VOP7siN731YSQ0WR0Vp7lWIrx3cbaqUS05MtAhG6jTC-RcVicNldy4wTgxJL2NxhLpP01FXqUBVh4nici

  

http://tech.powereasy.net/Item.aspx?id=3681

  

0、先安装.net framework 3.0 和IIS6全部勾选安装

  

1、正常安装任一版本的SQL Server 2005.

  

2、安装到SqlServer服务的时候提示启动服务失败，这里就是关键啦，

下载本文的两个附件,里面是SP4（2005.90.5000.0）版本的sqlservr.exe和sqlos.dll。

32位下载sqlservr32.rar，64位下载sqlservr64.rar。

sqlservr32

sqlservr64

  

3、你的<SQL Server 2005安装路径>\\binn，先备份下sqlservr.exe，

然后把解压之后对应的 sqlservr.exe和sqlos.dll复制到里面覆盖原文件，

例如“C:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Binn”。

  

4、点击“重试”，安装继续，安装程序安装成功。

  

5、安装完成之后，停止SQL Server服务，把备份的sqlservr.exe文件还原回去

（否则SP4安装程序以为你已经应用过SP4补丁），然后立即打上SP4补丁。

（在此之前不要运行SQL任何软件）

  

6、安装完SP4补丁，SQL Server运行正常，教程完成。