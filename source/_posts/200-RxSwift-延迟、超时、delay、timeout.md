---
title: RxSwift-延迟、超时、delay、timeout
categories: [Swift]
tags: [RxSwift]
date: 2020-11-20
---
# delay
对所有发送事件(包括`onCompleted`)后延迟 n 秒接收
```
let ob = PublishSubject<String>()
ob.delay(RxTimeInterval.seconds(2), scheduler: MainScheduler.asyncInstance).subscribe { event in
    print(event)
}.disposed(by: disposeBag)
ob.onNext("发送了")
```

# timeout
 设置超时时间，超过规定时间的事件将发送  `error`
```
let ob = PublishSubject<String>()
ob.timeout(RxTimeInterval.seconds(3), scheduler: MainScheduler.instance).subscribe { event in
    print(event)
}.disposed(by: disposeBag)
ob.onNext("发送1")
DispatchQueue.global().asyncAfter(deadline: .now() + 4) {
    ob.onNext("超时发送")
}
//next(发送1)
//error(Sequence timeout.)
```
