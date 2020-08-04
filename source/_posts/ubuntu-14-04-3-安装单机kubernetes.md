---
title: ubuntu 14.04.3 安装单机kubernetes
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '295'
abbrlink: 2045748854
date: 2015-10-26 21:46:00
---

  
以下只能通过科学上网后才能实现  
1、安装docker  

> http://www.docker.org.cn/book/install/26\_install-docker-trusty-14.04.html  
> http://docker.widuu.com/  

2、安装etcd  

> https://github.com/coreos/etcd/releases/  

3、安装golang  

> https://golang.org/dl/  
> http://wiki.ubuntu.org.cn/Golang  
> http://www.linuxdiyf.com/linux/8790.html  

4、安装单机kubernetes  

> http://kubernetes.io/v1.0/docs/getting-started-guides/docker.html  

> https://github.com/kubernetes/kubernetes/releases  

> https://www.ustack.com/blog/kubernetes1/  
> http://blog.csdn.net/zhang\_\_jiayu/article/details/42745507  
> http://kubernetes.io/v1.0/  

  
安装docker  

> curl -sSL https://get.docker.com/ | sh  
> sudo usermod -aG docker ywz  

  
安装etcd

> `sudo nano /etc/environment  
> `
> 
> > `加入/opt/bin`  
> 
> `mkdir /opt/bin  
> curl -L https://github.com/coreos/etcd/releases/download/v2.2.1/etcd-v2.2.1-linux-amd64.tar.gz -o etcd-v2.2.1-linux-amd64.tar.gz`  
> `tar xzvf etcd-v2.2.1-linux-amd64.tar.gz`  
> `cd etcd-v2.2.1-linux-amd64  
> cp ./etcd /opt/bin  
> `

`  
安装go语言`  

> sudo add-apt-repository ppa:evarlast/golang1.5  
> sudo apt-get update  
> sudo apt-get install golang  
>   

安装单机kubernetes  

> wget https://github.com/kubernetes/kubernetes/releases/download/v1.2.0-alpha.2/kubernetes.tar.gz  
> tar -xvf  kubernetes.tar.gz  
> cd ~/kubernetes  
> 安装客户端  
> 
> > sudo cp -a ./platforms/linux/amd64/kubectl /usr/bin  
> 
> 安装服务端  
> 
> > cd ~/kubernetes/server  
> > tar -xvf kubernetes-server-linux-amd64.tar.gz  
> > sudo cp -a ~/kubernetes/server/kubernetes/server/bin/\* /opt/bin  
> > cd ~/kubernetes/cluster/ubuntu/master  
> > sudo cp ./init\_scripts/\* /etc/init.d/  
> > sudo cp ./init\_conf/\* /etc/init/  
> 
> 安装upstart脚本  
> 
> > cd ~/kubernetes/cluster/ubuntu  
> > sudo ./util.sh  
> 
> 验证`  
> kubectl version  
> `
> 
> ![ubuntu 14.04.3 安装单机kubernetes - leaf - ------勤解万难------](http://img0.ph.126.net/nG9RK6DmfvQph2hUnioHmQ==/6631420708932790935.png "ubuntu 14.04.3 安装单机kubernetes - leaf - ------勤解万难------")