---
title: MYSQL：1基础
tags:
  - mysql
categories:
  - Database
  - mysql
id: '363'
abbrlink: 3997419446
date: 2012-11-29 14:12:00
---

数据库技术：  

> 数据库系统  
> 
> > 数据库  
> > 数据库管理系统  
> > 应用系统：使用数据库的软件  
> > 应用开发工具  
> > 数据库管理员  
> 
> SQL语言  
> 
> > DDL：对数据库和表的操作  
> > DML：对数据的操作  
> > DCL：控制访问权限  
> 
> 数据库访问技术  
> 
> > ODBC  
> > JDBC  
> > ADO.NET  
> > mysql模块和mysql接口  
> > 只有使用访问技术，sql语言才能起作用。  

  
MYSQL数据类型：  

> 整数类型  
> 
> > tinyint                 1B  
> > smallint               2B  
> > mediumint          3B  
> > int                       4B  
> > inteage               4B  
> > bigint                  8B  
> > #有符号数就是把一个字节中的最前面的数当符号使用，这样能表示的最大值就少了1半。  
> >   
> 
> 浮点数、定点数类型  
> 
> > float                   4B  
> > double               8B  
> > decimal(M+D)   M+2     #M是整数部分的长度，D是小数点部分的长度。  
> > 
> > > > > >   #定点数默认M=10，D=0，  
> > > > > >   #定点数使用字符串形式存储。数据精度高。  
> > 
> >   
> 
> 日期、时间类型  
> 
> > year                 1B         #4位范围：1901-2155   #2位字符串：2000-2069，1970-1999  
> > 
> > > > > >   #2位数字：0000，2001-2069，1970-1999  
> > 
> > date                 4B          
> > time                 3B  
> > datetime          8B  
> > timestamp       4B  
> > #NOW()可以显示当前时间  
> 
> 字符串类型  
> 
> > char  
> > varchar  
> > text                             #用于存字符数据  
> > enum  
> > set  
> 
> 二进制类型