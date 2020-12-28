---
title: Swift 协议与扩展
categories: [Swift]
tags: [Protocol,Extension]
date: 2020-12-25 17:15
---

# 协议 Protocol 

## 使用 Protocol 关键字创建一个协议
> 让遵守该协议的 class 与 struct 实现约定一些方法与属性。
```
protocol PageNumberProtocol {
    /// 添加的实例属性
    var pageNumber: Int { get set }
    /// 添加的实例方法
    func add()

    /// 添加的类属性
    static var name: String? { get set }
    /// 添加的类方法
    static func logName()
}
```

## 遵守协议
```
struct Person: PageNumberProtocol {
    var pageNumber: Int

    func add() {}

    static var name: String?

    static func logName() {}
}

class Car: PageNumberProtocol {
    var pageNumber: Int = 0

    func add() {}

    static var name: String?

    static func logName() {}
}
```

# 扩展 extension
## 扩展使用的很多应该都很熟悉
> 分散代码实现
```
extension Car {
    func dididi() {
        print("滴滴滴")
    }
}

```
## 使用
```
Car().dididi()
```

# Protocl + Extension 
> 给出协议并实现协议，这样遵守协议的 class 和 struct 就能直接使用协议方法。

## runtime 添加属性
```
func getAssociatedObject<T>(_ object: Any, _ key: UnsafeRawPointer) -> T? {
    return objc_getAssociatedObject(object, key) as? T
}

func setRetainedAssociatedObject<T>(_ object: Any, _ key: UnsafeRawPointer, _ value: T) {
    objc_setAssociatedObject(object, key, value, .OBJC_ASSOCIATION_RETAIN_NONATOMIC)
}
```

## 协议
```

protocol PageNumberProtocol {
    /// 添加的实例属性
    var pageNumber: Int { get set }
    /// 添加的实例方法
    func add()

    /// 添加的类属性
    static var name: String? { get set }
    /// 添加的类方法
    static func logName()
}
```

## 扩展遵守协议
```

private var pageNumberKey: Void?

private var nameKey: Void?

extension UIViewController: PageNumberProtocol {
    static func logName() {
        debugPrint(name ?? "无名")
    }

    static var name: String? {
        get {
            getAssociatedObject(self, &nameKey)
        }
        set {
            setRetainedAssociatedObject(self, &nameKey, newValue)
        }
    }

    func add() {
        pageNumber += 1
    }

    var pageNumber: Int {
        get {
            getAssociatedObject(self, &pageNumberKey) ?? 0
        }
        set {
            setRetainedAssociatedObject(self, &pageNumberKey, newValue)
        }
    }
}

```
这样所有遵守 PageNumberProtocol 协议的 UIViewController 就都有了协议要求的属性与方法且已经实现了。