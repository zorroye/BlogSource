---
title: kvm下激活win2012
tags:
  - 未分类
id: '302'
abbrlink: 111771363
date: 2016-04-16 22:10:00
---

总体思路是改BIOS，然后激活  
参考：  
http://zhidao.baidu.com/link?url=CoAMwyW3Bpl4l0kODMu-BqA4YlTHqhdW\_kTfd9PKZ8oaTuySxBawbt39CWtNLO76SaPOAYGrqzHkXfbjyrcRE70H76BEQDs6kz7\_kjvD6P3  
  
  
0、所需文件  

> DELL\[PE\_SC3\]2.2.7z  
> seabios-1.9.1.tar.gz (我用1.7.2.3版有错误，1.9.1是当前最新版)  
>   

1、实验环境  

> 宿主机：centos7.2  
> 虚拟机：win2012  
>   

2、BIOS制作说明  

> 解压DELL\[PE\_SC3\]2.2.7z 并将DELL-SLIC.bin文件放到随便哪个目录下。(如/opt/)  
> tar -xvf seabios-1.9.1.tar.gz  
> yum -y install git iasl      #安装依赖包  
> mkdir bios  
> cd bios  
> git clone git://github.com/ghuntley/seaslic  
> cd seaslic  
> rmdir seabios.submodule  
> mv seabios-1.9.1 seabios.submodule       
> #将下载的seabios放到seaslic目录下并改名为seabios.submodule  
> cd seabios.submmodule  
> make distclean  
> cd ..  
> nano patch.sh  
> 
> > 将xxd这行的/sys改成DELL-SLIC.bin存放位置  
> > 备注：xxd这行是把slic文件转换为c语言格式  
> > 
> > ![kvm下激活win2012 - leaf - ------勤解万难------](http://img2.ph.126.net/vHqZkuK1gyxpMo9glz3rTw==/6598196766136289105.png "kvm下激活win2012 - leaf - ------勤解万难------")
> > 
> >  
> 
> ./patch.sh    #然后直接运行就行  
> 备注：seabios.patch就是打了如下三处补丁
> 
> ![kvm下激活win2012 - leaf - ------勤解万难------](http://img1.ph.126.net/LnPUW6l-gqrZID6HmrtZag==/6598128596415370666.png "kvm下激活win2012 - leaf - ------勤解万难------")
> 
> \--------BIOS制作完毕--------  
> 将./seabios.submodule/out/bios.bin 替换掉/usr/share/seabios/bios.bin  
> 重启宿主机  
>   

3、安装win2012  

> virt-install --name=win2012-lvm --ram=4096 --vcpus=4 --os-type=windows  --hvm \\  
> \--cdrom=/home/ywz/iso/win2012.iso \\  
> \--file=/dev/kvmvg/kvmlvm \\  
> \--network bridge=br0  \\  
> \--vnc --vncport=5992 --vnclisten=0.0.0.0 --force --autostart  
> 
> ![kvm下激活win2012 - leaf - ------勤解万难------](http://img0.ph.126.net/JrPU0VFLQBpJRkZe-hfrCA==/1629458640279273318.png "kvm下激活win2012 - leaf - ------勤解万难------")
> 
>   

4、导入DELL证书  

> slmgr -ilc DELL2.2.XRM-MS  
> 
> ![kvm下激活win2012 - leaf - ------勤解万难------](http://img2.ph.126.net/U-LMLd6m0hC-Icc1Eeqb_Q==/1993968735119613899.png "kvm下激活win2012 - leaf - ------勤解万难------")
> 
>   

5、填入注册号激活  

> ![kvm下激活win2012 - leaf - ------勤解万难------](http://img2.ph.126.net/zJrnz8iDWIFgVVq_eKurag==/6598085715461889824.png "kvm下激活win2012 - leaf - ------勤解万难------")

  

>