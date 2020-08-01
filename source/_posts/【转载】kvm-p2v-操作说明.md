---
title: 【转载】kvm p2v 操作说明
tags:
  - 未分类
id: '303'
date: 2016-04-18 22:40:00
---

  
转载自：  
http://xiaoli110.blog.51cto.com/1724/1552723  
  
说明：  

> 先转换成IDE硬盘方式，恢复完后再通过添加virtio硬盘将驱动转换掉，  

> 这样不容易蓝屏。  
>   

1、操作前的准备工作很重要  

> 清空垃圾站；  
> 删除不需要的软件；  
> 清空各种缓存文件，尤其是浏览器的  
>   

2、转换成IDE硬盘格式操作  

> 导入注册表  

> Windows Registry Editor Version 5.00\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\primary\_ide\_channel\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="atapi"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\secondary\_ide\_channel\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="atapi"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\\*pnp0600\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="atapi"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\\*azt0502\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="atapi"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\gendisk\]"ClassGUID"="{4D36E967-E325-11CE-BFC1-08002BE10318}""Service"="disk"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#cc\_0101\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_0e11&dev\_ae33\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1039&dev\_0601\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1039&dev\_5513\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1042&dev\_1000\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_105a&dev\_4d33\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0640\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0646\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0646&REV\_05\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0646&REV\_07\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0648\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1095&dev\_0649\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1097&dev\_0038\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_10ad&dev\_0001\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_10ad&dev\_0150\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_10b9&dev\_5215\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_10b9&dev\_5219\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_10b9&dev\_5229\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="pciide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_1106&dev\_0571\]"Service"="pciide""ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_1222\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_1230\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_2411\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_2421\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_7010\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_7111\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide"\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CriticalDeviceDatabase\\pci#ven\_8086&dev\_7199\]"ClassGUID"="{4D36E96A-E325-11CE-BFC1-08002BE10318}""Service"="intelide";Add driver for Atapi (requires Atapi.sys in Drivers directory)\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\atapi\]"ErrorControl"=dword:00000001"Group"="SCSI miniport""Start"=dword:00000000"Tag"=dword:00000019"Type"=dword:00000001"DisplayName"="Standard IDE/ESDI Hard Disk Controller""ImagePath"=hex(2):53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,44,00,\\   52,00,49,00,56,00,45,00,52,00,53,00,5c,00,61,00,74,00,61,00,70,00,69,00,2e,\\   00,73,00,79,00,73,00,00,00;Add driver for intelide (requires intelide.sys in drivers directory)\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\IntelIde\]"ErrorControl"=dword:00000001"Group"="System Bus Extender""Start"=dword:00000000"Tag"=dword:00000004"Type"=dword:00000001"ImagePath"=hex(2):53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,44,00,\\   52,00,49,00,56,00,45,00,52,00,53,00,5c,00,69,00,6e,00,74,00,65,00,6c,00,69,\\   00,64,00,65,00,2e,00,73,00,79,00,73,00,00,00;Add driver for Pciide (requires Pciide.sys and Pciidex.sys in Drivers directory)\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\PCIIde\]"ErrorControl"=dword:00000001"Group"="System Bus Extender""Start"=dword:00000000"Tag"=dword:00000003"Type"=dword:00000001"ImagePath"=hex(2):53,00,79,00,73,00,74,00,65,00,6d,00,33,00,32,00,5c,00,44,00,\\   52,00,49,00,56,00,45,00,52,00,53,00,5c,00,70,00,63,00,69,00,69,00,64,00,65,\\   00,2e,00,73,00,79,00,73,00,00,00  
> 
> 下载驱动到windows\\system32\\driver目录下  
> 用ghost备份  
>   

3、还原  

>   

>