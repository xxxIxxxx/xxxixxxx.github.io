---
title: RxSwift-发送、订阅-Subjects、Variables
categories: [Swift]
tags: [RxSwift]
---

# Subjects 介绍
### 1. `Subjects` 是订阅者，也是`Observable`
- 订阅者：它能动态的接收新的值。
- `Observable`： 当`Subjects`有了新值后会通过`Event`将新值发出给他的所有订阅者。
---
### 2. 常用的方法
`onNext(:)：`是` on(.next(:))` 的简便写法。该方法相当于 `subject` 接收到一个`.next` 事件。
`onError(:)：`是` on(.error(:)) `的简便写法。该方法相当于 `subject` 接收到一个` .error` 事件。
`onCompleted()：`是 `on(.completed)`的简便写法。该方法相当于 `subject` 接收到一个 `
.completed `事件。


---
### 3. `Subjects` 有四种`PublishSubject`、`BehaviorSubject`、`ReplaySubject`、`Variable`
##### 相同点
- 都是`Observable`，他们的订阅者都能接收他们发出的新的`Event`
- 直到 `Subject` 发出 `.complete` 或者 `.error` 的 `Event` 后，该 `Subject` 便终结了，同时它也就不会再发出`.next`事件。
- 对于那些在` Subject` 终结后再订阅他的订阅者，也能收到 `subject`发出的一条` .complete` 或` .error`的` event`，告诉这个新的订阅者它已经终结了。
##### 不同点
-  `PublishSubject`
最普通的`Subject`，不需要初始值就能初始化。
他的订阅者只能收到他们订阅后的 `Event`。
```
let sub = PublishSubject<String>()

sub.onNext("订阅之前的不能接收到")

sub.subscribe { event in
    print(event.element)
//Optional("订阅之后的可以接收到")
//nil
}.disposed(by: disposeBag)

sub.onNext("订阅之后的可以接收到")
//结束
sub.onCompleted()
/// 结束之后添加的订阅能收到 completed
sub.subscribe { event in
    print(event)
}

sub.onNext("结束后发的都收不到")
```
- `BehaviorSubject`
需要一个默认值初始化
当一个订阅者订阅之后会立马收到上一个`Event`，之后就是正常情况发一个收一个。
`onCompleted()`之后的订阅者也只能收到`Completed`。
```
let sub = BehaviorSubject(value: "默认值")

sub.subscribe { event in
    print("订阅1", event)
}.disposed(by: disposeBag)
sub.onNext("发送1")
sub.subscribe { event in
    print("订阅2", event)
}.disposed(by: disposeBag)
sub.onCompleted()
sub.subscribe { event in
    print("订阅3", event)
}.disposed(by: disposeBag)

订阅1 next(默认值)
订阅1 next(发送1)
订阅2 next(发送1)
订阅1 completed
订阅2 completed
订阅3 completed
```
- `ReplaySubject`
创建的时候需要一个参数`bufferSize`设置记录个数
新添加的订阅会接收到之前发送的两个  `Event`，如果不足两个就只接收一个。
如果超过两个只接收最新的两个。
如果订阅时已经结束除了会接收到最新的两个`Event`外还有结束的`complete `或`error `。

```
let sub = ReplaySubject<String>.create(bufferSize: 2)

sub.subscribe { event in
    print("订阅1", event)
}.disposed(by: disposeBag)
sub.onNext("发送1")
print("-------")
sub.subscribe { event in
    print("订阅2", event)
}.disposed(by: disposeBag)

sub.onNext("发送2")
sub.onNext("发送3")
sub.onNext("发送4")
print("-------")
sub.subscribe { event in
    print("订阅3", event)
}.disposed(by: disposeBag)
sub.onCompleted()
print("-------")
/// 不仅会收到最后的两个 event 还有 Completed
sub.subscribe { event in
    print("订阅4", event)
}

订阅1 next(发送1)
-------
订阅2 next(发送1)
订阅1 next(发送2)
订阅2 next(发送2)
订阅1 next(发送3)
订阅2 next(发送3)
订阅1 next(发送4)
订阅2 next(发送4)
-------
订阅3 next(发送3)
订阅3 next(发送4)
订阅1 completed
订阅2 completed
订阅3 completed
-------
订阅4 next(发送3)
订阅4 next(发送4)
订阅4 completed
```
- `BehaviorRelay ` 
基本同 `BehaviorSubject `功能一样，但是不能主动调用`onCompleted`和`error `，会在`BehaviorRelay `释放前调用
```
let sub = BehaviorRelay(value: "初始值")

sub.subscribe { event in
    print("第一次订阅", event)
}.disposed(by: disposeBag)
sub.accept("新值1")
sub.subscribe { event in
    print("第二次订阅", event)
}.disposed(by: disposeBag)
```









