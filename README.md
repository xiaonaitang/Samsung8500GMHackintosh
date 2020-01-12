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
— 使用黑果小兵镜像，参考小兵教程制作安装启动盘
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
如果你决定使用clover作为你黑苹果引导的话请看本节，否则不必看


## 5.OC使用说明
如果你决定使用OC引导的话请看本节，否则不必看
OC添加生成的信息
![Image text](https://https://raw.githubusercontent.com/xiaonaitang/Samsung8500GMHackintosh/master/images/addsysteminfo.png)

试试


## 6.HIDPI开启
将HIDPI文件夹下的DisplayVendorID-9e5和Icons.plist文件复制替换到S/L/Displays/Contents/Resources/Overrides
最好备份一下原有的Icons.plist
重启生效




## 你品，你细品！
## 欢迎加入同机型交流群讨论完善！

