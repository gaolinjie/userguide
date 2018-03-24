# UEFI 下的 Windows 10 与 Ubuntu 16.04.1 共存安装教程

因为本吧内绝大多数教程过时、沉贴等问题
特开一贴UEFI安装教程

本教程基于
I5-4590
技嘉B85M-D3V-A
HD4600核显
8G内存
西数1T蓝盘 【硬盘为GPT分区表】
机器已经安装好了Windows10 专业版 1607 X64

---

## 第一步
Ⅰ：下载：
不建议安装所谓中国版的 ubuntu 也就是 Ubuntu Kylin
没有为什么
请自行官网下载原版（国际版）Ubuntu
这里用 16.04.1 64 位版作为例子
Ⅱ：制作 U 盘镜像：
请自行百度一个下载一个 软碟通
然后在如图所示 点击 写入硬盘映像 按钮
![1](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/1.jpg)

然后选择你的 u 盘 然后点写入
然后启动 u 盘就制作好了
Ⅲ：分区：
请自行百度 DiskGenius
然后把想要装 ubuntu 的分区删除 让它成为一个空闲分区 就像 lz 的这样
![2](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/2.jpg)

然后准备工作就做完辣

## 第二步：
选择 u 盘的 uefi 启动 也就是图中高亮的那个
lz 的电脑在 bios 里设置了仅用 uefi 启动 所以不会显示传统启动的启动项
由于 u 盘品牌不一 所以显示的也不尽相同 反正是 uefi 开头的那个非硬盘就好
![3](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/3.jpg)

接下来选择第二个选项
Install Ubuntu
这个我就不上图了

如果硬盘是 gpt 分区 一定要用 uefi 启动, 硬盘是 mbr 一定要用传统启动,否则一定会识别不到硬盘。

![4](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/4.jpg)
左侧选择中文
然后点继续
![5](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/5.jpg)

这里什么也不要选 要不会安装的很慢很慢

这里就是关键的一步了！
选择默认的 安装 Ubuntu，与 windows 共存

![6](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/6.jpg)

然后点击现在安装 会出现这个 将改动写入磁盘 但是
【【【请确保第一块磁盘上只有一块空闲分区！！】】】
有多个空闲分区的 lz 并不能保证 Ubuntu 会安装在哪个空闲分区里面

![7](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/7.jpg)

然后点继续
会提示你选择时区
默认的只要是中国的东八区就好

再然后是选择键盘布局
一般会识别到汉语-汉语
（这个也可以调成英语-美国 不过具体区别lz没有注意过）

再然后就是输入用户名密码了
（没有特殊要求的请不要选择 加密我的主目录 如果加密了 一旦系统出现问题 你的文件有可能会全部丢失）

再下一步就开始自动安装系统了
![8](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/8.jpg)

然后安装完了
你可能会说
这踏马不跟别的一样吗
但是
后面可就不一样了

点完现在重启
开机的时候再按 f12 选择启动项
（反正我的主板是按 f12）
你就会发现
有两个 win 和两个 ubuntu
虽然我也不知道为什么会有俩 win 但是 Ubuntu 有两个是正常的

（还有我是双硬盘 都是 gpt 分区表 所以就会有个硬盘的uefi启动项）

![9](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/9.jpg)

再然后重启进入 bios
到选择启动顺序的里面
把 windows 调成第一个
Ubuntu 调成第二个
后面的随便调就行

![10](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/10.jpg)

再然后 就是进入 Ubuntu 里面 调一下启动的时候的延时
修改 `/etc/default/grub` 文件
```
$ sudo gedit /etc/default/grub
```
然后修改其中的第 8 行 也就是
```
grub_timeout=1
```
但是 最好别调到 0 秒 原因我就不说了
修改完后点保存不用管命令行里的报错
然后再运行下面这个命令重建 grub 引导
```
$ sudo update-grub
```
![11](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/11.jpg)

然后 你就会发现
自动启动的时候是进入的 windows 10
而且速度和原来一样
想进 Ubuntu 的时候 可以按下 f12 选择 Ubuntu 引导
然后 Ubuntu 启动也快的飞起
再也不会像在网吧里似的突然大喊一声
卧槽我忘了选系统二了

## 另外
对了！如果你要是想从硬盘的其中一个盘符里面的剩余空间安装的话

请用 windows 的磁盘管理

我的电脑（此电脑）（计算机）右键 ----> 磁盘管理------>选中一个盘符右键----->压缩卷

然后根据引导来做就好了

![12](https://raw.githubusercontent.com/UbuntuBar/userguide/master/image/UEFI下Win10-Ubuntu双系统共存教程/12.jpg)

还有个 ubuntu 和 win 时间不一致的问题

原因是 Windows 和 Linux 默认看待 PC 的 CMOS 记录的时钟是不一样的。

而 Windows 将这个时钟作为本地时间来看待，也就是 CMOS 时间就是北京时间。

Linux 将这个时钟作为 Coordinated Universal Time (UTC) 世界标准时间看待，也就是 Greenwich Mean Time (GMT) 格林威治时间。

所以如果你在 Linux 和 Windows 都选北京时间作为本地时区是，一旦连到互联网上，同步过时间后，就会造成时间的不一致。


解决方法：（修改 Windows 注册表）

将 Windows 的缺省对待 CMOS 的方式改成 UTC，也就是和 Linux 一样
　　
修改 Windows 的注册表，定位到
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\
```
添加一个名为 `RealTimeIsUniversal` 的 DWORD 项，把值设为 1。

这样你在 Windows 和 Linux 下将本地时区都设到北京时间，不论是 Windows 还是 Linux 同步过时间后，都不会影响到另一边。
