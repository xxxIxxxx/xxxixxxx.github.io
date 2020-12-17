---
title: Swift GCD barrier
categories: [Swift]
tags: [GCD,多线程]
+ sticky:  #9999
---


# 异步读写造成数组越界
```
let count = 100000
var array = Array(0 ... count)

func getLast() -> Int {
// ⚠️⚠️ 这里加了判断看似安全，但在异步操作时 判断 array.count > 0 的同时可能就有一个异步的操作改变了数组
    if array.count > 0 {
        return array[array.count - 1]
    }
    return -1
}

func removeLast() {
    array.removeLast()
}

DispatchQueue.global().async {
    for _ in 0 ... count {
        removeLast()
    }
}

DispatchQueue.global().async {
    for _ in 0 ... count {
        print(getLast())
    }
}
```

# 使用 barrier
> 会保证在同一个队列中 .barrier 执行完之后才会去做其他线程操作
```
let count = 100000
var array = Array(0 ... count)
let arrayQueue = DispatchQueue(label: "arrayQueue", attributes: DispatchQueue.Attributes.concurrent)

func getLast() -> Int {
    arrayQueue.sync { () -> Int in
        if array.count > 0 {
            return array[array.count - 1]
        }
        return -1
    }
}

func removeLast() {
//⚠️⚠️ 这里使用 barrier 
    let workItem = DispatchWorkItem(qos: DispatchQoS.default, flags: DispatchWorkItemFlags.barrier) {
        array.removeLast()
    }
    arrayQueue.async(execute: workItem)
}

DispatchQueue.global().async {
    for _ in 0 ... count {
        removeLast()
    }
}

DispatchQueue.global().async {
    for _ in 0 ... count {
        print(getLast())
    }
}

```
