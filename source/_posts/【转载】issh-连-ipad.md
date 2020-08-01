---
title: 【转载】issh 连 IPAD
tags:
  - 未分类
id: '251'
date: 2014-11-14 11:37:00
---

设置端口：22的话会提示 operation not permitted

  

0、ipad 用cydia安装openssh，nano

1、ipad，电脑要同一网段

2、电脑用ssh连接ipad （默认密码alpine）

3) 備份兩個設定檔 (/etc/service, /Library/LaunchDaemons/com.openssh.sshd.plist)

        cp /etc/service ~/

        cp /Library/LaunchDaemons/com.openssh.sshd.plist ~/

4) 更改設定檔

     說明：把內鍵 ssh port 從 22 改到 50000 (假設)，其實 50000以上的port都可以

   a)     echo 'pttssh 50000/tcp #Secure sshd port' >> /etc/services

   b)     用喜好的軟體(vim, nano)編輯

          nano /Library/LaunchDaemons/com.openssh.sshd.plist

          尋找 <string>ssh</string>

          會有兩個位置 (Sockets/Listeners/Bonjour, SockServiceName)（ipad只有Sock一处）

          改為 <string>pttssh</string>

5) 儲存後 reboot