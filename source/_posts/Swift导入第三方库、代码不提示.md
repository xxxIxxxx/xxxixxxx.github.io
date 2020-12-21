
---
title: 第三方库提示
categories: [Swift]
tags: []
sticky:  #9999
date: 2020-11-11
---

#### 1.像OC的pch文件一样导入第三方库
```
创建一个Swift文件，在导入的库前添加 @_exported
🌰

@_exported import Alamofire

```
#### 2.Swift导入的第三方库代码没提示
```
1.选择target 
2.选择Build Settings 
3.搜索 User Header Search Paths
4.填写 $(PODS_ROOT)，并设置为“recursive”  
```



