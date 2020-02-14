# 美化过程中出现的问题汇总

## Xorg服务自启

### 不同shell的方法

- bash&zsh

  bash用户需要在`~/.bash_profile`加入以下内容;zsh用户需要在`~/.zprofile`中加入一下内容：

  ```bash
  if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
      exec startx
  fi
  ```

- fish

  fish用户需要在`~/.config/fish/config.fish`中加入以下内容：

  ```bash
  if status is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx -- -keeptty
    end
  end
  ```
