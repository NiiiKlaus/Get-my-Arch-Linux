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

### `Xorg使用方法`

- 找到`/etc/X11/xinit/xinitrc`文件，使用编辑器在文件末尾进行以下操作：

  ```bash
  exec dwm   # 如果你并不打算使用dwm作为你的窗口管理器，
             # 就将其改为你所使用的窗口管理器的启动命令
  twm &
  xclock -geometry 50x50-1+1 &
  xterm -geometry 80x50+494+51 &
  xterm -geometry 80x20+494-0 &
  exec xterm -geometry 80x66+0+0 -name login
  # 找到以上这几行，在它们开头插入“#”以此注释掉
  ```

- 在进行了以上操作后，在`tty`下运行`startx`命令开启`X`服务，随后即可进入窗口管理器。

- 如果你觉得每次修改`xinitrc`文件要到`/etc`目录下很麻烦，可以创建软链接到你的用户目录：

  ```bash
  $ sudo -E ln -sf /etc/X11/xinit/xinitrc ~/.xinitrc
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
