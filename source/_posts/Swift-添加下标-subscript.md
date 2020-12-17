---
title: Swift 添加下标 subscript
categories: [Swift]
tags: [下标]
+ sticky:  #9999
---

# 关键子 `subscript `
参数和返回值可以是任意类型（`inout`输入输出除外）
```
struct People {
    var name = "", age = 0

// 给实例添加下标
    subscript(n: String) -> Int {
        get {
            return age
        }
        set {
            age = newValue
        }
    }

// 给结构体添加下标
    static subscript(name: String, age: Int) -> People {
        People(name: name, age: age)
    }
}

var a = People(name: "哈哈哈", age: 18)
print(a["哈哈哈"])//18
a["哈哈哈"] = 20
print(a["哈哈哈"])//20
let p = People["哈喽", 20]
print(p)//People(name: "哈喽", age: 20)
```
