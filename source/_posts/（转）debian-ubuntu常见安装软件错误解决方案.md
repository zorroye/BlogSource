---
title: （转）Debian/Ubuntu常见安装软件错误解决方案
tags:
  - 未分类
id: '205'
abbrlink: 2441145418
date: 2011-02-13 16:47:00
---

1、错误： Can't find X includes. Please check your installation and add the correct paths!  
原因：没有X的包含文件  
解决：安装xlibs-dev即可  
  
2、错误： Qt (>= Qt 3.0) (headers and libraries) not found. Please check your installation!  
原因：查找提供qt的lib&&headers的软件包,并安装之  
解决：apt-get install libqt3-headers libqt3-mt-dev  
  
3、错误：in the prefix, you've chosen, are no KDE headers installed. This will fail.  
So, check this please and use another prefix!  
原因：install a KDE application in a Gnome environment。  
解决：which basically means its going to want to install a lot of KDE specific packages to work. This 'configure:error'  
is due to it expecting you to be running KDE and again refers to some 'headers'.  
sudo apt-get update  
sudo apt-get install kdelibs4-dev kdelibs4c2a  
  
4、错误： C compiler cannot create executables  
原因：  
解决：sudo apt-get gcc libc6-dev  
  
5、错误：checking for C compiler default output... configure: error: C compiler cannot create executables  
原因：  
解决：sudo apt-get install libc6-dev  
  
6、错误：configure: error: C++ preprocessor "/lib/cpp" fails sanity check  
原因：gcc的组件没装全  
解决：apt-get install build-essential  
  
7、错误：./admin/cvs.sh: 585: autoconf: not found  
原因：  
解决：apt-get install autoconf  
  
8、错误： \*\*\* GTK >= 2.4.0 not installed! \*\*\*  
原因：没装GTK  
解决：apt-get build-dep gedit  
  
9、错误：heching for gtk-config... no  
checking for GTK - version = 1.2.0... no  
\*\*\* The gtk-config script installed by GTK could not be found  
\*\*\* If GTK was installed in PREFIX, make sure PREFIX/bin is in  
\*\*\* your path, or set the GTK\_CONFIG enviroment variable to the  
\*\*\* full path to gtk-config.  
configure: error: Cannot find GTK: Is gtk-config in path?  
原因：  
解决：sudo apt-get install libgtk1.2-dev  
  
10、问题：eclipse中encoding不支持中文  
解决：编辑/var/lib/locales/supported.d/local，加一行zh\_CN.GBK GBK，执行sudo locale-gen  
  
11、问题：eva不弹出输入法  
解决：sudo apt-get install scim-qtimm  
  
12、问题：No package 'gtk+-2.0' found  
No package 'gtksourceview-1.0' found  
No package 'libgnomeui-2.0' found  
No package 'libglade-2.0' found  
No package 'libgnomeprintui-2.2' found  
解决：sudo apt-get install libgtk2.0-dev libgtksourceview-dev libgnomeui-dev libglade2-dev libgnomeprint2.2-dev  
  
13、问题：No package 'libpanelapplet-2.0' found  
解决：sudo apt-get install libpanelappletmm-2.6-dev  
  
  
错误：configure: error: C++ preprocessor "/lib/cpp" fails sanity check  
  
原因：gcc的组件没装全  
解决：apt-get install build-essential  
  
  
  
问题：eclipse中encoding不支持中文  
解决：编辑/var/lib/locales/supported.d/local，加一行zh\_CN.GBK GBK，执行sudo locale-gen  
  
错误：gnome.h: No such file or directory  
  
  
  
  
问题：No package 'gtk+-2.0' found  
No package 'gtksourceview-1.0' found  
No package 'libgnomeui-2.0' found  
No package 'libglade-2.0' found  
No package 'libgnomeprintui-2.2' found  
解决：sudo apt-get install libgtk2.0-dev libgtksourceview-dev libgnomeui-dev libglade2-dev libgnomeprint2.2-dev  
  
问题：No package 'libpanelapplet-2.0' found  
解决：sudo apt-get install libpanelappletmm-2.6-dev  
  
  
  
  
还有摘录：  
  
编译  
./configure （建议使用 –help 查询需要用到的参数）  
make  
sudo make install  
如果在 ./configure 这一步出现错误  
  
错误一：  
configure: error:  
  
You must have the GTK+ 2.0 development headers installed to compile Pidgin.  
If you only want to build Finch then specify –disable-gtkui when running configure.  
解决：  
sudo apt-get install libgtk2.0-dev  
  
错误二：  
configure: error:  
  
You must have libxml2 >= 2.6.0 development headers installed to build.  
解决：  
sudo apt-get install libxml2-dev  
  
错误三：  
configure: error:  
  
The msgfmt command is required to build libpurple. If it is installed on your system, ensure that it is in your path. If it is not, install GNU gettext to continue.  
解决：  
sudo apt-get install gettext  
如果在使用 GTalk 或 MSN 时出现错误  
  
错误：  
SSL Library/Libraries……… : None (MSN and Google Talk will not work  
without SSL!)  
解决：  
sudo apt-get install libnss-dev libnspr-dev  
  
如果在./configure中还出现问题，那么要找到问题所在，安装缺失的包即可。  
  
在配置过程中，config.log文件是很有帮助的。我们可以在这里面找出错误的根源，从而寻找应对措施。