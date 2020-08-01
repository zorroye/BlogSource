---
title: msi EX465安装MACOSX 其他
tags:
  - 未分类
id: '249'
date: 2013-12-11 12:28:00
---

PCI configuration begin

> 测试：替换AppleACPIPlatform 和 IOPCIFamily
> 
> 10.6 3-7 可行，10.6.8不可用
> 
> 10.7 dp1可行， dp2-4不可用
> 
> 10.7                     0-5 不可用
> 
> 10.8                  dp1-4不可用
> 
> 10.8                     0-2 不可用

  

电池驱动

> 直接用AppleACPIBatteryManager.kext 即可
> 
> http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1038183

  

> ![msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------](http://img1.ph.126.net/LTYvusqdY-kXe1evuGR9zg==/4938478466488554991.jpg "msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------")
> 
> ![msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------](http://img0.ph.126.net/Z9aGs6n4SDMrLFQtvDhH1A==/1689694285294383846.jpg "msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------")
> 
>   

触摸板

> 我的触摸板是synaptics touchpad6.2 版本的
> 
> 下载以下版本应该都可以，我还不怎么会用。
> 
> ![msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------](http://img0.ph.126.net/_DpcAlGdRoiYNzN5I0yhKA==/6597899897937354807.jpg "msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------")
> 
>  

> http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1399288
> 
> http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1104482
> 
> http://bbs.pcbeta.com/viewthread-1260111-1-1.html
> 
> http://bbs.pcbeta.com/viewthread-1155823-2-1.html

  

> 键盘位
> 
> ![msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------](http://img0.ph.126.net/Wqgaujby7h6L1XjfKpCAHA==/1384856885516706702.jpg "msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------")
> 
>  
> 
>  

亮度

> http://bbs.pcbeta.com/viewthread-825117-1-3.html

> http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=889877

> http://dell.benyouhui.it168.com/thread-4533070-1-1.html

> 我的按FN+方向键就能调亮度，只是没有亮度图标

> dsdt搜索Device (PWRB)，在其上面加上代码即可。

> > Device (PNLF)
> 
> > {

> > > Name (\_HID, EisaId ("APP0002"))
> 
> > > Name (\_CID, "backlight")
> 
> > > Name (\_UID, 0x0A)
> 
> > > Name (\_STA, 0x0B)

> > }
> 
> ![msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------](http://img0.ph.126.net/NOcTcpmWJMOj1-E6vVcjZw==/4844184349290525828.jpg "msi EX465安装MACOSX 其他 - leaf - ------坚持雅操------")
> 
>  
> 
> 亮度保存
> 
> 1、nvram -x -p > /Extra/nvram.plist
> 
> 2、复制rc.shutdown.local放到/etc下 (需要显示隐藏文件)

>  复制com.delta.nvram.set.plist放到/Library/launchDaemons/下 
> 
> 3、修复权限
> 
> 01.sudo chown 0:0 /Library/LaunchDaemons/com.delta.nvram.set.plist
> 
> 02.sudo chown 0:0 /private/etc/rc.shutdown.local
> 
>   
> 
> 备注：感觉还是上下键方便，亮度保存没试过。