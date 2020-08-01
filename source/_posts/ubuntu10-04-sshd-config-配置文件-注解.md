---
title: ubuntu10.04 sshd_config 配置文件 注解
tags:
  - 未分类
id: '272'
abbrlink: 3822141323
date: 2010-09-23 08:36:00
---

  

\# Package generated configuration file  
\# See the sshd\_config(5) manpage for details  
  
\# What ports, IPs and protocols we listen for  
    # 端口号  
Port 22  
\# Use these options to restrict which interfaces/protocols sshd will bind to  
    #监听服务器的哪个网卡的ssh联机  
#ListenAddress ::  
#ListenAddress 0.0.0.0  
    #使用的协议  
Protocol 2  
\# HostKeys for protocol version 2  
    #服务器密钥存放地址  
HostKey /etc/ssh/ssh\_host\_rsa\_key  
HostKey /etc/ssh/ssh\_host\_dsa\_key  
#Privilege Separation is turned on for security  
UsePrivilegeSeparation yes  
  
\# Lifetime and size of ephemeral version 1 server key  
    #v1的key存活时间  
KeyRegenerationInterval 3600  
    #公钥的长度  
ServerKeyBits 768  
  
\# Logging  
SyslogFacility AUTH  
LogLevel INFO  
  
\# Authentication:  
LoginGraceTime 120  
    #是否允许root登录  
PermitRootLogin no  
    #用户的host key改变时就不接受联机  
StrictModes yes  
  
RSAAuthentication yes  
PubkeyAuthentication yes  
    #不用密码即可登录  
AuthorizedKeysFile    %h/.ssh/authorized\_keys  
  
\# Don't read the user's ~/.rhosts and ~/.shosts files  
    #取消.rhosts来做认证  
IgnoreRhosts yes  
\# For this to work you will also need host keys in /etc/ssh\_known\_hosts  
RhostsRSAAuthentication no  
\# similar for protocol version 2  
HostbasedAuthentication no  
\# Uncomment if you don't trust ~/.ssh/known\_hosts for RhostsRSAAuthentication  
#IgnoreUserKnownHosts yes  
  
\# To enable empty passwords, change to yes (NOT RECOMMENDED)  
    #不允许空密码登录  
PermitEmptyPasswords no  
  
\# Change to yes to enable challenge-response passwords (beware issues with  
\# some PAM modules and threads)  
ChallengeResponseAuthentication no  
  
\# Change to no to disable tunnelled clear text passwords  
#PasswordAuthentication yes  
  
\# Kerberos options  
#KerberosAuthentication no  
#KerberosGetAFSToken no  
#KerberosOrLocalPasswd yes  
#KerberosTicketCleanup yes  
  
\# GSSAPI options  
#GSSAPIAuthentication no  
#GSSAPICleanupCredentials yes  
  
X11Forwarding yes  
X11DisplayOffset 10  
PrintMotd no  
PrintLastLog yes  
TCPKeepAlive yes  
#UseLogin no  
  
#MaxStartups 10:30:60  
#Banner /etc/issue.net  
  
\# Allow client to pass locale environment variables  
AcceptEnv LANG LC\_\*  
  
Subsystem sftp /usr/lib/openssh/sftp-server  
  
\# Set this to 'yes' to enable PAM authentication, account processing,  
\# and session processing. If this is enabled, PAM authentication will  
\# be allowed through the ChallengeResponseAuthentication and  
\# PasswordAuthentication.  Depending on your PAM configuration,  
\# PAM authentication via ChallengeResponseAuthentication may bypass  
\# the setting of "PermitRootLogin without-password".  
\# If you just want the PAM account and session checks to run without  
\# PAM authentication, then enable this but set PasswordAuthentication  
\# and ChallengeResponseAuthentication to 'no'.  
UsePAM yes