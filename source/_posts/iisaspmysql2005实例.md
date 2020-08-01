---
title: IIS+asp+mysql2005实例
tags:
  - 未分类
id: '155'
abbrlink: 2377210841
date: 2011-01-03 08:49:00
---

网页---IIS----------asp---mysql2005  
IIS的作用：生成页面  
asp的作用：在IIS和mysql之间传输数据  
mysql的作用：存储数据  
  
0、安装 [framwork2.0](http://download.microsoft.com/download/5/6/7/567758a3-759e-473e-bf8f-52154438565a/dotnetfx.exe) 和[framwork4.0](http://download.microsoft.com/download/1/B/E/1BE39E79-7E39-46A3-96FF-047F95396215/dotNetFx40_Full_setup.exe)  
1、安装[IIS for winxp](http://lib.ldsoft.cc/download/iis_setup_xp.rar) ([for win2003](http://lib.ldsoft.cc/download/iis_setup_2003.rar) [for win2008](http://ldsoft.cc/download/iis7_setup.rar))  
      1、解压，然后用windows的添加/删除程序装，再运行bat文件即可  
      2、iis相关配置查看安装说明  
      3、安装好后跳出HTTP 500，  打开IE-菜单--工具--Internet选项--高级--去掉钩显示友好的HTTP错误信息  
            显示The specified module could not be found 解决方法见[http://www.mycodes.net/78/2387.htm](http://www.mycodes.net/78/2387.htm)  
2、安装SQL2005企业版  
     1、配置看说明书  
     2、提示 MMC检测到此管理单元发生一个错误。建议关闭并重新启动MMC  
          要安装SQLServer2005SP3-KB955706-x86-CHS.exe  
  
待续。。。