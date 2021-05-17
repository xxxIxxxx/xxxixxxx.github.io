---
title: 在 M1 芯片的 Mac 上使用 CocoaPods
date: 2021-5-17 20:36
categories: [iOS]
tags: [CocoaPods]
sticky: #9999
---

# 问题

最近换了 M1 芯片的 MacBook Pro，在配置环境完成后 `pod install` 操作发现出错了。

# 在 M1 上使用 CocoaPods 的方法。

## 1. 首先执行一次

`sudo arch -x86_64 gem install ffi`

## 2. 然后再替换之前 pod install

`arch -x86_64 pod install`

# 如何查找解决方案

第一时间想到去 [CocoaPods issues](https://github.com/CocoaPods/CocoaPods/issues) 搜索相关问题。
然后果然在 [Got error while trying pod install](https://github.com/CocoaPods/CocoaPods/issues/10220) 中找到了解决方案。
