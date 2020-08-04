---
title: LFS制作-概念、原理
tags:
  - lfs
categories:
  - Linux
  - lfs
id: '224'
abbrlink: 319038377
date: 2012-10-18 13:56:00
---

  
关键词：  

> 核心、核心模块、内核函数库、核心头文件  
> 函数库、函数库头文件、静态链接、动态链接  
> 命令、命令驱动硬件  

关键词理解：  

> 核心：主要就是驱动硬件。  
> 模块：提供对某种硬件的支持，供内核使用  
> 内核函数库：实现某种功能，供内核使用  
> 核心头文件：提供操作硬件的接口  
>   
> 函数库：提供某些软件功能  
> 函数库头文件：提供软件实现某些功能的接口  

  
程序调用函数库和操作硬件  

> 动态链接程序的源代码：  
> 
> > 包含动态函数库头文件、内核函数库头文件  
> 
> 程序的编译：  
> 
> > 包含哪些头文件，由ld命令找到对应的函数库，并链接起来制作成可执行文件。  
> 
> 命令如何调用动态函数库：  
> 
> > ld.inux.so.2通过查找/etc/ld.so.cache、/lib、/usr/lib 来找到对应的动态函数库  
> 
> 命令的运行：  
> 
> > 调用动态函数库--->实现软件功能  
> 
> > 调用动态函数库--->调用内核函数库---->实现对硬件的操作  

  
  
程序编译流程：  
源代码 (source code) → 预处理器 (preprocessor) → [编译器](http://baike.baidu.com/view/487018.htm) (compiler) → [汇编程序](http://baike.baidu.com/view/1315652.htm) (assembler) →  
→目标代码 (object code) → [链接器](http://baike.baidu.com/view/1402117.htm) (Linker) → 可执行程序 (executables)  
  
程序制作：         源代码(包含内核头文件和函数头文件)------->gcc------->as-------->  

> > > ld(ld搜索路径并将头文件中提到的函数库进行链接)--->可执行程序  

程序的执行：     程序------->ld-linux.so加载相关的函数库------>实现操作。  
  
工具链说明  
linux-header：   [API](http://baike.baidu.com/view/16068.htm#2)(函数库)，用户可以使用其接口编程来实现对计算机软件及硬件的操作。  

> > > 存放位置：/usr/include  

  
Glibc：              包含了主要的C函数库  

> > > 存放位置：/lib、/usr/lib  

> [ld-linux.so](http://zh.wikipedia.org/wiki/Ld.so)：动态加载器，由glibc提供。  

> > >  当应用程序需要使用动态链接库里的函数时，动态链接需要去找函数库，  
> > >  怎么找呢，就用到这个ld.so函数库。  
> > >  那ld.so去那里找动态函数库呢？下面就提供了搜索路径。  
> > > 
> > > > 搜索动态链接库的顺序依此是  
> > > > 1、环境变量：LD\_AOUT\_LIBRARY\_PATH([a.out](http://zh.wikipedia.org/wiki/A.out "A.out")格式)  
> > > >       环境变量：LD\_LIBRARY\_PATH([ELF](http://zh.wikipedia.org/wiki/%E5%8F%AF%E5%9F%B7%E8%A1%8C%E8%88%87%E5%8F%AF%E9%8F%88%E6%8E%A5%E6%A0%BC%E5%BC%8F)格式)  
> > > > 2、/etc/ld.so.conf  
> > > > 3、缓存文件/etc/ld.so.cache。  
> > > >      此为环境变量、/lib、/usr/lib、/etc/ld.so.conf指定目录的二进制索引文件。  
> > > >      放入新函数库后要更新缓存，更新的命令是ldconfig。  
> > > > 4、默认目录，先在/lib中寻找，再到/usr/lib中寻找。  
> 
>   

Binutils：           包括连接器、汇编器  

> > > 存放位置：/usr  

> as：          汇编器，由binutils提供。  
> 
> > > 用来汇编gcc 的输出，产生的目标文件然后交由连接器 ld 连接

> ld：           链接器(连接器)，由binutils提供。此为编译时候用的命令。  
> 
> > > 将一个或多个由编译器或汇编器生成的“目标文件”外加“库”链接为一个可执行文件。
> 
> > > ld搜索路径：ld --verbose | grep SEARCH  
> 
> > > ld从下面地方找出动态函数库文件，然后进行连接。  
> 
> ![LFS制作-概念、原理 - leaf - ------坚持雅操------](http://img1.ph.126.net/4slhQLhSG3gGwp_Gxxn6eg==/630785422826341551.png "LFS制作-概念、原理 - leaf - ------坚持雅操------")

  
GCC：              包含C、C++等编译器  

> > > 存放位置：/usr  
> > >   

> 注意一点：  

> > 所有的程序都是由/usr里面的工具制作出来的。  
> > /usr目录就相当于windows下的program files + windows  

  
对linux内核不了解，以后会深入学的。以上只是自己的理解  

>   

参考：  

> lfs6.2中文版  
> http://zh.wikipedia.org/wiki/Ld.so  
> http://lsscto.blog.51cto.com/779396/904078  
> http://blog.csai.cn/user1/265/archives/2005/2465.html  
> http://www.simplemind.info/technolife/linuxsystem/lfs-problem.html  
> http://zh.wikipedia.org/wiki/%E7%B3%BB%E7%BB%9F%E8%B0%83%E7%94%A8  
>