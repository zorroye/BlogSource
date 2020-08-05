---
title: 2、mac启动过程
tags:
  - hackintosh
categories:
  - Hackintosh
  - base
id: '238'
abbrlink: 1407524629
date: 2013-03-20 20:46:00
---

  
白苹果的启动  
\--------------------  

> UEFI自检----->  
> 
> > SMC芯片验证和识别信息-------->  
> > 
> > > mac启动  

  
  
  
黑苹果的启动  
\--------------------  

> UEFI自检----->  
> 
> > 变色龙引导----->  
> > 
> > > 变色龙读取配置文件org.apple.Boot.plist----->  
> > > 
> > > > 解压核心--->  
> 
> > > > > 变色龙读取DSDT.aml------->  
> > > > > 变色龙调用SMBIOS添加机型信息------->  
> 
> > > > > 变色龙调用FakeSMC添加模拟的BIOS信息和硬件信息----->  
> > > 
> > > > > > 变色龙调用DSDT.aml并添加硬件信息--->  
> > > > > > 
> > > > > > > 变色龙调用SSDT.aml并应用------>  
> > > > > > > 
> > > > > > > > 核心加载模块--------->  
> > > 
> > > > > > > > > mac启动  

>   

#这里我们可以看到，我们直接修改FakeSMC就可以使mac识别，如果不改FakeSMC则可以添加DSDT等使mac识别  
  
  
  
附变色龙引导log  
\--------------------  
Chameleon 2.2svn (svn-r2187) \[2013-02-21 13:57:37\]  
msr(383): platform\_info 60011f00  
msr(387): flex\_ratio 00000000  
Sticking with \[BCLK: 103Mhz, Bus-Ratio: 310\]  
CPU: Brand String:             Intel(R) Core(TM) i3-2100 CPU @ 3.10GHz  
CPU: Vendor/Family/ExtFamily:  0x756e6547/0x6/0x0  
CPU: Model/ExtModel/Stepping:  0x2a/0x2/0x7  
CPU: MaxCoef/CurrCoef:         0x0/0x1f  
CPU: MaxDiv/CurrDiv:           0x0/0x0  
CPU: TSCFreq:                  3193MHz  
CPU: FSBFreq:                  103MHz  
CPU: CPUFreq:                  3193MHz  
CPU: NoCores/NoThreads:        2/4  
CPU: Features:                 0x000002ff  
Attempting to read GPT  
Read GPT  
Reading GPT partition 1, type C12A7328-F81F-11D2-BA4B-00A0C93EC93B  
Reading GPT partition 2, type 48465300-0000-11AA-AA11-00306543ECAC  
Read HFS+ file: \[hd(0,2)/System/Library/CoreServices/SystemVersion.plist\] 478 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/org.chameleon.Boot.plist\] 476 bytes.  
Module 'Symbols.dylib' by 'Chameleon' Loaded.  
    Description: Chameleon symbols for linking  
    Version: 0  
    Compat:  0  
Read HFS+ file: \[hd(0,2)/Extra/modules/klibc.dylib\] 44252 bytes.  
Module 'klibc.dylib' by 'Unknown' Loaded.  
    Description:  
    Version: 0  
    Compat:  0  
Read HFS+ file: \[hd(0,2)/Extra/modules/uClibcxx.dylib\] 77808 bytes.  
Module 'uClibcxx.dylib' by 'Unknown' Loaded.  
    Description:  
    Version: 0  
    Compat:  0  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/theme.plist\] 2787 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/background.png\] 160 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/logo.png\] 9791 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_generic.png\] 30749 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_generic\_o.png\] 31641 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus.png\] 33224 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_o.png\] 34030 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_ml.png\] 29768 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_ml\_o.png\] 30578 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_lion.png\] 28223 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_lion\_o.png\] 28963 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_sl.png\] 29902 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_sl\_o.png\] 30684 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_leo.png\] 28892 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_leo\_o.png\] 29666 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_tiger.png\] 28400 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsplus\_tiger\_o.png\] 29157 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid.png\] 33806 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_o.png\] 34633 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_ml.png\] 30436 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_ml\_o.png\] 31257 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_lion.png\] 28949 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_lion\_o.png\] 29725 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_sl.png\] 30605 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_sl\_o.png\] 31378 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_leo.png\] 29649 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_leo\_o.png\] 30429 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_tiger.png\] 29104 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_hfsraid\_tiger\_o.png\] 29917 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_ext3.png\] 33010 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_ext3\_o.png\] 33943 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_freebsd.png\] 27264 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_freebsd\_o.png\] 28018 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_openbsd.png\] 28850 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_openbsd\_o.png\] 29596 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_befs.png\] 27817 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_befs\_o.png\] 28529 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_fat.png\] 32113 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_fat\_o.png\] 33007 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_ntfs.png\] 34190 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_ntfs\_o.png\] 34992 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_cdrom.png\] 31453 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_cdrom\_o.png\] 31312 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_selection.png\] 148 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_scroll\_prev.png\] 3995 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/device\_scroll\_next.png\] 3898 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_boot.png\] 137 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_verbose.png\] 137 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_ignore\_caches.png\] 137 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_single\_user.png\] 137 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_memory\_info.png\] 136 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_video\_info.png\] 136 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_help.png\] 136 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_verbose\_disabled.png\] 135 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_ignore\_caches\_disabled.png\] 135 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_single\_user\_disabled.png\] 135 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/menu\_selection.png\] 158 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/progress\_bar.png\] 292 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/progress\_bar\_background.png\] 139 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/text\_scroll\_prev.png\] 562 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/text\_scroll\_next.png\] 557 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/font\_console.png\] 2931 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/Themes/Default/font\_small.png\] 3371 bytes.  
Read HFS+ file: \[hd(0,2)/Library/Preferences/SystemConfiguration/com.apple.Boot.plist\] 232 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/org.chameleon.Boot.plist\] 476 bytes.  
Loading Darwin 10.8  
No Kernel Cache File '/System/Library/Caches/com.apple.kext.caches/Startup/kernelcache' found  
Loading kernel /mach\_kernel  
Read HFS+ file: \[hd(0,2)/mach\_kernel\] 4096 bytes.  
Read HFS+ file: \[hd(0,2)/mach\_kernel\] 8188064 bytes.  
Read HFS+ file: \[hd(0,2)/Extra/dadt.aml\] 102813 bytes.  
Using PCI-Root-UID value: 0  
LAN Controller \[10ec:8168\] :: PciRoot(0x0)/Pci(0x1c,0x2)/Pci(0x0,0x0)  
Setting up lan keys  
Read HFS+ file: \[hd(0,2)/Extra/SMBios.plist\] 687 bytes.  
SMBus CmdReg: 0x3  
Scanning SMBus \[8086:1c22\], mmio: 0xfe604004, ioport: 0xf040, hostc: 0x1  
SPD\[0\] (size): 146 @0x50  
Slot: 0 Type 24 2048MB (DDR3 SDRAM) 1333MHz Vendor=Apacer Technology  
      PartNo=78.A1GC6.9LZ SerialNo=02010212  
SPD\[0\] (size): 255 @0x51  
SPD\[0\] (size): 146 @0x52  
Slot: 2 Type 24 2048MB (DDR3 SDRAM) 1333MHz Vendor=Apacer Technology  
      PartNo=78.A1GC6.9LZ SerialNo=02010212  
SPD\[0\] (size): 255 @0x53  
SPD\[0\] (size): 255 @0x54  
SPD\[0\] (size): 255 @0x55  
SPD\[0\] (size): 255 @0x56  
SPD\[0\] (size): 255 @0x57  
CPU is Intel(R) Core(TM) i3-2100 CPU @ 3.10GHz, family 0x6, model 0x2a  
  
Type: 0, Length: 24, Handle: 0x0  
BIOSInformation:  
    vendor: Apple Inc.  
    version: IM121.88Z.0047.B0A.1104221555  
    releaseDate: 04/22/11  
  
Type: 1, Length: 27, Handle: 0x1  
SystemInformation:  
    manufacturer: Apple Inc.  
    productName: iMac12,1  
    version: 1.0  
    serialNumber: C02JL367DHJT  
    uuid: 4093C112-8064-E011-816C-F46D0423CA64  
    wakeupReason: 0x6  
    skuNumber: To be filled by O.E.M.  
    family: iMac  
  
Type: 2, Length: 15, Handle: 0x2  
BaseBoard:  
    manufacturer: Apple Inc.  
    product: Mac-942B5BF58194151B  
    version: Rev x.0x  
    serialNumber: 109424350001705  
    assetTagNumber: To be filled by O.E.M.  
    locationInChassis: To be filled by O.E.M.  
    boardType: 0xA  
  
Type: 3, Length: 21, Handle: 0x3  
SystemEnclosure:  
    manufacturer: Chassis Manufacture  
    type: 3  
    version: Chassis Version  
    serialNumber: Chassis Serial Number  
    assetTagNumber: Asset-1234567890  
  
Type: 4, Length: 42, Handle: 0x4  
ProcessorInformation:  
    socketDesignation: LGA1155  
    processorType: 3  
    processorFamily: 0xBF  
    manufacturer: Intel  
    processorID: 0x206A7  
    processorVersion: Intel(R) Core(TM) i3-2100 CPU @ 3.10GHz  
    externalClock: 0MHz  
    maximumClock: 3193MHz  
    currentClock: 3223MHz  
    serialNumber: To Be Filled By O.E.M.  
    assetTag: To Be Filled By O.E.M.  
    partNumber: To Be Filled By O.E.M.  
  
Type: 7, Length: 19, Handle: 0x5  
Type: 7, Length: 19, Handle: 0x6  
Type: 7, Length: 19, Handle: 0x7  
Type: 8, Length: 9, Handle: 0x8  
Type: 8, Length: 9, Handle: 0x9  
Type: 8, Length: 9, Handle: 0xa  
Type: 8, Length: 9, Handle: 0xb  
Type: 8, Length: 9, Handle: 0xc  
Type: 8, Length: 9, Handle: 0xd  
Type: 8, Length: 9, Handle: 0xe  
Type: 8, Length: 9, Handle: 0xf  
Type: 8, Length: 9, Handle: 0x10  
Type: 8, Length: 9, Handle: 0x11  
Type: 8, Length: 9, Handle: 0x12  
Type: 8, Length: 9, Handle: 0x13  
Type: 8, Length: 9, Handle: 0x14  
Type: 8, Length: 9, Handle: 0x15  
Type: 8, Length: 9, Handle: 0x16  
Type: 8, Length: 9, Handle: 0x17  
Type: 8, Length: 9, Handle: 0x18  
Type: 8, Length: 9, Handle: 0x19  
Type: 8, Length: 9, Handle: 0x1a  
Type: 9, Length: 17, Handle: 0x1b  
Type: 9, Length: 17, Handle: 0x1c  
Type: 9, Length: 17, Handle: 0x1d  
Type: 9, Length: 17, Handle: 0x1e  
Type: 10, Length: 6, Handle: 0x1f  
Type: 11, Length: 5, Handle: 0x20  
Type: 12, Length: 5, Handle: 0x21  
Type: 16, Length: 15, Handle: 0x22  
Type: 18, Length: 23, Handle: 0x23  
Type: 19, Length: 15, Handle: 0x24  
Type: 17, Length: 28, Handle: 0x25  
MemoryDevice:  
    deviceLocator: DIMM0  
    bankLocator: BANK0  
    memoryType: DDR3  
    memorySpeed: 1333MHz  
    manufacturer: Apacer Technology  
    serialNumber: 02010212  
    assetTag: AssetTagNum0  
    partNumber: 78.A1GC6.9LZ  
  
Type: 18, Length: 23, Handle: 0x26  
Type: 20, Length: 19, Handle: 0x27  
Type: 17, Length: 28, Handle: 0x28  
MemoryDevice:  
    deviceLocator: DIMM1  
    bankLocator: BANK1  
    memoryType: DDR3  
    memorySpeed: 1333MHz  
    manufacturer: Apacer Technology  
    serialNumber: 02010212  
    assetTag: AssetTagNum1  
    partNumber: 78.A1GC6.9LZ  
  
Type: 18, Length: 23, Handle: 0x29  
Type: 20, Length: 19, Handle: 0x2a  
Type: 32, Length: 20, Handle: 0x2b  
Type: 34, Length: 11, Handle: 0x2c  
Type: 26, Length: 22, Handle: 0x2d  
Type: 36, Length: 16, Handle: 0x2e  
Type: 35, Length: 11, Handle: 0x2f  
Type: 28, Length: 22, Handle: 0x30  
Type: 36, Length: 16, Handle: 0x31  
Type: 35, Length: 11, Handle: 0x32  
Type: 27, Length: 14, Handle: 0x33  
Type: 36, Length: 16, Handle: 0x34  
Type: 35, Length: 11, Handle: 0x35  
Type: 27, Length: 14, Handle: 0x36  
Type: 36, Length: 16, Handle: 0x37  
Type: 35, Length: 11, Handle: 0x38  
Type: 29, Length: 22, Handle: 0x39  
Type: 36, Length: 16, Handle: 0x3a  
Type: 35, Length: 11, Handle: 0x3b  
Type: 39, Length: 22, Handle: 0x3c  
Type: 34, Length: 16, Handle: 0x3d  
Type: 26, Length: 22, Handle: 0x3e  
Type: 36, Length: 16, Handle: 0x3f  
Type: 35, Length: 11, Handle: 0x40  
Type: 26, Length: 22, Handle: 0x41  
Type: 36, Length: 16, Handle: 0x42  
Type: 35, Length: 11, Handle: 0x43  
Type: 28, Length: 22, Handle: 0x44  
Type: 36, Length: 16, Handle: 0x45  
Type: 35, Length: 11, Handle: 0x46  
Type: 27, Length: 14, Handle: 0x47  
Type: 36, Length: 16, Handle: 0x48  
Type: 35, Length: 11, Handle: 0x49  
Type: 28, Length: 22, Handle: 0x4a  
Type: 36, Length: 16, Handle: 0x4b  
Type: 35, Length: 11, Handle: 0x4c  
Type: 27, Length: 14, Handle: 0x4d  
Type: 36, Length: 16, Handle: 0x4e  
Type: 35, Length: 11, Handle: 0x4f  
Type: 29, Length: 22, Handle: 0x50  
Type: 36, Length: 16, Handle: 0x51  
Type: 35, Length: 11, Handle: 0x52  
Type: 29, Length: 22, Handle: 0x53  
Type: 36, Length: 16, Handle: 0x54  
Type: 35, Length: 11, Handle: 0x55  
Type: 39, Length: 22, Handle: 0x56  
Type: 41, Length: 11, Handle: 0x57  
Type: 41, Length: 11, Handle: 0x58  
Type: 41, Length: 11, Handle: 0x59  
Type: 139, Length: 94, Handle: 0x5a  
Type: 13, Length: 22, Handle: 0x5b  
Type: 131, Length: 6, Handle: 0x5b  
AppleProcessorType:  
    ProcessorType: 0x901  
  
Type: 127, Length: 4, Handle: 0x5c  
  
Customizing SystemID with : 4093c112-8064-e011-816c-f46d0423ca64  
Read HFS+ file: \[hd(0,2)/Extra/dadt.aml\] 102813 bytes.  
ACPI table not found: SSDT.aml  
FADT: Using custom DSDT!  
FADT: Using custom DSDT!  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Accusys6xxxx.kext/Contents/Info.plist\] 2409 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/acfs.kext/Contents/Info.plist\] 1319 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/acfsctl.kext/Contents/Info.plist\] 1197 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ALF.kext/Contents/Info.plist\] 1659 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AMDRadeonAccelerator.kext/Contents/Info.plist\] 15314 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Apple16X50Serial.kext/Contents/Info.plist\] 2047 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Apple16X50Serial.kext/Contents/PlugIns/Apple16X50ACPI.kext/Contents/Info.plist\] 1912 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Apple\_iSight.kext/Contents/Info.plist\] 2033 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleACPIPlatform.kext/Contents/Info.plist\] 3715 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleACPIPlatform.kext/Contents/PlugIns/AppleACPIButtons.kext/Contents/Info.plist\] 2964 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleACPIPlatform.kext/Contents/PlugIns/AppleACPIEC.kext/Contents/Info.plist\] 2141 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleAHCIPort.kext/Contents/Info.plist\] 6744 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleAPIC.kext/Contents/Info.plist\] 1818 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleAVBAudio.kext/Contents/Info.plist\] 2306 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleAVBAudio.kext/Contents/PlugIns/AppleAVBAudioPlugin.kext/Contents/Info.plist\] 2459 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleBacklight.kext/Contents/Info.plist\] 17087 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleBacklightExpert.kext/Info.plist\] 1923 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleBluetoothMultitouch.kext/Contents/Info.plist\] 56598 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleBMC.kext/Contents/Info.plist\] 2140 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleEFIRuntime.kext/Contents/Info.plist\] 2077 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleEFIRuntime.kext/Contents/PlugIns/AppleEFINVRAM.kext/Contents/Info.plist\] 2073 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleFileSystemDriver.kext/Contents/Info.plist\] 3067 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleFSCompressionTypeDataless.kext/Contents/Info.plist\] 2405 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleFSCompressionTypeZlib.kext/Contents/Info.plist\] 2379 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleFWAudio.kext/Contents/Info.plist\] 7590 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleGraphicsControl.kext/Contents/Info.plist\] 2024 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleGraphicsControl.kext/Contents/PlugIns/AppleMuxControl.kext/Contents/Info.plist\] 13227 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleGraphicsControl.kext/Contents/PlugIns/ApplePolicyControl.kext/Contents/Info.plist\] 2557 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleGraphicsPowerManagement.kext/Contents/Info.plist\] 79681 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/Info.plist\] 3213 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/PlugIns/AppleHDAController.kext/Contents/Info.plist\] 4807 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/PlugIns/AppleHDAHardwareConfigDriver.kext/Contents/Info.plist\] 12558 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/PlugIns/AppleMikeyDriver.kext/Contents/Info.plist\] 2207 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/PlugIns/DspFuncLib.kext/Contents/Info.plist\] 1859 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHDA.kext/Contents/PlugIns/IOHDAFamily.kext/Contents/Info.plist\] 1995 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDKeyboard.kext/Contents/Info.plist\] 41939 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDKeyboard.kext/Contents/PlugIns/AppleBluetoothHIDKeyboard.kext/Contents/Info.plist\] 45724 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDKeyboard.kext/Contents/PlugIns/AppleUSBHIDKeyboard.kext/Contents/Info.plist\] 14763 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDMouse.kext/Contents/Info.plist\] 1606 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDMouse.kext/Contents/PlugIns/AppleBluetoothHIDMouse.kext/Contents/Info.plist\] 17736 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHIDMouse.kext/Contents/PlugIns/AppleUSBHIDMouse.kext/Contents/Info.plist\] 10106 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHPET.kext/Contents/Info.plist\] 1985 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleHWSensor.kext/Contents/Info.plist\] 2265 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleIRController.kext/Contents/Info.plist\] 5668 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleKeyStore.kext/Contents/Info.plist\] 2245 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleKeyswitch.kext/Contents/Info.plist\] 2720 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleLPC.kext/Contents/Info.plist\] 4043 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleLSIFusionMPT.kext/Contents/Info.plist\] 4038 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMatch.kext/Contents/Info.plist\] 1411 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMCCSControl.kext/Contents/Info.plist\] 3525 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMCEDriver.kext/Contents/Info.plist\] 1800 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMCP89RootPortPM.kext/Contents/Info.plist\] 2117 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMikeyHIDDriver.kext/Contents/Info.plist\] 1972 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMobileDevice.kext/Contents/Info.plist\] 3618 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleMultitouchDriver.kext/Contents/Info.plist\] 1695 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ApplePlatformEnabler.kext/Contents/Info.plist\] 1857 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleRAID.kext/Contents/Info.plist\] 2294 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleRAIDCard.kext/Contents/Info.plist\] 4292 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleRTC.kext/Contents/Info.plist\] 1969 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSDXC.kext/Contents/Info.plist\] 2915 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSEP.kext/Contents/Info.plist\] 2970 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSmartBatteryManager.kext/Contents/Info.plist\] 2063 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSMBIOS.kext/Contents/Info.plist\] 1929 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSMBusController.kext/Contents/Info.plist\] 2912 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSMBusPCI.kext/Contents/Info.plist\] 1999 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSMC.kext/Contents/Info.plist\] 1940 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSMCLMU.kext/Contents/Info.plist\] 2053 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleSRP.kext/Contents/Info.plist\] 1352 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/Info.plist\] 1159 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleATAPIStorage.kext/Contents/Info.plist\] 3097 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleFireWireStorage.kext/Contents/Info.plist\] 2619 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleHollywood.kext/Contents/Info.plist\] 16755 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleMemorexCDROMDriver.kext/Contents/Info.plist\] 2314 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleUSBCardReader.kext/Contents/Info.plist\] 5123 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleUSBODD.kext/Contents/Info.plist\] 2620 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/AppleXserveRAID.kext/Contents/Info.plist\] 2495 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/CanonEOS1D.kext/Contents/Info.plist\] 2727 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/FireWireStorageDeviceSpecifics.kext/Contents/Info.plist\] 7367 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/FWPreferredProtocolSpeed.kext/Contents/Info.plist\] 2775 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/initioFWBridge.kext/Contents/Info.plist\] 2703 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/IOFireWireSerialBusProtocolSansPhysicalUnit.kext/Contents/Info.plist\] 2757 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/LSI-FW-500.kext/Contents/Info.plist\] 3865 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/MaxTranserSizeOverrideDriver.kext/Contents/Info.plist\] 3088 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/MKE-LF-D211A.kext/Contents/Info.plist\] 2844 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/MKE-SR-8171.kext/Contents/Info.plist\] 2261 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/OxfordSemiconductor.kext/Contents/Info.plist\] 2719 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/PioneerSuperDrive.kext/Contents/Info.plist\] 2208 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/PlasmonUDO.kext/Contents/Info.plist\] 2218 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/PreventMediaMountDriver.kext/Contents/Info.plist\] 2693 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/QPSQueFire.kext/Contents/Info.plist\] 2661 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/SanyoIDShot.kext/Contents/Info.plist\] 2798 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/SonyXDCAMDriver.kext/Contents/Info.plist\] 2698 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/StorageLynx.kext/Contents/Info.plist\] 2565 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/UFIWriteProtectedMediaDriver.kext/Contents/Info.plist\] 3108 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/USBStorageDeviceSpecifics.kext/Contents/Info.plist\] 112471 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleStorageDrivers.kext/Contents/PlugIns/WriteProtectedMediaDriver.kext/Contents/Info.plist\] 6905 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltDPAdapters.kext/Contents/Info.plist\] 1289 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltDPAdapters.kext/Contents/PlugIns/AppleThunderboltDPAdapterFamily.kext/Contents/Info.plist\] 1867 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltDPAdapters.kext/Contents/PlugIns/AppleThunderboltDPInAdapter.kext/Contents/Info.plist\] 2396 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltDPAdapters.kext/Contents/PlugIns/AppleThunderboltDPOutAdapter.kext/Contents/Info.plist\] 2485 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltEDMService.kext/Contents/Info.plist\] 1296 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltEDMService.kext/Contents/PlugIns/AppleThunderboltEDMSink.kext/Contents/Info.plist\] 2557 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltEDMService.kext/Contents/PlugIns/AppleThunderboltEDMSource.kext/Contents/Info.plist\] 2509 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltNHI.kext/Contents/Info.plist\] 2392 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltPCIAdapters.kext/Contents/Info.plist\] 1350 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltPCIAdapters.kext/Contents/PlugIns/AppleThunderboltPCIDownAdapter.kext/Contents/Info.plist\] 2207 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltPCIAdapters.kext/Contents/PlugIns/AppleThunderboltPCIUpAdapter.kext/Contents/Info.plist\] 2281 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleThunderboltUTDM.kext/Contents/Info.plist\] 2914 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleTyMCEDriver.kext/Contents/Info.plist\] 2301 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUpstreamUserClient.kext/Contents/Info.plist\] 2238 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBAudio.kext/Contents/Info.plist\] 4033 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBDisplays.kext/Contents/Info.plist\] 26094 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBEthernetHost.kext/Contents/Info.plist\] 2693 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBMultitouch.kext/Contents/Info.plist\] 386012 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBTopCase.kext/Contents/Info.plist\] 1523 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCButtons.kext/Contents/Info.plist\] 87849 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext/Contents/Info.plist\] 53670 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyEventDriver.kext/Contents/Info.plist\] 127228 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTrackpad.kext/Contents/Info.plist\] 40192 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleWWANAutoEject.kext/Contents/Info.plist\] 4296 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AppleXsanFilter.kext/Contents/Info.plist\] 2258 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ArcMSR.kext/Contents/Info.plist\] 2803 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATI4600Controller.kext/Contents/Info.plist\] 2037 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATIFramebuffer.kext/Contents/Info.plist\] 22576 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATIRadeonX2000.kext/Contents/Info.plist\] 3532 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATISupport.kext/Contents/Info.plist\] 2030 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOCelerityFC.kext/Contents/Info.plist\] 3046 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOCelerityFC8.kext/Contents/Info.plist\] 3000 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressPCI4.kext/Contents/Info.plist\] 2487 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressSASHBA.kext/Contents/Info.plist\] 2945 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressSASHBA2.kext/Contents/Info.plist\] 3018 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressSASHBA3.kext/Contents/Info.plist\] 2893 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressSASRAID.kext/Contents/Info.plist\] 2955 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ATTOExpressSASRAID2.kext/Contents/Info.plist\] 3028 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/AudioAUUC.kext/Info.plist\] 2194 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/autofs.kext/Contents/Info.plist\] 1740 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/BJUSBLoad.kext/Contents/Info.plist\] 125615 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/BootCache.kext/Contents/Info.plist\] 2093 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/CalDigitHDProDrv.kext/Contents/Info.plist\] 2364 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/cd9660.kext/Contents/Info.plist\] 1666 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/cddafs.kext/Contents/Info.plist\] 1587 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/CellPhoneHelper.kext/Contents/Info.plist\] 100096 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/corecrypto.kext/Contents/Info.plist\] 1978 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/CoreStorage.kext/Contents/Info.plist\] 3004 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/CoreStorage.kext/Contents/PlugIns/CoreStorageFsck.kext/Contents/Info.plist\] 2419 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Dont Steal Mac OS X.kext/Contents/Info.plist\] 2453 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/EVOenabler.kext/Contents/Info.plist\] 101757 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/exfat.kext/Contents/Info.plist\] 1637 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/FakeSMC.kext/Contents/Info.plist\] 2452 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/GeForce.kext/Contents/Info.plist\] 2335 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/HDAEnabler1.kext/Contents/Info.plist\] 1953 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/HighPointIOP.kext/Contents/Info.plist\] 3180 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/HighPointRR.kext/Contents/Info.plist\] 4538 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IO80211Family.kext/Contents/Info.plist\] 1869 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IO80211Family.kext/Contents/PlugIns/AirPortAtheros40.kext/Contents/Info.plist\] 2545 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IO80211Family.kext/Contents/PlugIns/AirPortBrcm4331.kext/Contents/Info.plist\] 2480 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IO80211Family.kext/Contents/PlugIns/AppleAirPortBrcm43224.kext/Contents/Info.plist\] 2827 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IO80211Family.kext/Contents/PlugIns/IO80211NetBooter.kext/Contents/Info.plist\] 2013 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAcceleratorFamily.kext/Contents/Info.plist\] 1876 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOACPIFamily.kext/Contents/Info.plist\] 1678 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAHCIFamily.kext/Contents/Info.plist\] 1603 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCIBlockStorage.kext/Contents/Info.plist\] 2180 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAHCIFamily.kext/Contents/PlugIns/IOAHCISerialATAPI.kext/Contents/Info.plist\] 2429 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOATAFamily.kext/Contents/Info.plist\] 1641 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOATAFamily.kext/Contents/PlugIns/AppleIntelPIIXATA.kext/Contents/Info.plist\] 6218 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOATAFamily.kext/Contents/PlugIns/IOATABlockStorage.kext/Contents/Info.plist\] 2120 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOATAFamily.kext/Contents/PlugIns/IOATAPIProtocolTransport.kext/Contents/Info.plist\] 2493 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAudioFamily.kext/Contents/Info.plist\] 1753 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAVBFamily.kext/Contents/Info.plist\] 2355 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAVBFamily.kext/Contents/PlugIns/IOAVBDiscoveryPlugin.kext/Contents/Info.plist\] 2719 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAVBFamily.kext/Contents/PlugIns/IOAVBPlugin.kext/Contents/Info.plist\] 4867 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOAVBFamily.kext/Contents/PlugIns/IOMRPPlugin.kext/Contents/Info.plist\] 5578 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOBDStorageFamily.kext/Contents/Info.plist\] 2578 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOBluetoothFamily.kext/Contents/PlugIns/IOBluetoothUSBDFU.kext/Contents/Info.plist\] 8250 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOCDStorageFamily.kext/Contents/Info.plist\] 3079 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IODVDStorageFamily.kext/Contents/Info.plist\] 2525 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireAVC.kext/Contents/Info.plist\] 3968 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireFamily.kext/Contents/Info.plist\] 2368 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireFamily.kext/Contents/PlugIns/AppleFWOHCI.kext/Contents/Info.plist\] 2835 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireIP.kext/Contents/Info.plist\] 2110 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireIP.kext/Contents/PlugIns/IOFireWireIPPrivate.kext/Contents/Info.plist\] 2554 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireSBP2.kext/Contents/Info.plist\] 2875 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOFireWireSerialBusProtocolTransport.kext/Contents/Info.plist\] 2643 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOGraphicsFamily.kext/Info.plist\] 3289 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/Info.plist\] 2253 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesCryptoEncoding.kext/Contents/Info.plist\] 2548 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesFileBackingStore.kext/Contents/Info.plist\] 2325 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesHTTPBackingStore.kext/Contents/Info.plist\] 2322 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesKernelBacked.kext/Contents/Info.plist\] 2558 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesPartitionBackingStore.kext/Contents/Info.plist\] 2549 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesRAMBackingStore.kext/Contents/Info.plist\] 2307 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesReadWriteDiskImage.kext/Contents/Info.plist\] 2291 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesSparseDiskImage.kext/Contents/Info.plist\] 2273 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHDIXController.kext/Contents/PlugIns/AppleDiskImagesUDIFDiskImage.kext/Contents/Info.plist\] 2573 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHIDFamily.kext/Contents/Info.plist\] 2839 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHIDFamily.kext/Contents/PlugIns/IOHIDEventDriver.kext/Contents/Info.plist\] 2420 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHIDFamily.kext/Contents/PlugIns/IOHIDEventDriverSafeBoot.kext/Contents/Info.plist\] 11673 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHIDFamily.kext/Contents/PlugIns/IOHIDSystem.kext/Contents/Info.plist\] 1787 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOHIDFamily.kext/Contents/PlugIns/IOHIDUserClient.kext/Contents/Info.plist\] 4016 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONDRVSupport.kext/Info.plist\] 3073 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/Info.plist\] 2529 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleBCM5701Ethernet.kext/Contents/Info.plist\] 4168 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleIntel8254XEthernet.kext/Contents/Info.plist\] 3180 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleRTL8169Ethernet.kext/Contents/Info.plist\] 4309 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleUSBEthernet.kext/Contents/Info.plist\] 5309 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleUSBGigEthernet.kext/Contents/Info.plist\] 4984 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/AppleYukon2.kext/Contents/Info.plist\] 23266 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/Intel82574L.kext/Contents/Info.plist\] 3147 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/IOEthernetAVBController.kext/Contents/Info.plist\] 1738 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IONetworkingFamily.kext/Contents/PlugIns/nvenet.kext/Contents/Info.plist\] 2431 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPCIFamily.kext/Info.plist\] 2780 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/Info.plist\] 1866 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/ACPI\_SMC\_PlatformPlugin.kext/Contents/Info.plist\] 2642 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/AppleSMCPDRC.kext/Contents/Info.plist\] 2170 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/IOPlatformPluginLegacy.kext/Contents/Info.plist\] 1941 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/X86PlatformPlugin.kext/Contents/Info.plist\] 2811 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/X86PlatformShim.kext/Contents/Info.plist\] 2132 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIArchitectureModelFamily.kext/Contents/Info.plist\] 2471 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIArchitectureModelFamily.kext/Contents/PlugIns/IOSCSIBlockCommandsDevice.kext/Contents/Info.plist\] 2573 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIArchitectureModelFamily.kext/Contents/PlugIns/IOSCSIMultimediaCommandsDevice.kext/Contents/Info.plist\] 2446 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIArchitectureModelFamily.kext/Contents/PlugIns/IOSCSIReducedBlockCommandsDevice.kext/Contents/Info.plist\] 2238 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIArchitectureModelFamily.kext/Contents/PlugIns/SCSITaskUserClient.kext/Contents/Info.plist\] 4960 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSCSIParallelFamily.kext/Contents/Info.plist\] 1712 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSerialFamily.kext/Contents/Info.plist\] 2542 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSerialFamily.kext/Contents/PlugIns/AppleUSBIrDA.kext/Contents/Info.plist\] 2229 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSerialFamily.kext/Contents/PlugIns/AppleWWANSupport.kext/Contents/Info.plist\] 4960 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSerialFamily.kext/Contents/PlugIns/AppleWWANSupport1.kext/Contents/Info.plist\] 7486 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSerialFamily.kext/Contents/PlugIns/AppleWWANSupport2.kext/Contents/Info.plist\] 2201 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSMBusFamily.kext/Contents/Info.plist\] 1491 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOStorageFamily.kext/Contents/Info.plist\] 5912 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOStreamFamily.kext/Contents/Info.plist\] 1398 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOStreamFamily.kext/Contents/PlugIns/IOStreamUserClient.kext/Contents/Info.plist\] 1984 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOSurface.kext/Contents/Info.plist\] 2181 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOThunderboltFamily.kext/Contents/Info.plist\] 1709 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOTimeSyncFamily.kext/Contents/Info.plist\] 1748 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOTimeSyncFamily.kext/Contents/PlugIns/IO8021ASPlugin.kext/Contents/Info.plist\] 2841 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBAttachedSCSI.kext/Contents/Info.plist\] 2955 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/Info.plist\] 1797 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDC.kext/Contents/Info.plist\] 15650 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCACMControl.kext/Contents/Info.plist\] 1976 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCACMData.kext/Contents/Info.plist\] 9481 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCDMM.kext/Contents/Info.plist\] 1984 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCECMControl.kext/Contents/Info.plist\] 2049 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCECMData.kext/Contents/Info.plist\] 3311 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCEEM.kext/Contents/Info.plist\] 2013 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBCDCWCM.kext/Contents/Info.plist\] 1916 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBEHCI.kext/Contents/Info.plist\] 2266 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBHub.kext/Contents/Info.plist\] 2388 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBMergeNub.kext/Contents/Info.plist\] 54239 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBOHCI.kext/Contents/Info.plist\] 2201 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBOpticalMouse.kext/Contents/Info.plist\] 6821 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBUHCI.kext/Contents/Info.plist\] 2219 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/Info.plist\] 5461 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBXHCI.kext/Contents/Info.plist\] 2279 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/IOUSBCompositeDriver.kext/Contents/Info.plist\] 3267 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/IOUSBHIDDriver.kext/Contents/Info.plist\] 2308 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/IOUSBHIDDriverSafeBoot.kext/Contents/Info.plist\] 5318 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/IOUSBUserClient.kext/Contents/Info.plist\] 3504 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUSBMassStorageClass.kext/Contents/Info.plist\] 6148 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOUserEthernet.kext/Contents/Info.plist\] 3093 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOVideoFamily.kext/Contents/Info.plist\] 1462 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/IOVideoFamily.kext/Contents/PlugIns/IOVideoDeviceUserClient.kext/Contents/Info.plist\] 2209 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/iPodDriver.kext/Contents/Info.plist\] 3937 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/iPodDriver.kext/Contents/PlugIns/iPodSBCDriver.kext/Contents/Info.plist\] 2995 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/JMicronATA.kext/Contents/Info.plist\] 2231 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/mcxalr.kext/Contents/Info.plist\] 1324 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/msdosfs.kext/Contents/Info.plist\] 1504 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/ntfs.kext/Contents/Info.plist\] 1630 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NullCPUPowerManagement.kext/Contents/Info.plist\] 1498 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NVDAGF100Hal.kext/Contents/Info.plist\] 2375 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NVDAGK100Hal.kext/Contents/Info.plist\] 1879 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NVDANV50Hal.kext/Contents/Info.plist\] 2427 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NVDAResman.kext/Contents/Info.plist\] 2607 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/NVSMU.kext/Contents/Info.plist\] 1977 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/OSvKernDSPLib.kext/Contents/Info.plist\] 1356 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/PPP.kext/Contents/Info.plist\] 1742 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/PromiseSTEX.kext/Contents/Info.plist\] 2494 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/Quarantine.kext/Contents/Info.plist\] 1870 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/RadeonHD.kext/Contents/Info.plist\] 2561 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/RealtekRTL81xx.kext/Contents/Info.plist\] 1969 bytes.  

> ...............................................................................  

Read HFS+ file: \[hd(0,2)/System/Library/Extensions/EVOenabler.kext/Contents/MacOS/EVOenabler\] 4096 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/EVOenabler.kext/Contents/MacOS/EVOenabler\] 36264 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/FakeSMC.kext/Contents/MacOS/fakesmc\] 4096 bytes.  
Read HFS+ file: \[hd(0,2)/System/Library/Extensions/FakeSMC.kext/Contents/MacOS/fakesmc\] 55992 bytes.  

> ...............................................................................  

Starting Darwin x86\_64  
Boot Args: boot-uuid=4159DDB1-8659-378A-8D3C-C8366B8B54EF rd=\*uuid -v