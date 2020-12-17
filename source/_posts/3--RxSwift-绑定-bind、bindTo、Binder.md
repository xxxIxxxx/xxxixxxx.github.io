---
title: RxSwift-绑定-bind、bindTo、Binder
categories: [Swift]
tags: [RxSwift]
---
### bind
```
let ob = Observable<Int>.interval(1, scheduler: MainScheduler.asyncInstance)

ob.map {
// 对值进一步处理然后返回
    "count " + "\($0)"
}
.bind { text in
    countLab.text = text
}.disposed(by: disposeBag)

ob.bind { x in
    print(x)
}.disposed(by: disposeBag)
```
### Binder + bindTo
```
let ob = Observable<Int>.interval(1, scheduler: MainScheduler.asyncInstance)
let observer: Binder<String> = Binder(countLab) { lab, text in
    lab.text = text
}

ob.map {
    "c" + "\($0)"
}
.bind(to: observer)
.disposed(by: disposeBag)
```
