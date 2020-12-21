---
title: Swift 数组
categories: [Swift]
tags: 
sticky:  #9999
date: 2020-11-22
---

# 删除元素
```
var list = ["1","2","3","4"]
list.removeAll{ $0 == "2" }
//["1","3","4"]
```


# Swift 数组遍历的几种方式
### 1. for-in 不带索引
```
let arr = [Int](7 ..< 10)
/// 不带索引
for obj in arr {
    print(obj)
}
```
### 2. forEach 不能使用 break continue ，只能使用 return
```
let arr = [Int](7 ..< 10)
/// 不带索引
arr.forEach { obj in
    // 不能使用 break continue ，只能使用 return
    print(obj)
}
```
### 3. enumerated() 带索引 和 值
```
let arr = [Int](7 ..< 10)
/// 带索引 和 值
for (index, obj) in arr.enumerated() {
    print("位置：\(index)" + "值：\(obj)")
}
```
### 4. while
```
let arr = [Int](7 ..< 10)
/// 迭代器
var arrIterator = arr.makeIterator()
while let obj = arrIterator.next() {
    print(obj)
}
```
### 5. indices 下标索引 遍历下标
```
let arr = [Int](7 ..< 10)
/// 下标索引 遍历下标
for index in arr.indices {
    print(index)
}
```
# 区间 for-in 区间 for 循环
```
let s = 5
/// 开区间不包含 50 ， 5 个一输出
for i in stride(from: 0, to: 50, by: s) {
    print(i)
}

/// 闭区间包含 50， 5 个一输出
for i in stride(from: 0, through: 50, by: s) {
    print(i)
}
```

# 数组的一些查找操作
```
let array = [Int](7 ..< 117)

let a = array.contains(100)
print("\(a ? "包含" : "不包含")" + "100")

let b = array.contains(where: { $0 > 8 })
print("\(b ? "含有大于8的数字" : "不含有大于8的数字")")

let c = array.allSatisfy { $0 >= 6 }
print("\(c ? "所有数字都大于等于6" : "有数字小于6")")

print("数组中第一个元素是" + "\(String(describing: array.first))")

print("数组中最后一个元素是" + "\(String(describing: array.last))")

let first = array.first(where: { $0 > 8 })
if let first = first {
    print("第一个大于8的数字是" + "\(first)")
}

let last = array.last(where: { $0 > 8 })
if let last = last {
    print("最后一个大于8的数字是" + "\(last)")
}

/// 10 在数组中第一次出现的位置
array.firstIndex(of: 10)
/// 17 在数组中最后一次出现的位置
array.lastIndex(of: 17)
```
