---
title: CONKY配置
tags:
  - 未分类
id: '25'
abbrlink: 77642516
date: 2011-03-19 15:35:00
---

![CONKY配置 - leaf - ------坚持雅操------](http://img128.ph.126.net/B6XKezhP09_iTUMhkmgO3A==/1621858815808469013.jpg "CONKY配置 - leaf - ------坚持雅操------")

 备注：有几个字体要下载的  
  

#http://conky.sourceforge.net/docs.html

#http://forum.ubuntu.org.cn/viewtopic.php?f=33&t=173214

#全局设置---------------------------------------------------------------------------

cpu\_avg\_samples         1   #监控几个CPU状况

net\_avg\_samples         1   #监控几个网络状况

double\_buffer         yes   #双倍缓存，用Ubuntu，不想看闪屏就这样写

no\_buffers            yes   #使用内存缓冲区

update\_interval       1.0   #定时更新时间,以秒为单位，Conky需要定时读取系统状态

total\_run\_times         0   #开起来之后一直运行

  

background            yes   #是否嵌入桌面

override\_utf8\_locale  yes   #强制用UTF8解码，谁都不想看乱码

out\_to\_console         no   #是否将Conky出错情况输出到终端

  

minimum\_size        170 5   #设定Conky的长宽，最小宽度为170像素，最小高度为5像素

maximum\_width         170   #设定Conky的长宽，最大宽度为170像素

default\_shade\_color   black #默认底纹颜色和边框的颜色底纹

default\_outline\_color white #默认轮廓色

  

use\_xft                yes  #指示conky用x字体，这样才能调用你安装的字体

xftalpha               0.1  #Alpha of Xft font  ??

xftfont Bitstream Charter:bold:size=9  #定义默认字体

default\_color        white  #定义默认字体颜色

uppercase               no  #如果值设为“yes”则所有输出的文字都变成大写字母

use\_spacer            none  #???

#全局设置---------------------------------------------------------------------------

  

  

#窗体设置---------------------------------------------------------------------------

own\_window              yes  #自己的窗口，这样可以不闪

own\_window\_transparent  yes  #背景透明

own\_window\_type    override  #不受WM控制

own\_window\_hints undecorated,below,sticky,skip\_taskbar,skip\_pager  

    #不装饰窗口（我们定义了他是个独立的窗口），

    #永远在根窗口上（也就是屏幕），

    #粘滞起来（不能让他乱跑）

    #无视一切1，无视一切2

#窗体设置---------------------------------------------------------------------------

  

  

#边框设置---------------------------------------------------------------------------

draw\_borders            no   #不要边框，当然个人喜好 

border\_margin            0   #边框宽度 0

draw\_graph\_borders      no   #不要边框图标      

draw\_shades             no   #字体绘制阴影

draw\_outline            no   #不要下划线

#边框设置---------------------------------------------------------------------------

  

  

#位置设置---------------------------------------------------------------------------

#alignment        top\_left   #设置最开始的位置

#alignment      top\_middle

alignment        top\_right        

#alignment     bottom\_left

#alignment   bottom\_middle

#alignment    bottom\_right

#alignment            none

gap\_x                    0   #相对屏幕边界的位置调横向位移，这里是相对屏幕右上方调位置

gap\_y                   26   #相对屏幕边界的位置调纵向位移，这里是相对屏幕右上方调位置

#位置设置---------------------------------------------------------------------------

  

  

  

###——功能模块备份——###

  

#图表显示硬盘实时读写状况--------------------------------------------------------------

#${color }Disk Read:${alignr}${color}$diskio\_read

#${color}${diskiograph\_read /dev/sda 10,160 000000 ffffff}

#${color }Disk Write:${alignr}${color}$diskio\_write

#${color}${diskiograph\_write /dev/sda 10,160 000000 ffffff}

  

#显示显卡型号------------------------------------------------------------------------

#Video Card: ${color #cdc8b1}${execi 20 glxinfo | grep "OpenGL renderer" | cut -c 25-39}

#GPUtemp:${execi 20 nvidia-settings -q gpucoretemp | grep "Attribute" | cut -d" " -f6 | cut -c -2} °C

#nvidia-settings -q gpucoretemp

  

#显示系统信息------------------------------------------------------------------------

#${font Microsoft YaHei:size=10}${color #F6E80C}主机:${font Bitstream Charter:bold:size=9}${color #c0ff3e} $alignr$nodename

#${font Microsoft YaHei:size=10}${color #F6E80C}用户: ${font Bitstream Charter:bold:size=9}${color #c0ff3e} $alignr${execi 9999 whoami}

  

###——功能模块备份——###

#${font}:设字体

#${color}:设字体颜色

#${offset}:横向偏移，+向右

#${voffset}：纵向偏移，+向下

#${execi}:运行外部命令

  

  

#功能设置----------------------------------------------------------------------------

TEXT

${color }$stippled\_hr

${font Bitstream Charter:bold:size=10}${color #F6E80C}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=CN}

${font Weather:size=44}${color gold}${offset 16}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=WF}

${font Microsoft YaHei:bold:size=9}${color #ffe7ba}${voffset -96}${offset 90}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=CC}

${font Bitstream Charter:bold:size=9}${color #ffe7ba}${offset 90}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=HT}

${font Bitstream Charter:bold:size=9}${color #ffe7ba}${offset 90}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=WS}${font Arrows:size=10}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=BF}

${font Microsoft YaHei:size=9}${color #ffe7ba}${offset 12}白天时间: ${color #ffe7ba}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=SR}-${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=SS}

${font Microsoft YaHei:bold:size=9}${color #F6E80C}${offset 15}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=DW --startday=1 --endday=4 --spaces=3 --shortweekday}

${font Weather:size=26}${color white}${offset 16}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=WF --startday=1 --endday=4 --spaces=0}

${font Weather:size=16}${color white}${voffset -20}z${font}:${color white}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=HT --startday=1 --endday=4 --spaces=5}

${font Weather:size=16}${color white}i${font}:${color white}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=PC --startday=1 --endday=4 --spaces=4}

${font Weather:size=16}${color white}v${font}:${color white}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=WS --startday=1 --endday=4 --spaces=1}

${font Arrows:size=10}${color gold}${voffset -15}${offset 38}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=BF --startday=1 --endday=1 --spaces=0}${offset 27}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=BF --startday=2 --endday=2 --spaces=0}${offset 30}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=BF --startday=3 --endday=3 --spaces=0}${offset 22}${execi 3600 python ~/.conky-rc/conkyForecast.py --location=CHXX0044 --datatype=BF --startday=4 --endday=4 --spaces=0}${font}${color}

${stippled\_hr 1}

${font Microsoft YaHei:size=9}${color #F6E80C}系统: ${font Bitstream Charter:bold:size=9}${color #c0ff3e} $alignr${execi 99999 lsb\_release -d -s -c | tr -s "\\n" " "}

${font Microsoft YaHei:size=9}${color #F6E80C}内核: ${font Bitstream Charter:bold:size=9}${color #c0ff3e}$alignr$kernel

${font Microsoft YaHei:size=9}${color #F6E80C}用时: ${font Bitstream Charter:bold:size=9}${color #c0ff3e}$alignr$uptime

${color }$stippled\_hr

${font Microsoft YaHei:size=9}${color #F6E80C}CPU温度:${font Bitstream Charter:bold:size=9}${color #c0ff3e}$alignr${acpitemp}°C

${color white}CPU us:$alignr${color } $cpu% 

${cpubar 4}

${color white}MEM:${color} $mem/$memmax$alignr$memperc%

${membar 4}

${color white}SWAP:${color} $swap/$swapmax$alignr$swapperc%

${swapbar 4}

${color }$stippled\_hr

${font Microsoft YaHei:size=9}${color #F6E80C}进程:${font Bitstream Charter:bold:size=9}${color #c0ff3e}$alignr$processes  ($running\_processes running)

${color #ffe7ba}Top Processes$alignr   CPU%  MEM%$color

${top name 1}${color #FB0808}$alignr${top cpu 1}   ${top mem 1}$color

${top name 2}${color #F6620C}$alignr${top cpu 2}   ${top mem 2}$color

${top name 3}${color #F6E80C}$alignr${top cpu 3}   ${top mem 3}$color

${top name 4}${color #08CB2F}$alignr${top cpu 4}   ${top mem 4}$color

${top name 5}${color #0DBCCE}$alignr${top cpu 5}   ${top mem 5}$color

${top name 6}${color #2758CF}$alignr${top cpu 6}   ${top mem 6}$color

${top name 7}${color #8A11CB}$alignr${top cpu 6}   ${top mem 7}$color

${color }$stippled\_hr

${font Microsoft YaHei:size=9}${color #F6E80C}硬盘温度:${font Bitstream Charter:bold:size=9}${color #c0ff3e}$alignr${hddtemp /dev/sda}°C

${color white}Boot: ${alignr}${fs\_free /boot} / ${fs\_size /boot}

${fs\_bar 4 /boot}

Root: ${alignr}${fs\_free /} / ${fs\_size /}

${fs\_bar 4 /}

Home: ${alignr}${fs\_free /home} / ${fs\_size /home}

${fs\_bar 4 /home}

Usr: ${alignr}${fs\_free /usr} / ${fs\_size /usr}

${fs\_bar 4 /usr}

Var: ${alignr}${fs\_free /var} / ${fs\_size /var}

${fs\_bar 4 /var}

Tmp: ${alignr}${fs\_free /tmp} / ${fs\_size /tmp}

${fs\_bar 4 /tmp}

${color }$stippled\_hr

${font Microsoft YaHei:size=9}${color #F6E80C}WAN地址:${font Bitstream Charter:bold:size=9}${color #c0ff3e} $alignr${execi 3600 wget -O - http://whatismyip.org/ | tail}

${font Microsoft YaHei:size=9}${color #F6E80C}IP地址:${font Bitstream Charter:bold:size=9}${color #c0ff3e} ${alignr} ${addr eth0}

${downspeedgraph eth0 25,80 556B2F 9ACD32}${alignr}${upspeedgraph eth0 25,80 556B2F 9ACD32}

${voffset -30}${font Microsoft YaHei:size=8}${color #F6E80C}down:${font Bitstream Charter:bold:size=9}${color white}${downspeed eth0}k/s${alignr}${font Microsoft YaHei:size=8}${color #F6E80C}up:${font Bitstream Charter:bold:size=9}${color white}${upspeed eth0}k/s

${voffset 5}${font Microsoft YaHei:size=8}${color #F6E80C}Total:${font Bitstream Charter:bold:size=9}${color white}${totaldown eth0}${alignr}${font Microsoft YaHei:size=8}${color #F6E80C}Total:${font Bitstream Charter:bold:size=9}${color white}${totalup eth0}

${color }$stippled\_hr