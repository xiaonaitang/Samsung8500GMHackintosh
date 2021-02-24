# Samsung8500GM黑苹果引导
- 前言 21.2.24版
- 重新整理，纠正谬误，岁月不再，至此断更！！！
- readme 20.7.24版
- 成功安装[macOS Big Sur11beta3](http://swcdn.apple.com/content/downloads/34/37/001-26097-A_OYW4Z0U99Z/gdas3ubse9fasb0217grmmyplfd6o7mqfp/InstallAssistant.pkg)，安装方法和beta2相同，启动盘变成preboot可安装IntelPowerGadget解决，
- readme 20.7.21版
- 完美从10.15.5更新10.15.6
- 另外成功全新安装上macOS Big Sur Beta2，和在Catalina一样触摸板电池蓝牙等各部件使用正常，但是暂时USB网卡驱动不太好装
- 安装过程：使用安装新系统的EFI进Catalina，格式化安装分区，使用的Big Sur beta2[下载地址](http://swcdn.apple.com/content/downloads/04/19/001-23553-A_1O2KYISWEK/58hrejz970xje070in5dorjoovnmw61x03/InstallAssistant.pkg),点击下载的pkg文件会生成一个安装app，运行后选择安装位置就可安装，会自动重启，重启好了在OC界面选择install，跑码，期间会重启多次，跑码完毕进入安装进度条，自动重启，在OC界面自动进入pre开头选项，重启进入安装分区名字选项进入新系统
- 使用感受：状态栏由于不能驱动Wi-Fi会卡顿，比Catalina耗电，UI有平板内味，暂时不能作为主力机系统使用
- readme 20.7.5版
- 可尝试恢复安装macOS11来尝鲜新系统，增加相应链接资料
- readme 20.7.2版
- 尝试直升11失败
- 制作了蓝牙空壳驱动，删掉了复杂的蓝牙文件修改
- 将设备仿冒为最新的MacBook Pro2020
- HDMI端口已修正

## 1.我的笔记本配置

| 电脑信息  |    |
| ------ | -------- |
| 电脑型号 |  Samsung 8500GM-X06 |
| 处理器 |  i5-7300HQ  |
| 内存 |  16G 2133 MHZ DDR4 |
| 声卡 |  ALC256 |
| 核显 |  HD630（英伟达独显新系统无解老系统无测试） |
| 网卡 |  高通AR9377板载无解 （自购USB网卡,我买的comfast）|

- 经测试玄龙骑士7700HQ等其他型号也可以

## 2.使用说明

- 推荐使用propertree或者OCC编辑OC配置文件，OCC需要对应OC版本,PlistEditPro或者Xcode也可以，我自己用的propertree
- 使用[黑果小兵](https://blog.daliansky.net)上面镜像，安装过程[参考](https://blog.daliansky.net/MacOS-installation-tutorial-XiaoMi-Pro-installation-process-records.html) ，做好启动盘后替换成本EFI，有问题仔细看本前言。
- 自行购买USB网卡或者插网线联网工作，我买的comfast的CF-WU810N的USB网卡
- 安装系统：11.2.1(20D74)
- 使用opencore版本：0.6.7
- 工作完美：蓝牙（本项目自制空壳驱动解决）、电量显示（本项目自制SSDT补丁解决）、原生电源管理、触摸板、键盘、鼠标、亮度调节、核显硬解、USB定制、睡眠、类白果启动、HDMI、隔空投放、声音、CPU睿频、H264解码、HEVC解码、有线网卡
- 不能工作：英伟达独显、内置无线网卡、airport（受限无线网卡焊死不可拆不能工作）、随航
- 本机型7300HQ+1050配置HDMI外接显示器完美，但对于7700HQ+1060配置HDMI外接有问题
- 初学者建议使用本项目最早发布[clover版EFI](https://github.com/xiaonaitang/Samsung8500GMHackintosh/releases/tag/V1.0)配合10.4.6系统，有所了解后还是建议使用OC上最新Big Sur系统，除最早发布外基本都是OC引导。可装系统版本14.2-11.2.1
- 项目[下载地址](https://github.com/xiaonaitang/Samsung8500GMHackintosh/releases)
- 亮度调节经过本项目努力下，映射和win一样的FN+F2/F3快捷键。

## 3.问题和解决

- 1.Big Sur开启系统权限操作很复杂，catalina系统开启系统文件修改权限需要打开终端依次输入
- sudo su(输入本机密码，不会显示出来）
- sudo mount -uw /
- killall Finder（注意是F不是f)
- 更推荐你尝试这个[链接](https://www.bugprogrammer.me/2019/07/13/unlockSystem.html)使得Catalina开机就开启系统文件修改权限，但可能进系统程序运行屏幕会刷新一下，介意的话不必弄了
- 2.进系统后接鼠标进偏好设置，触摸板里把轻触点击打开体验会好很多，辅助功能里打开三指移动功能会很好用。如果不识别触摸板，开启上述文件修改权限，不能关闭终端，然后用kext utility或者hackintool软件重建缓存一下，重启看能不能识别，倘若还不识别我也没得法子，release里有我补充一些触摸板相关资料，本项目没研究下去了
- 4.声音ALC256注入ID为56，57，这个数值的来源是查看aplealc驱动里面右键显示包内容的info.plist文件查到的ALC256注入ID，声音有时候进系统没声音不能调节，可关机开机解决或者更换ID，更换ID的位置在config.plist文件的deviceproperties/add/声卡PCI路径/layoutid，或者启动参数添加ALC=XX这样参数
- 目前为止你可以直接使用EFI安装体验Mac系统了，如果有什么问题再往下看

## 4.OC的EFI配制方法

- 有点长，我会说的简明些，记录自己从无到有配置玄龙骑士，走过的坑吃过的亏，避免后来者踩坑！
- 参考xjn大佬的 [OC博客](https://blog.xjn819.com/?p=543) 来修改制作文件,这里提一些和博客内容不同的本机型设置

### 4.1 资料文件准备
- 这些驱动只是为了本项目做个链接指引，你可以无视这些链接继续往下看
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
- FakeAppleUSBMouse   仿冒白果USB鼠标驱动
- NoTouchID    解决MacBook Pro15以上机型卡ID问题驱动
- RealtekRTL8111   有线网卡驱动
- Samsung8500GMBluetoothInjector   本机型蓝牙能开能关驱动
- SMCBatteryManager    电池驱动需要配合电池SSDT布丁
- SMCLightSensor    亮度传感器驱动配合亮度SSDT驱动能自动调节亮度
- SMCProcessor    处理器传感器驱动
- SMCSuperIO。  总线驱动
- SystemProfilerMemoryFixup   像白果一样关于本机有显示内存一项驱动
- USBPorts      定制USB驱动
- VoodooI2CHID      触摸板驱动
- VoodooInput     voodoo依赖驱动
- VoodooPS2Controller     键鼠驱动
- [OC-little-master](https://github.com/daliansky/OC-little)    宪武大佬OC补丁

### 4.2 利用clover引导获取本机DSDT.aml文件

- 将本机clover的EFI放入U盘的EFI分区，开机U盘启动，在clover主题界面，按一下F4键，不会有任何反应，进系统后在EFI/clover/ACPI/origin文件里有一个DSDT.aml文件，其他文件也可保留可反编译用。这个文件是为了配合宪武补丁来寻找代码使用的，本项目已经把能打的补丁都做好了，如发现有问题可提取文件自制补丁

### 4.3 注意事项

- CFG主板默认没解锁，需要以下设置
kernel/Quirks/AppleCpuPmCfgLock设置true，kernel/Quirks/AppleXcpmCfgLock设置true，UEFI/Quirks/IgnoreInvalidFlexRatio设置true
- USB没有定制的话需要用USBinjectall.kext，并且kernel/Quirks/XhciPortLimit设置true,定制好USB驱动就可以设置false，当然本项目集成好USB驱动如无问题可不管
- 空壳驱动相较于完整驱动，在config.plist文件中kernel/Add/ExecutablePath是留空的，比如定制USB的驱动USBport就是空壳驱动，因为驱动右键显示包内容，只有一个info.plist文件没有其他文件，需要注意与其他非空壳驱动在config.plist文件中的区别。
- FakeAppleUSBMouse.kext这个驱动是仿冒苹果鼠标的，使用要在关于本机/系统报告/USB找到自己鼠标，查看厂商ID和产品ID，转换成16进制修改进FakeAppleUSBMouse.kext右键包展开里的info.plist最后的厂商和产品数值，使用后系统偏好设置/鼠标里面能够设置鼠标各个键的功能。
- config.plist文件中Misc/Boot/ShowPicker为是否显示OC启动选择项，Timeout为显示的时间秒，Misc/Security/ScanPolicy为OC的扫描策略，具体怎么算出来的可以用OCC计算出来，我设置的是只扫描MAC盘，改成0就是全部格式都扫描
- 三码用OCC或者clover编辑器都能生成相应的码，config.plist里面需要填写机型信息
- 如果安装过程中遇到安装包损坏之类报错，可问度娘，大概原因是因为机型和系统以及时间不太匹配导致的，临时修改时间即可解决

### 4.4 SSDT文件说明

- [SSDT编辑器下载](https://github.com/acidanthera/MaciASL/releases)
- SSDT-BAT 电池补丁，需要配合电池重命名以及SMC电池驱动或者R神的电池驱动，本项目参考大量教程制作电池补丁，大体完美但可能有瑕疵
- SSDT-EC-USBX-PLUG  三补丁合一，仿冒EC部件，增加USB插入苹果手机能快充以及原生电源管理，添加后偏好设置/节能里有四项
SSDT-GPRW、SSDT-DeepIdle、SSDT-LIDpatch-AOAC、SSDT-S3-disable、SSDT-WakeScreen、SSDT-PTSWAK解决睡眠问题几大补丁，本子采用了AOAC技术，对睡眠影响很大，不加补丁会使得睡眠睡死
- SSDT-HRTF  声卡补丁，屏蔽原有的几个声卡相关的部件并仿冒里部件起作用，还是有一定概率无声音只不过比之前好多了
- SSDT-MEM2-PMCR-DMAC、SSDT-SBUS-MCHC、SSDT-SLPB缺失部件，即白果有的部件而我们本子ACPI没有的部件
- SSDT-NVMe  nvme补丁，修正一些错误显示
- SSDT-PNLF-ALS0  调节亮度，偏好设置/显示器有亮度自动调节按钮，需要配合SMC的light驱动
- SSDT-Q63Q64   亮度快捷键映射补丁，使得Mac里面能够和win用一样的快捷键，需要配合亮度重命名使用，并且偏好设置/快捷键里面亮度调节的快捷键必须是默认的F14F15调节
- SSDT-SPTP-GPEN-XOSI  触摸板补丁，配合I2C两个驱动，值得注意的是这个补丁进win蓝屏，所以并不推荐OC进win
- SSDT-DGPU 屏蔽独显

## 5.HIDPI开启和关闭

- HIDPI字面意思就是高DPI，通俗来说好比拿两三个像素点渲染一个像素，所以开启后分辨率设置越低，画面越清楚，但同时字体界面啥的会变大，一般建议4K显示开启，但如果自己喜欢也可以开启，毕竟眼睛怎么舒服怎么来
- 需要注意的是开启后OC下进度条前后半段图标大小不一致，可以设置前后半段一样的大小NVRAM/Add/4D1E..../UIScale设置01就是默认大小02就是开启HIDPI后放大了的大小
- 首先需要开启系统文件修改权限
- 使用终端一键开启HIDPI代码[详细请看](https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md)
- 上条代码用不了可以用[国内的代码](https://www.sqlsec.com/2018/09/hidpi.html)

## 6.HDMI

- 通过hackintool可以修改缓冲祯，修改端口定义来使得HDMI能够使用，在应用补丁里面设置好信息参数，Kaby lake,0x591B0000,基本显存和缓冲祯默认，接口这要把除了第一条索引，其他两条全改为HDMI而不是其他的类型，第一条LVDS是笔记本自带的屏幕无需修改，应用补丁/通用里面取消勾选自动侦测变化，勾选设备属性，接口，基本显存，图形卡，高级里面勾选仿冒图形卡、修复热拔插重启、HDMI无限循环修复、禁用egpu,VDMT32预分配、显存2048MB，启用HDMI20，点击生成补丁，点击左上角文件-导出-config.plist，将参数添加到OC的配置文件的device properties对应的PCI里面。

## 7.hackintool

- 这一软件有很多用法，可参考小兵的hackintool教程,内核扩展可查看用到的驱动版本，显示器选项玩法多，可生成HIDPI文件，可解决部分显示问题，USB部分可定制USB驱动，PCIE部分可查看部件的PCI路径，声音部分可直接查看当前声卡型号可以用什么注入ID，电源部分可点击底部修复深度睡眠解决部分睡眠问题，计算机部分可计算进制，工具部分挺多工具，可重建缓存，可查看一些参数例如CFG是否锁，日志可查看开机的代码，可查看是否有error并解决

## 8.Fusion Drive组建

- 目的是为了将小容量固态和大容量机械组合成融合硬盘，达到固态读写速度，不组建可跳过
- 确认电脑固态硬盘和机械硬盘已经全盘备份好资料。
- 打开macOS实用工具-终端，输入命令“diskutil resetFusion”并按回车键。
- 出现提示时键入Yes，大小写要严格对应，按回车键完成。
- 目前OC19年6月以后版本仅支持nvme+HDD不支持sata+HDD，6月之前版本不支持fusiondrive
- [参考资料1](https://post.smzdm.com/p/a3gv9n0k/)
- [参考资料2](https://www.jianshu.com/p/d4e1fd94dcef)

## 9.一些资料链接

- [Mac推荐的小软件](https://www.zuiyu1818.cn/posts/Mac_software1.html)
- [非常好用的Mac应用程序、软件以及工具](https://github.com/jaywcjlove/awesome-mac/blob/master/README-zh.md)
- [iOS开发常用三方库、插件、知名博客等](https://github.com/Tim9Liu9/TimLiu-iOS)
- [Mac software Homepage](https://mac.softpedia.com)
- [触摸设备DSDT修补补充](https://github.com/williambj1/VoodooI2C-PreRelease/blob/master/触摸板补充.md)
- [CFG解锁详细说明](http://bbs.pcbeta.com/viewthread-1834965-1-2.html)
- [参考暗影精灵3EFI](https://github.com/shimakazechan/OMEN-by-HP-3-Hackintosh)
- [利用AppleALC驱动声卡(也推荐此博客)](https://blog.tlhub.cn/Driver-audio-for-hackintosh.html)
- [NDK版opencore引导](https://github.com/n-d-k/OpenCorePkg)
- [解决iMessage与Facetime以及苹果三码的问题](https://blog.csdn.net/weixin_40684028/article/details/85270633)
- [黑苹果自定义键盘Fn快捷键(也推荐此博客)](https://blog.skk.moe/post/ssdt-map-fn-shortcuts/)
- [HDMI音频资料](https://github.com/xxxzc/xps15-9570-macos/issues/12)
- [黑苹果英特尔全系核显显卡驱动教程](http://bbs.pcbeta.com/viewthread-1849099-1-2.html)
- [FCPX核显独显全程满速指南](http://bbs.pcbeta.com/viewthread-1836920-1-4.html)
- [黑苹果安装macOS11](https://xiaobaistudio.com/AMD黑苹果安装macOS-11.html)
- [黑苹果如何调整风扇的转速](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1037700&ordertype=1)

## 10.致谢

- [远景论坛](http://bbs.pcbeta.com)
- 参考[xjin大佬博客](https://blog.xjn819.com/?p=543)
- 国内外许多驱动开发者
- 本机型和相似电脑的前辈工作积累
- [黑果小兵](https://blog.daliansky.net)和[len的镜像](http://bbs.pcbeta.com/viewthread-1836586-1-2.html)以及安装教程;
- [宪武大佬大量补丁](https://github.com/daliansky/OC-little)工作和指导，尤其让我对重命名有深刻理解
       
## 欢迎加入同机型交流群（群号:588964385）讨论完善！
