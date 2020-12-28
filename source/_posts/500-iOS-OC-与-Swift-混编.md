---
title: iOS OC 与 Swift 混编
categories: [iOS]
tags: [iOS混编]
date: 2020-12-06
---


# 1. XXX-Bridging-Header.h
新建Swift文件时一般会自动提示创建` XXX-Bridging-Header.h `文件。如果没有那么自己新建一个 Header 文件，命名为` 项目名-Bridging-Header.h `
![新建 Header 文件](https://upload-images.jianshu.io/upload_images/2331323-40814d95e9d8b2f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 2. 打开 Target -> BuildSettings 搜索 `Header`

`User Header Search Paths` 填写 `$(SRCROOT)`
--
`Enable Modules(c and objective-C)` 填写 `YES`
--
`Objective-C Bridging Header` 填写 `项目名称/项目名称-Bridging-Header.h` ⚠️这里是个路径
--
`Objective-C Generated Interface Header Name` 填写 `项目名称-Swift.h` 这里是 OC 引用 Swift 需要用到的。
--

![BuildSettings 需要修改的地方](https://upload-images.jianshu.io/upload_images/2331323-c91b49763e023f54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 3. pod 需要修改的地方
Podfile 增加 `use_frameworks!` 后重新 `pod install`
```
target'XXXXX' do
use_frameworks!
```
**⚠️并把所有 `pod` 导入的库 使用 `<>` 导入 而不是`""` 例如`#import <AFNetworking.h>`**
> ⚠️第三库报错大多都是导入方式不对引起的⚠️
# 4. OC 引用 Swift
在需要的地方导入 `#import "项目名-Swift.h"` 然后在需要被引用的属性、方法前增加 `@objc` 
⚠️ ` 项目名-Swift.h 这个是隐藏文件看不到`
```
class XXXViewController: UIViewController {

    @objc var name:String = ""

    override func viewDidLoad() {
        super.viewDidLoad()
    }  
    @objc func data()  {
    }
}
```
# 5. Swift 引用 OC
把需要引用的文件导入到 `项目名-Bridging-Header.h` ，即可在 Swift 中引用。
