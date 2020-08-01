---
title: LFS制作-4、目标系统-2目标工具链
tags:
  - 未分类
id: '230'
abbrlink: 991075949
date: 2012-10-25 15:22:00
---

1、Linux-2.6.22.5 API Headers 

#头文件，安装位置/usr/include，里面的\*.h都是头文件

#内核就相当于CPU，而头文件就相当于CPU的针脚，对CPU的操作都是通过针脚传命令进去的。

sed -i '/scsi/d' include/Kbuild

> #当前行的上一行插入/scsi/d

make mrproper

make headers\_check

make INSTALL\_HDR\_PATH=dest headers\_install

cp -rv dest/include/\* /usr/include

  

2、Man-pages-2.63 

make install

  

3、Glibc-2.5.1

#包含了主要的C库。这个库提供了基本例程，用于分配内存、搜索目录、打开关闭文件、读写文件、字串处理、模式匹配、数学计算等等。Glibc 的编译系统是高度自给自足的，即使当前编译器 specs 文件和连接器还指向 /tools 目录，也能正确安装

#安装位置:/usr/bin、/usr/lib

#包含的命令如：ldd、ldconfig

#包含的库文件：ld.so、libc

\------------------------------------------------------------------

tar -xvf ../glibc-libidn-2.5.1.tar.gz

mv glibc-libidn-2.5.1 libidn

sed -i '/vi\_VN.TCVN/d' localedata/SUPPORTED

> #当前行的上一行插入/vi\_VN.TCVN/d

sed -i \\

's|libs -o|libs -L/usr/lib -Wl,-dynamic-linker=/lib/ld-linux.so.2 -o|' \\

        scripts/test-installation.pl

sed -i 's|@BASH@|/bin/bash|' elf/ldd.bash.in

  

mkdir -v ../glibc-build

cd ../glibc-build

../glibc-2.5.1/configure --prefix=/usr \\

    --disable-profile --enable-add-ons \\

    --enable-kernel=2.6.0 --libexecdir=/usr/lib/glibc

make

touch /etc/ld.so.conf

make install

make localedata/install-locales

  

cat > /etc/nsswitch.conf << "EOF"

> \# Begin /etc/nsswitch.conf
> 
>   
> 
> passwd: files
> 
> group: files
> 
> shadow: files
> 
>   
> 
> hosts: files dns
> 
> networks: files
> 
>   
> 
> protocols: files
> 
> services: files
> 
> ethers: files
> 
> rpc: files
> 
>   
> 
> \# End /etc/nsswitch.conf

EOF

#nsswitch.conf：系统数据库及名字服务开关配置文件

  

cp -v --remove-destination /usr/share/zoneinfo/Asia/Shanghai \\

    /etc/localtime

cat > /etc/ld.so.conf << "EOF"

> \# Begin /etc/ld.so.conf
> 
>   
> 
> /usr/local/lib
> 
> /opt/lib
> 
>   
> 
> \# End /etc/ld.so.conf

EOF

  

4、调整工具链

mv -v /tools/bin/{ld,ld-old}

mv -v /tools/$(gcc -dumpmachine)/bin/{ld,ld-old}

mv -v /tools/bin/{ld-new,ld}

ln -sv /tools/bin/ld /tools/$(gcc -dumpmachine)/bin/ld

  

gcc -dumpspecs | sed \\     -e 's@/tools/lib/ld-linux.so.2@/lib/ld-linux.so.2@g' \\     -e '/\\\*startfile\_prefix\_spec:/{n;s@.\*@/usr/lib/ @}' \\     -e '/\\\*cpp:/{n;s@$@ -isystem /usr/include@}' > \\     \`dirname $(gcc --print-libgcc-file-name)\`/specs

测试：很重要

echo 'main(){}' > dummy.c

cc dummy.c -v -Wl,--verbose &> dummy.log

readelf -l a.out | grep ': /lib'

> 结果：\[Requesting program interpreter: /lib/ld-linux.so.2\]

  

grep -o '/usr/lib.\*/crt\[1in\].\*succeeded' dummy.log

> 结果：
> 
> /usr/lib/crt1.o succeeded
> 
> /usr/lib/crti.o succeeded
> 
> /usr/lib/crtn.o succeeded

  

grep -B1 '^ /usr/include' dummy.log

> 结果：
> 
> #include <...> search starts here:
> 
>  /usr/include

  

  

grep 'SEARCH.\*/usr/lib' dummy.log |sed 's|; |\\n|g'

> 结果：
> 
> SEARCH\_DIR("/tools/i686-pc-linux-gnu/lib")
> 
> SEARCH\_DIR("/usr/lib")
> 
> SEARCH\_DIR("/lib");

  

grep "/lib/libc.so.6 " dummy.log

> 结果：attempt to open /lib/libc.so.6 succeeded

  

grep found dummy.log

> 结果：found ld-linux.so.2 at /lib/ld-linux.so.2

  

5、 Binutils-2.17 

#Binutils 是一组开发工具，包括连接器、汇编器和其他用于目标文件和档案的工具。

#安装位置/usr/bin下

#包含的命令：as、ld

  

expect -c "spawn ls"

> 结果：spawn ls

  

mkdir -v ../binutils-build

cd ../binutils-build

../binutils-2.17/configure --prefix=/usr \\

    --enable-shared

make tooldir=/usr

make tooldir=/usr install

cp -v ../binutils-2.17/include/libiberty.h /usr/include

  

6、GCC-4.1.2 

#GCC 软件包包含 GNU 编译器，其中有 C 和 C++ 编译器。

#安装位置/usr/bin

#包含的命令如gcc、c++、g++等

  

sed -i 's/install\_to\_$(INSTALL\_DEST) //' libiberty/Makefile.in

sed -i 's/^XCFLAGS =$/& -fomit-frame-pointer/' gcc/Makefile.in

sed -i 's@\\./fixinc\\.sh@-c true@' gcc/Makefile.in

sed -i 's/@have\_mktemp\_command@/yes/' gcc/gccbug.in

  

mkdir -v ../gcc-build

cd ../gcc-build

../gcc-4.1.2/configure --prefix=/usr \\

    --libexecdir=/usr/lib --enable-shared \\

    --enable-threads=posix --enable-\_\_cxa\_atexit \\

    --enable-clocale=gnu --enable-languages=c,c++

make

make install

ln -sv ../usr/bin/cpp /lib

ln -sv gcc /usr/bin/cc

  

测试

echo 'main(){}' > dummy.c

cc dummy.c -v -Wl,--verbose &> dummy.log

readelf -l a.out | grep ': /lib'

> 结果：
> 
> \[Requesting program interpreter: /lib/ld-linux.so.2\]

  

grep -o '/usr/lib.\*/crt\[1in\].\*succeeded' dummy.log

> 结果：
> 
> /usr/lib/gcc/i686-pc-linux-gnu/4.1.2/../../../crt1.o succeeded
> 
> /usr/lib/gcc/i686-pc-linux-gnu/4.1.2/../../../crti.o succeeded
> 
> /usr/lib/gcc/i686-pc-linux-gnu/4.1.2/../../../crtn.o succeeded

  

grep -B1 '^ /usr/include' dummy.log

> 结果：
> 
> #include <...> search starts here:
> 
>  /usr/local/include
> 
>  /usr/lib/gcc/i686-pc-linux-gnu/4.1.2/include
> 
>  /usr/include

  

  

grep 'SEARCH.\*/usr/lib' dummy.log |sed 's|; |\\n|g'

> 结果：
> 
> SEARCH\_DIR("/usr/i686-pc-linux-gnu/lib")
> 
> SEARCH\_DIR("/usr/local/lib")
> 
> SEARCH\_DIR("/lib")
> 
> SEARCH\_DIR("/usr/lib");

  

grep "/lib/libc.so.6 " dummy.log

> 结果：attempt to open /lib/libc.so.6 succeeded

  

grep found dummy.log

> 结果：found ld-linux.so.2 at /lib/ld-linux.so.2