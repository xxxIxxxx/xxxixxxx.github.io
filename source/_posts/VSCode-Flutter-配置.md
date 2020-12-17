---
title: VSCode Flutter 配置
categories: [Flutter]
tags: [VSCode]
+ sticky:  #9999
---

# 插件
- Dart
- Flutter
- Flutter Generators
- Flutter Widget Snippets
- Flutter Helpers
- [FF] Flutter Files
- Awesome Flutter Snippets
# 运行配置
`shift + cmd + d` 添加以下配置，这样就不用每次都在终端输入命令了
![操作图](https://upload-images.jianshu.io/upload_images/2331323-c47d75e75723b671.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "debug", //debug 模式
            "request": "launch",
            "type": "dart",
        },
        {
            "name": "profile", //profile 模式 可解决非联机调试白屏
            "request": "launch",
            "type": "dart",
            "flutterMode": "profile"
        },
        {
            "name": "release", //release 模式 可解决非联机调试白屏
            "request": "launch",
            "type": "dart",
            "flutterMode": "release"
        },
    ]
}
```


### 搜索关键词
VSCode 插件
VSCode Flutter 调试配置
VSCode Flutter release 模式
Flutter release
Flutter 启动白屏


# 如果有帮助求点赞！
