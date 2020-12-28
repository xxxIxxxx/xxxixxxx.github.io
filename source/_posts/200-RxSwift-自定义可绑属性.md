---
title: RxSwift-自定义可绑属性
categories: [Swift]
tags: [RxSwift]
date: 2020-11-14
---
### 对 Reactive 进行扩展
```
// 给 UILabel 增加了 fontSize 可绑属性
extension Reactive where Base: UILabel {
    public var fontSize: Binder<CGFloat> {
        return Binder(base) { lab, size in
            lab.font = UIFont.systemFont(ofSize: size)
        }
    }
}

// 使用
let ob = Observable<Int>.interval(1, scheduler: MainScheduler.asyncInstance)
ob.map { CGFloat($0) + 10.0 }
    .bind(to: lab.rx.fontSize) // 这里要使用 .rx
    .disposed(by: disposeBag)
```
