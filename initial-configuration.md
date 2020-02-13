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
