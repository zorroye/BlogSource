---
title: '[转载] A卡、N卡、还是 I 卡？'
tags:
  - base
categories:
  - Ubuntu
  - Q&A
id: '22'
abbrlink: 770010477
date: 2011-01-19 10:57:00
---

　　对于 Linux 新手来说，由于对 Linux 平台上显卡驱动支持不是很了解，所以可能会在选择显卡品牌时无从下手。而 Ubuntu Gamer 上这篇文章，则用简明的语言阐述了 Nvidia ， AMD/ATI 及 Intel 这三种最普遍的品牌显卡在 Linux 平台上的驱动现状，我简单翻译了一下，希望对你有所帮助。  
  
　　**－ Nvidia**  
  
　　除了提供最基本的仅支持 2D 的开源驱动（用于各个发行版的内置驱动，现在已经被 Nouveau 驱动所取代）外，基本上 Nvidia 只提供闭源驱动。但闭源驱动的性能非常好，与 Windows 上的性能几乎差不多。而且 Nvidia 的驱动更新很频繁，有些会每月更新一次。而且他们还会使用 VDPAU 加速 API 来提供快速视频加速，这个加速 API 功能仅被当前最新的 Adobe Flash beta 支持。所以，如果你经常观看全屏高清视频的话，一块 Nvidia 显卡加上他们的驱动应该是最佳方案了。  
  
　　但不幸的是，闭源的 Nvidia 也存在着不好的一面，主要一点是 Nvidia 至今（已经有好几年了）还不支持 Xrandr 协议，Xrandr 协议可以允许 X 来调整显示分辨率，或者扩展/克隆到外部显示器。如果你正在使用 Nvidia 显卡的话，这就是不能用 Ubuntu 自带的屏幕分辨率工具来调整分辨率的原因了。另外，有些软件需要依赖 Xrandr 的输出信息在显示器中进行定位，所以某些出错原因也是归纠于此。另一点就是 Nivida 的闭源驱动不支持内核模式设置 （ kernel mode setting – KMS) ，因此就无法提供高清晰的 Plymouth 启动显示画面（当然这个情况应该说存在于所有的闭源驱动中）。  
  
　　在开源的 Nouveau 驱动项目方面，利用逆向工程开发出了支持 2D 和 3D 的 Nvidia 驱动，并取得了极大的进展。但与闭源的驱动相比，在性能上要相差很多，不过还是足以运行一些简单的游戏。而且还有一点有必要提醒的是，目前 Nvidia 方面也没有任何要帮助 Nouveau 项目的意图。  
  
　　**－ AMD/ATI**  
  
　　在 AMD 收购 ATI 之前，可以说在 Linux 上基本没有像样的 ATI 驱动。不过自从被 AMD 收购后，情况就变得大为不同。ATI 的闭源 Linux 驱动有了跨越式的发展，而且还支持 Xrandr 协议，这样你就可以完全使用 Ubuntu 内置分辨率调整工具了。而且在性能方面也非常好，也可以与 Wine 一起很好的工作。另外，AMD 也与 Canonical 共同合作，在每一个 Ubuntu 发行版中都会得到预发布的驱动。当然有一点与 Nividia 驱动相似的，那就是也不支持 KMS 。闭源的 AMD 驱动使用与 Nvidia 不同的视频 API ，而是唤作的 VA-API，不幸的是 Adobe 目前至今还没有支持它，所以基于 Flash 的高清视频受到一定的影响。另外与 Nvidia 相比欠缺的一点是，AMD 驱动需要花费更多的时间来支持新版内核及新的 X Server 版本，但对于 Ubuntu 用户来说并不是问题，因为它会默认搭载在 Ubuntu 发行版中。  
  
　　在开源方面，AMD 也表现完美，不仅会发布卡的规格详情给开源社区，同时还聘请人员全职工作于开源驱动的开发。此驱动目前正在经历过渡到新的 Gallium3D 框架，但已接近完成，从现在起我们可以看到这些驱动的性能有了极大的改善。基本上，如果你拥有一块 AMD 卡的话，在 Ubuntu 上就可以用到 3D 加速功能。虽然性能也许不如闭源驱动，但如果你想安装闭源驱动的话，那也只是点一下鼠标的事情。所以说， AMD 在 Linux 驱动方面确实贡献卓越，大赞！  
  
　　Update \[2011.1.12\] : 根据 Phoronix 的报道， VIA 的 KMS 支持代码已接近完成。  
  
　　**－ Intel  
**  
　　可以说， Intel 是开源 Linux 图形卡驱动方面的王者，他们只发布 Linux 平台上的开源驱动，这也意味着你能体验到像 KMS 及 Xrandar 支持这样的所有功能。但 Intel 也并不完美，如果你拥有一块基于 GMA500 的卡的话，它基本上无法工作于 Ubuntu 上，因为这是英特尔购买了其他公司的芯片组后并更名了它，而且他们也不能为其开发开源驱动，虽然目前英特尔还在解决此问题。  
  
　　Intel 的另外一个最大缺点是他们的硬件性能远远不如 AMD 和 Nvidia ，并且对于游戏支持也不够好。  
  
　　**－总结**  
  
　　如果对于你来说有开源驱动是非常重要的事，那么你可以用 Intel 或 AMD 的卡；如果你更关注性能，那么你可以用 AMD 或 Nvidia 的卡。总的来说， AMD/ATI 是更加前沿，更加值得推荐，因为他们在提供稳定开源驱动的同时，还提供了可靠快速的闭源驱动，堪称两全其美。  
  
原文出处：http://wowubuntu.com/nvidia-ati-intel.html