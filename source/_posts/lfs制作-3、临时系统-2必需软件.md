---
title: LFS制作-3、临时系统-2必需软件
tags:
  - lfs
categories:
  - Linux
  - lfs
id: '228'
abbrlink: 1902492967
date: 2012-10-25 12:35:00
---

Ncurses-5.6 

./configure --prefix=/tools --with-shared \\

    --without-debug --without-ada --enable-overwrite

make && make install 

  

Bash-3.2 

patch -Np1 -i ../bash-3.2-fixes-5.patch

./configure --prefix=/tools --without-bash-malloc

ln -vs bash /tools/bin/sh

  

Bzip2-1.0.4 

make && make PREFIX=/tools install

  

Coreutils-6.9

./configure --prefix=/tools && make && make install

cp -v src/su /tools/bin/su-tools

  

Diffutils-2.8.1 

./configure --prefix=/tools && make && make install

  

Findutils-4.2.31 

./configure --prefix=/tools && make && make install

  

Gawk-3.1.5

./configure --prefix=/tools

cat >> config.h << "EOF"

> #define HAVE\_LANGINFO\_CODESET 1
> 
> #define HAVE\_LC\_MESSAGES 1

EOF

make && make install

  

Gettext-0.16.1

cd gettext-tools

./configure --prefix=/tools --disable-shared

make -C gnulib-lib

make -C src msgfmt

cp -v src/msgfmt /tools/bin

  

Grep-2.5.1a

./configure --prefix=/tools \\

    --disable-perl-regexp

make && make install

  

Gzip-1.3.12

./configure --prefix=/tools && make && make install

  

Make-3.81

./configure --prefix=/tools && make && make install

  

Patch-2.5.4 

./configure --prefix=/tools && make && make install

  

Perl-5.8.8 

patch -Np1 -i ../perl-5.8.8-libc-2.patch

./configure.gnu --prefix=/tools -Dstatic\_ext='Data/Dumper Fcntl IO POSIX'

make perl utilities

cp -v perl pod/pod2man /tools/bin

mkdir -pv /tools/lib/perl5/5.8.8

cp -Rv lib/\* /tools/lib/perl5/5.8.8

  

Sed-4.1.5 

./configure --prefix=/tools && make && make install

  

Tar-1.18 

./configure --prefix=/tools && make && make install

  

Texinfo-4.9 

./configure --prefix=/tools && make && make install

  

Util-linux-2.12r 

sed -i 's@/usr/include@/tools/include@g' configure

> #把/usr/include替换为/tools/include

./configure

make -C lib

make -C mount mount umount

make -C text-utils more

cp -v mount/{,u}mount text-utils/more /tools/bin

> #把mount/mount mount/umount text-utils/more 复制到/tools/bin下

  

清理和改权限

不做也没关系

  

logout