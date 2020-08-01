---
title: 将桌面文件夹移到D盘
tags:
  - 未分类
id: '96'
abbrlink: 980642546
date: 2010-08-05 08:19:00
---

在正常模式下把桌面改到d盘中去，

具体如下：先在d盘建一个文件夹，

然后点开始---〉运行---〉regedit，

点击HKEY\_CURRENT\_USER--〉Software--〉Microsoft--〉Windows--〉CurrentVersion--〉Explorer--〉user Shell Folders

双击右边的dosktop，弹出一个对话框，

在数据数值里写上你想存到那个文件夹的路径（就是打开文件夹，上面地址栏里的那行字），

确定，关闭。注销系统就ok了。以后桌面上的东西就都在d盘里了