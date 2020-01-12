# Samsung8500GM黑苹果引导
修改制作的三星玄龙骑士一代黑苹果接近完美引导文件。
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/computerinfo.png)


## 1.电脑配置

| 电脑信息  |    |
| ------ | -------- |
| 电脑型号 |  Samsung 8500GM-X06 |
| 处理器 |  i5-7300HQ 2.5G/3.5G |
| 内存 |  8G 2133 MHZ DDR4 |
| 声卡 |  ALC256 |
| 核显 |  HD630（独显无解） |
| 网卡 |  AR9377板载无解 |

## 2.clover使用结论
- 使用黑果小兵镜像，参考小兵教程制作安装启动盘
- 使用USB网卡联网工作
###2.1clover结论
- 安装系统：MacOS1.14.3-10.15.2
- 工作完美：电量显示，触摸板，亮度调节、核显硬解
- 不能工作：独显，内置网卡，声音和蓝牙一定几率有问题、USB端口可能有问题
###2.2opencore结论
- 安装系统：10.15.2
- 工作完美：蓝牙、电量显示，原生电源管理、触摸板、亮度调节、核显硬解、USB定制、睡眠
- 不能工作：独显、内置网卡

## 3.在此致谢
- 远景论坛
- 国内外许多驱动开发者
- 本机型和相似电脑的前辈工作积累
- 黑果小兵和len的镜像以及安装教程;
- 宪武大佬大量补丁工作和指导，尤其让我对重命名有深刻理解
- 感谢玄龙骑士群主的帮助以及群友的问题反馈（玄龙Hackintosh QQ群号588964385）

## 4.clover使用说明
- 如果你决定使用clover作为你黑苹果引导的话请看本节，否则不必看
- clover编辑器集成了三码，不必再设置但你最好设置一下免得和别人用一样的码
- 详细说明参照clover目录里面的说明设置即可

## 5.OC使用说明
- 如果你决定使用OC引导的话请看本节，否则不必看
- OC是一种更加接近原生Mac的新引导方式，推荐使用propertree编辑配置文件
- 我配置的oc引导文件默认只认Mac盘并进入Mac，开机没有选择界面，如需选择请按esc键即可
- OC需要添加clover编辑器生成的机型信息码
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/addsysteminfo.png)

- 我个人解锁了cfg等bios设置，没有解锁的不推荐使用我的config文件，需要修改一些设置。

## 6.HIDPI开启和关闭
- 将HIDPI文件夹下的DisplayVendorID-9e5和Icons.plist文件复制替换到S/L/Displays/Contents/Resources/Overrides
- 最好备份一下原有的Icons.plist
- 重启生效
- 还原的话需要删掉这两个文件并将备份的文件还原
- 不建议开启HIDPI，进度条中间会黑一下很不友好，而且图标大小前后不一致
## 7.bios隐藏选项设置
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

- 具体方法查看该目录下说明文档
## 你品，你细品！
## 欢迎加入同机型交流群讨论完善！
![Image text](https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/QQ.png)
