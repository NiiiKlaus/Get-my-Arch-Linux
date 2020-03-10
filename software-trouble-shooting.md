# 软件安装以及使用过程中出现的问题汇总

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

## `fish`下`source /etc/profile`报错

- 这里主要是因为`fish`和Arch Linux默认的`bash`是两个不同的终端命令解析器。就如`Python2.x`和`Python3.x`一样，两个终端命令解析器的对于`shell`脚本的`parsing`有一些差别。

- 这里我的解决办法是将`fish`切换为了`zsh`…毕竟不是特别熟悉`fish`…

  ```bash
  $ chsh -s /bin/zsh   # 更改当前用户的默认shell，并重启终端。
  ```

## `alacritty`下使用`clear`命令清屏幕报错`'alacritty': unknown terminal type.`

- 我自己出现这个情况时，在终端敲入命令`clear`无效，但是敲入`/usr/bin/clear`有效。所以当时怀疑是环境变量的问题。又切换了终端模拟器到`st`，问题没有出现…所以又怀疑是`alacritty`的问题。上网搜索了一下，找到了有效的解决办法，但我没搞懂是为什么…

- 解决办法：

  修改环境变量，在`/etc/profile`中添加如下：

  ```bash
  $ export TERMINFO=/usr/share/terminfo
  ```

  重启终端生效。

## `alacritty`和`st`在未完全配置的情况下，使用安装好插件的`vim`中的字体颜色是纯白

- 出现这个情况时，我自己本机一共安装了4个终端模拟器：
  - `alacritty`
  - `lxterminal`
  - `st`
  - `deepin-terminal`

- 在`alacritty`和`st`中，`vim`无法显示其他除白色以外的颜色。起初以为是插件的问题，后来查阅资料之后发现是一个终端变量的问题：

  - 对于同一条命令`echo $TERM`，四个终端模拟器的返回各不相同：
    - `alacritty`：`alacritty`
    - `lxterminal`：`xterm-256color`
    - `st`：`st-256color`
    - `deepin-terminal`：`xterm-256color`

  `lxterminal`和`deepin-terminal`是可以正常显示`vim`的颜色的，所以问题出在哪里就显而易见了。

- 对于`vim`而言，要想正确显示颜色，`TERM`变量的值只能是`xterm-256color`或者`screen-256color`。

- 解决办法：

  修改环境变量，在`/etc/profile`中加入`export TERM=xterm-256color`，然后重新加载环境变量`source /etc/profile`

- 参考：<https://unix.stackexchange.com/questions/261576/vim-color-scheme-not-being-applied>

## 在跟着[教程](https://www.bilibili.com/video/av79909133?from=search&seid=884209540666222108)配合`dwm`时，`statusbar`出现小方框

- 这主要是因为系统缺少某些字体。教程中 UP主 状态栏的一些图标，譬如说上传、下载的箭头，都是`unicode`的字符。如果出现小方框，多半是未安装需要的字体，或者是表情字体的默认项有误。

- 这里我在安装了之前 UP 推荐安装的一些表情字体之后，上传和下载的箭头正常显示了。其余的符号存在于另一个字体包中。

- 解决办法：

  安装所需字体：

  ```bash
  $ sudo pacman -S tty-symbola
  ```

  安装完成之后重启系统即可。

