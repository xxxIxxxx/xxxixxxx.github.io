---
title: RxSwift-订阅操作过滤2-distinctUntilChanged、single、elementAt、ignoreElement
categories: [Swift]
tags: [RxSwift]
date: 2020-11-17
---
# distinctUntilChanged 
过滤连续重复的事件
```
let ob = Observable.of(1, 1, 1, 3, 5, 7, 9, 9)
ob.distinctUntilChanged().subscribe(onNext: { element in
    print(element)
//1 3 5 7 9
}).disposed(by: disposeBag)

```

# single
只发送一次正常事件，如果没有或者超过 1 个会发送 `error` 事件
```
let ob = Observable.of(1,2)
ob.single().subscribe(onNext: { element in
    print(element)
}, onError: { error in
    print("错误",error)
}).disposed(by: disposeBag)
//        1
//        错误 Sequence contains more than one element.


//----- single 增加过滤
let ob = Observable.of(1, 2, 1)
ob.single { $0 == 2 }.subscribe(onNext: { element in
    print(element)
}, onError: { error in
    print("错误", error)
}).disposed(by: disposeBag)
//        2
```

# elementAt
获取指定位置的事件，0 开始。 如果没有发生该指定位置事件 会发送错误
```
let ob = Observable.of(0, 1, 2, 3, 4)
ob.elementAt(2).subscribe(onNext: { element in
    print(element)
}, onError: { error in
    print(error)
}).disposed(by: disposeBag)
//2
```

# ignoreElements
会忽略所有主动发送的`event`事件，只保留 `error` 事件和 `Completed`事件
```
let ob = Observable.of(0,1,2,3,4)
ob.ignoreElements().subscribe {
    print("Completed")
} onError: { (error) in
    print(error)
}.disposed(by: disposeBag)
```
# take
只取前 n 个事件，数量达到或不足会发送 `Completed`。
```
let ob = Observable.of(0, 1, 2, 3)
ob.take(2).subscribe { element in
    print(element)
} onError: { error in
    print(error)
} onCompleted: {
    print("onCompleted")
}.disposed(by: disposeBag)
```

# takeLast
只取后 n 个事件，数量达到或不足会发送 `Completed`。
```
let ob = Observable.of(0, 1, 2, 3, 4)
ob.takeLast(12).subscribe { element in
    print(element)
} onError: { error in
    print(error)
} onCompleted: {
    print("onCompleted")
}.disposed(by: disposeBag)
```

# skip
跳过前 n 个事件，发送完剩下的事件后会发送`onCompleted`。不足 n 个直接发送`onCompleted`。
```
let ob = Observable.of(0,1,2,3,4,5)
ob.skip(4).subscribe { (element) in
    print(element)
} onError: { (error) in
    print(error)
} onCompleted: {
    print("onCompleted")
}.disposed(by: disposeBag)
```

# debounce
当两个事件的发送间隔大于约定时间时才会收到该事件，常用的例子是搜索时延迟搜索
```
let ob = PublishSubject<String>()
ob.debounce(RxTimeInterval.seconds(1), scheduler: MainScheduler.instance).subscribe(onNext: { element in
    print("收", element, CFAbsoluteTimeGetCurrent())
}).disposed(by: disposeBag)
print("发", "aaa", CFAbsoluteTimeGetCurrent())
ob.onNext("aaa")
DispatchQueue.global().asyncAfter(deadline: .now() + 0.5) {
    print("发", "bbb", CFAbsoluteTimeGetCurrent())
    ob.onNext("bbb")
}
DispatchQueue.global().asyncAfter(deadline: .now() + 1.5) {
    print("发", "ccc", CFAbsoluteTimeGetCurrent())
    ob.onNext("ccc")
}
DispatchQueue.global().asyncAfter(deadline: .now() + 3.5) {
    print("发", "ddd", CFAbsoluteTimeGetCurrent())
    ob.onNext("ddd")
}

//发 aaa 627481044.719082
//发 bbb 627481045.241852
//发 ccc 627481046.231139
//收 ccc 627481047.233378
//发 ddd 627481048.552644
//收 ddd 627481049.55595

```
