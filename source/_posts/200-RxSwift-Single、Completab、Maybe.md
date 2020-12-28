---
title: RxSwift-Single、Completab、Maybe
categories: [Swift]
tags: [RxSwift]
date: 2020-11-22
---
# Single
只发出一次事件，常用于网络请求
```
enum DataError: Error {
    case error1
}

func getData() -> Single<[String: Any]> {
    return Single<[String: Any]>.create { (single) -> Disposable in
        single(.success(["": 1]))
//                single(.error(DataError.error1))
        return Disposables.create {}
    }
}

getData().subscribe { req in
    switch req {
    case .success(let value):
        print(value)
    case .error(let error):
        print(error)
    }
}.disposed(by: disposeBag)
```

# Completable
只会发出`completed`或`error` 事件，用于只关心操作结果
```
func cancel() -> Completable {
    return Completable.create { (comp) -> Disposable in
        comp(.completed)
//                comp(.error(ObError.error1))
        return Disposables.create {}
    }
}

cancel().subscribe { rep in
    switch rep {
    case .completed:
        print("成功")
    case let .error(error):
        print(error)
    }
}.disposed(by: disposeBag)
```

# Maybe
也是只能发出一个事件，正常的`event`或`completed `或`error`
```

func test() -> Maybe<String> {
    return Maybe<String>.create { (mayBe) -> Disposable in
        mayBe(.success("成功"))
//                mayBe(.completed)
//                mayBe(.error(ObError.error1))
        return Disposables.create {}
    }
}

test().subscribe { event in
    switch event {
    case .success(let value):
        print(value)
    case .completed:
        print("completed")
    case .error(let error):
        print(error)
    }
}.disposed(by: disposeBag)
```
