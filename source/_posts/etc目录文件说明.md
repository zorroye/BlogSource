---
title: etc目录文件说明
tags:
  - 未分类
id: '92'
abbrlink: 771146178
date: 2015-06-01 10:42:00
---

参考文档

http://www.freedesktop.org/software/systemd/man/index.html

  

/etc各文件用途

adjtime设置同步时间

alias设置别名

anacrontab系统计划任务的扩展文件：在一个指定时间间隔错过后自动执行任务

http://www.2cto.com/os/201208/146487.html

asound.conf声卡设置文件，非必须

http://blog.sina.com.cn/s/blog\_a04184c101010kry.html

at.deny哪些人不能用at

bashrcbash环境设置，如PS1，umask，

chrony.conf时间同步配置文件

http://os.51cto.com/art/201403/431692.htm

chrony.keys时间同步SHA码

cron.deny哪些人不能用cron

http://wuseven.blog.51cto.com/6237275/1098591

crontab例行任务设置

crypttab设置启动过程中的块设备的加密

http://www.freedesktop.org/software/systemd/man/crypttab.html

http://www.2cto.com/Article/201309/243900.html

csh.cshrccsh环境设置

csh.login对启动环境的csh环境设置

DIR\_COLORS终端登录后的颜色设置

DIR\_COLORS.256color

DIR\_COLORS.lightbgcolor

dnsmasqdns和dhcp配置工具

http://www.thekelleys.org.uk/dnsmasq/doc.html

http://www.freehao123.com/dnsmasq/

dracut.conf引导镜像配置文件

http://www.360doc.com/content/13/0428/09/12139495\_281449877.shtml

drirc未知

dumpdates

e2fsck.conf只针对事件错误的修复配置

environment

ethertypes以太网帧类型定义

exports全局变量定义

filesystems支持的文件系统

fprintd.confhttp://www.freedesktop.org/wiki/Software/fprint/fprintd/

fatab默认挂载的文件系统

fw\_env.config内存地址配置

GREP\_COLORSgrep显示的颜色设置

group系统组用户

gshadow系统组用户密码

host.conf设置主机名查询顺序

http://lxsym.blog.51cto.com/1364623/311989

http://www.linuxidc.com/Linux/2010-10/28982.htm

hostname主机名

hostsIP地址和主机名映射表

hosts.allow网络服务允许列表

hosts.deny网络服务禁止列表

inittabinit配置文件，现已不需要

inputrc键盘键符设置

issue登录提示

issue.net网络登录提示

jwhois.confwhois客户端配置文件

http://wuhongsheng.com/tag/conf/

krb5.confkerberos认证配置

http://www.freebsd.org/doc/zh\_CN/books/handbook/kerberos5.html

ld.so.conf动态库文件配置

lftp.conflftp配置文件

libuser.conf

localtime当前时间

login.defs登录密码，uid，gid等设置

logrotate.conf轮替设置

machine-idhttp://www.freedesktop.org/software/systemd/man/machine-id.html

magic

mail.rcheirloom mail config

mailcap

man\_db.confman文件路径设置

mime.types一个mime类型说明文件

mke2fs.conf默认的文件系统参数设置

motd

mtab默认加载的文件系统

mtools.conf模拟许多MS-DOS的指令

nanorcnano配置文件

networks

nsswitch.conf系统数据库和名称服务切换配置文件

oddjobd.confoddjob daemon config

os-release系统版本号

passwd

passwdqc.conf密码规则

pidora-release

pinforc

prelink.conf

printcapcups方面的配置文件

profile系统环境设置

protocols网络协议标识说明

rc0-6.d启动项文件

rearj.cfg压缩文件命令说明

request-key.conf

resolv.confdns设置

rpcrpc相关服务说明

rsyncd.conf同步配置文件

rsyslog.confsyslog配置文件

securetty终端配置

services服务说明文件

sestatus.confselinux状态工具配置

shadow

shellsshell列表

sudoerssudo配置文件

sysctl.conf内核参数设置文件

updatedb.conflocate的db文件

vconsole.conf

wgetrcwget配置文件

yum.confyum配置文件

yumex.confyum配置文件