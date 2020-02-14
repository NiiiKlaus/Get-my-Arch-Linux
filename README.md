# Get my Arch Linux

# 写在前面

- 安装参考的视频：

  <https://www.bilibili.com/video/av81146687>

  <https://www.bilibili.com/video/av86485933>

- 非常感谢UP主（Github：[@theniceboy](https://github.com/theniceboy)）提供的保姆级教程。

- 这里是我自己安装过程的记录。

- 我在安装时使用的编辑器是`Nano`，如果你使用的是`Vim`等编辑器，阅读下面内容时请自行替换。

# 目录

- [系统安装](system-installation.md/#系统安装)
  - [1. 修改`tty`界面下的字体](system-installation.md/#1-修改tty界面下的字体)
  - [2. 连接网络](system-installation.md/#2-连接网络)
    - [2.1 扫描当前互联网设备](system-installation.md/#21-扫描当前互联网设备)
    - [2.2 启用设备](system-installation.md/#22-启用设备)
    - [2.3 扫描当前设备下的WiFi列表并得到所有WIFI的名字](system-installation.md/#23-扫描当前设备下的wifi列表并得到所有wifi的名字)
    - [2.4 使用`wpa_supplicant`连接网络并后台运行](system-installation.md/#24-使用wpasupplicant连接网络并后台运行)
    - [2.5 动态分配IP地址](system-installation.md/#25-动态分配ip地址)
    - [2.6 测试](system-installation.md/#26-测试)
  - [3. 更正系统时间](system-installation.md/#3-更正系统时间)
  - [4. 硬盘分区](system-installation.md/#4-硬盘分区)
    - [4.1 查看现有的磁盘](system-installation.md/#41-查看现有的磁盘)
    - [4.2 进入磁盘编辑](system-installation.md/#42-进入磁盘编辑)
    - [4.3 定义分区格式](system-installation.md/#43-定义分区格式)
    - [4.4 打开`SWAP`](system-installation.md/#44-打开swap)
  - [5. 配置`pacman`](system-installation.md/#5-配置pacman)
  - [6. 使用`pacstrap`安装Arch Linux基础至磁盘中](system-installation.md/#6-使用pacstrap安装arch-linux基础至磁盘中)
    - [6.1 查看当前的磁盘](system-installation.md/#61-查看当前的磁盘)
    - [6.2 挂载磁盘](system-installation.md/#62-挂载磁盘)
    - [6.3 开始安装](system-installation.md/#63-开始安装)
    - [6.4 生成挂载文件](system-installation.md/#64-生成挂载文件)
  - [7. 使用`arch-chroot`对安装好的系统进行配置](system-installation.md/#7-使用archchroot对安装好的系统进行配置)
    - [7.1 进入`arch-chroot`](system-installation.md/#71-进入archchroot)
    - [7.2 设置时区和时间](system-installation.md/#72-设置时区和时间)
    - [7.3 编辑本地化的文件](system-installation.md/#73-编辑本地化的文件)
    - [7.4 生成本地化](system-installation.md/#74-生成本地化)
    - [7.5 设置语言](system-installation.md/#75-设置语言)
    - [7.6 (可选)设置键盘布局和键位绑定](system-installation.md/#76-可选设置键盘布局和键位绑定)
    - [7.7 编辑网络相关的文件](system-installation.md/#77-编辑网络相关的文件)
    - [7.8 更改`root`用户密码](system-installation.md/#78-更改root用户密码)
    - [7.9 安装`grub`相关](system-installation.md/#79-安装grub相关)
    - [7.10 安装基础工具](system-installation.md/#710-安装基础工具)
    - [7.11 重启，完成安装](system-installation.md/#711-重启，完成安装)

- [系统安装中出现问题的汇总](system-installation-trouble-shooting.md/#系统安装中出现问题的汇总)
  - [1. 分区时出现警告：逻辑分区和物理分区不对齐](system-installation-trouble-shooting.md/#1-分区时出现警告：逻辑分区和物理分区不对齐)
  - [2. 关于`grub`和分区](system-installation-trouble-shooting.md/#2-关于grub和分区)

- [初步配置](initial-configuration.md/#初步配置)
  - [1. 安装`man`](initial-configuration.md/#1-安装man)
  - [2. 安装`base-devel`](initial-configuration.md/#2-安装basedevel)
  - [3. 添加用户](initial-configuration.md/#3-添加用户)
  - [4. 修改用户权限](initial-configuration.md/#4-修改用户权限)
  - [5. 切换到低权限的用户](initial-configuration.md/#5-切换到低权限的用户)
  - [6. 安装`Xorg`](initial-configuration.md/#6-安装xorg)
  - [7. 安装桌面环境](initial-configuration.md/#7-安装桌面环境)
  - [8. (可选)安装`lightdm`](initial-configuration.md/#8-可选安装lightdm)

- [初步配置出现的问题汇总](initial-configuration-trouble-shooting.md/#初步配置出现的问题汇总)
  - [配备有`intel`集成显卡和`NVIDIA`独立显卡的机器登入图形界面时机器挂起（关机）](initial-configuration-trouble-shooting.md/#配备有intel集成显卡和nvidia独立显卡的机器登入图形界面时机器挂起（关机）)

- [软件安装](software-installation.md/#软件安装)
  - [终端相关](software-installation.md/#终端相关)
    - [`yay`](software-installation.md/#yay)
    - [`ranger`](software-installation.md/#ranger)
    - [`neofetch`](software-installation.md/#neofetch)
    - [`htop`](software-installation.md/#htop)
    - [`fish`](software-installation.md/#fish)
    - [`openssh`](software-installation.md/#openssh)
    - [`alacritty`](software-installation.md/#alacritty)
	- [`st`](software-installation.md/#st)
  - [输入法](software-installation.md/#输入法)
    - [`fcitx`](software-installation.md/#fcitx)
  - [浏览器](software-installation.md/#浏览器)
    - [`Chromium`](software-installation.md/#chromium)
    - [`Midori`](software-installation.md/#midori)
  - [录屏相关](software-installation.md/#录屏相关)
    - [`SimpleScreenRecorder`](software-installation.md/#simplescreenrecorder)
    - [`Screenkey`](software-installation.md/#screenkey)
  - [视频编辑](software-installation.md/#视频编辑)
    - [`Kdenlive`](software-installation.md/#kdenlive)
  - [图片编辑](software-installation.md/#图片编辑)
    - [`Gimp`](software-installation.md/#gimp)
  - [办公](software-installation.md/#办公)
    - [`Libreoffice`](software-installation.md/#libreoffice)
    - [`Thunderbird`](software-installation.md/#thunderbird)
  - [社交](software-installation.md/#社交)
    - [QQ](software-installation.md/#qq)
    - [微信](software-installation.md/#微信)
  - [游戏](software-installation.md/#游戏)
    - [`Steam`](software-installation.md/#steam)
  - [下载工具](software-installation.md/#下载工具)
    - [`transmission`](software-installation.md/#transmission)
  - [视频播放](software-installation.md/#视频播放)
    - [`Vlc`](software-installation.md/#vlc)
  - [其他](software-installation.md/#其他)
    - [`Gparted`](software-installation.md/#gparted)
    - [`Virtualbox`](software-installation.md/#virtualbox)
    - [`AppImageLauncher`](software-installation.md/#appimagelauncher)
    - [`Tlp`](software-installation.md/#tlp)
    - [`Blueman`](software-installation.md/#blueman)

- [软件安装出现的问题汇总](software-installation-trouble-shooting.md/#软件安装出现的问题汇总)
  - [搜狗输入法不显示候选框](software-installation-trouble-shooting.md/#搜狗输入法不显示候选框)

- [美化](prettification.md/#美化)
  - [窗口管理器](prettification.md/#窗口管理器)
    - [`i3`](prettification.md/#i3)
	- [`dwm`](prettification.md/#dwm)

- [美化过程中出现的问题汇总](prettification-trouble-shooting.md/#美化过程中出现的问题汇总)
