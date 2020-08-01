---
title: fedora安装
tags:
  - 未分类
id: '55'
abbrlink: 2744993236
date: 2011-02-06 15:59:00
---

  
使用ubuntu很方便，但是linux的书大多以redhat的文件结构来讲的，所以学会用fedora也是必要的。  
我在vmware里面装了Fedora-17-i686-Live-XFCE.iso  
  
1、vmware运行不了gnome版本的fedora17，原因是其显示效果vmware支持不了，但是virtualbox能支持  
  
2、把账户添加到/etc/sudoers，以方便操作  

> su -  
> chmod 600 /etc/sudoers  
> visudo  
> 添加  xxx   ALL(ALL)=ALL   xxx为账户名  
> sources /etc/sudoers  
> exit

  
3、装了yum源，添加了163的和sohu的源。  

> yum源和apt源不一样，yum是添加文件，然后更新；apt是添加地址，然后再更新  
> yum源下载：  
> 
> > mirrors.163.com  
> > mirrors.sohu.com  
> > ......  

> > 放入 /etc/yum.repos.d/下面
> > 
> > 把原先的repo文件删掉，因多个repo会导致同一个包添加删除会有重复
> > 
> > 然后运行 yum makecache 来更新
> 
> yum用法：
> 
> yum update                        #更新系统
> 
> yum install --                      #安转软件
> 
> yum remove  --    -y           #删除软件
> 
> yum clean all                      #删除多余rpm包

  
4、安装第三方软件仓库

> http://rpmfusion.org

  
5、由于是live版的，所以GCC和linux header多没装  

> sudo yum -y install gcc make kernel-headers kernel-devel  
>   

6、安装vmware-tools  

> 我的linux版本是3.3.4-5.fc17.i686 但是yum下载的却是3.5.4-1.fc17.i686  
> 只能自己去下载了安装 kernel-devel-3.3.4-5.fc17.i686.rpm  
> 地址：http://rpmfind.net/linux/rpm2html/search.php?query=kernel-devel  
>   

7、安装easylife  

> 地址：http://easylifeproject.org/  
> 这个软件可以帮我们安装flash等插件，觉得还可以虽然没有tweak这么好  
>   

8、安装fedorautils  

> fedorautils比easylife还要多一点，好东西阿～～  

> http://sourceforge.net/projects/fedorautils/?source=directory

  
9、关闭SELINUX  

> 默认选项是：permissive  
> 更改：sudo vi /etc/selinux/config  
> SELINUX=disabled