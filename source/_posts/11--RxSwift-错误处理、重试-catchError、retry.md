---
title: RxSwift-错误处理、重试-catchError、retry
categories: [Swift]
tags: [RxSwift]
---
# catchError
当发送了`error`事件后可以返回一个新的序列
```
enum ObError: Error {
    case error1
}

let ob1 = PublishSubject<String>()
let ob2 = PublishSubject.of("A", "B")

ob1.catchError { (error) -> Observable<String> in
    print(error)
    return ob2
}.subscribe { event in
    print(event)
}.disposed(by: disposeBag)
ob1.onNext("111")
ob1.onError(ObError.error1)
//next(111)
//error1
//next(A)
//next(B)
//completed
```
# retry
当发送了`error`后可以重新发送
```
var isFail = true
let obs = Observable<String>.create { (ob) -> Disposable in
    ob.onNext("成功1")
    if isFail {
        ob.onError(ObError.error1)
        isFail = false
    }
    ob.onNext("重试成功")
    ob.onCompleted()
    return Disposables.create()
}

obs.retry(2).subscribe { event in
    print(event)
}.disposed(by: disposeBag)

next(成功1)
next(成功1)
next(重试成功)
completed
```
