---
title: Flutter 配置相关
categories: [Flutter]
tags: []
+ sticky:  #9999
---

### 问题一
> CocoaPods requires your terminal to be using UTF-8 encoding 
Consider adding the following to ~/.profile:
export LANG=en_US.UTF-8

解决方案
```
1.打开终端 输入命令open -e .bash_profile
2.在终端输入 export LANG=en_US.UTF-8 保存
3.重启VSCode

⚠️⚠️安装zsh导致全局配置还不行的话⚠️⚠️
1. vim ~/.zshrc
2. 按E进入编辑 （大写E）
3. 在最后一行加入  export LANG=en_US.UTF-8
4. 按ESC退出编辑  键入 :wq 保存退出
5. 重启VSCode

```

### 问题二
> -bash: flutter: command not found

解决方案
```
1.打开终端 输入命令open -e .bash_profile
2.在终端输入 

export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
export PATH=${PATH}:/Users/(你的用户名)/flutter/bin:$PATH
export PATH=${PATH}:/Users/(你的用户名)/flutter/bin
export NO_PROXY=localhost,127.0.0.1


3.终端输入 source ~/.bash_profile保存

⚠️⚠️安装zsh导致全局配置还不行的话⚠️⚠️
1. vim ~/.zshrc
2. 按E进入编辑 （大写E）
3. 在最后一行加入  
export PATH=/Users/z/flutter/bin:$PATH
export NO_PROXY=localhost,127.0.0.1

4. 按ESC退出编辑  键入 :wq 保存退出


```
