---
title:  Swift 类型转换 
tags: 
categories: [Swift]
sticky:  #9999
date: 2020-12-21 16:57:00
---

# Swift 类型转换 as 的使用

## if let as

 类型转换，此时 `btn` 是 `Any` 类型，使用 `as?` 将他尝试转为 `UIButton`类型。并赋值给 `a`。 实际开发中建议 `a` 与 `btn` 命名一致，这里为了便于区分
```

if let a = btn as? UIButton {
    print(a)
    // 这里 a 为真
}
```

## guard let as
和 `if let as` 基本一致，只是当转换失败时提前退出。适用于一些异步回调里。
```
guard let btn = btn as? UIButton else { return }
```
