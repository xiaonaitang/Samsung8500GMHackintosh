# Samsung8500GM黑苹果引导
三星玄龙骑士一代黑苹果接近完美引导
最终效果
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/computerinfo.png)

# 目录

| 章节  | 内容  |
| ------ | -------- |
| 1 |  电脑配置 |
| 2 |  使用效果 |
| 3 |  致谢 |
| 4 |  clover使用说明 |
| 5 |  OC使用说明 |
| 6 |  HIDPI开启和关闭 |
| 7 |  BIOS隐藏选项设置 |
| 8 |  开启系统文件权限 |
| 9|  相关软件 |
| 10 |  文件提取 |
| 11 |  OC热补丁定制 |
| 12 |  其他优化 |
| 本机型QQ交流群 |  588964385 |



## 1.电脑配置

| 电脑信息  |    |
| ------ | -------- |
| 电脑型号 |  Samsung 8500GM-X06 |
| 处理器 |  i5-7300HQ 2.5G/3.5G |
| 内存 |  8G 2133 MHZ DDR4 |
| 声卡 |  ALC256 |
| 核显 |  HD630（独显无解） |
| 网卡 |  高通AR9377板载无解 |

## 2.使用效果
- 使用黑果小兵镜像，参考小兵教程安装
- 自行购买USB网卡联网工作
- 没有测试HDMI外接显示器有无问题
- 随航应该不行

### 2.1clover效果
- 安装系统：MacOS1.14.3-10.15.2，推荐10.14.6系统
- 工作完美：电量显示、触摸板、键盘、鼠标、亮度调节、核显硬解
- 不能工作：独显、内置网卡、声音和蓝牙一定几率有问题、USB端口可能有问题、airport

### 2.2opencore效果
- 安装系统：10.15.2
- 使用opencore版本：0.5.4
- 工作完美：蓝牙、电量显示、原生电源管理、触摸板、键盘、鼠标、亮度调节、核显硬解、USB定制、睡眠、类白果启动
- 不能工作：独显、内置网卡、airport

## 3.致谢
- [远景论坛](http://bbs.pcbeta.com)
- 参考[xjin大佬博客](https://blog.xjn819.com/?p=543)
- 国内外许多驱动开发者
- 本机型和相似电脑的前辈工作积累
- [黑果小兵](https://blog.daliansky.net)和[len的镜像](http://bbs.pcbeta.com/viewthread-1836586-1-2.html)以及安装教程;
- [宪武大佬大量补丁](https://github.com/daliansky/OC-little)工作和指导，尤其让我对重命名有深刻理解
- 感谢玄龙骑士群友的帮助和问题反馈（玄龙Hackintosh QQ群号588964385）

## 4.clover使用说明
- EFI目录就是clover引导文件，注意事项参照[clover目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/blob/master/EFI/使用方法.txt)里说明，目前clover引导我不再维护

## 5.OC使用说明
- 如果你不决定使用OC引导的话不必看本节

![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/loser.jpg)

### 5.1 总述
    OC全称opencore，是一个着眼于未来开源引导工具, 最初诞生于HermitCrabs实验室, 现在接手于Acidanthera, 其目的是创造一个更加严谨的模组化的轻量引导系统。尽管 OpenCore 的主要用途是黑苹果, 它也支持其它操作系统的引导，目前本EFI的OC引导win10有问题不建议尝试。
    是一种更加接近原生Mac的新引导方式，体现在：
    1.开机可以更加白果，直接进系统不出现选择启动盘页面（会有配置文件介绍）
    2.使用原生电源管理，可进一步优化睿频（还没做）
    3.提高开机速度体验，文件结构更精简

- 推荐使用Propertree编辑配置文件,PlistEditPro也可以

### 5.2 plist文件说明（文件有问题还没上传四个文件）
    1.所有文件都需要你加三码，如需使用重命名为config.plist，放在EFI/OC路径里面
    2.config1.plist：已解锁CFG和DVMT等bios设置，默认开机无启动盘选择界面,直接进Mac，按esc键出现选择启动盘界面
    3.config2.plist：已解锁CFG和DVMT等bios设置，开机有启动盘界面，扫描所有启动项可供选择，停留10秒钟待选择
    4.config3.plist：没有解锁CFG和DVMT等bios设置，默认开机无启动盘选择界面,直接进Mac，按esc键出现选择启动盘界面
    5.config4.plist：没有解锁CFG和DVMT等bios设置，开机有启动盘界面，扫描所有启动项可供选择，停留10秒钟待选择

### 5.3 OC文件加三码
- 因为目前的opencore还没有内置苹果三码的生成，所以需要利用clover编辑器生成的机型信息码

选择机型，推荐选择MacBook Pro14.2机型
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/change.png)

添加clover编辑器生成的机型信息码
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/info.png)

添加到这个位置
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/addsysteminfo.png)

退出保存

## 6.HIDPI开启和关闭
- 不建议开启HIDPI，OC下进度条中间会黑一下很不友好，而且进度条前后半段图标大小不一致
- HIDPI是苹果一项缩放设置技术，优化屏幕缩放显示效果，建议至少2K屏幕使用
- 首先需要开启系统文件修改权限（有说明）
- 将HIDPI文件夹下的DisplayVendorID-9e5和Icons.plist文件复制替换到S/L/Displays/Contents/Resources/Overrides
- 最好备份一下原有的Icons.plist
- 重启生效
- 还原的话需要删掉这两个文件并将备份的文件还原
- 也可以不采用这方式而使用终端一键开启HIDPI代码[详细请看](https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md)

## 7.BIOS隐藏选项设置
- 我个人解锁了cfg和DVMT等bios设置，强烈推荐你这么做，能更完美
- 如果你选择不解锁bios隐藏设置也行，但需要使用合适的config文件，而且本节不用看了

- 照搬小兵博客设置

| 禁用  |    |
| ------ | -------- |
| Fast Boot |  快速启动 |
| CFG Lock (MSR 0xE2 write protection) |  CFG 锁 (MSR 0xE2 写入保护) |
| VT-d |  VT-d |
| CSM |  兼容性支持模块 |

| 启用  |    |
| ------ | -------- |
| VT-x |  VT-x |
| Above 4G decoding |  大于 4G 地址空间解码 |
| Hyper Threading |  处理器超线程 |
| Execute Disable Bit |  执行禁止位 |
| EHCI/XHCI Hand-off |  接手 EHCI/XHCI 控制 |
| OS type: other types |  操作系统类型: 其他 |

- 实际上只需要解锁CFG lock和DVMT大小等几项设置,但最好把所有的设置都看一遍
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
- 更推荐你尝试这个[链接](https://www.bugprogrammer.me/2019/07/13/unlockSystem.html)使用的方法来使得Catalina开机就开启系统文件修改权限
日常使用中一些软件没有系统修改权限不能安装
## 9.相关软件
    Hackintool:黑果工具
    IORegistryExplorer:查看一些系统总线关系
    Kext Utility:重建缓存软件
    MaciASL:编辑修改ACPI文件
    ProperTree:OCconfig编辑器
    PlistEdit Pro:OCconfig编辑器
- [soft目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/tree/master/soft)下是一些可能需要使用到的软件
## 10.ACPI文件提取
- [origin目录](https://github.com/xiaonaitang/Samsung8500GMHackintosh/tree/master/origin)下是我机子提取出的原生ACPI文件，本节说明提取方法
待更（拖更）
## 11.OC热补丁制定制
- 出现相关问题需要定制热补丁可查看此节
- 实际上本机型OC相关补丁我也经制作好，但可能同型电脑设备和我稍有差异，若如此可自行翻阅本节制作属于你们机子的热补丁
### 11.1电池
待更（拖更）
### 11.2触摸板
待更（拖更）
### 11.3亮度
待更（拖更）

## 12.其他优化
待更（拖更）
       
## 欢迎加入同机型交流群讨论完善！
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/QQ.png)
