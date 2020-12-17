---
title: 在Swift中使用 NSClassFromString
categories: [Swift]
tags: 
---
在Swift中使用 NSClassFromString

需要 `工程名` + ` .`  +  `string`

```
NSClassFromString(Bundle.main.object(forInfoDictionaryKey: "CFBundleName")! + "." + "CustomCell")
```

### 每次写这些很麻烦,所以简单封装下
```
public func GetClassFromString(_ classString: String) -> AnyClass? {
    
    guard let bundleName: String = Bundle.main.object(forInfoDictionaryKey: "CFBundleName") as? String else {
        return nil
    }
        
    var anyClass: AnyClass? = NSClassFromString(bundleName + "." + classString)
    if (anyClass == nil) {
        anyClass = NSClassFromString(classString)
    }
    return anyClass
}
```

### 以后就可以直接调用

```
GetClassFromString("cellName")
```
