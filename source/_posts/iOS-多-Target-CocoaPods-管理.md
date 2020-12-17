---
title: iOS 多 Target CocoaPods 管理
categories: [iOS]
tags: [CocoaPods,Target]
+ sticky:  #9999
---

# 1. iOS 多 Target CocoaPods 管理，直接来看例子
```
platform :ios, "11.0"
source "https://cdn.cocoapods.org/"
#source 'https://github.com/CocoaPods/Specs.git'

#定义公共库
def commonPods
  use_frameworks!

  pod "KakaJSON", "~> 1.1.2"
  pod "SnapKit", "~> 5.0.1"
end

#为 Target1 配置自己独有的库
target "Target1" do
  commonPods
  pod "YYCategories"
  pod "Alamofire", "~> 5.2.2"
end
#为 Target2 配置自己独有的库
target "Target2" do
  commonPods
  pod "Moya", "~> 14.0.0"
end

```
# 2. 判断在哪一个 Target，iOS Target 判断
### Swift 设置 
Build Settings 搜索 `swift compiler` 具体看图
![添加 Target 判断条件](https://upload-images.jianshu.io/upload_images/2331323-da3235308811d72b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 使用
```
        #if MAINTARGET
        tipLab.text = "mmmm"
        #endif
```

### OC 设置 
Build Settings 搜索 `macros` 具体看图
![OC 操作图](https://upload-images.jianshu.io/upload_images/2331323-3ae5817bcb53187d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 使用
```
     #ifdef TARGETMAIN
    NSLog(@"=======TARGETMAIN=======");
     #endif
```
