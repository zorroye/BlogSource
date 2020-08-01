---
title: ubuntu12.04 安装kvm
tags:
  - 未分类
id: '48'
date: 2014-01-07 15:15:00
---

笔记本原先是T4500，一直用不了kvm。前段时间换成P8700了，终于有机会试验一下了。  
因我使用net模式就够用了，所以就没设置/etc/network/interfaces 文件  
  
参考：  
http://blog.csdn.net/chdhust/article/details/7690119  
http://blog.csdn.net/sheismylife/article/category/1256795  
  
命令如下;  
0、BIOS开启虚拟化，我的没有这个选项，但是能用  
1、检查CPU是否支持虚拟化  

> egrep '(vmx|svm)' --color=always /proc/cpuinfo  

>   

2、安装相关软件  

> apt-get install ubuntu-virt-server python-vm-builder kvm-ipxe virt-manager  

  
3、将当前root用户加入到kvm和libvirtd组  

> adduser \`id -un\` libvirtd  
> adduser \`id-un\` kvm  

  
4、注销并重新登录，检查相关服务是否已开启  

> virsh -c qemu:///system list  
> 
> >  Id 名称               状态  
> > \----------------------------------  
> 
> lsmod | grep kvm  
> 
> > kvm\_intel             137888  0  
> > kvm                   422160  1 kvm\_intel  
> 
> service libvirt-bin status  
> 
> > service libvirt-bin status  
> > libvirt-bin start/running, process 13309  
> >   

管理器界面  

> ![ubuntu12.04 安装kvm - leaf - ------坚持雅操------](http://img0.ph.126.net/G6LQVX0IqLkYjN5Q_y9mNw==/1374442311378353604.png "ubuntu12.04 安装kvm - leaf - ------坚持雅操------")

  
5、新建/删除存储池  

> 1、virsh pool-define-as kvm-disk --type dir --target /home/ywz/5Soft/kvm/       建存储池  
> 2、virsh pool-start kvm-disk                设置状态为活动  
> 3、virsh pool-autostart kvm-disk        设置为自动开始  
> \-------------------------------  
> 1、virsh pool-destroy default              设置状态为不活跃  
> 2、virsh pool-undefine default            删除存储池  

  
  
6、使用virtio模式  

> 我的电脑使用这个模式没有啥感觉，可能是我的笔记本本身无法设置achi的缘故吧  
> 针对XP系统，安装的时候按F6直接加载软驱的驱动安装即可  
>   
> 使用vmvga，安装vmware显卡驱动。