---
title: USB量产操作
tags:
  - Udisk
categories:
  - Hardware
  - Udisk
id: '168'
abbrlink: 2647626534
date: 2011-08-30 17:17:00
---

以下全部按照 [数码之家](http://bbs.mydigit.cn/) 里介绍的进行操作

买了一款 pny-m1-8G的U盘，准备做光驱用，这样就不用买光驱了

方法有2种：1、UltraISO      2、对USB进行底层设置

\---------------------------------------------------------------------------------------------------------------------

我买的pny m1 详细信息：

芯片是：SMI SM3255AB 的

![USB量产 - leaf - ------坚持雅操------](http://img.ph.126.net/YJlXLQdXDVuMgJ5Vb_-P3Q==/2742973648062255091.jpg "USB量产 - leaf - ------坚持雅操------")

用量产工具检测出flash型号，并用闪存精灵检查出闪存的参数如下：

![USB量产 - leaf - ------坚持雅操------](http://img.ph.126.net/Ogwg3oMmUVw5fryb5Y7bhA==/2490772068929505785.jpg "USB量产 - leaf - ------坚持雅操------")

\---------------------------------------------------------------------------------------------------------------------

软件：

MyDiskTest V2.93｜U盘扩容检测/速度测试工具 [http://dl.mydigit.net/2010/09/mydisktest.html](http://dl.mydigit.net/2010/09/mydisktest.html)

ChipGenius芯片精灵V3.01｜USB主控芯片检测工具 ：[http://www.mydigit.cn/chipgenius.htm](http://www.mydigit.cn/chipgenius.htm) 

SMI3255AB最新量产工具SM32x\_K0530\_SM3255AB\_(v2.03.42  )

[http://bbs.mydigit.cn/read.php?tid=290932](http://bbs.mydigit.cn/read.php?tid=290932)

FlashGenius V3.5｜闪存精灵/FLASH参数查询 [http://dl.mydigit.net/2010/09/FlashGenius.html](http://dl.mydigit.net/2010/09/FlashGenius.html)

\-----------------------------------------------------------------------------------------------------------------------

量产操作：

1、第一次量产操作

按照这个一步一步操作即可

 [慧荣SM321~SM3257 量产CDROM成功 全文图解](http://bbs.mydigit.cn/read.php?tid=211490)

[一看就会，smi32x量产详细图示教程(已添加说明文字）](http://bbs.mydigit.cn/read.php?tid=46874)

做好后我看跳出来说要格式化，然后就格式化了，格了之后才知道错了。。。把光驱格成空了。(本来直接拔出来，再插即可)

2、然后工程调试，把权限分出去的盘清除掉

参考 [预防及解决“SMI方案量产CDROM后，再次量产引起无法识别出盘符问题”](http://bbs.mydigit.cn/read.php?tid=107138)

点-tools-multiple erase all 清除

清除后拔出内存再插虽然能显示USB，却显示0M空间，我郁闷了。。。。

而且setting也不能操作

3、重做量产操作，然后直接拔掉U盘，再插上，搞定

这时，setting可以重新设置，跟第一步是一样的，做好后就是你想要的U盘了

![USB量产操作 - leaf - ------坚持雅操------](http://img.ph.126.net/Oj36vbdG1tsPwPUN9FdXZg==/3098758018624523789.jpg "USB量产操作 - leaf - ------坚持雅操------")

其他：[SMI方案U盘不识别盘后安装工厂驱动详细步骤](http://bbs.mydigit.cn/read.php?tid=117966)