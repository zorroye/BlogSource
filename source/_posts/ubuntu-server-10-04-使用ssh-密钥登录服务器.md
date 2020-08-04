---
title: 'ubuntu server 10.04 :使用ssh 密钥登录服务器'
tags:
  - ubuntuserver
categories:
  - Ubuntu
  - server
id: '273'
abbrlink: 2047342109
date: 2010-11-06 15:02:00
---

1、在客户端生成私钥：  
      sudo apt-get install ssh-client  
      ssh-keygen -t rsa            # (ssh-keygen -t rsa -C "my key")  
                                             #生成密钥：包含公钥、私钥，存放在～/.ssh/  下  
                                             #提示输入密钥加密口令，而不是登录服务器的密码  
  
2、将公钥复制到服务器上  
     ssh-copy-id -i ~/.ssh/id\_rsa.pub  test@192.168.1.10  
     会提示要求你测试一下  
     输入 ssh   test@192.168.1.10 会提示你输入密钥的加密口令，输入后即可登录远程服务器  
  
配置ssh  
配置文件在 /etc/init.d/sshd\_config  
1、更改端口 将22 更改为其他端口 更改后以后登录的格式为  ssh test@192.168.1.10 -p 端口号  
2、禁用密码登录，仅允许密钥登录  
   PermitRootLogin no  
   PasswordAuthentication no  
   UsePAM no  
  然后重启 ssh ：sudo /etc/init.d/ssh restart  
  
其他：  
1、修改密钥加密口令： ssh-keygen -p  
2、限制scp占用的带宽： scp -l 256 test@192.168.1.10:/ .       #256Kb/s