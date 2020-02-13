# <center>Get my Arch Linux</center>

<!-- TOC GFM -->

* [写在前面](#写在前面)
* [安装](#安装)
  * [1. 修改tty界面下的字体](#1-修改tty界面下的字体)
  * [2. 连接网络](#2-连接网络)
     * [2.1 扫描当前互联网设备](#21-扫描当前互联网设备)
     * [2.2 启用设备](#22-启用设备)
     * [2.3 扫描当前设备下的WiFi列表并得到所有WIFI的名字](#23-扫描当前设备下的wifi列表并得到所有wifi的名字)
     * [2.4 使用wpa_supplicant连接网络并后台运行](#24-使用wpa_supplicant连接网络并后台运行)
     * [2.5 动态分配IP地址](#25-动态分配ip地址)
     * [2.6 测试](#26-测试)
  * [3. 更正系统时间](#3-更正系统时间)
  * [4. 硬盘分区](#4-硬盘分区)
     * [4.1 查看现有的磁盘](#41-查看现有的磁盘)
     * [4.2 进入磁盘编辑](#42-进入磁盘编辑)
     * [4.3 定义分区格式](#43-定义分区格式)
     * [4.4 打开SWAP](#44-打开swap)
  * [5. 配置pacman](#5-配置pacman)
  * [6. 使用pacstrap安装Arch Linux基础至磁盘中](#6-使用pacstrap安装arch-linux基础至磁盘中)
     * [6.1 查看当前的磁盘](#61-查看当前的磁盘)
     * [6.2 挂载磁盘](#62-挂载磁盘)
     * [6.3 开始安装](#63-开始安装)
     * [6.4 生成挂载文件](#64-生成挂载文件)
  * [7. 使用arch-chroot对安装好的系统进行配置](#7-使用arch-chroot对安装好的系统进行配置)
     * [7.1 进入arch-chroot](#71-进入arch-chroot)
     * [7.2  设置时区和时间](#72--设置时区和时间)
     * [7.3 编辑本地化的文件](#73-编辑本地化的文件)
     * [7.4 生成本地化](#74-生成本地化)
     * [7.5 设置语言](#75-设置语言)
     * [7.6 (可选)设置键盘布局和键位绑定](#76-可选设置键盘布局和键位绑定)
     * [7.7 编辑网络相关的文件](#77-编辑网络相关的文件)
     * [7.8 更改root用户密码](#78-更改root用户密码)
     * [7.9 安装grub相关](#79-安装grub相关)
     * [7.10 安装基础工具](#710-安装基础工具)
     * [7.11 重启，完成安装](#711-重启完成安装)
* [安装Arch Linux中出现问题的汇总](#安装arch-linux中出现问题的汇总)
  * [1. 分区时出现警告：逻辑分区和物理分区不对齐](#1-分区时出现警告逻辑分区和物理分区不对齐)
  * [2. 关于grub和分区](#2-关于grub和分区)
* [初步配置](#初步配置)
  * [1. 安装man](#1-安装man)
  * [2. 安装base-devel](#2-安装base-devel)
  * [3. 添加用户](#3-添加用户)
  * [4. 修改用户权限](#4-修改用户权限)
  * [5. 切换到低权限的用户](#5-切换到低权限的用户)
  * [6. 安装Xorg](#6-安装xorg)
  * [7. 安装桌面环境](#7-安装桌面环境)
  * [8. (可选)安装lightdm](#8-可选安装lightdm)
* [软件安装](#软件安装)
  * [终端相关](#终端相关)
     * [yay](#yay)
     * [ranger](#ranger)
     * [htop](#htop)
     * [openssh](#openssh)
     * [alacritty](#alacritty)
  * [输入法](#输入法)
     * [fcitx](#fcitx)
  * [浏览器](#浏览器)
     * [Chromium](#chromium)
     * [Midori](#midori)
  * [录屏相关](#录屏相关)
     * [SimpleScreenRecorder](#simplescreenrecorder)
     * [Screenkey](#screenkey)
  * [图片编辑](#图片编辑)
     * [Gimp](#gimp)
  * [办公](#办公)
     * [Libreoffice](#libreoffice)
     * [Thunderbird](#thunderbird)
  * [社交](#社交)
     * [QQ](#qq)
     * [微信](#微信)
  * [游戏](#游戏)
     * [steam](#steam)
  * [下载工具](#下载工具)
     * [transmission](#transmission)
     * [qbittorrent](#qbittorrent)
  * [视频播放](#视频播放)
     * [Vlc](#vlc)
  
  * [其他](#其他)
    * [Gparted](#gparted)
    * [Virtualbox](#virtualbox)
    * [AppImageLauncher](#appimagelauncher)
    * [Tlp](#tlp)
    * [Blueman](#blueman)
* [软件安装以及配置出现的问题汇总](#软件安装以及配置出现的问题汇总)
  * [搜狗输入法不显示候选框](#搜狗输入法不显示候选框)
  * [配备有intel集成显卡和NVIDIA独立显卡的机器登入图形界面时机器挂起（关机）](#配备有intel集成显卡和nvidia独立显卡的机器登入图形界面时机器挂起关机)
* [美化](#美化)
  * [窗口管理器](#窗口管理器)
     * [i3](#i3)
	 * [dwm](#dwm)

<!-- /TOC -->

# 写在前面

- 安装参考的视频：

  <https://www.bilibili.com/video/av81146687>

  <https://www.bilibili.com/video/av86485933>

- 非常感谢UP主（Github：[@theniceboy](https://github.com/theniceboy)）提供的保姆级教程。

- 这里是我自己安装过程的记录。

- 我在安装时使用的编辑器是`Nano`，如果你使用的是`Vim`等编辑器，阅读下面内容时请自行替换。

# 安装

## 1. 修改`tty`界面下的字体

- 所有字体都存放在`/usr/share/kbd/consolefonts`目录下。

- 这里将其设置为：

  ```bash
  $ setfont /usr/share/kbd/consolefonts/LatGrkCyr-12*22.psfu.gz
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

- 这里我采用的启动方式是`UEFI + GPT`，其他的启动方式请参考[下文](#2-关于grub和分区)。

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

- 可能原因：SSD或者是HDD上原来装过Windows，则硬盘最开始的32M空间（图形界面下使用`Gparted`可以看到）是默认空白的。这样就会导致分区的不对齐。但其实对于SSD来说只是影响到速度，使用还是比较正常的

- 解决方法：

  - （未试验）使用`shred`命令彻底清洗磁盘，但耗时一般较长。
  
    ```bash
    $ shred -v /dev/sda
    ```

## 2. 关于`grub`和分区

- Arch Linux支持三种启动方式，但启动方式分区和`grub`的安装略有不同。

  1. `UEFI + GPT`

     这是我采用的方式。具体对于`grub`的操作见[上文](#79-安装grub相关)。

     较新的主板推荐采用这种方式。

  2. `BIOS + MBR`

     这是较老的主板支持的分区方式，但在某些新的主板上已经不支持了。值得注意的是这种分区方式支持的硬盘是小于`2T`的。

  3. `BIOS + GPT`

     个人感觉这种分区方法的好处是方便后续在这块硬盘上安装别的Linux发行版并提高设备的兼容性。因为最好保证一块硬盘的分区表前后都是一致的，否则会出现兼容性的问题（这是我的猜想，有错误还请指正）。

- 三种分区方式具体如下图：

  ![image-20200211110852980](README.assets/image-20200211110852980.png)

- 三种分区方式及后续挂载方式等的完整命令示例：

  - `UEFI + GPT`

    ```bash
    # 进入磁盘编辑
    $ fdisk /dev/sda   # /dev/sda为磁盘设备的位置
    $ g   # 清除原有分区并创建一个GPT分区表
    $ n   # 创建一个新的分区/dev/sda1 -- 引导分区
    $ n   # 创建一个新的分区/dev/sda3 -- SWAP分区（用于保存内存中的文件以及作为内存的扩展，此
          # 分区不需要太大）
          # 这里我大小设置为1G
    $ n   # 创建一个新的分区/dev/sda2 -- 主分区
          # 大小我设置为磁盘的所有剩余空间
    $ p   # 查看待写入的分区结果
    $ w   # 写入
    
    # 制作文件系统
    # 这里会出现一些关于磁盘性能的警告，不用特别在意。
    $ mkfs.fat -F32 /dev/sda1   # /dev/sda1为引导分区，制作为“fat32”格式
    $ mkfs.ext4 /dev/sda2       # /dev/sda2为主分区，制作为“ext4”格式
    $ mkswap /dev/sda3          # /dev/sda3为SWAP分区
    
    # 打开swap
    $ swapon /dev/sda3
    
    # 挂载
    $ mount /dev/sda2 /mnt        # 挂载主分区
    $ mkdir /mnt/boot             # 创建启动分区在Live CD上的目录
    $ mount /dev/sda1 /mnt/boot   # 挂载启动分区
    
    # 安装Linux所需的最基础的软件、框架等
    $ pacstrap /mnt base linux linux-firmware
    
    # 生成挂载文件
    $ genfstab -U /mnt >> /mnt/etc/fstab
    
    # 使用arch-chroot
    $ arch-chroot /mnt
    
    # 安装grub相关
    $ pacman -S grub efibootmgr intel-ucode os-prober
    # intel-ucode   厂家更新CPU驱动用，如果是AMD的显卡，则安装amd-ucode
    # os-probe      用来寻找电脑中其他操作系统
    $ mkdir /boot/grub
    $ grub-mkconfig > /boot/grub/grub.cfg                      # 生成grub配置文件
    $ uname -m                                                 # 查看系统架构
    $ grub-install --target=x86_64-efi --efi-directory=/boot   # 根据自己的系统架构安装                                                            # grub,我这里系统架构是                                                            # x86_64，所以选择安装                                                            # x86_64-efi
    ```

  - `BIOS + MBR`

    ```bash
    # 进入磁盘编辑
    $ fdisk /dev/sda   # /dev/sda为磁盘设备的位置
    $ o   # 清除原有分区并创建一个MBR分区表
    $ n   # 创建一个新的分区/dev/sda1 -- 主分区
    $ n   # 创建一个新的分区/dev/sda2 -- SWAP分区（用于保存内存中的文件以及作为内存的扩展，此
          # 分区不需要太大）
          # 这里我大小设置为1G
    $ n   # 创建一个新的分区/dev/sda3 -- /home分区
          # 大小我设置为磁盘的所有剩余空间
    $ p   # 查看待写入的分区结果
    $ w   # 写入
    
    # 制作文件系统
    # 这里会出现一些关于磁盘性能的警告，不用特别在意。
    $ mkfs.ext4 /dev/sda1   # /dev/sda1为主分区，制作为“ext4”格式
    $ mkswap /dev/sda2      # /dev/sda2为SWAP分区
    $ mkfs.ext4 /dev/sda3   # /dev/sda3为/home分区，制作为“ext4”格式
    
    # 打开swap
    $ swapon /dev/sda2
    
    # 挂载
    $ mount /dev/sda1 /mnt        # 挂载主分区
    $ mkdir /mnt/home             # 创建/home分区在Live CD上的目录
    $ mount /dev/sda3 /mnt/home   # 挂载/home分区
    
    # 安装Linux所需的最基础的软件、框架等
    $ pacstrap /mnt base linux linux-firmware
    
    # 生成挂载文件
    $ genfstab -U /mnt >> /mnt/etc/fstab
    
    # 使用arch-chroot
    $ arch-chroot /mnt
    
    # 安装grub相关
    $ pacman -S grub intel-ucode os-prober
    # intel-ucode   厂家更新CPU驱动用，如果是AMD的显卡，则安装amd-ucode
    # os-probe      用来寻找电脑中其他操作系统
    $ mkdir /boot/grub
    $ grub-mkconfig > /boot/grub/grub.cfg      # 生成grub配置文件
    $ grub-install --target=i386-pc /dev/sda   # 敲入这条命令即可，使用BIOS的在grub-                                              # install时--target参数统一是i386-pc
                                               # 值得注意的是，这里grub安装的位置选择的直                                            # 接是硬盘/dev/sda，而不是任何一个分区
    ```

  - `BIOS + GPT`

    ```bash
    # 进入磁盘编辑
    $ fdisk /dev/sda   # /dev/sda为磁盘设备的位置
    $ g   # 清除原有分区并创建一个GPT分区表
    $ n   # 创建一个新的分区/dev/sda1 -- 空白分区，大小为1M
    $ n   # 创建一个新的分区/dev/sda2 -- 主分区
    $ n   # 创建一个新的分区/dev/sda3 -- SWAP分区（用于保存内存中的文件以及作为内存的扩展，此
          # 分区不需要太大）
          # 这里我大小设置为1G
    $ n   # 创建一个新的分区/dev/sda4 -- /home分区
          # 大小我设置为磁盘的所有剩余空间
    $ p   # 查看待写入的分区结果
    $ w   # 写入
    
    # 制作文件系统
    # 这里会出现一些关于磁盘性能的警告，不用特别在意。
    # 注意这里的/dev/sda1空白分区不需要挂载，也不需要制作文件系统。
    $ mkfs.ext4 /dev/sda2   # /dev/sda2为主分区，制作为“ext4”格式
    $ mkswap /dev/sda3      # /dev/sda2为SWAP分区
    $ mkfs.ext4 /dev/sda4   # /dev/sda4为/home分区，制作为“ext4”格式
    
    # 打开swap
    $ swapon /dev/sda3
    
    # 挂载
    $ mount /dev/sda2 /mnt        # 挂载主分区
    $ mkdir /mnt/home             # 创建/home分区在Live CD上的目录
    $ mount /dev/sda4 /mnt/home   # 挂载/home分区
    
    # 安装Linux所需的最基础的软件、框架等
    $ pacstrap /mnt base linux linux-firmware
    
    # 生成挂载文件
    $ genfstab -U /mnt >> /mnt/etc/fstab
    
    # 使用arch-chroot
    $ arch-chroot /mnt
    
    # 安装grub相关
    $ pacman -S grub intel-ucode os-prober
    # intel-ucode   厂家更新CPU驱动用，如果是AMD的显卡，则安装amd-ucode
    # os-probe      用来寻找电脑中其他操作系统
    $ mkdir /boot/grub
    $ grub-mkconfig > /boot/grub/grub.cfg              # 生成grub配置文件
    $ grub-install --force --target=i386-pc /dev/sda   # 敲入这条命令即可，使用BIOS的在                                                    # grub-install时--target参数                                                    # 统一是i386-pc
                                                       # 这里也需要使用--force参数强制                                                    # 安装grub，因为无参数情况下的两                                                    # 个警告会使得grub安装失败
                                                       # 值得注意的是，这里grub安装的位                                                    # 置选择的直接是硬盘/dev/sda，而                                                    # 不是任何一个分区
    ```

    

  - 如果还有问题，请移步`Arch Wiki`：

    <https://wiki.archlinux.org/index.php/Partitioning#GUID_Partition_Table>

    <https://wiki.archlinux.org/index.php/GRUB>

    <https://wiki.archlinux.org/index.php/Partitioning>

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

- 文件管理器。

- ```bash
  $ sudo pacman -S ranger
  ```
  如果要对其进行配置，执行以下操作：

  ```bash
  $ ranger --copy-config=all
  ```
  这时就会生成ranger的配置文件，一般路径在`~/.config/ranger/`

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

- Suckless下X的极简终端。

- ```bash
  $ git clone https://git.suckless.org/st
  $ cd st/
  $ make
  $ make clean install
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

### `Midori`

- 轻量、快速的浏览器。

- ```bash
  $ sudo pacman -S midori
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

## 办公

### `Libreoffice`

- Office三件套。

- ```bash
  $ sudo pacman -S libreoffice
  ```

### `Thunderbird`

- 邮件管理。

- ```bash
  $ sudo pacman -S thunderbird
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

### `Steam`

- 游戏商店。

- ```bash
  $ sudo pacman -S steam
  ```

## 下载工具

### `transmission`

- 支持磁力下载。

- ```bash
  $ sudo pacman -S transmission-qt    # 基于GTK的图形化界面
  $ sudo pacman -S transmission-gtk   # 基于Qt的图形化界面
  # 两种皆可
  ```
```
  

### `qbittorrent`

- 磁力下载。

- ```bash
  $ sudo pacman -S qbittorrent
```

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

### `Tlp`

- 电池性能优化。

- ```bash
  $ sudo pacman -S tlp
  ```

### `Blueman`

- 有图形界面的蓝牙设备管理。

- ```bash
  $ sudo pacman -S blueman
  ```

- 使用之前需要将`bluetooth`添加至守护进程：

  ```bash
  $ sudo systemctl enable bluetooth
  ```


# 软件安装以及配置出现的问题汇总

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

  然而在我的`LXDE`并且在默认壁纸下，搜狗输入法的状态栏和候选框周围会有一个黑框...不太美观但不影响使用。

## 配备有`intel`集成显卡和`NVIDIA`独立显卡的机器登入图形界面时机器挂起（关机）

- 这主要是Linux对于`NVIDIA`显卡驱动的问题引起的。

- 如果不启动图形界面，只用`tty`，是没有问题的。

- 解决方法（由于我个人不太需要使用N卡，所以没有选择安装对应驱动等）：

  - 如果你将你的`Display Manager`加入了守护进程，那么我目前能想到的方法是使用一个`Live CD`，将你的Arch Linux挂载在`Live CD`上，然后使用`arch-chroot`进行操作。

  - 如果你开机进入的是`tty`，即你每次都是手动启动图形界面，那么就按照平时在终端中的操作来进行操作。

  - 操作如下：

    ```bash
    $ sudo pacman -S bumblebee   # 安装bumblebee
    $ sudo nano /etc/modprobe.d/modprobe.conf
    # 在文件中添加“options nvidia NVreg_Mobile=1”，然后保存退出，重启机器
    ```

- 参考：

  <https://wiki.archlinux.org/index.php/NVIDIA/Troubleshooting#Laptops:_X_hangs_on_login/out,_worked_around_with_Ctrl+Alt+Backspace>

# 美化

## 窗口管理器

### `i3`

- ```bash
  $ sudo pacman -S i3      # 软件包组中有冲突，选择移除即可
  $ sudo pacman -S dmenu   # i3下常用的一个快速启动器
  ```

### `dwm`

- 介绍：

  dwm是Suckless社区下X的动态窗口管理器。它以平铺，单片和浮动布局管理窗口。可以动态应用所有布局，从而为正在使用的应用程序和执行的任务优化环境。

- 优点：

  - 全部代码由纯C进行编写
  - 代码格式十分整洁(毕竟Suckless都是极简主义者)
  - 运行速度快，因为没有配置文件，源代码本身就包含了配置文件

- 缺点：

  - 由于代码太过于简单，缺少很多功能，可通过官方提供的补丁解决，不过对于C新手来说并不容易
  - 由于没有配置文件，所以每次更改源码后必须重新启动dwm才能使修改生效;幸运的是，Arch WiKi上有[解决方法](https://wiki.archlinux.org/index.php/Dwm)

- 安装dwm

- ```bash
  $ git clone https://git.suckless.org/dwm
  $ cd ./dwm
  $ make
  $ sudo make clean install
  ```
- 注意事项：
  - dwm下载后，如果你目前所使用的终端并不是[st](https://st.suckless.org/)(Simple Terminal)，就需要在`config.h`中进行一下操作:
  ```c
  static const char *termcmd[] = { "st", NULL }; //找到这一行，将"st"修改为你现在用的终端的启动命令
  ```

  - dwm一般下载后配置文件是`config.def.h`，但在使用`make`编译后，会生成`config.h`，这时可以将`config.def.h`删除掉，在打补丁时，有些补丁需要修改`config.def.h`，但它们没有找到，因此会询问文件名，这时，只要输入`config.h`后回车即可

  - dwm下载后，默认的MODKEY是`Mod1`(也就是`Alt`)，如果需要修改，就需要在`config.h`里进行下面这个操作：
  ```c
  #define MODKEY Mod1Mask; // 找到这一行，将Mod1Mask更改为你想要的键即可。如果要改为Win键，就将其改为Mod4Mask
  ```
