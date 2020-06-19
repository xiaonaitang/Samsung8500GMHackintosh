# Samsung8500GM黑苹果引导
- readme 2.0版

- 增加HDMI端口修正方法
- 增加一些小技巧助力使用macOS
- 增加一些其他资源链接
- 增加各驱动各补丁含义
- 普及一些黑果奇怪的知识

## 1.我的笔记本配置

| 电脑信息  |    |
| ------ | -------- |
| 电脑型号 |  Samsung 8500GM-X06 |
| 处理器 |  i5-7300HQ 2.5G/3.5G |
| 内存 |  16G 2133 MHZ DDR4 |
| 声卡 |  ALC256 |
| 核显 |  HD630（独显无解） |
| 网卡 |  高通AR9377板载无解 （自购USB网卡,我买的comfast）|

- 经测试玄龙7700HQ等其他型号也可以

## 2.使用OC说明
- OC全称opencore，是一个着眼于未来开源引导工具, 最初诞生于HermitCrabs实验室, 现在接手于Acidanthera, 其目的是创造一个更加严谨的模组化的轻量引导系统。尽管 OpenCore 的主要用途是黑苹果, 它也支持其它操作系统的引导，目前OC引导win10有问题不建议尝试。主要是有些部件要在Mac生效就要启用一些补丁，而这些关键补丁会在win里面导致蓝屏，OC是一种更加接近原生Mac的新引导方式，体现在：开机可以更加白果，可直接进系统不出现选择启动盘页面；使用原生电源管理，可进一步优化睿频；提高开机速度体验，文件结构更精简。
- 推荐使用propertree或者OCC编辑OC配置文件,PlistEditPro或者Xcode也可以
- 使用黑果小兵镜像，参考[小兵教程](https://blog.daliansky.net/MacOS-installation-tutorial-XiaoMi-Pro-installation-process-records.html) 安装，做好启动盘后替换成我的EFI，有问题就看后面的自制本机型OC的EFI试试
- 自行购买USB网卡或者插网线联网工作
- 安装系统：10.15.4
- 使用opencore版本：0.6.0
- 工作完美：蓝牙、电量显示、原生电源管理、触摸板、键盘、鼠标、亮度调节、核显硬解、USB定制、睡眠、类白果启动、HDMI、隔空投放、声音、CPU睿频、H264解码、HEVC解码
- 不能工作：独显、内置网卡、airport
- 本机型15.4及以下HDMI外接显示器完美，但测试对于7700HQ+1060+Catalina15.5的机子HDMI始终不行，猜测可能HDMI走独显无法驱动或者15.5的问题，本机型暂未测试15.5的HDMI问题，不少八九代的电脑都有HDMI需要仿冒七代才能暂时工作，不晓得15.5搞什么幺蛾子，我也就没升级15.5了
- 随航未测试因为我没有苹果设备
- clover能使用，用14.2-15.2，虽然有些瑕疵吧，推荐clover上14.6系统，我就不更新了，后面有一小部分关于clover的内容（还没写）
- 项目文件夹里的EFI等文件就不要用了，去release里面下载使用吧
- 系统偏好设置或者App Store中更新Catalina系统

## 3.安装成功进系统后遇到问题和解决
- 1.进系统亮度不能调节，一般clover会遇到或者OC没加补丁，因为键盘映射有问题，要么自行修改亮度调节快捷键，路径为系统偏好设置-键盘-快捷键-显示器，但是有一定概率会没有显示器选项；要么使用键盘映射软件修改亮度快捷键的映射；个人最推荐使用本机型键盘亮度快捷键布丁。
- 2.进系统蓝牙不能关闭，请修改蓝牙硬件驱动ID，具体做法分为两步，开启文件修改权限和修改文件。catalina系统下开启文件权限需要打开终端依次输入
- sudo su(输入本机密码，不会显示出来）
- Sudo mount -uw /
- Killall Finder
- 保持终端不能关闭（更推荐你尝试这个[链接](https://www.bugprogrammer.me/2019/07/13/unlockSystem.html)使用的方法来使得Catalina开机就开启系统文件修改权限，但可能进系统程序运行屏幕会刷新一下，介意的话不必弄了）修改文件具体为将S/L/E（就是系统/资源/拓展）路径中的IOBluetoothFamily.kext/ 右键显示包内容/Contents/PlugIns/BroadcomBluetoothHostControllerUSBTransport.kext/ 右键显示包内容/Contents/Info.plist，将这一文件拖出，例如放到桌面一份，使用文本编辑或者propertree打开，在IOKitPersonalities属性中找到第一个，注意是第一个com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport属性，修改其中的idProduct数字为58624，idVendor数字为3315，保存文件，将桌面修改好的文件再次拖进文件原位置，替换输入密码。最后使用kext utility重建缓存或者hackintool-工具来重建缓存后，才能关闭终端
- 3.刚进系统一定概率触摸板不能识别可外接鼠标使用，修复权限后重建缓存，重启大概率会识别，若还没有识别，查看自制OC的EFI里面自己制作触摸板补丁有没有问题，若还不能识别，就有些复杂了，后面我再补充一些触摸板相关资料自己试试吧，我没研究下去了
- 4.声音ALC256注入ID为56，57，这个数值的来源是查看aplealc驱动里面的info.plist文件查到的ALC256注入ID，如遇有问题可关机开机解决或者更换ID。

## 4.OC的EFI配制方法

- 有点长，我会说的详细些，记录自己从无到有配置玄龙骑士，走过的坑吃过的亏，避免后来者踩坑！
- 请参考xjn大佬的 [OC博客](https://blog.xjn819.com/?p=543) 来修改制作文件,我主要说一些和博客内容不一样的本机型设置

### 4.1 资料文件准备

- [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases)    OC官方更新包
- [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)   驱动电池CPU等
- [AppleSupportPkg](https://github.com/acidanthera/AppleSupportPkg/releases)  苹果文件格式驱动
- [CPUFriend](https://github.com/acidanthera/CPUFriend/releases)       定制CPU电源管理
- [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)    核显驱动
- [Lilu](https://github.com/acidanthera/Lilu/releases)    综合型驱动 
- [VoodooPS2](https://github.com/acidanthera/VoodooPS2)    键盘触摸板驱动
- [AppleALC](https://github.com/acidanthera/AppleALC/releases)  声卡驱动
- [NVMeFix](https://github.com/acidanthera/NVMeFix/releases)   NVME固态修补驱动
- [VoodooInput](https://github.com/acidanthera/VoodooInput/releases)   妙控板拓展驱动
- [USBInjectAll](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads)  USB驱动
- [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C/releases)  触摸板驱动
- [OC-little-master](https://github.com/daliansky/OC-little)    宪武大佬OC补丁
- 将下载好的文件里面的KEXT文件放入OC的kext文件夹里

### 4.2 利用clover引导获取本机DSDT.aml文件

- 将本机clover的EFI放入U盘的EFI分区，开机U盘启动，在clover引导选择进哪个系统界面，按一下F4键，不会有任何反应，进系统后在EFI/clover/ACPI/origin文件里有一个DSDT.aml文件，其他文件也可保留可反编译用。

### 4.3 文件结构

- 看release自用的OC文件结构这样就行就不贴图了，图片不显示也没办法

### 4.4 本机型config设置

- 看release自用的OC文件设置这样就行就不贴图了，图片不显示也没办法

### 4.5 特别说明
- CFG主板默认没解锁，需要以下设置
kernel/Quirks/AppleCpuPmCfgLock设置true，kernel/Quirks/AppleXcpmCfgLock设置true，UEFI/Quirks/IgnoreInvalidFlexRatio设置true
- USB没有定制的话需要用USBinjectall.kext，并且kernel/Quirks/XhciPortLimit设置true,定制好USB驱动就可以设置false
- 空壳驱动相较于完整驱动，在kernel/Add/ExecutablePath是留空的，比如定制USB的驱动USBport就是空壳驱动，因为驱动右键显示包内容，只有一个info.plist文件没有其他文件。
- FakeAppleUSBMouse.kext这个驱动是仿冒苹果鼠标的，使用要在关于本机/系统报告/USB找到自己鼠标，查看厂商ID和产品ID，转换成16进制修改FakeAppleUSBMouse.kext右键包展开里的info.plist最后的数值，注意这是空壳驱动，使用后系统偏好设置/鼠标里面能够设置鼠标各个键的功能。
- Misc/Boot/ShowPicker为是否显示OC启动选择项，Timeout为显示的时间秒，Misc/Security/ScanPolicy为OC的扫描策略，具体怎么算出来的可以用OCC计算出来，我设置的是只扫描MAC盘，改成0就是全部格式都扫描

### 4.6 SSDT文件说明
- SSDT-BAT 电池补丁，需要配合电池重命名以及SMC电池驱动或者R神的电池驱动
- SSDT-EC-USBX-PLUG  三补丁合一，仿冒EC部件，增加USB插入苹果手机能快充以及原生电源管理
SSDT-GPRW、SSDT-DeepIdle、SSDT-LIDpatch-AOAC、SSDT-S3-disable解决睡眠问题补丁
- SSDT-HRTF  声卡补丁
- SSDT-MEM2-PMCR-DMAC、SSDT-SBUS-MCHC、SSDT-SLPB缺失部件
- SSDT-NVMe  nvme补丁
- SSDT-PNLF-ALS0  能够调节亮度，并且偏好设置/显示器有亮度自动调节按钮，需要配合SMC的light驱动
- SSDT-Q63Q64   亮度快捷键映射补丁，使得Mac里面能够和win用一样的快捷键，需要配合亮度重命名使用
- SSDT-SPTP-GPEN-XOSI    触摸板补丁，要配合I2C两个驱动使用，值得注意的是这个补丁会使得win蓝屏

## 5.HIDPI开启和关闭
- HIDPI字面意思就是高DPI，通俗来说好比拿两三个像素点渲染一个像素，所以开启后分辨率设置越低，画面越清楚，但同时字体界面啥的会变大，一般建议4K显示开启，但如果自己喜欢也可以开启，毕竟眼睛怎么舒服怎么来，这是我的个人理解
- 需要注意的是开启后OC下进度条前后半段图标大小不一致，当然可以设置前后半段一样的大小NVRAM/Add/4D1E..../UIScale设置01就是默认大小02就是开启HIDPI后放大了的大小
- 首先需要开启系统文件修改权限
- 使用终端一键开启HIDPI代码[详细请看](https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md)
- 上条代码用不了可以用[国内的镜像代码](https://www.sqlsec.com/2018/09/hidpi.html)

## 6.HDMI
- 通过hackintool可以修改缓冲祯，修改端口定义来使得HDMI能够使用，在应用补丁里面设置好信息参数，Kaby lake,0x591B0000,基本显存和缓冲祯默认，接口这要把除了第一条索引，其他两条全改为HDMI而不是其他的类型，第一条LVDS是笔记本自带的屏幕无需修改，应用补丁/通用里面取消勾选自动侦测变化，勾选设备属性，接口，基本显存，图形卡，高级里面勾选仿冒图形卡、修复热拔插重启、HDMI无限循环修复、禁用egpu,VDMT32预分配、显存2048MB，启用HDMI20，点击生成补丁，点击左上角文件-导出-config.plist，将参数添加到OC的配置文件的device properties对应的PCI里面。

## 7.hackintool
- 这一软件有很多用法，可参考小兵的hackintool教程,内核扩展可查看用到的驱动版本，显示器选项玩法多，可生成HIDPI文件，可解决部分显示问题，USB部分可定制USB驱动，PCIE部分可查看部件的PCI路径，电源部分可点击底部修复深度睡眠解决部分睡眠问题，计算机部分可计算进制，工具部分挺多工具，可重建缓存，可查看一些参数例如CFG是否锁，日志可查看开机的代码，可查看是否有error并解决

## .致谢
- [远景论坛](http://bbs.pcbeta.com)
- 参考[xjin大佬博客](https://blog.xjn819.com/?p=543)
- 国内外许多驱动开发者
- 本机型和相似电脑的前辈工作积累
- [黑果小兵](https://blog.daliansky.net)和[len的镜像](http://bbs.pcbeta.com/viewthread-1836586-1-2.html)以及安装教程;
- [宪武大佬大量补丁](https://github.com/daliansky/OC-little)工作和指导，尤其让我对重命名有深刻理解
       
## 欢迎加入同机型交流群（群号:588964385）讨论完善！
