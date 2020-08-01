---
title: buffalo nas 设置web服务器
tags:
  - 未分类
id: '170'
date: 2014-02-05 16:31:00
---

1、新建文件夹：

ph/leaf

ph/data

  

2、进管理界面开启web和mysql服务，并选择相关文件夹

web 选ph/leaf ，端口设置8080

mysql 选ph/data

这时：

ph/leaf下多出htdocs文件夹

ph/data下多出相关文件

  

3、点打开phpmyadmin，账号：admin 密码 password 进入

添加数据库：leaf

添加管理该数据库的账号密码

  

4、下载wordpress，解压放入 ph/leaf/htdocs/ 下

  

5、浏览器打开 192.168.3.6：8080/wp-admin/install.php 配置一下即可

  

搞定

![buffalo nas 设置web服务器 - leaf - ------坚持雅操------](http://img2.ph.126.net/-_hee80LfIuYEbJKKWuRHA==/57139420372759511.png "buffalo nas 设置web服务器 - leaf - ------坚持雅操------")