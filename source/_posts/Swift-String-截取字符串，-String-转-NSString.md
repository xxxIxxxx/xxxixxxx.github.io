---
title: Swift String 截取字符串，String 转 NSString
categories: [Swift]
tags: []
+ sticky:  #9999
---

# String 转 NSString，转为 NSString 后 OC 的方法就能使用了
```
// 转为 NSString
 ("ABCD" as NSString)
// 调用 NSString 的方法
 ("ABCD" as NSString).substring(to: 1)
```

# Swift 中 String 的字符串截取
```

 let str = "ABCDEFGHIGK"

        print("前5个" + "\(str.prefix(5))")
        // 前5个ABCDE

        print("前150个" + str.prefix(150))
        // 前150个ABCDEFGHIGK

        print("后3个" + "\(str.suffix(3))")
        // 后3个IGK

        print("后150个" + "\(str.suffix(150))")
        // 后150个ABCDEFGHIGK

        let startIndex = str.index(str.startIndex, offsetBy: 2)
        let endIndex = str.index(str.startIndex, offsetBy: 5)

        print("2-5是" + str[startIndex ..< endIndex])
        // 2-5是CDE

```
