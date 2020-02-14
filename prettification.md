# 美化
## 窗口管理器

使用窗口管理器需要X服务的支持，[Xorg安装方法](initial-configuration.md#6-安装xorg)

### `Xorg使用方法`

- 找到`/etc/X11/xinit/xinitrc`文件，使用编辑器在文件末尾进行以下操作：

  ```
  exec dwm #如果你并不打算使用dwm作为你的窗口管理器，就将其改为你所使用的窗口管理器的启动命令

  twm &
  xclock -geometry 50x50-1+1 &
  xterm -geometry 80x50+494+51 &
  xterm -geometry 80x20+494-0 &
  exec xterm -geometry 80x66+0+0 -name login
  #找到以上这几行，在它们开头插入#以此注释掉
  ```

- 在进行了以上操作后，在tty下运行`startx`命令开启X服务，随后即可进入窗口管理器。

- 如果你觉得每次修改`xinitrc`文件要到`etc`目录下很麻烦，可以创建软链接到你的用户目录：

  ```bash
  $ sudo -E ln -sf /etc/X11/xinit/xinitrc ~/.xinitrc
  ```

### `i3`

- 介绍：

  i3wm是一个比较好用的平铺式窗口管理器，它的功能比较齐全，自带状态栏、锁屏等工具。

- 优点：

  - 自带功能齐全，用户体验较好
  - 拥有配置文件，能够让用户自定义，启动i3后会生成配置文件，一般在`~/.config/i3/`

- 缺点：

  - 二进制可执行文件较大，对于配置低的电脑运行起来可能会卡顿
  - 由于拥有配置文件，在每次启动i3时会读取配置文件，因此启动速度会较慢

- 安装i3

  ```bash
  $ sudo pacman -S i3      # 软件包组中有冲突，选择移除即可
  $ sudo pacman -S dmenu   # i3下常用的一个快速启动器
  ```

- 注意事项：

  - 在配置文件里设置自启程序时，可能会使鼠标呈现"繁忙"的状态(我个人无法忍受)，解决办法就是在程序启动命令之前加上`--no-startup-id`参数

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

  ```bash
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
