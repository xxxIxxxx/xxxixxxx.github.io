---
title: RxSwift-创建可观察序列
categories: [Swift]
tags: [RxSwift]
---


### empty() 方法初始化
```
// 创建了一个空内容的 Observable
let ob = Observable<Int>.empty()
// 先简单的写一种订阅的方法
ob.subscribe { print("执行了") }
```

###  just() 方法 传入默认值初始化
```
// 这里不用给定泛型，会根据 just 自动推倒出
let ob = Observable.just("初始化默认值")
```

###  of() 方法 传入可变数量的值，但必须是同一类型
```
let ob = Observable.of("可", "变", "数", "量")
```

###  from() 传入数组初始化
```
let ob = Observable.from(["数", "组"])
```

### never() 永远不会发出 event 的 Observable 序列
```
let ob = Observable<Any>.never()
```

### error() 直接发送一个错误
```
enum OBError: Error {
    case abc
}
let ob = Observable<OBError>.error(OBError.abc)
```

### interval() 每一秒发送一次
```
let ob = Observable<Int>.interval(1, scheduler: MainScheduler.asyncInstance)
```

### timer() 定时发送
```
// 3 秒后，仅发送一次
let ob = Observable<Int>.timer(3, scheduler: MainScheduler.instance)

// 3 秒后，每 2 秒发送一次
let ob = Observable<Int>.timer(3, period: 2, scheduler: MainScheduler.asyncInstance)
```
