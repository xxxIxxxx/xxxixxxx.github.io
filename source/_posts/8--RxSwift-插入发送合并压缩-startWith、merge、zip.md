---
title: RxSwift-插入发送合并压缩-startWith、merge、zipignoreElement
categories: [Swift]
tags: [RxSwift]
---
# startWith
在订阅的时候插入发送事件，后加入的先发送。完成事件发送时不会插入。
```
let ob = PublishSubject<String>()
ob.startWith("插入1").startWith("插入2").subscribe(onNext: { element in
    print(element)
}).disposed(by: disposeBag)
ob.onNext("发送1")
插入2
插入1
发送1
```

# merge
合并操作，将多个 `Observable` 合并成一个
```
let ob1 = PublishSubject<String>()
let ob2 = PublishSubject<String>()
Observable.of(ob1,ob2).merge().subscribe { (event) in
    print(event)
}.disposed(by: disposeBag)
ob1.onNext("ob1 发1")
ob2.onNext("ob2 发1")
ob1.onNext("ob1 发2")
ob2.onNext("ob2 发2")
```

# zip
将 n 个`Observable`压缩成一个发送事件，必须每个都参与的发送完才会发送一次事件。参与的成对发送完
```
let ob1 = PublishSubject<String>()
let ob2 = PublishSubject<String>()
Observable.zip(ob1,ob2).subscribe { (event) in
    print(event)
}

ob1.onNext("ob1  2")
ob1.onNext("ob1  3")
ob2.onNext("ob2  A")
ob2.onNext("ob2  B")
ob2.onNext("ob2  C")
ob1.onNext("ob1  1")

//next(("ob1  2", "ob2  A"))
//next(("ob1  3", "ob2  B"))
//next(("ob1  1", "ob2  C"))
```
