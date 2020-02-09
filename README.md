# <center>Get my Arch Linux</center>

# 写在前面

- 安装参考的视频：

  <https://www.bilibili.com/video/av81146687>

  <https://www.bilibili.com/video/av86485933>

- 非常感谢UP主（Github：[@theniceboy](https://github.com/theniceboy)）提供的保姆级教程。

- 这里是我自己安装过程的记录。

- 我在安装时使用的编辑器是`Nano`，如果你使用的是`Vim`等编辑器，阅读下面内容时自行替换。

# 安装

## 1. 修改`tty`界面下的字体

- 所有字体都存放在`/usr/share/kbd/consolefonts`目录下。

- 这里将其设置为：

  ```bash
  $ setfont /usr/share/kbd/consolefonts/LatGrkCyr-12*22.psfz.gz
  ```

## 2. 连接网络

### 2.1 扫描当前互联网设备

```bash
$ ip link
```

### 2.2 启用设备

```bash
$ ip link set 设备名 up
```

### 2.3 扫描当前设备下的WiFi列表并得到所有WIFI的名字

```bash
$ iwlist 设备名 scan | grep ESSID
```

### 2.4 使用`wpa_supplicant`连接网络并后台运行

```bash
$ wpa_passphrase 网络名 密码 > internet.conf
$ wpa_supplicant -c internet.conf -i 设备名 &
```

### 2.5 动态分配IP地址

```bash
$ dhcpcd &
```

### 2.6 测试

```bash
$ ping baidu.com
```

## 3. 更正系统时间

```bash
$ timedatectl set-ntp true
```

## 4. 硬盘分区

### 4.1 查看现有的磁盘

```bash
$ fdisk -l
```

### 4.2 进入磁盘编辑

```bash
$ fdisk /dev/sda   # /dev/sda为磁盘设备的位置
$ g   # 清除原有分区并创建一个GPT分区表
$ n   # 创建一个新的分区/dev/sda1 -- 引导分区
      # 接下来选择分区的编号、起始位置、终止位置（分区大小，可用例如“+300M”的形式）
$ n   # 创建一个新的分区/dev/sda3 -- SWAP分区（用于保存内存中的文件以及作为内存的扩展，此
      # 分区不需要太大）
      # 这里我大小设置为1G
$ n   # 创建一个新的分区/dev/sda2 -- 主分区
      # 大小我设置为磁盘的所有剩余空间
$ p   # 查看待写入的分区结果
$ w   # 写入
```

### 4.3 定义分区格式

```bash
$ mkfs.fat -F32 /dev/sda1   # /dev/sda1为引导分区
$ mkfs.ext4 /dev/sda2       # /dev/sda2为主分区
$ mkswap /dev/sda3          # /dev/sda3为SWAP分区
```

### 4.4 打开`SWAP`

```bash
$ swapon /dev/sda3
```

## 5. 配置`pacman`

```bash
$ nano /etc/pacman.conf
```

- 去掉注释：
  
- `Color`
  
- `Arch Linux`软件源列表：`/etc/pacman.d/mirrorlist`

- 寻找中国的服务器，将它移动到`mirrorlist`的最顶上，保存退出。

- 我这里使用的是清华的源：

  ```
  ## China
  Server = http://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
  ```

## 6. 使用`pacstrap`安装Arch Linux基础至磁盘中

### 6.1 查看当前的磁盘

```bash
$ fdisk -l
```

### 6.2 挂载磁盘

```bash
$ mount /dev/sda2 /mnt        # 挂载主分区
$ mkdir /mnt/boot             # 创建启动分区在Live CD上的目录
$ mount /dev/sda1 /mnt/boot   # 挂载启动分区
```

### 6.3 开始安装

```bash
$ pacstrap /mnt base linux linux-firmware   # 安装Linux所需的最基础的软件、框架等
```

### 6.4 生成挂载文件

```bash
$ genfstab -U /mnt >> /mnt/etc/fstab
```

## 7. 使用`arch-chroot`对安装好的系统进行配置

### 7.1 进入`arch-chroot`

```bash
$ arch-chroot /mnt   # /mnt为安装好的系统的主分区在Live CD上的挂载位置
```

### 7.2  设置时区和时间

```bash
$ ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime   # 创建链接
$ hwclock --systohc                                         # 同步时间
```

### 7.3 编辑本地化的文件

```bash
$ exit                       # 先退出arch-chroot
$ nano /mnt/etc/locale.gen   # 编辑本地化文件
                             # 去掉“en_US.UTF-8 UTF-8”前面的注释，保存退出         
```

### 7.4 生成本地化

```bash
$ arch-chroot /mnt
$ locale-gen   # 生成本地化
```

### 7.5 设置语言

```bash
$ exit                        # 退出arch-chroot
$ nano /mnt/etc/locale.conf   # 编辑本地化的配置文件
                              # 在其中输入“LANG=en_US.UTF-8”（将系统设置为英文），保存退出。
```

### 7.6 (可选)设置键盘布局和键位绑定

```bash
$ nano /mnt/etc/vconsole.conf
```

### 7.7 编辑网络相关的文件

```bash
$ nano /mnt/etc/hostname   # 编辑主机名称
                           # 我将其设置为niklaus，保存退出
$ nano /mnt/etc/hosts      # 编辑域名与IP地址的对应
                           # 127.0.0.1   localhost
                           # ::1         localhost
                           # 127.0.1.1   niklaus.localdomain   niklaus
```

### 7.8 更改`root`用户密码

```bash
$ arch-chroot /mnt
$ passwd
```

### 7.9 安装`grub`相关

```bash
$ pacman -S grub efibootmgr intel-ucode os-prober
# intel-ucode   厂家更新CPU驱动用，如果是AMD的显卡，则安装amd-ucode
# os-probe      用来寻找电脑中其他操作系统
$ mkdir /boot/grub
$ grub-mkconfig > /boot/grub/grub.cfg                      # 生成grub配置文件
$ uname -m                                                 # 查看系统架构
$ grub-install --target=x86_64-efi --efi-directory=/boot   # 根据自己的系统架构安装grub
```

### 7.10 安装基础工具

```bash
$ pacman -S zsh nano vim wpa_supplicant dhcpcd
# zsh              shell
# nano             编辑器
# vim              编辑器
# wpa_supplicant   上网工具
# dhcpcd           动态分配IP地址工具
```

### 7.11 重启，完成安装

```bash
$ exit                            # 退出arch-chroot
$ killall wpa_supplicant dhcpcd   # 终止掉网络相关的进程
$ reboot                          # 重启，电脑黑屏后就可以拔掉Live CD了
```

# 安装Arch Linux中出现问题的汇总

## 1. 分区时出现警告：逻辑分区和物理分区不对齐

- 可能原因：SSD或者是HDD上原来装过Windows，则硬盘最开始的32M空间（图形界面下使用Gparted可以看到）是默认空白的。这样就会导致分区的不对齐。但其实对于SSD来说只是影响到速度，使用还是比较正常的

- 解决方法：

  - （未试验）使用`shred`命令彻底清洗磁盘，但耗时一般较长。
  
    ```bash
    $ shred -v /dev/sda
    ```

# 初步配置

- 在配置之前记得检查网络连接，确保连上了网。

## 1. 安装`man`

```bash
$ pacman -S man   # 用户手册
```

## 2. 安装`base-devel`

```bash
$ pacman -S base-devel   # sudo、编译器等等的基础工具
```

## 3. 添加用户

```bash
$ useradd -m -G wheel niklaus   # -m        创建家目录
                                # -G        用户所属的组
                                # niklaus   我的用户名
$ passwd niklaus   # 修改密码
```

## 4. 修改用户权限

```bash
$ nano /etc/sudoers   # 编辑sudoer file
                      # 去掉“%wheel ALL=(ALL) ALL”前面的注释，保存退出
```

## 5. 切换到低权限的用户

```bash
$ exit# 退出root用户，并登陆niklaus用户
```

## 6. 安装`Xorg`

```bash
$ sudo pacman -S xorg   # 图形界面的服务器
```

## 7. 安装桌面环境

- 这里我选择的桌面环境是`LXDE`。

- ```bash
  $ sudo pacman -S lxde
  ```

- 若选择最小安装，则为：

  ```bash
  $ sudo pacman -S lxde-common lxsession openbox
  ```

## 8. (可选)安装`lightdm`

- ```bash
  $ sudo pacman -S lightdm   # Display Manager   登陆管理器
  ```

- 配置`lightdm`：

  ```bash
  $ sudo nano /etc/lightdm/lightdm.conf   # 修改皮肤
  # 去掉“greeter-session=example-gtk-gnome”前面的注释
  # 将其改为自己需要使用的登陆界面皮肤
  ```

# 软件安装

## 终端用

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

- 文件管理器。

- ```bash
  $ sudo pacman -S ranger
  ```

- 

### `neofetch`

- 系统硬件信息查看。

- ```bash
  $ sudo pacman -S neofetch
  ```

### `htop`

- 系统资源占用查看。

- ```bash
  $ sudo pacman -S htop
  ```
  

### `fish`

- shell

- ```bash
  $ sudo pacman -S fish
  ```

## 输入法

### `fcitx`

- 输入法管理器。

- ```bash
  sudo pacman -S fcitx fcitx-im fcitx-configtool
  ```

- 中文字体、emoji等的安装：

  ```bash
  $ yay -S ttf-linux-libertine ttf-inconsolata ttf-joypixels ttf-twemoji-color noto-fonts-emoji ttf-liberation ttf-droid   # Emoji
  
  $ yay -S wqy-bitmapfont wqy-microhei wqy-microhei-lite wqy-zenhei adobe-source-han-mono-cn-fonts adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts   # 中文字体
  ```

## 浏览器

### `Chromium`

- 开源、支持多扩展的浏览器。

- ```bash
  $ sudo pacman -S chromium
  ```

## 录屏相关

### `SimpleScreenRecorder`

- 轻量的录屏软件。

- ```bash
  $ sudo pacman -S simplescreenrecorder
  ```

### `Screenkey`

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

### `Kdenlive`

- 视频剪辑。

- ```bash
  $ sudo pacman -S kdenlive
  ```

## 图片编辑

### `Gimp`

- 图片编辑。

- ```bash
  $ sudo pacman -S gimp
  ```

## 办公套件

### `Libreoffice`

- Office三件套。

- ```bash
  $ sudo pacman -S libreoffice
  ```

## 游戏

### `Steam`

- 游戏商店。

- ```bash
  $ sudo pacman -S steam
  ```

- 

## 视频播放

### `Vlc`

- 视频播放器。

- ```bash
  $ sudo pacman -S vlc
  ```

## 其他

### `Gparted`

- 有图形界面的磁盘无损分区工具。

- ```bash
  $ sudo pacman -S gparted
  ```

### `Virtualbox`

- 开源的虚拟机。

- ```bash
  $ sudo pacman -S virtualbox
  ```

### `AppImageLauncher`

-  `.appimage`文件的启动器。

- ```bash
  $ sudo pacman -S appimagelauncher
  ```

  

# 软件安装出现的问题汇总

## 搜狗输入法不显示候选框

- 如果出现了问题，搜狗输入法会提示：

  `搜狗输入法异常！请删除~/.config/SogouPY并重启。`

- 如果以上操作不能解决问题，那么打开终端，输入`sogou-qimpanel`。

  如果此时报错：

  `sogou-qimpanel: error while loading libraries: libfcitx-qt.so.0: cannot open shared object file: No such file or directory`

  那么就是缺少库文件的问题，目前最好的解决办法是取消使用`fcitx`：

  ```bash
  $ sudo pacman -S fcitx-lilydjwg-git
  # 在安装这个包时，pacman会提示有包冲突，移除冲突的fcitx等相关包即可
  ```

  然而在我的`LXDE`并且在默认壁纸下，搜狗输入法的状态栏周围会有一个黑框...不太美观但不影响使用。