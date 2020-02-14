# 初步配置出现的问题汇总

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