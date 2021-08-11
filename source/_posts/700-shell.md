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
# Path to your oh-my-zsh installation.
export ZSH="/Users/z/.oh-my-zsh"

# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="robbyrussell"

plugins=(git
    #自动建议
    zsh-autosuggestions
    #高亮
    zsh-syntax-highlighting)

source $ZSH/oh-my-zsh.sh

```
