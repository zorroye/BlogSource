---
title: LFS制作-2、预工具链
tags:
  - 未分类
id: '226'
date: 2012-10-22 09:46:00
---

  
预工具链的作用就是用来编译临时系统的glibc，使临时系统摆脱宿主系统的依赖关系  
  
说明：  
1、解压命令就不输了，全部都解压在build下面了。  
2、如lfs说明里面要求另建编译目录，则另建目录  
  

>   

1、编译binutils-2.17

> cd $LFS/build  
> tar -xvf ../sources/binutils-2.17.tar.bz2  
> mkdir -v binutils-build  
> cd binutils-build
> 
> > CC="gcc -B/usr/bin/" ../binutils-2.17/configure \\  
> >     --prefix=/tools --disable-nls --disable-werror  
> > 
> > > #CC="gcc -B/usr/bin/"：指定用哪个位置的gcc
> > 
> > > #--prefix=/tools：安装在/tools下  
> > > #--disable-nls：禁用i18n(国际化)  
> > > #--disable-werror：有错误的话也继续编译  
> > 
> > make -j4 && make install  
> > 
> > > #这边编译的ld搜索函数库的路径是/usr/lib，也就是宿主的库文件  
> > 
> > make -C ld clean                           
> > 
> > > #为从新编译ld，先清除ld的编译  
> > 
> > make -C ld LIB\_PATH=/tools/lib    
> > 
> > > #重新编译ld，并设置ld使用/tools/lib下面的库文件，  
> > > #这样，调整工具链的时候把ld复制过去，ld的搜索路径就变为/tools/lib  
> > 
> > cp -v ld/ld-new /tools/bin  
> 
> cd ..  
> mv binutils-2.17 ./ygjl/  
>   

2、编译gcc-4.1.2  

> mkdir -v ../gcc-build  
> cd ../gcc-build  
> 
> > CC="gcc -B/usr/bin/" ../gcc-4.1.2/configure --prefix=/tools \\  
> >     --with-local-prefix=/tools --disable-nls --enable-shared \\  
> >     --enable-languages=c  
> > 
> > > #--enable-languages=c 只编译出c编译器  
> > 
> > make -j4 bootstrap  
> > make install  
> > ln -vs gcc /tools/bin/cc  
> >