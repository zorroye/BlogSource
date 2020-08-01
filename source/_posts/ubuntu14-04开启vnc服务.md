---
title: ubuntu14.04开启vnc服务
tags:
  - 未分类
id: '277'
date: 2012-10-30 14:40:00
---

  
参考：http://broderick-tech.com/vncxstartup-files-ubuntu-14-04/  
ubuntu14.04操作：前面的步骤跟ubuntu10.04一样的，只需要改一改xstartup即可  

#!/bin/sh  
def  
export XKL\_XMODMAP\_DISABLE=1  
unset SESSION\_MANAGER  
unset DBUS\_SESSION\_BUS\_ADDRESS  
   
gnome-panel &  
gnome-settings-daemon &  
metacity &  
nautilus &  
gnome-terminal &  
  

效果  

![ubuntu14.04开启vnc服务 - leaf - ------勤解万难------](http://img2.ph.126.net/5w9tvL6jeHMrOgSmaN2J_Q==/6598112103739446374.png "ubuntu14.04开启vnc服务 - leaf - ------勤解万难------")

   
  
  
  
  
备注：一般我们都用ssh连接  
  
实验配置：  
服务器：ubuntu10.04 X86，win7  
客户端：ubuntu10.04 X64  
  
客户端：  

> 安装命令：sudo apt-get install vncviewer  
> 连接命令：vncviewer  172.16.43.135:1    #连入ubuntu  
> 
> > > vncviewer  172.16.43.135       #连入win7  

  
win7服务端：  

> 加密选项：设置为：更喜欢打开  
> 这是为了防止：No configured security type is supported by 3.3 viewer  

  
ubuntu服务器端：  

> 安装：sudo apt-get install vnc4server  

> 当前用户输入：  
> 
> > vnc4server  :1  
> > 输入密码  
> 
> 会建立.vnc目录：passwd  xstartup  ywz-desktop:1.log  ywz-desktop:1.pid  

> xstartup默认配置如下：  

> #!/bin/sh  
> \# Uncomment the following two lines for normal desktop:  
> \# unset SESSION\_MANAGER  
> \# exec /etc/X11/xinit/xinitrc  
> \[ -x /etc/vnc/xstartup \] && exec /etc/vnc/xstartup  
> \[ -r $HOME/.Xresources \] && xrdb $HOME/.Xresources  
> xsetroot -solid grey  
> vncconfig -iconic &  
> x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &  
> x-window-manager &

1、修改配置：  

> 修改配置的目的：能进图形界面，而不是字符界面  
> 也为了解决：could not acquire name on session bus  

> #!/bin/sh  
> \# Uncomment the following two lines for normal desktop:  
> unset SESSION\_MANAGER  
> exec /etc/X11/xinit/xinitrc  
> \[ -x /etc/vnc/xstartup \] && exec /etc/vnc/xstartup  
> \[ -r $HOME/.Xresources \] && xrdb $HOME/.Xresources  
> #xsetroot -solid grey  
> #vncconfig -iconic &  
> #x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &  
> #x-window-manager &

  
2、修改/etc/X11/xinit/xinitrc权限：sudo chmod a+x /etc/X11/xinit/xinitrc  
3、设置防火墙：  

> netstat -tunlp  
> 
> > tcp        0      0 0.0.0.0:6001            0.0.0.0:\*               LISTEN      5080/Xvnc4             
> > tcp6      0     0 :::5901                      :::\*                        LISTEN      5080/Xvnc4    
> 
> sudo ufw allow from 172.16.43.100 to any port 5901  

  
4、然后重启vnc4server  

> vnc4server -kill :1  
> vnc4server :1      #:1表示开启第一个界面  

  
5、开机自启动vnc服务  
sudo gedit  /etc/init.d/vncserver  

> `#!/bin/sh -e  
> ### BEGIN INIT INFO  
> # Provides:          vncserver  
> # Required-Start:    networking  
> # Default-Start:     3 4 5  
> # Default-Stop:      0 6  
> ### END INIT INFO`
> 
> `PATH="$PATH:/usr/X11R6/bin/"`
> 
> `# The Username:Group that will run VNC  
> export USER="使用哪个账户来远程连接"  
> #${RUNAS}`
> 
> `# The display that VNC will use  
> DISPLAY="1"`
> 
> `# Color depth (between 8 and 32)  
> DEPTH="24"`
> 
> `# The Desktop geometry to use.  
> #GEOMETRY="<WIDTH>x<HEIGHT>"  
> GEOMETRY="800x600"  
> #GEOMETRY="1024x768"  
> #GEOMETRY="1280x1024"`
> 
> `# The name that the VNC Desktop will have.  
> NAME="vnc-server"`
> 
> `OPTIONS="-name ${NAME} -depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"`
> 
> `. /lib/lsb/init-functions`
> 
> `case "$1" in  
> start)  
> log_action_begin_msg "Starting vncserver for user '${USER}' on localhost:${DISPLAY}"  
> su ${USER} -c "/usr/bin/vnc4server ${OPTIONS}"  
> ;;`
> 
> `stop)  
> log_action_begin_msg "Stoping vncserver for user '${USER}' on localhost:${DISPLAY}"  
> su ${USER} -c "/usr/bin/vnc4server -kill :${DISPLAY}"  
> ;;`
> 
> `restart)  
> $0 stop  
> $0 start  
> ;;  
> esac`
> 
> `exit 0`
> 
>   

`sudo chmod +x /etc/init.d/vncserver  
``sudo update-rc.d vncserver defaults`  
  
  
参考：  
http://www.linuxidc.com/Linux/2011-10/46228.htm  
http://www.abdevelopment.ca/blog/start-vnc-server-ubuntu-boot  
  

![ubuntu开启vnc服务 - leaf - ------坚持雅操------](http://img8.ph.126.net/s4wmt5pmV-QYi5ZwIq8wvg==/6597163225146148528.jpg "ubuntu开启vnc服务 - leaf - ------坚持雅操------")