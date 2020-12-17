---
title: RxSwift-转数组、累计操作-toArray、reduce
categories: [Swift]
tags: [RxSwift]
---
# toArray
将所有的事件集合在一起作为一个数组发出，需要发送`onCompleted`事件
```
let ob = PublishSubject<String>()
ob.toArray().subscribe { strArr in
    print(strArr)
} onError: { _ in
}.disposed(by: disposeBag)
ob.onNext("1")
ob.onNext("2")
ob.onNext("3")
ob.onCompleted()
```

# reduce
累计操作，将每一次的事件都累积在一起在发送`onCompleted`时统一发送。
```
let ob = PublishSubject<String>()
ob.reduce("初始值", accumulator: +).subscribe { event in
    print(event)
}.disposed(by: disposeBag)
ob.onNext("1")
ob.onNext("2")
ob.onNext("3")
ob.onCompleted()
```
