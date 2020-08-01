---
title: LFS制作-4、目标系统-3必要程序
tags:
  - 未分类
id: '231'
abbrlink: 2307134587
date: 2012-10-25 16:31:00
---

Berkeley DB-4.5.20

> 包含一些程序和工具，供其他的一些程序来在做数据库相关函数时调用  
> \-----------------  
> patch -Np1 -i ../db-4.5.20-fixes-1.patch  
> cd build\_unix  
> ../dist/configure --prefix=/usr --enable-compat185 --enable-cxx  
> make  
> make docdir=/usr/share/doc/db-4.5.20 install  
> chown -Rv root:root /usr/share/doc/db-4.5.20  
>   

Sed-4.1.5

> sed编辑器  
> \----------------  
> ./configure --prefix=/usr --bindir=/bin --enable-html  
> make  
> make install  
> 
>   

E2fsprogs-1.40.2

> 提供用于 ext2 文件系统的工具。它还支持 ext3 日志文件系统
> 
> 包含命令：chattr、lsattr、mkfs、fsck等  
> \---------------  
> sed -i -e 's@/bin/rm@/tools&@' lib/blkid/test\_probe.in  
> mkdir -v build  
> cd build  
> ../configure --prefix=/usr --with-root-prefix="" \\  
>     --enable-elf-shlibs  
> make  
> make install  
> make  
> make install-libs  
>   

Coreutils-6.9

> 包括一套显示、设置基本系统属性的工具
> 
> 包含命令：chroot、chown、cp、dd、dir、env、ln、ls、mkdir、mv、rm、seq、tee、touch、tty等
> 
> 安装位置/usr，移动命令到/bin 、/sbin下  
> \------------------------  
> patch -Np1 -i ../coreutils-6.9-uname-1.patch  
> patch -Np1 -i ../coreutils-6.9-suppress\_uptime\_kill\_su-1.patch  
> patch -Np1 -i ../coreutils-6.9-i18n-1.patch  
> chmod +x tests/sort/sort-mb-tests  
> ./configure --prefix=/usr  
> make  
> make install  
> mv -v /usr/bin/{cat,chgrp,chmod,chown,cp,date,dd,df,echo} /bin  
> mv -v /usr/bin/{false,hostname,ln,ls,mkdir,mknod,mv,pwd,readlink,rm} /bin  
> mv -v /usr/bin/{rmdir,stty,sync,true,uname} /bin  
> mv -v /usr/bin/chroot /usr/sbin  
> mv -v /usr/bin/{head,sleep,nice} /bin  
>   

Iana-Etc-2.20

> 提供了网络服务和协议的数据
> 
> 安装文件：/etc/protocols, /etc/services  
> \-----------------------  
> make  
> make install  
>   

M4-1.4.10

> 宏处理器  
> \---------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Bison-2.3

> 语法分析程序生成器
> 
> 命令：bison、yacc  
> \----------------------  
> ./configure --prefix=/usr  
> echo '#define YYENABLE\_NLS 1' >> config.h  
> make  
> make install  
>   

Ncurses-5.6

> 提供字符终端处理库，包括面板和菜单
> 
> 命令：clear、reset等  
> \-----------------------  
> patch -Np1 -i ../ncurses-5.6-coverity\_fixes-1.patch  
> ./configure --prefix=/usr --with-shared --without-debug --enable-widec  
> make  
> make install  
> chmod -v 644 /usr/lib/libncurses++w.a  
> mv -v /usr/lib/libncursesw.so.5\* /lib  
> ln -sfv ../../lib/libncursesw.so.5 /usr/lib/libncursesw.so  
> for lib in curses ncurses form panel menu ; do \\  
>     rm -vf /usr/lib/lib${lib}.so ; \\  
>     echo "INPUT(-l${lib}w)" >/usr/lib/lib${lib}.so ; \\  
>     ln -sfv lib${lib}w.a /usr/lib/lib${lib}.a ; \\  
> done  
> ln -sfv libncurses++w.a /usr/lib/libncurses++.a  
> rm -vf /usr/lib/libcursesw.so  
> echo "INPUT(-lncursesw)" >/usr/lib/libcursesw.so  
> ln -sfv libncurses.so /usr/lib/libcurses.so  
> ln -sfv libncursesw.a /usr/lib/libcursesw.a  
> ln -sfv libncurses.a /usr/lib/libcurses.a  
>   

Procps-3.2.7

> 用于监视系统进程的程序
> 
> 命令：free、top、ps、uptime、kill等  
> \----------------------  
> make  
> make install  
>   

Libtool-1.5.24

> 通用库支持脚本，将使用动态库的复杂性隐藏在统一的、可移植的接口中  
> \---------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Perl-5.8.8

> 编程语言，各编程语言转换等用处  
> \-----------------  
> echo "127.0.0.1 localhost leaf" > /etc/hosts  
> ./configure.gnu --prefix=/usr \\  
>     -Dman1dir=/usr/share/man/man1 \\  
>     -Dman3dir=/usr/share/man/man3 \\  
>     -Dpager="/usr/bin/less -isR"  
> make  
> make install  
>   

Readline-5.2

> 提供命令行编辑和历史纪录功能的库集合  
> \---------------------  
> sed -i '/MV.\*old/d' Makefile.in  
> sed -i '/{OLDSUFF}/c:' support/shlib-install  
> patch -Np1 -i ../readline-5.2-fixes-3.patch  
> ./configure --prefix=/usr --libdir=/lib  
> make SHLIB\_LIBS=-lncurses  
> make install  
> mv -v /lib/lib{readline,history}.a /usr/lib  
> rm -v /lib/lib{readline,history}.so  
> ln -sfv ../../lib/libreadline.so.5 /usr/lib/libreadline.so  
> ln -sfv ../../lib/libhistory.so.5 /usr/lib/libhistory.so  
>   

Zlib-1.2.3

> 很多程序中的压缩或者解压缩程序都会用到这个库  
> \---------------------  
> ./configure --prefix=/usr --shared --libdir=/lib  
> make  
> make install  
> rm -v /lib/libz.so  
> ln -sfv ../../lib/libz.so.1.2.3 /usr/lib/libz.so  
> make clean  
> ./configure --prefix=/usr  
> make  
> make install  
> chmod -v 644 /usr/lib/libz.a  
>   

Autoconf-2.61

> 生成用于自动配置源代码的 shell 脚本
> 
> 命令：autoconf、autoheader等  
> \--------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Automake-1.10

> 与 Autoconf 配合使用，产生 Makefile 文件  
> \-------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Bash-3.2

> bash shell  
> \----------------------  
> tar -xvf ../bash-doc-3.2.tar.gz  
> sed -i "s|htmldir = @htmldir@|htmldir = /usr/share/doc/bash-3.2|" \\  
>     Makefile.in  
> patch -Np1 -i ../bash-3.2-fixes-5.patch  
> ./configure --prefix=/usr --bindir=/bin \\  
>     --without-bash-malloc --with-installed-readline  
> make  
> sed -i 's/LANG/LC\_ALL/' tests/intl.tests  
> sed -i 's@tests@& </dev/tty@' tests/run-test  
> chown -Rv nobody ./  
> su-tools nobody -s /bin/bash -c "make tests"  
> make install  
> exec /bin/bash --login +h  
>   

Bzip2-1.0.4

> 包含了对文件进行压缩和解压缩的工具  
> \----------------------  
> patch -Np1 -i ../bzip2-1.0.4-install\_docs-1.patch  
> make -f Makefile-libbz2\_so  
> make clean  
> make  
> make PREFIX=/usr install  
> cp -v bzip2-shared /bin/bzip2  
> cp -av libbz2.so\* /lib  
> ln -sv ../../lib/libbz2.so.1.0 /usr/lib/libbz2.so  
> rm -v /usr/bin/{bunzip2,bzcat,bzip2}  
> ln -sv bzip2 /bin/bunzip2  
> ln -sv bzip2 /bin/bzcat  
>   

Diffutils-2.8.1

> 显示两个文件或目录的差异
> 
> 命令：cmp、diff  
> \------------------------  
> patch -Np1 -i ../diffutils-2.8.1-i18n-1.patch  
> touch man/diff.1  
> ./configure --prefix=/usr  
> make  
> make install  
>   

File-4.21

> 用来判断文件类型的工具
> 
> 命令：file  
> \-------------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Findutils-4.2.31

> 查找文件的工具
> 
> 命令：find、updatedb、locate、xargs  
> \-----------------------  
> ./configure --prefix=/usr --libexecdir=/usr/lib/findutils \\  
>     --localstatedir=/var/lib/locate  
> make  
> make install  
> mv -v /usr/bin/find /bin  
> sed -i -e 's/find:=${BINDIR}/find:=\\/bin/' /usr/bin/updatedb  
>   

Flex-2.5.33

> 能生成识别文本模式的程序的工具  
> \--------------------  
> ./configure --prefix=/usr  
> make  
> make install  
> ln -sv libfl.a /usr/lib/libl.a  
> 
> > cat > /usr/bin/lex << "EOF"  
> > #!/bin/sh  
> > \# Begin /usr/bin/lex  
> >   
> > exec /usr/bin/flex -l "$@"  
> >   
> > \# End /usr/bin/lex  
> > EOF  
> 
> chmod -v 755 /usr/bin/lex  
>   
>   

GRUB-0.97

> 包含 GRand 统一引导装载程序  
> \-----------------  
> patch -Np1 -i ../grub-0.97-disk\_geometry-1.patch  
> ./configure --prefix=/usr  
> make  
> make install  
> mkdir -v /boot/grub  
> cp -v /usr/lib/grub/i386-pc/stage{1,2} /boot/grub  
>   
>   

Gawk-3.1.5

> 包含用于管理文本文件的程序
> 
> 命令：awk等  
> \---------------------  
> patch -Np1 -i ../gawk-3.1.5-segfault\_fix-1.patch  
> ./configure --prefix=/usr --libexecdir=/usr/lib  
> 
> > cat >> config.h << "EOF"  
> > #define HAVE\_LANGINFO\_CODESET 1  
> > #define HAVE\_LC\_MESSAGES 1  
> > EOF  
> 
> make  
> make install  
>   

Gettext-0.16.1

> 系统的国际化和本地化  
> \----------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Grep-2.5.1a

> 搜索文件中符合指定匹配模式的行
> 
> 命令：grep  
> \---------------  
> patch -Np1 -i ../grep-2.5.1a-redhat\_fixes-2.patch  
> chmod +x tests/fmbtest.sh  
> ./configure --prefix=/usr --bindir=/bin  
> make  
> make install  
>   

Groff-1.18.1.4

> 包含几个处理和格式化文本的程序  
> \-----------------  
> patch -Np1 -i ../groff-1.18.1.4-debian\_fixes-1.patch  
> sed -i -e 's/2010/002D/' -e 's/2212/002D/' \\  
>     -e 's/2018/0060/' -e 's/2019/0027/' font/devutf8/R.proto  
> PAGE=A4 ./configure --prefix=/usr --enable-multibyte  
> make  
> make install  
> ln -sv eqn /usr/bin/geqn  
> ln -sv tbl /usr/bin/gtbl  
>   

Gzip-1.3.12

> 压缩和解压文件的程序  
> \--------------------  
> ./configure --prefix=/usr --bindir=/bin  
> make  
> make install  
> mv -v /bin/{gzexe,uncompress,zcmp,zdiff,zegrep} /usr/bin  
> mv -v /bin/{zfgrep,zforce,zgrep,zless,zmore,znew} /usr/bin  
>   

Inetutils-1.5

> 包含基本的网络程序
> 
> 配置文件:/etc
> 
> 命令：ping、ftp、telnet等  
> \--------------------  
> patch -Np1 -i ../inetutils-1.5-no\_server\_man\_pages-2.patch  
> ./configure --prefix=/usr --libexecdir=/usr/sbin \\  
>     --sysconfdir=/etc --localstatedir=/var \\  
>     --disable-ifconfig --disable-logger --disable-syslogd \\  
>     --disable-whois --disable-servers  
> make  
> make install  
> mv -v /usr/bin/ping /bin  
>   

IPRoute2-2.6.20-070313

> 基本的和高级的基于 IPv4 网络的程序
> 
> 命令：ip、arpd守护程序、  
> \-----------------  
> sed -i -e '/tc-bfifo.8/d' -e '/tc-pfifo.8/s/pbfifo/bfifo/' Makefile  
> make SBINDIR=/sbin  
> make SBINDIR=/sbin install  
> mv -v /sbin/arpd /usr/sbin  
>   

Kbd-1.12

> 键盘映射表和键盘工具  
> \--------------------  
> patch -Np1 -i ../kbd-1.12-backspace-1.patch  
> patch -Np1 -i ../kbd-1.12-gcc4\_fixes-1.patch  
> ./configure --datadir=/lib/kbd  
> make  
> make install  
> mv -v /usr/bin/{kbd\_mode,openvt,setfont} /bin  
>   
>   

Less-406

> 一个文本文件查看器
> 
> 命令：less  
> \----------------------  
> ./configure --prefix=/usr --sysconfdir=/etc  
> make  
> make install  
>   

Make-3.81

> 自动地确定一个大型程序的哪些片段需要重新编译，并且发出命令去重新编译它们
> 
> 应该和autoconf和automake有关系  
> \---------------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Man-DB-2.4.4

> 查找和显示 man 手册页的程序
> 
> 命令：man等
> 
> \----------------------  
> sed -i -e '\\%\\t/usr/man%d' -e '\\%\\t/usr/local/man%d' src/man\_db.conf.in
> 
> > cat >> include/manconfig.h.in << "EOF"

> > #define WEB\_BROWSER "exec /usr/bin/lynx"
> 
> > #define COL "/usr/bin/col"
> 
> > #define VGRIND "/usr/bin/vgrind"
> 
> > #define GRAP "/usr/bin/grap"

> > EOF
> 
> patch -Np1 -i ../man-db-2.4.4-fixes-1.patch
> 
> ./configure --prefix=/usr --enable-mb-groff --disable-setuid
> 
> make && make install  
>   

Mktemp-1.5

> 包含用于在 shell 脚本中创建安全临时文件的程序  
> \---------------------  
> patch -Np1 -i ../mktemp-1.5-add\_tempfile-3.patch  
> ./configure --prefix=/usr --with-libc  
> make  
> make install  
> make install-tempfile  
>   

Module-Init-Tools-3.2.2

> 处理 2.5.47 及以上版本的内核模块时使用的工具
> 
> 命令：modprobe、insmod、depmod、lsmod
> 
> 安装位置:/sbin  
> \-------------------  
> patch -Np1 -i ../module-init-tools-3.2.2-modprobe-1.patch  
> ./configure  
> make check  
> make distclean  
> ./configure --prefix=/ --enable-zlib  
> make  
> make INSTALL=install install  
>   

Patch-2.5.4

> 补丁命令，一般和diff一起用

> 命令：patch  
> \-----------------  
> ./configure --prefix=/usr  
> make  
> make install  
>   

Psmisc-22.5

> 用于显示进程信息的程序
> 
> 命令：pstree、killall  
> \------------------  
> ./configure --prefix=/usr --exec-prefix=""  
> make  
> make install  
> mv -v /bin/pstree\* /usr/bin  
> ln -sv killall /bin/pidof  
>   

Shadow-4.0.18.1

> 用于在安全方式下处理密码的程序
> 
> 配置文件/etc
> 
> 库文件:/usr/lib、/lib
> 
> 命令位置:/bin、/usr/bin
> 
> 命令：su、passwd、login、useradd、userdel、chsh
> 
> \------------------  
> patch -Np1 -i ../shadow-4.0.18.1-useradd\_fix-2.patch
> 
> ./configure --libdir=/lib --sysconfdir=/etc --enable-shared \\
> 
>     --without-selinux
> 
> sed -i 's/groups$(EXEEXT) //' src/Makefile
> 
> find man -name Makefile -exec sed -i 's/groups\\.1 / /' {} \\;
> 
> sed -i -e 's@#MD5\_CRYPT\_ENAB.no@MD5\_CRYPT\_ENAB yes@' \\
> 
>     -e 's@/var/spool/mail@/var/mail@' etc/login.defs
> 
> make
> 
> make install
> 
> mv -v /usr/bin/passwd /bin
> 
> mv -v /lib/libshadow.\*a /usr/lib
> 
> rm -v /lib/libshadow.so
> 
> ln -sfv ../../lib/libshadow.so.0 /usr/lib/libshadow.so
> 
> pwconv
> 
> grpconv
> 
> useradd -D -b /home
> 
> sed -i 's/yes/no/' /etc/default/useradd
> 
> passwd root   #一定要设置root密码  
>   

Sysklogd-1.4.1

> 记录系统日志信息的程序
> 
> 命令：klogd守护程序、syslogd  
> \-----------------  
> patch -Np1 -i ../sysklogd-1.4.1-fixes-2.patch  
> patch -Np1 -i ../sysklogd-1.4.1-8bit-1.patch  
> make  
> make install  
> 
> > cat > /etc/syslog.conf << "EOF"  
> > \# Begin /etc/syslog.conf  
> >   
> > auth,authpriv.\* -/var/log/auth.log  
> > \*.\*;auth,authpriv.none -/var/log/sys.log  
> > daemon.\* -/var/log/daemon.log  
> > kern.\* -/var/log/kern.log  
> > mail.\* -/var/log/mail.log  
> > user.\* -/var/log/user.log  
> > \*.emerg \*  
> >   
> > \# End /etc/syslog.conf  
> > EOF  
> 
>   

Sysvinit-2.86  

> 一些控制系统启动、运行、关闭的程序
> 
> 配置文件：/etc/inittab
> 
> 命令：shutdown、init、reboot等  
> \-------------------  
> sed -i 's@Sending processes@& configured via /etc/inittab@g' \\  
>     src/init.c  
> make -C src  
> make -C src install  
> 
> > cat > /etc/inittab << "EOF"  
> > \# Begin /etc/inittab  
> >   
> > id:3:initdefault:  
> >   
> > si::sysinit:/etc/rc.d/init.d/rc sysinit  
> >   
> > l0:0:wait:/etc/rc.d/init.d/rc 0  
> > l1:S1:wait:/etc/rc.d/init.d/rc 1  
> > l2:2:wait:/etc/rc.d/init.d/rc 2  
> > l3:3:wait:/etc/rc.d/init.d/rc 3  
> > l4:4:wait:/etc/rc.d/init.d/rc 4  
> > l5:5:wait:/etc/rc.d/init.d/rc 5  
> > l6:6:wait:/etc/rc.d/init.d/rc 6  
> >   
> > ca:12345:ctrlaltdel:/sbin/shutdown -t1 -a -r now  
> >   
> > su:S016:once:/sbin/sulogin  
> >   
> > 1:2345:respawn:/sbin/agetty tty1 9600  
> > 2:2345:respawn:/sbin/agetty tty2 9600  
> > 3:2345:respawn:/sbin/agetty tty3 9600  
> > 4:2345:respawn:/sbin/agetty tty4 9600  
> > 5:2345:respawn:/sbin/agetty tty5 9600  
> > 6:2345:respawn:/sbin/agetty tty6 9600  
> >   
> > \# End /etc/inittab  
> 
> > EOF  
> 
>   

Tar-1.18

> 一个归档程序  
> \--------------  
> ./configure --prefix=/usr --bindir=/bin --libexecdir=/usr/sbin  
> make  
> make install  
>   

Texinfo-4.9

> 读取、写入、转换 Info 文档的程序
> 
> 命令：info等  
> \----------------  
> patch -Np1 -i ../texinfo-4.9-multibyte-1.patch  
> patch -Np1 -i ../texinfo-4.9-tempfile\_fix-1.patch  
> ./configure --prefix=/usr  
> make  
> make install  
> make TEXMF=/usr/share/texmf install-tex  
> cd /usr/share/info  
> rm dir  
> for f in \*  
> do install-info $f dir 2>/dev/null  
> done  
>   

Udev-113

> 包含动态地创建设备节点的程序
> 
> 命令：udevinfo等  
> \------------------  
> tar -xvf ../udev-config-6.3.tar.bz2  
> install -dv /lib/{firmware,udev/devices/{pts,shm}}  
> mknod -m0666 /lib/udev/devices/null c 1 3  
> ln -sv /proc/self/fd /lib/udev/devices/fd  
> ln -sv /proc/self/fd/0 /lib/udev/devices/stdin  
> ln -sv /proc/self/fd/1 /lib/udev/devices/stdout  
> ln -sv /proc/self/fd/2 /lib/udev/devices/stderr  
> ln -sv /proc/kcore /lib/udev/devices/core  
> make EXTRAS="\`echo extras/\*/\`"  
> make DESTDIR=/ EXTRAS="\`echo extras/\*/\`" install  
> cp -v etc/udev/rules.d/\[0-9\]\* /etc/udev/rules.d/  
> cd udev-config-6.3  
> make install  
> make install-doc  
> make install-extra-doc  
> cd ..  
> install -m644 -v docs/writing\_udev\_rules/index.html \\  
>     /usr/share/doc/udev-113/index.html  
>   

Util-linux-2.12r

> 包含许多工具。其中比较重要的是加载、卸载、格式化、分区和管理硬盘驱动器，打开 tty 端口和得到内核消息
> 
> 命令位置：/usr/bin
> 
> 命令：mount、whereis、cfdisk、  
> \----------------  
> sed -e 's@etc/adjtime@var/lib/hwclock/adjtime@g' \\  
>     -i $(grep -rl '/etc/adjtime' .)  
> mkdir -pv /var/lib/hwclock  
> patch -Np1 -i ../util-linux-2.12r-cramfs-1.patch  
> patch -Np1 -i ../util-linux-2.12r-lseek-1.patch  
> ./configure  
> make HAVE\_KILL=yes HAVE\_SLN=yes  
> make HAVE\_KILL=yes HAVE\_SLN=yes install  
>   

Vim-7.1 

> 强大的文本编辑器  
> \--------------  
> patch -Np1 -i ../vim-7.1-fixes-1.patch  
> patch -Np1 -i ../vim-7.1-mandir-1.patch  
> echo '#define SYS\_VIMRC\_FILE "/etc/vimrc"' >> src/feature.h  
> ./configure --prefix=/usr --enable-multibyte  
> make  
> make install  
> ln -sv vim /usr/bin/vi  
> for L in "" fr it pl ru; do  
>     ln -sv vim.1 /usr/share/man/$L/man1/vi.1  
> done  
> ln -sv ../vim/vim71/doc /usr/share/doc/vim-7.1  
> 
> > cat > /etc/vimrc << "EOF"  
> > " Begin /etc/vimrc  
> >   
> > set nocompatible  
> > set backspace=2  
> > syntax on  
> > if (&term == "iterm") || (&term == "putty")  
> >   set background=dark  
> > endif  
> >   
> > " End /etc/vimrc  
> > EOF  
> 
>   
> 
>   

2、清理

logout

mv $LFS/tools $LFS/root

mv $LFS/sources $LFS/root

mv $LFS/build $LFS/root