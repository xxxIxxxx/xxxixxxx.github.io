---
title: iOS 多线程
categories: [iOS]
tags: [Thread,GCD,多线程]
+ sticky:  #9999
---

# 1. Thread

#### 闭包内直接执行代码
```
/// 闭包内直接执行代码
Thread.detachNewThread {
                print("111")
}
```
#### 创建一个方法 开启子线程后去调用
```
//创建一个方法 开启子线程后去调用
let tr = Thread(target: self, selector: #selector(threadTest), object: nil)
//开启
tr.start()

@objc func threadTest () {
        print("777")
}
```

# 2. Operation
#### BlockOperation
```
/// BlockOperation
let operation = BlockOperation {
      print(" ----- BlockOperation  -----")
}
let queue = OperationQueue()
queue.addOperation(operation)
```

#### 继承自 Operation
```

/// 继承自 Operation
class MyOperation: Operation {
            override func main() {
                print("--- MyOperation do ... ----")
            }
}
let operation = MyOperation()
/// 当 operation 执行完 会执行这个
operation.completionBlock = {
            print("----- completionBlock  ------")
}
let queue = OperationQueue()
queue.addOperation(operation)
```

# 3. GCD
#### 队列 Queue 常用的

```
// 异步 并行
DispatchQueue.global().async {
            
        }
// 回到主线程异步
DispatchQueue.main.async {
            
        }
// 异步延时
DispatchQueue.global().asyncAfter(deadline: .now() + 1) {
            
        }
```


#### Queue
> label：名字标签  
qos：优先级
attributes：串行队列、并行队列 concurrent
autoreleaseFrequency：频率
```

let queue = DispatchQueue(label: "myQueue", qos: DispatchQoS.default, attributes: DispatchQueue.Attributes.concurrent, autoreleaseFrequency: DispatchQueue.AutoreleaseFrequency.inherit, target: nil)
        
queue.async {
            print(" --- 异步 ---")
        }
        
queue.sync {
            print("--- 同步 -----")
        }
        
queue.asyncAfter(deadline: .now() + 5) {
            print("---- 5s ------")
        }
```

#### 串行队列

> 同步会等待他上一个进入的线程执行完才会开始(无论上一个线程是同步还是异步)，并且阻挡线程等待自己执行完毕才会继续往下执行
```
/// 串行队列
let queue = DispatchQueue(label: "myQueue")
let group = DispatchGroup()

print("------- 开始 -------")

group.enter()
queue.async {
    sleep(3)
    print("------- 异步 A -------")
    group.leave()
}


group.enter()
queue.sync {
    print("------- 同步 A -------")
    group.leave()
}
print("------- 同步 A 结束 -------")


group.enter()
queue.sync {
    print("------- 同步 B -------")
    group.leave()
}
print("------- 同步 B 结束 -------")


group.enter()
queue.async {
    sleep(1)
    print("------- 异步 B -------")
    group.leave()
}

print("------- 等待 -------")
// wait 会阻塞线程
group.wait()
print("------- 结束 -------")

// notify 不会阻塞
//group.notify(queue: queue) {
//print("------- 结束 -------")
//}

------- 开始 -------
------- 异步 A -------
------- 同步 A -------
------- 同步 A 结束 -------
------- 同步 B -------
------- 同步 B 结束 -------
------- 等待 -------
------- 异步 B -------
------- 结束 -------
```

#### 并行队列
> 同步会阻塞后面的线程执行，且同步不受前边异步的影响
```
let queue = DispatchQueue(label: "myQueue", attributes: DispatchQueue.Attributes.concurrent)
let group = DispatchGroup()

print("------- 开始 -------")

group.enter()
queue.async {
    sleep(1)
    print("------- 异步 A -------")
    group.leave()
}

group.enter()
queue.sync {
    sleep(1)
    print("------- 同步 A -------")
    group.leave()
}
print("------- 同步 A 结束 -------")

group.enter()
queue.sync {
    sleep(3)
    print("------- 同步 B -------")
    group.leave()
}
print("------- 同步 B 结束 -------")

group.enter()
queue.async {
    sleep(2)
    print("------- 异步 B 耗时操作 -------")
    group.leave()
}

group.notify(queue: queue) {
    print("------- 全部结束 -------")
}
print("------- 未被耗时操作阻塞 -------")

------- 开始 -------
------- 同步 A -------
------- 同步 A 结束 -------
------- 异步 A -------
------- 同步 B -------
------- 同步 B 结束 -------
------- 未被耗时操作阻塞 -------
------- 异步 B 耗时操作 -------
------- 全部结束 -------
```
#### DispatchSource 定时器例子
```
var time = 7
let timer = DispatchSource.makeTimerSource(flags: [], queue: .global())
//每秒执行一次
timer.schedule(deadline: .now(), repeating: 1)
timer.setEventHandler {
//  由于使用的 queue 是  .global()   这里不是主线程 
    time -= 1
    print("----- \(time)")
    if time == 1 {
        timer.cancel()
    }
}
timer.resume()
```
