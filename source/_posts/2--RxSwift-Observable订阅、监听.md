---
title: RxSwift-Observable订阅、监听
categories: [Swift]
tags: [RxSwift]
---
### 订阅
```
let ob = Observable.of("A", "B", "C")
/// 直接订阅所有的
ob.subscribe { event in
    print("事件", event)
// 通过 event.element 可以获取值
    print("值是", event.element)
}

///分开订阅
ob.subscribe { element in
    print("onNext", element)
} onError: { error in
    print("onError", error)
} onCompleted: {
    print("onCompleted")
} onDisposed: {
    print("onDisposed")
}

///仅订阅 onNext
ob.subscribe(onNext: { element in
    print(element)
})
```

### 监听 do
```
let ob = Observable.of("A", "B", "C")
ob.do { element in
    print("onNext", element)
} afterNext: { element in
    print("afterNext", element)
} onError: { error in
    print("onError", error)
} afterError: { error in
    print("afterError", error)
} onCompleted: {
    print("onCompleted")
} afterCompleted: {
    print("afterCompleted")
} onSubscribe: {
    print("onSubscribe")
} onSubscribed: {
    print("onSubscribed")
} onDispose: {
    print("onDispose")
}
/// 这里是订阅部分
.subscribe { element in
    print("onNext", element)
} onError: { error in
    print("onError", error)
} onCompleted: {
    print("onCompleted")
} onDisposed: {
    print("onDisposed")
}
```
