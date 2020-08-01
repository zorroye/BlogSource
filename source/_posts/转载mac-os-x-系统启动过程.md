---
title: '[转载]Mac OS X 系统启动过程'
tags:
  - 未分类
id: '236'
date: 2013-03-13 08:21:00
---

转自：[http://nbbbs.zol.com.cn/24/544\_237379.html](http://nbbbs.zol.com.cn/24/544_237379.html)  
文章是07年的，有点旧  
  
启动过程：  
1、 电源开启。  
2、 执行固件中的代码。  
3、 收集硬件信息并初始硬件。  
4、 选择启动项（通常是选择 OS ，但有时会选择硬件测试等类似情况。）。用户可能会被提示进行启动选择。  
5、 控制权交给 /System/Library/CoreServices/BootX （启动引导器）。 BootX 载入内核并描绘 OS 标识（如有）。BootX 尝试载入先前缓存的设备驱动列表（根据 /usr/sbin/kextcache 进行创建或更新）。缓存的类型为 mkext 且为多内核扩展包含了信息词典（info dictionaries）与二进制文件。注意：如果 mkext 缓存丢失或损坏，BootX 将在 /System/Library/Extensions 中搜索当前方案中所需要的扩展（由该扩展包中 Info.plist 文件的 OSBundleRequired 属性值进行决定。）  
6、 执行内核中的 init 例程。决定要启动之系统的根设备。从此刻起，将不再使用固件中的程序。  
7、 由内核初始各种 Mach/BSD 数据结构。  
8、 初始 I/O （输入输出）设备。  
9、 内核开始运行 /sbin/mach\_init ，Mach 服务命名（引导程序）后台。mach\_init 为服务名和要准备访问其它服务所用的 Mach 端口提供映射。  
到这步时，启动开始转为用户等级：  
10、 mach\_init 开始 /sbin/init，传统的 BSD 初始化（init）进程。初始化将决定运行等级，并运行 /etc/rc.boot （设置让机器能够运行单用户－single user 模式）。  
在此步中，将执行： rc.boot 与其它 rc 脚本源程序 /etc/rc.common，一个包含实用功能的 shell 脚本，如 CheckForNetwork() （检查如网络已启动）， GetPID(), purgedir() （仅删除目录内容， 而非结构），等。  
11、 rc.boot 会显示要启动的类型（多用户，安全模式，光驱，网络等等）。网络启动的情况下（ sysctl 的变量 kern.netboot 将会为何种情况而设之为 1 ），其将用一个启动参数来运行 /etc/rc.netboot 。  
/etc/rc.netboot 会处理网络启动的参数特征。例如:执行网络和（如有）本地挂载。其还会呼叫 /usr/bin/nbst 来关联当作根设备使用的磁盘镜像到一个影子文件（shadow file）。此方法是将那个希望处于本地存储器的文件（磁盘）重定向写入到影子文件。  
12、 rc.boot 会在必须进行文件系统一致性检查（file system consistency check， fsck）时，显示图形。单用户模式和用光盘启动时不会运行 fsck。安全模式启动时总会运行 fsck。rc.boot 也会处理 fsck 的返回状态。  
13、 如果 rc.boot 成功退出， /etc/rc 多用户启动脚本将会运行。如果正在从一个光驱启动，脚本将切换到 /etc/rc.cdrom （安装）。  
14、 /etc/rc 挂载本地文件系统 (HFS+、HFS、UFS、/dev/fd、/.vol)，确保目录 /private/var/tmp 存在，然后运行 /etc/rc.installer\_cleanup 如果有（重启前，会由安装器离开）。  
15、 /etc/rc.cleanup 运行。其将“清理”一定数量的 Unix 与 Mac 特殊目录/文件。  
16、 启动缓存 （BootCache）开始。  
17、 各种 sysctl 变量被设置（如：vnodes 的最大值、System V IPC 等）。如果 /etc/sysctl.conf 已存在 (在 Mac OS X Server 中为 /etc/sysctl-macosxserver.conf)，它将读取和设置 sysctl 变量为已包含在其中的。  
18、 syslogd 开始。  
19、 创建机器检查符号文件（Mach symbol file）。  
20、 /etc/rc 开始 kextd 后台进程，用来从内核或委托进程 （client processes）加载所需的内核扩展。  
21、 /usr/libexec/register\_mach\_bootstrap\_servers 将运行以加载包含在 /etc/mach\_init.d 中的各种 Mach 引导程序所基于的服务。  
22、 portmap 与 netinfo 开始。  
23、 如 /System/Library/Extensions.mkext 旧于 /System/Library/Extensions， /etc/rc 将删除已存在的 mkext 并创建一个新的（不存在时，会创建）。  
24、 /etc/rc 启动 /usr/sbin/update，一个后台程序，用来频繁地清空磁盘上的互联网文件系统缓存。  
25、 /etc/rc 启动虚拟内存系统。 设置 /private/var/vm 为一个交换目录。/sbin/dynamic\_pager 以适当的参数启动（交换文件名路径模板、已创建的交换文件大小、当创建额外交换文件或删除已存在文件时，指定高、低水平的警报切换开关。）  
26、 /etc/rc 启动 /usr/libexec/fix\_prebinding 以修复错误地预连编二进制文件 （prebound binaries）  
27、 /etc/rc 执行 /etc/rc.cleanup 以清除并重置文件与设备。  
28、 /etc/rc 最后将启动 /sbin/SystemStarter ，处理启动项从下列位置： /System/Library/StartupItems 与 /Library/StartupItems。一个启动项是一个程序、一个 shell 脚本、匹配一个文件夹名的名称。文件夹包含一个属性列表文件含有一些配对的关键值，如： Deion、Provides、Requires、 OrderPreference、启动与停止信息等等。您可以运行 SystemStarter -n -D 以作为根用户 (root) 来进行程序打印调试与从属信息（不包含现在已经在运行的任何项目）。  
29、 CoreGraphics 启动开始 Apple 类型服务后台(ATSServer) 和 Window 服务器 (WindowServer)。  
默认下，loginwindow 程序 (loginwindow.app 位于 /System/Library/CoreServices 目录下) 已为控制设备执行。如果您不想运行到图形登录，可以修改 /etc/ttys 中相关的行。