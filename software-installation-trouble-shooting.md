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

  然而在我的`LXDE`并且在默认壁纸下，搜狗输入法的状态栏和候选框周围会有一个黑框...不太美观但不影响使用。