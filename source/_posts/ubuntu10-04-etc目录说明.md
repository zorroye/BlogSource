---
title: ubuntu10.04     /etc目录说明
tags:
  - ubuntu
categories:
  - Ubuntu
  - Q&A
id: '20'
abbrlink: 3248068869
date: 2010-06-14 19:40:00
---

ls -al /etc | awk '{print $8}'

  

acpi                              #管电源

adduser.conf                 #adduser默认配置

alternatives

anacrontab                   #anacron配置文件，anacron用于执行关机期间的cron

apache2                       #apache配置文件夹

apm                             #管电源

apparmor                     #应用程序访问控制系统，类似selinux

apparmor.d       

apport                          #用于生成系统崩溃报告

apt                              #apt配置

at.deny                        #设置哪些用户不能用at

avahi                           #IPv4LL网络地址配置后台

bash.bashrc                 #.bashrc默认配置

bash\_completion          #bash自动补齐功能

bash\_completion.d       

bindresvport.blacklist    #600-1024的端口绑定

blkid.conf                     #查看文件系统信息等

blkid.tab

bluetooth                     #蓝牙配置文件

bogofilter.cf                 

bonobo-activation

brlapi.key

brltty

byobu

ca-certificates

ca-certificates.conf

calendar

chatscripts

checkbox.d

compizconfig

computer-janitor.d

ConsoleKit

console-setup

couchdb

cron.d                          #cron配置文件

cron.daily

cron.hourly

cron.monthly

crontab

cron.weekly

crypttab

cups                            #cups配置

cvs-cron.conf

cvs-pserver.conf

dbconfig-common

dbus-1                         #输入法配置

debconf.conf

debian\_version

default

defoma

deluser.conf

depmod.d

dhcp3

dictionaries-common

doc-base

dpkg                           #dpkg配置

eioXpack

emacs

environment               #环境参数

esound

Evermore

firefox

firefox-3.0

fonts                          #字体配置

foomatic

fstab                          #默认文件系统加载

fuse.conf

gai.conf

gamin

gconf

gdb

gdm

gimp

gnome

gnome-app-install

gnome-system-tools

gnome-vfs-2.0

gnome-vfs-mime-magic

gre.d

groff

group

group-

grub.d

gshadow                       #组密码配置

gshadow-

gtk-2.0

hal

hdparm.conf

host.conf            

hostname                      #计算机名

hosts                            #IP地址对应

hosts.allow                    

hosts.deny

hp

ifplugd

init

init.d

initramfs-tools

inputrc

insserv

insserv.conf

insserv.conf.d

iproute2

issue                           #登录提示

issue.net                     #网络登录提示

.java

java-6-openjdk

kbd

kernel

kernel-img.conf

kerneloops.conf

ldap

ld.so.cache

ld.so.conf

ld.so.conf.d

legal

lftp.conf

libpaper.d

locale.alias

localtime

logcheck

login.defs

logrotate.conf            #轮替配置

logrotate.d                #轮替包含文件

lsb-base

lsb-base-logging.sh

lsb-release

ltrace.conf

magic

magic.mime

mailcap

mailcap.order

manpath.config

menu

menu-methods

mime.types

mke2fs.conf

modprobe.d

modules

mono

motd

mplayer

mtab                         #所有加载的文件系统记录

mtab.fuselock

mtools.conf

mysql

nanorc

netscsid.conf

network

NetworkManager

networks

nsswitch.conf

obex-data-server

ocsinventory

openal

openoffice

opt

pam.conf

pam.d

pango

papersize

passwd                      #系统账户

passwd-

pcmcia

perl

php5

pm

pnm2ppa.conf

polkit-1

popularity-contest.conf

ppp

profile

profile.d

protocols

pulse

purple

.pwd.lock

python

python2.6

rc0.d                          #系统启动时要开启的服务

rc1.d

rc2.d

rc3.d

rc4.d

rc5.d

rc6.d

rc.local

rcS.d

request-key.conf

resolvconf

resolv.conf                  #DNS配置

rmt

rpc

rsyslog.conf

rsyslog.d

samba                        #共享配置

sane.d

screenrc

securetty

security

sensors3.conf

sensors.d

services                        #服务端口记录

sgml

shadow                         #密码记录文件

shadow-

shells                            #系统所有的shell

skel                               #预配置目录

sound

speech-dispatcher

ssh                                #ssh配置

ssl

sudoers                          #sudo权限设置

sudoers.d

su-to-rootrc

sysctl.conf

sysctl.d

sysstat

terminfo

thnuclnt

thunderbird                     #邮箱配置

timezone

timidity

ts.conf

ucf.conf

udev

ufw                               #ufw防火墙配置

updatedb.conf

update-manager

update-motd.d

update-notifier

vga

vim                               #vi配置

vlc                                #影音软件VLC配置

vmware                        #vmware配置

vmware-installer           #vmware-tools文件

vmware-vix

w3m

wgetrc

wildmidi

wodim.conf

wpa\_supplicant

X11                              #XWINDOW配置

xdg

xml

xul-ext

xulrunner-1.9.2

zsh\_command\_not\_found