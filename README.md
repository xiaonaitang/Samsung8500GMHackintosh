# Samsung8500GM黑苹果引导
列个计划吧我头晕
增加HDMI端口修正方法
增加OC从无到有配置方法
修改以前的胡言乱语
增加驱动编译方法（可能不需要
增加一些小技巧助力使用macOS
努力出个针对本机型特点的装macOS视频吧QWQ（过段时间，其实我写文字也比较累）
增加一些其他资源链接
打赏我就免了本来都是开源的东西
普及一些黑果奇怪的知识
尽力写到最好让我满意为止
等满意了我就出掉玄龙骑士了哈哈哈哈
头秃了昂
为什么显示不了图片啊，简直了
姑且叫readme2.0吧，因为真的要改好多东西内容
也方便别人用我efi能尽可能达到完美吧，也希望读者能完整看完吧，尚不辜负我一番心思
三星玄龙骑士一代黑苹果接近完美引导
我得花几天时间重写这部分，准备写个本机型最全的readme，我太难了
最终效果
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/computerinfo.png)

# 目录



## 1.笔记本配置

| 电脑信息  |    |
| ------ | -------- |
| 电脑型号 |  Samsung 8500GM-X06 |
| 处理器 |  i5-7300HQ 2.5G/3.5G |
| 内存 |  16G 2133 MHZ DDR4 |
| 声卡 |  ALC256 |
| 核显 |  HD630（独显无解） |
| 网卡 |  高通AR9377板载无解 （自购USB网卡（我买的很便宜就不放出来商品链接了）|

tips:经测试玄龙7700HQ的型号也可以

## 2.使用OC效果
- 使用黑果小兵镜像，参考小兵教程安装，就是要做好启动盘，替换成我的EFI
- 自行购买USB网卡或者插网线联网工作
- 安装系统：10.15.4（我暂时稳定用这个系统了）
- 使用opencore版本：0.6.0
- 工作完美：蓝牙、电量显示、原生电源管理、触摸板、键盘、鼠标、亮度调节、核显硬解、USB定制、睡眠、类白果启动、HDMI、隔空投放
- 不能工作：独显、内置网卡、airport
- 本机型15.4及以下HDMI外接显示器完美，但对于7700HQ+1060+Catalina15.5的机子HDMI始终不行，猜测可能HDMI走独显无法驱动或者15.5的问题
- 随航隔空投放不行
- clover能使用，起码我15.2之前还用的好好的，虽然有些瑕疵吧，推荐clover上14.6系统，我不更新了，后面有一小部分关于clover的内容（还没写）



## 4.clover使用说明
- EFI目录就是clover引导文件，注意事项参照[clover目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/blob/master/EFI/使用方法.txt)里说明，目前clover引导不再维护

先说明结论
使用本efi完美使用Mojave10.14.3-Catalina10.15.2系统
蓝牙、亮度、电池、触摸板、声音、核显、CPU睿频、H264解码、HEVC解码均无问题
独显、网卡无解使用USB网卡上网，不排除使用过程中偶发性出现其他问题。

注意事项:

有两种安装方法可供您选择
1.使用本引导文件在Mojave系统下，在系统偏好设置或者App Store中更新Catalina系统；
2.使用黑果小兵镜像的10.15.1（或者10.15.2）镜像文件（百毒云下载链接: https://pan.baidu.com/s/1OG8Dm88bH66A38E0_ek0yg 提取码: 5tub）制作完成启动盘，将镜像自带EFI删除粘贴本EFI安装Catalina
安装教程参考小兵教程（https://blog.daliansky.net/MacOS-installation-tutorial-XiaoMi-Pro-installation-process-records.html）。

安装好进系统后的必要设置！！！：
1.进系统亮度不能调节因为键盘映射有问题，需自行修改亮度调节快捷键，路径为系统偏好设置-键盘-快捷键-显示器，最好刚安装好系统第一次进了系统进行调整，之后进系统打开偏好设置有一定概率会没有显示器选项。
2.进系统蓝牙不能关闭，请修改蓝牙硬件驱动ID，具体做法分为两步，开启文件移动权限和修改文件。
catalina系统下开启文件权限需要打开终端依次输入sudo su
Sudo mount -uw /
Killall Finder
修改文件具体为将S/L/E路径中的IOBluetoothFamily.kext/右键显示包内容/Contents/PlugIns/BroadcomBluetoothHostControllerUSBTransport.kext/右键显示包内容/Contents/Info.plist，将这一文件拖出，例如放到桌面一份，使用文本编辑打开，在IOKitPersonalities属性中找到第一个，注意是第一个com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport属性，修改其中的idProduct下一行数字为58624，idVendor下一行数字为3315，保存文件，将桌面修改好的文件再次拖进文件原位置，替换。
最后推荐使用kext utility重建缓存
3.刚进系统一定概率触摸板不能识别可外接鼠标使用，重建缓存后拔掉鼠标重启即可识别
4.本EFI默认开启啰嗦模式方便排错，安装好可自行关闭啰嗦模式，即使用clover configurator软件打开config文件去掉引导-v参数。
5.声音ALC256注入ID为5，如遇有问题可关机开机解决或者更换注入ID，注入ID可通过查询efi中的applealc驱动文件，也可以更换这一声音驱动文件的同时不要忘了更换相应的注入ID。

希望你能食用愉快。

## 5.OC使用说明
- 如果你不决定使用OC引导的话不必看本节

![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/loser.jpg)

# 前言
- 记录自己从无到有配置玄龙骑士，走过的坑吃过的亏，避免后来者踩坑！
# 目录
## 1.资料准备
### a.在OC官方维护者主页能[下载](https://github.com/acidanthera)到大部分所需文件
具体为:
- [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases)    OC官方更新包
- [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)   驱动电池CPU等
- [AppleSupportPkg](https://github.com/acidanthera/AppleSupportPkg/releases)  苹果文件格式驱动
- [CPUFriend](https://github.com/acidanthera/CPUFriend/releases)       定制CPU电源管理
- [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)    核显驱动
- [Lilu](https://github.com/acidanthera/Lilu/releases) 综合型驱动 
- [VoodooPS2](https://github.com/acidanthera/VoodooPS2)  键盘触摸板驱动
- [AppleALC](https://github.com/acidanthera/AppleALC/releases)  声卡驱动
- [NVMeFix](https://github.com/acidanthera/NVMeFix/releases)   NVME固态修补驱动（可选）
- [VoodooInput](https://github.com/acidanthera/VoodooInput/releases)   妙控板拓展驱动（可选）

### b.其他必须的驱动
### c.宪武大佬OC补丁[OC-little-master](https://github.com/daliansky/OC-little)
### d.利用clover引导获取本机DSDT文件得到origin文件夹
e.


## 2.文件结构
如图所示
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/list.png)

## 3.config设置
如图所示
## 4.电池补丁制作
补丁原理：
## 5.触摸板补丁制作
补丁原理：
## 6.其余补丁完善

## 7.错误和解决



### 5.1 总述
    OC全称opencore，是一个着眼于未来开源引导工具, 最初诞生于HermitCrabs实验室, 现在接手于Acidanthera, 其目的是创造一个更加严谨的模组化的轻量引导系统。尽管 OpenCore 的主要用途是黑苹果, 它也支持其它操作系统的引导，目前本EFI的OC引导win10有问题不建议尝试。
    是一种更加接近原生Mac的新引导方式，体现在：
    1.开机可以更加白果，直接进系统不出现选择启动盘页面（会有配置文件介绍）
    2.使用原生电源管理，可进一步优化睿频（还没做）
    3.提高开机速度体验，文件结构更精简

- 推荐使用propertree编辑OC配置文件,PlistEditPro也可以

### 5.2 OC文件加三码
- 使用propertree添加机型信息


## 6.HIDPI开启和关闭
- HIDPI字面意思就是高DPI，通俗来说好比拿两三个像素点渲染一个像素，所以开启后分辨率设置越低，画面越清楚，但同时字体界面啥的会变大，一般建议4K显示开启，但如果自己喜欢也可以开启，毕竟眼睛怎么舒服怎么来，这是我的个人理解
- 需要注意的是开启后OC下进度条中间会黑一下，而且进度条前后半段图标大小不一致，当然可以设置前后半段一样的大小
- 首先需要开启系统文件修改权限（请看第八节）
- 使用终端一键开启HIDPI代码[详细请看](https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md)
- 上条用不了可以用国内的镜像代码我待会更新

## 7.BIOS隐藏选项设置（有风险我还是考虑要不要删了吧
- 我个人使用OC并解锁了cfg和DVMT等bios设置，推荐你这么做，不做也没关系可以打补丁小兵上有教程自己去了解吧，我待会移植过来相关内容
- 主要就是两个
| 禁用  |    |
| ------ | -------- |
| CFG Lock (MSR 0xE2 write protection) |  CFG 锁 (MSR 0xE2 写入保护) |

| 调整  |    |
| ------ | -------- |
| DVMT |  64M |

- 使用hackintool工具确认是否解锁了cfg lock
1.点击工具
2.点击intel图标
3.输入密码确定，找到cfg lock参数
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/hack.png)

cfg lock显示为0即已经在bios中解锁
- 具体解锁操作看该目录下[说明文档](https://github.com/xiaonaitang/Samsung8500GMHackintosh/blob/master/修改BIOS隐藏选项/使用方法.txt)
## 8.开启系统文件权限
     sudo su
     (输入本机密码，不会显示出来）
     sudo mount -uw /
     killall Finder
    
- 终端输入如上命令
- 更推荐你尝试这个[链接](https://www.bugprogrammer.me/2019/07/13/unlockSystem.html)使用的方法来使得Catalina开机就开启系统文件修改权限，但可能进系统程序运行屏幕会刷新一下，介意的话不必弄了
- 日常使用中一些软件没有系统修改权限不能安装，我会说明一些（待会儿）
## 9.相关软件
    Hackintool:黑果工具
    IORegistryExplorer:查看一些系统总线关系
    Kext Utility:重建缓存软件
    MaciASL:编辑修改ACPI文件

- [soft目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/tree/master/soft)下是一些可能需要使用到的软件
## 10.ACPI文件提取
- [origin目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/tree/master/origin)下是我机子提取出的原生ACPI文件，本节说明提取方法
待更（拖更）
## 11.OC热补丁制定制
- 出现相关问题需要定制热补丁可查看此节
- 实际上本机型OC相关补丁我也经制作好，但可能同型电脑设备和我稍有差异，若如此可自行翻阅本节制作属于你们机子的热补丁
### 11.1电池
待更（拖更）参考套路的教程
### 11.2触摸板
待更（拖更）参考套路的教程
### 11.3亮度
待更（拖更）

## 12.其他优化
待更（拖更）

## 3.致谢（应该放最后，瞎搞
- [远景论坛](http://bbs.pcbeta.com)
- 参考[xjin大佬博客](https://blog.xjn819.com/?p=543)
- 国内外许多驱动开发者
- 本机型和相似电脑的前辈工作积累
- [黑果小兵](https://blog.daliansky.net)和[len的镜像](http://bbs.pcbeta.com/viewthread-1836586-1-2.html)以及安装教程;
- [宪武大佬大量补丁](https://github.com/daliansky/OC-little)工作和指导，尤其让我对重命名有深刻理解
- 感谢玄龙骑士群友的帮助和问题反馈（玄龙Hackintosh QQ群号588964385）
       
## 欢迎加入同机型交流群讨论完善！
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/QQ.png)
