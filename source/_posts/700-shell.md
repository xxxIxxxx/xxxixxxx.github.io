---
title: shell 配置
date: 2021-8-11 23:50
categories: [shell]
tags: []
sticky:  #9999
---
# 安装 iterm2
**[前往官网 https://iterm2.com](https://iterm2.com)**

# 安装 ohmyzsh

**[ohmyzsh 介绍](https://github.com/ohmyzsh/ohmyzsh)**

## 主题
[主题预览列表](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

1. 打开 zshrc，推荐 VSCode 可格式化
 `open ~/.zshrc`
2. 添加主题
`ZSH_THEME="robbyrussell"`
3. 保存
`source ~/.zshrc`



## 插件
### 高亮插件

1. 下载
`
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
`
2. 打开 zshrc，推荐 VSCode 可格式化
 `open ~/.zshrc`

3. 添加插件描述
    ```
    plugins=(
    #高亮
    zsh-syntax-highlighting)
    ```
4. 保存 
    `source ~/.zshrc`

### 输入建议插件
1. 下载
`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

2. 打开 zshrc，推荐 VSCode 可格式化
 `open ~/.zshrc`

3. 添加插件描述
    ```
    plugins=(
    #高亮
    zsh-syntax-highlighting
    #输入建议
    zsh-autosuggeestions)
    ```
4. 保存 
    `source ~/.zshrc`

# .zshrc 样例
```

# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# Path to your oh-my-zsh installation.
export ZSH="/Users/z/.oh-my-zsh"
# clash
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890

#git 使用 clash
git config --global http.proxy 'socks5://127.0.0.1:7890'
git config --global https.proxy 'socks5://127.0.0.1:7890'

# mongoldb
export PATH=${PATH}:/usr/local/mongodb/bin
export PATH=${PATH}:/usr/local/mongodb/bin:$PATH

# homebrew
path=('/opt/homebrew/bin' $path)
export PATH

# flutter
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
export PATH=${PATH}:/Users/z/flutter/bin:$PATH
export PATH=${PATH}:/Users/z/flutter/bin
export LANG=en_US.UTF-8
export NO_PROXY=localhost,127.0.0.1

# java
JAVA_HOME="/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home"
PATH="$JAVA_HOME/bin:$PATH"
CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
export JAVA_HOME
export PATH
export CLASSPATH

# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
# ZSH_THEME="robbyrussell"
ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(git
    #自动建议
    zsh-autosuggestions
    #高亮
    zsh-syntax-highlighting)

source $ZSH/oh-my-zsh.sh

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

export MonkeyDevPath=/opt/MonkeyDev
export MonkeyDevDeviceIP=
export PATH=/opt/MonkeyDev/bin:$PATH



```
