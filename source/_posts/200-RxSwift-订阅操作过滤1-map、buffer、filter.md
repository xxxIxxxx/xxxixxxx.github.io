---
title: RxSwift-订阅操作过滤1-map、buffer、filter
categories: [Swift]
tags: [RxSwift]
date: 2020-11-16
---
# map
同 `Swift`中 `map` 用法一样，对值进行处理并返回
```
let sub = PublishSubject<String>()

sub.map { $0 + "mmmmm" }
    .subscribe { event in
        print(event.element)
    }
    .disposed(by: disposeBag)
sub.onNext("a")
//Optional("ammmmm")

```
# buffer
`timeSpan ` 缓存间隔时间、              `count `缓存个数 、  `scheduler `线程
发送两个`event`后会触发订阅。满 2 秒也会触发订阅 ，如果`event` 没有发送空数组
```
let sub = PublishSubject<String>()
sub.buffer(timeSpan: 2, count: 2, scheduler: MainScheduler.asyncInstance)
    .subscribe { event in
        print("订阅1", event)
    }.disposed(by: disposeBag)

sub.onNext("发送1")
sub.onNext("发送2")
```

# filter 
过滤 同`Swift`中`filter`一样
```
let ob = Observable.of(10, 11, 12, 99, 33, 55, 77)
ob.filter { $0 > 20
}.subscribe(onNext: { element in
    print(element)
}).disposed(by: disposeBag)
```
