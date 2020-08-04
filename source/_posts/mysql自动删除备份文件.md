---
title: mysql自动删除备份文件
tags:
  - mysql
categories:
  - Database
  - mysql
id: '364'
abbrlink: 1856401235
date: 2013-01-23 16:18:00
---

  

从工具箱中拖入 “执行 T-SQL 语句”任务 到维护计划中

双击 “执行 T-SQL 语句”任务 编辑SQL 执行内容：

  
  
declare @d Nvarchar(64);  
set @d = convert(varchar,dateadd(day,-7,getdate()),120);  
EXECUTE master.dbo.xp\_delete\_file 0,N'E:\\OA数据备份',N'bak',@d;  
EXECUTE master.dbo.xp\_delete\_file 0,N'E:\\OA数据备份',N'bak',@d  
  

![mysql自动删除备份文件 - leaf - ------坚持雅操------](http://img8.ph.126.net/S7Z1OyGH80HwQRN9hkoiBw==/6598124198307828308.jpg "mysql自动删除备份文件 - leaf - ------坚持雅操------")

   
  
  
转载自：http://hi.baidu.com/hiheishuai/item/af0c44af9c76ba17a9cfb741