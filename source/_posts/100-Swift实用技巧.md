---
title: Swift 实用技巧
date: 2021-6-05 16:13
categories: [Swift]
tags: []
sticky: #9999
---

# 1. protocol + extension 初始化后直接配置相应属性

```
protocol XXXBuilder {}

extension XXXBuilder {
    public func with(configure: (inout Self) -> Void) -> Self {
        var this = self
        configure(&this)
        return this
    }
}

extension NSObject: XXXBuilder {}

// 使用
let tipLab = UILabel().with { lab in
            lab.textColor = .red
            lab.backgroundColor = .black
        }
```
