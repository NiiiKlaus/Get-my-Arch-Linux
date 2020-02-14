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

  