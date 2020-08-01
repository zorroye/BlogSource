---
title: LFS制作-1、准备工作
tags:
  - 未分类
id: '225'
date: 2012-10-22 09:45:00
---

  
平台配置  

> 虚拟机：vmware workstation 9  
> 配置：    4核、1G内存、20G IDE硬盘(强烈建议用IDE硬盘)、软驱、IDE光驱  

宿主版本：lfslivecd-x86-6.3-r2145.iso  
LFS目标版本：LFS 6.3  
包下载地址：http://ftp.lfs-matrix.net/pub/lfs/lfs-packages/lfs-packages-6.3.tar  
操作方式：ssh  
参考手册：  

> http://www.linuxfromscratch.org/lfs/view/6.3/  
> http://blog.chinaunix.net/uid-436750-id-2123580.html  
> lfs6.2中文版  

制作流程  
宿主------------------->临时系统--------------------->目标系统  

> > |                    |                                          |  
> 
>   预工具链    kernel-header                     kernel-header  
>    binutils            glibc                                    glibc  
>      gcc              binutils                                binutils
> 
> > > > gcc                                      gcc
> > > 
> > >      其他工具                              其他工具
> > > 
> > > > > > > >        kernel  
> > > > > > > >   设置配置文件  
> > > > > > > 
> > > > > > >         引导信息写入扇区  
> > > > > > > 
> > > > > > > > >    |  
> > > > > > > > > 重启  

学习目的：  

> 1、了解制作详细流程  
> 2、读懂每条制作命令  
> 3、学习linux是如何组织、构建起来的。  
> 4、学习linux如何运作的  
> 5、了解每个包的作用，及包含的命令和函数的作用，存放位置  

其他说明：  

> 1、强烈建议用IDE硬盘，SCSI有可能导致不识别，我编译核心后还是识别不了。  
> 2、建议多编译几遍。  
>       我第一次编译的时候所有代码都是手动输入，而且还是按照孙海勇的那本书上输入的，花了整整2周时间。  
>       而按照LFS说明书手动输入，花了13个小时。而SSH连入操作的话，8小时就差不多了。  

  
0、ssh连接  

> 1、进livecd，passwd root  
> 2、/etc/rc.d/init.d/sshd restart 即可使用ssh连接了  

> 引自：[搭建LFS之ssh连接虚拟机的livecd](http://zouyi.ixiezi.com/2009/08/18/%E6%90%AD%E5%BB%BAlfs%E4%B9%8Bssh%E8%BF%9E%E6%8E%A5%E8%99%9A%E6%8B%9F%E6%9C%BA%E7%9A%84livecd/)

\----------------------------------------------------------------------------------------------------  
准备工作  

> 分区  
> 
> > cfdisk  
> > /dev/hda1，设置boot标志  
> > dev/hda5  
> 
> 格式化  
> 
> > mke2fs -jv /dev/hda1  
> > mkswap /dev/hda5  
> 
> 设置全局目录变量  
> 
> > export LFS=/mnt/lfs  
> 
> 新建并挂载目录  
> 
> > mkdir -pv $LFS  
> > mkdir -pv $LFS/tools $LFS/sources  $LFS/build  
> > mount -v -t ext3 /dev/hda1 $LFS  
> > swapon -v /dev/hda5  
> > cd $LFS  
> > chmod a+wt tools sources build  
> 
> 下载软件包和补丁  
> 
> > cd $LFS/sources  
> 
> > wget http://ftp.lfs-matrix.net/pub/lfs/lfs-packages/lfs-packages-6.3.tar  
> > tar -xvf lfs-packages-6.3.tar  
> > #http://ftp.lfs-matrix.net/pub/lfs/lfs-packages/ ，每个版本都有  
> > #如果用wget-list下载  
> > 
> > > wget -i wget-list &  
> > 
> > > #用正则表达式把下载列表和wget-list核对一下  
> > > 
> > > > #cat wget-list | sed 's/^.\*\\///g' |sort  > 1  
> > > > #ls ./sources | sort >2  
> > > > #diff 1 2  
> > 
> >   
> 
> 最后的准备工作  
> 
> > ln -sv $LFS/tools /  
> 
> > groupadd lfs  
> > useradd -s /bin/bash -g lfs -m -k /dev/null lfs  
> 
> > passwd lfs  
> > chown -v lfs $LFS/tools $LFS/sources $LFS/build  
> > su - lfs  
> > 
> > > cat > ~/.bash\_profile << "EOF"  
> > > `exec env -i HOME=$HOME TERM=$TERM PS1='\u:\w\$ ' /bin/bash`  
> > > #不知道TERM变量什么用  
> > > EOF
> > 
> > \---------------------  
> > 
> > > cat > ~/.bashrc << "EOF"  
> > > `set +h`  
> > > #关闭bash的hash功能，hash是建hash表来记录命令的路径，以免每次都从PATH里搜索  
> > > `umask 022`  
> > > `LFS=/mnt/lfs`  
> > > `LC_ALL=POSIX`  
> > > `PATH=/tools/bin:/bin:/usr/bin`  
> > > #设置tool路径的话，每建好一个命令就能直接用，不需要再用宿主的命令  
> > > `export LFS LC_ALL PATH`  
> > > EOF  
> > 
> > \----------------------  
> > 
> > > source ~/.bash\_profile  
> > 
> >   
> 
> 备注：编译文件时使用“make -j4”来使编译时使用4个核心一起编译，编译目标系统时不建议用