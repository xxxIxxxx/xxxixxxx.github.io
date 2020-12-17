---
title: Swift GCD 死锁
categories: [Swift]
tags: [GCD,多线程]
+ sticky:  #9999
---


# 1. 串行队列中，在异步任务中添加同步任务
```
/// 由于没有定义 attributes 所以是串行队列
let queue = DispatchQueue(label: "myQueue")
queue.async {
    print("----- task 1 -------")
    queue.sync {
        print("----- task 2 -------")
    }
}

⚠️解决方法
/// 解决方法将串行改为并行
let queue = DispatchQueue(label: "myQueue", attributes: DispatchQueue.Attributes.concurrent)

```


# 2. 主线程同步
```
let queue = DispatchQueue.main
queue.sync {
    print("----- task 1 -------")
} 
```
