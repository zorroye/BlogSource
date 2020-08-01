---
title: ubuntu server 10.04 NFS设置
tags:
  - 未分类
id: '331'
date: 2010-10-09 10:25:00
---

1、安装软件  
       portmap：sudo apt-get install portmap  
       nfs：    sudo apt-get install nfs-kernel-server  
  
       1>相关服务  
            portmap  
            nfs  
        2>相关端口  
             RPC端口        111  
             nfs启动端口   2049  
        3>相关命令  
             rpc相关命令：    
                   rpcinfo -p ip             查看rpc开放的端口  
             nfs 相关命令：  
                   showmount -a         查看哪些人连接到本机  
                   showmount -e IP     查看IP的这台主机共享出来的目录  
                   exportfs -arv            本机的共享目录全部重新加载  
                   exportfs -auv           本机的共享目录全部卸载  
  
2、相关设置  
     1>防火墙设置  
                 针对IP和端口111  
     2>tcp wrappers设置  
                /etc/hosts.allow  
                /etc/hosts.deny  
     3>共享文件权限设置  
                rwx  
     4>nfs配置文件设置  
                 /etc/exports  
     5>uid/gid相关权限说明  
               1>相同uid和帐号、组：直接以该帐号操作  
               2>相同uid但帐号不同：以该uid所对应的帐号操作  
               3>没有该uid：以匿名方式操作uid号：65534  
                            root：以匿名方式操作uid号：65534  
     6>本机加载时对mount进行限制  
  
      1、防火墙设置：sudo ufw (不能设置端口，不安全)  
                       sudo ufw allow 192.168.2.0/24  
      2、/etc/hosts.allow  
                       mountd:192.168.2.0/24 :allow  
      3、rwx  
      4、/etc/exports  
             共享目录        分享对象(相关的权限)  
                                  相关权限：rw，sync，root\_squash，all\_squash，anonuid，anongid  
      5、从4、进行设置  
      6、mount设置  
              mount  -t nfs \-o nosuid,noexec,nodev,rw 192.168.2.187:/home/nfsshare /media/nfs  
  
  
详细设置  
1、sudo apt-get install portmap  
      sudo apt-get install nfs-kernel-server  
2、sudo ufw allow 192.168.2.0/24  
3、mkdir /home/nfsshare  
      chmod 777 /home/nfsshare  
4、/etc/exports  
      /home/nfsshare     192.168.2.0/24(rw,sync,all\_squash,anonuid=65534,anongid=65534)  
5、sudo service portmap restart  
      sudo service nfs-kernel-server restart  
6、本地加载：  
      mount  -t nfs \-o nosuid,noexec,nodev,rw 192.168.2.187:/home/nfsshare /media/nfs