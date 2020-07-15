# 软件

## 终端相关

### `yay`

- AUR的包管理器。

- ```bash
  $ git clone https://aur.archlinux.org/yay.git
  $ cd yay/
  $ makepkg -si   # 编译安装
  ```

- 配置中国镜像：

  ```bash
  $ yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
  ```

  配置文件的位置位于`~/.config/yay/config.json`，也可通过下面的命令查看修改过的配置：

  ```bash
  $ yay -P -g
  ```

### `ranger`

- 终端下的文件管理器，`Python`编写。

- ```bash
  $ sudo pacman -S ranger
  ```


### `neofetch`

- 系统硬件信息查看。

- ```bash
  $ sudo pacman -S neofetch
  ```

### `htop`

- 终端下系统资源占用查看工具。

- ```bash
  $ sudo pacman -S htop
  ```

### `BashTop`

- 作用同 `htop`，但是有更精美的界面和更多的功能。

- ```
  $ sudo pacman -S bashtop
  ```

### `fish`

- 功能强大、智能友好的终端命令解析器。

- ```bash
  $ sudo pacman -S fish
  ```

### `zsh`

- 功能强大的Linux Shell，配合[`Oh-My-Zsh`](https://ohmyz.sh/)使用更佳。

- ```bash
  $ sudo pacman -S zsh
  ```

### `openssh`

- 远程连接工具。

- ```bash
  $ sudo pacman -S openssh
  ```

### `alacritty`

- 使用显卡渲染的终端模拟器。

- ```bash
  $ sudo pacman -S alacritty
  ```

### `st`

- 来自 Suckless 社区的`X`下的极简终端模拟器。

- ```bash
  $ git clone https://git.suckless.org/st   # 克隆源代码的仓库
  $ cd st/
  $ make                                    # 编译
  $ sudo make clean install                 # 安装
  ```

- 关于如何配置可参考以下视频：

[【极简主义】打造Linux下精巧强大的终端：Simple Terminal （st） —— 【Suckless的极简主义01】](https://www.bilibili.com/video/av74807286)

### `tree`

- 展示目录下的文件。

- ```bash
  $ sudo pacman -S tree
  ```

### `pactree`

- 展示本地或远程的包的结构。

- ```bash
  $ sudo pacman -S pacman-contrib   # 包的结构发生了一些改变，现在pactree在pacman-contrib内
  ```

### `zip`

- 解压缩软件。

- ```bash
  $ sudo pacman -S zip
  ```

### `xsel`

- 可以将终端输出的内容重定向到剪切板上。

- ```bash
  $ sudo pacman -S xsel
  ```

### `task`

- 终端下的一个`Todo List`。

- ```bash
  $ sudo pacman -S task
  ```

### `proxychains`

- 终端命令代理。

- ```bash
  $ sudo pacman -S proxychains-ng
  ```

## 输入法

### Fcitx

- 输入法管理器。

- ```bash
  sudo pacman -S fcitx fcitx-im fcitx-configtool
  ```

- 中文字体、emoji等的安装：

  ```bash
  $ yay -S ttf-linux-libertine ttf-inconsolata ttf-joypixels ttf-twemoji-color noto-fonts-emoji ttf-liberation ttf-droid   # Emoji
  
  $ yay -S wqy-bitmapfont wqy-microhei wqy-microhei-lite wqy-zenhei adobe-source-han-mono-cn-fonts adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts   # 中文字体
  ```

### IBus

- 输入法管理器。`fcitx`比较好的替代品。

- ```bash
  $ sudo pacman -S ibus
  ```

## 浏览器

### Chromium

- 开源、支持多扩展的浏览器。

- ```bash
  $ sudo pacman -S chromium
  ```

### Midori

- 轻量、快速的浏览器。

- ```bash
  $ sudo pacman -S midori
  ```

## 录屏相关

### SimpleScreenRecorder

- 轻量的录屏软件。

- ```bash
  $ sudo pacman -S simplescreenrecorder
  ```

### Screenkey

- 捕捉键盘按键。

- 首先添加`archlinuxcn`，同时去掉`multilib`前面的注释。

  ```bash
  $ sudo nano /etc/pacman.conf
  # 添加如下两行：
  # [archlinuxcn]
  # Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
  ```

- ```bash
  $ sudo pacman -S screenkey
  ```

## 视频编辑

### Kdenlive

- 视频剪辑。

- ```bash
  $ sudo pacman -S kdenlive
  ```

## 图片编辑

### Gimp

- 图片编辑。

- ```bash
  $ sudo pacman -S gimp
  ```

## 办公

### Libreoffice

- Office三件套。

- ```bash
  $ sudo pacman -S libreoffice
  ```

### Thunderbird

- 邮件管理。

- ```bash
  $ sudo pacman -S thunderbird
  ```

### Typora

- 跨平台的`Markdown`编辑器，所见即所得。

- ```bash
  $ sudo pacman -S typora
  ```

## 社交

### QQ

- 社交软件。

- ```bash
  $ sudo pacman -S deepin.com.qq.im
  ```

### 微信

- 社交软件。

- ```bash
  $ sudo pacman -S electronic-wechat   # 基于Electron的微信，本质上是网页版的微信
  $ sudo pacman -S wine-wechat         # Wine集成的Windows平台的微信
  # wine-wechat可能需要安装wine-mono字体，它建议使用pacman进行管理：
  # sudo pacman -S wine-mono
  ```

## 游戏

### Steam

- 游戏商店。

- ```bash
  $ sudo pacman -S steam
  ```

## 下载工具

### Transmission

- 支持磁力下载。

- ```bash
  $ sudo pacman -S transmission-qt    # 基于Qt的图形化界面
  $ sudo pacman -S transmission-gtk   # 基于GTK的图形化界面
  # 两种皆可
  ```
  
### qBittorrent

- 磁力下载。

- ```bash
  $ sudo pacman -S qbittorrent
  ```

## 视频播放

### Vlc

- 视频播放器。

- ```bash
  $ sudo pacman -S vlc
  ```

## 系统工具

### Gparted

- 有图形界面的磁盘无损分区工具。

- ```bash
  $ sudo pacman -S gparted
  ```

### Tlp

- 电池性能优化。

- ```bash
  $ sudo pacman -S tlp
  ```

### Blueman

- 有图形界面的蓝牙设备管理。

- ```bash
  $ sudo pacman -S blueman
  ```

- 使用之前需要将`bluetooth`添加至守护进程：

  ```bash
  $ sudo systemctl enable bluetooth
  ```

### NTFS-3G

- Windows文件系统（NTFS）的挂载工具。

- ```bash
  $ sudo pacman -S ntfs-3g
  ```
  
### AppImageLauncher

- `.appimage`文件的启动器。

- ```bash
  $ sudo pacman -S appimagelauncher
  ```
  
### Xcompmgr

- `X`下的窗口渲染工具。可以使得窗口透明化。作为`Xorg`的拓展工具。

- ```bash
  $ sudo pacman -S xcompmgr
  ```

- 与它类似的窗口渲染器`compton`貌似已经不在维护，这里也有它的一个替代，叫`picom`。

### Trayer

- 轻量的系统托盘。

- ```bash
  $ sudo pacman -S trayer
  ```

- `trayer`有很多的选项。这里可以参考我的启动选项：

  ```bash
  trayer --transparent true --expand false --align right --width 20 --SetDockType false --tint 0x88888888 &
  ```

### ACPI

- 电池状况监控。

- ```bash
  $ sudo pacman -S acpi
  ```

## 其他

### Virtualbox

- 开源的虚拟机。

- ```bash
  $ sudo pacman -S virtualbox
  ```

### Xarchiver

- 图形化的解压缩软件。

- ```bash
  $ sudo pacman -S xarchiver
  ```
