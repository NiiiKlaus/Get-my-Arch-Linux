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
