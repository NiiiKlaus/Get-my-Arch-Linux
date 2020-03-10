# Get my Arch Linux

# 写在前面

- 安装参考的视频：

  <https://www.bilibili.com/video/av81146687>

  <https://www.bilibili.com/video/av86485933>

- 非常感谢UP主（Github：[@theniceboy](https://github.com/theniceboy)）提供的保姆级教程。

- 这里是大多是我自己安装过程的记录。欢迎补充。

- 我在安装时使用的编辑器是`Nano`，如果你使用的是`Vim`等编辑器，阅读下面内容时请自行替换。

# Billboard

- 为了尽量保证阅读体验，保持文档前后风格一致，请在做更改前，花一点时间阅读一下[我的风格](my-style.md)，以方便我合并分支。感谢配合。

- 近期由于仓库大体结构还没有最终确定，如果有PR的话，我大多会选择手动合并。敬请谅解。

- 疫情期间，线上授课与正常开学几乎一样…所以更新频率会下降。我尽量保持一周一更。

  PR会看，但可能都会在更新时一起合并。

- 武汉加油！

# 目录

- [系统安装](system-installation.md/#系统安装)
  - [1. 修改`tty`界面下的字体](system-installation.md/#1-修改tty界面下的字体)
  - [2. 连接网络](system-installation.md/#2-连接网络)
    - [2.1 扫描当前互联网设备](system-installation.md/#21-扫描当前互联网设备)
    - [2.2 启用设备](system-installation.md/#22-启用设备)
    - [2.3 扫描当前设备下的WiFi列表并得到所有WiFi的名字](system-installation.md/#23-扫描当前设备下的wifi列表并得到所有wifi的名字)
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
    - [`Xorg使用方法`](initial-configuration.md/#xorg使用方法)
  - [7. 安装桌面环境](initial-configuration.md/#7-安装桌面环境)
  - [8. (可选)安装`lightdm`](initial-configuration.md/#8-可选安装lightdm)
- [初步配置出现的问题汇总](initial-configuration-trouble-shooting.md/#初步配置出现的问题汇总)
  - [配备有`intel`集成显卡和`NVIDIA`独立显卡的机器登入图形界面时机器挂起（关机）](initial-configuration-trouble-shooting.md/#配备有intel集成显卡和nvidia独立显卡的机器登入图形界面时机器挂起（关机）)
- [软件](software.md/#软件)
  - [终端相关](software.md/#终端相关)
    - [`yay`](software.md/#yay)
    - [`ranger`](software.md/#ranger)
    - [`neofetch`](software.md/#neofetch)
    - [`htop`](software.md/#htop)
    - [`fish`](software.md/#fish)
    - [`zsh`](software.md/#zsh)
    - [`openssh`](software.md/#openssh)
    - [`alacritty`](software.md/#alacritty)
    - [`st`](software.md/#st)
    - [`tree`](software.md/#tree)
    - [`pactree`](software.md/#pactree)
    - [`zip`](software.md/#zip)
    - [`xsel`](software.md/#xsel)
    - [`task`](software.md/#task)
    - [`proxychains`](software.md/#proxychains)
  - [输入法](software.md/#输入法)
    - [Fcitx](software.md/#fcitx)
    - [IBus](software.md/#ibus)
  - [浏览器](software.md/#浏览器)
    - [Chromium](software.md/#chromium)
    - [Midori](software.md/#midori)
  - [录屏相关](software.md/#录屏相关)
    - [SimpleScreenRecorder](software.md/#simplescreenrecorder)
    - [Screenkey](software.md/#screenkey)
  - [视频编辑](software.md/#视频编辑)
    - [Kdenlive](software.md/#kdenlive)
  - [图片编辑](software.md/#图片编辑)
    - [Gimp](software.md/#gimp)
  - [办公](software.md/#办公)
    - [Libreoffice](software.md/#libreoffice)
    - [Thunderbird](software.md/#thunderbird)
    - [Typora](software.md/#typora)
  - [社交](software.md/#社交)
    - [QQ](software.md/#qq)
    - [微信](software.md/#微信)
  - [游戏](software.md/#游戏)
    - [Steam](software.md/#steam)
  - [下载工具](software.md/#下载工具)
    - [Transmission](software.md/#transmission)
    - [qBittorrent](software.md/#qbittorrent)
  - [视频播放](software.md/#视频播放)
    - [Vlc](software.md/#vlc)
  - [系统工具](software.md/#系统工具)
    - [Gparted](software.md/#gparted)
    - [Tlp](software.md/#tlp)
    - [Blueman](software.md/#blueman)
    - [NTFS-3G](software.md/#ntfs3g)
    - [AppImageLauncher](software.md/#appimagelauncher)
    - [Xcompmgr](software.md/#xcompmgr)
    - [Trayer](software.md/#trayer)
    - [ACPI](software.md/#acpi)
  - [其他](software.md/#其他)
    - [Virtualbox](software.md/#virtualbox)
    - [Xarchiver](software.md/#xarchiver)
- [软件安装以及使用过程中出现的问题汇总](software-trouble-shooting.md/#软件安装以及使用过程中出现的问题汇总)
  - [搜狗输入法不显示候选框](software-trouble-shooting.md/#搜狗输入法不显示候选框)
  - [`fish`下`source /etc/profile`报错](software-trouble-shooting.md/#fish下source-etcprofile报错)
  - [`alacritty`下使用`clear`命令清屏幕报错`'alacritty': unknown terminal type.`](software-trouble-shooting.md/#alacritty下使用clear命令清屏幕报错alacritty-unknown-terminal-type)
  - [`alacritty`和`st`在未完全配置的情况下，使用安装好插件的`vim`中的字体颜色是纯白](software-trouble-shooting.md/#alacritty和st在未完全配置的情况下，使用安装好插件的vim中的字体颜色是纯白)
  - [在跟着教程配置`dwm`时，`statusbar`出现小方框](software-trouble-shooting.md/#在跟着教程配置dwm时，statusbar出现小方框)
- [美化](prettification.md/#美化)
  - [窗口管理器](prettification.md/#窗口管理器)
    - [`i3`](prettification.md/#i3)
    - [`dwm`](prettification.md/#dwm)
- [美化过程中出现的问题汇总](prettification-trouble-shooting.md/#美化过程中出现的问题汇总)
# TODO

