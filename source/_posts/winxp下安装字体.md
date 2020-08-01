---
title: winxp下安装字体
tags:
  - 未分类
id: '105'
date: 2012-06-14 14:37:00
---

系统原先是win7，后来装了winxp。  
重装之前把win7的字体全部复制出来了 ，然后装好后进winpe把字体复制回去了，  
结果复制进去的字体一个多找不到  
  
解决方法：  
http://wenku.baidu.com/view/9772b5c18bd63186bcebbcb9.html  
  
1、cmd下输入 attrib +s +c c:\\windows\\fonts  
  
2、c:\\windows\\fonts\\desktop.ini下写入  
\[.ShellClassInfo\]  
UICLSID ={BD84B380 -8CA2 -1069 -ABID -08000948F534}  
  
  
里面的第三种是文件被病毒破坏  
c:\\windows\\system32\\fontext.dll