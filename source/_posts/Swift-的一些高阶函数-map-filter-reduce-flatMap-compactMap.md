---
title: Swift 的一些高阶函数 map、filter、reduce、flatMap、compactMap
categories: [Swift]
tags: [高阶函数]
sticky:  #9999
date: 2020-11-17
---


# map 对集合里的每一个元素进行操作，然后返回个新的集合
```
let numbers = [1, 3, 5, 7, 9]
/// 对集合里的每一个元素进行操作，然后返回个新的集合
print(numbers.map { $0 * 10 })
// [10, 30, 50, 70, 90]
```

# filter 过滤集合里面的每一个元素，返回一个满足条件的新的集合
```
let numbers = [1, 3, 5, 7, 9]
/// 过滤集合里面的每一个元素，返回一个满足条件的新的集合
print(numbers.filter { $0 > 5 })
// [7, 9]
```

# reduce  对集合里面的每一个元素 作用在当前累计的结果上
```
/// 对集合里面的每一个元素 作用在当前累计的结果上
let abc = ["a", "b", "c"]
print(abc.reduce("100") { $0 + ($1 + "kk") })
// 100akkbkkckk
```

# flatMap 集合内的元素全是集合，那么把元素拆成同一级 放在一个新的集合里
```
let list = [[1, 2, 3], [4, 5], [7]]
/// 集合内的元素全是集合，那么把元素拆成同一级 放在一个新的集合里
print(list.flatMap { $0 })
// [1, 2, 3, 4, 5, 7]

/// 只会拆一层
let list1 = [[1, 2, 3], [4, 5], [7], [[8], [9]]]
print(list1.flatMap { $0 })
// [1, 2, 3, 4, 5, 7, [8], [9]]
```

# compactMap 过滤空值

```
let names: [String?] = ["am",nil,"qw","er",nil]
/// 过滤空值
print(names.compactMap{ $0 })
//["am", "qw", "er"]
```
