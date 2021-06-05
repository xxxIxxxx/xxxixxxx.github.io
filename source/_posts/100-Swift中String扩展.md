---
title: 在 Swift 中为 String 添加扩展
date: 2021-6-05 15:55
categories: [Swift]
tags: []
sticky: #9999
---

# String extension 代码

```
extension String {
    func index(from: Int) -> Index {
        // 增加越界防护， 负数就不考虑了吧
        if from < count {
            return index(startIndex, offsetBy: from)
        }
        return endIndex
    }

    func substring(from: Int) -> String {
        let fromIndex = index(from: from)
        return String(self[fromIndex...])
    }

    func substring(to: Int) -> String {
        String(prefix(to))
    }

    func substring(with r: Range<Int>) -> String {
        let startIndex = index(from: r.lowerBound)
        let endIndex = index(from: r.upperBound)
        return String(self[startIndex ..< endIndex])
    }
}
```

# 使用

```
        let str = "01234567"

        _ = str.substring(from: 0) // "01234567"
        _ = str.substring(from: 4) // "4567"
        _ = str.substring(from: 100) // ""


        _ = str.substring(to: 0) // ""
        _ = str.substring(to: 1) // "0"
        _ = str.substring(to: 100) // "01234567"


        _ = str.substring(with: 0 ..< 1) // "0"
        _ = str.substring(with: 0 ..< 100) // "01234567"
```
