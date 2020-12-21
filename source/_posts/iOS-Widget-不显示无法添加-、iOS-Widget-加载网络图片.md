---
title: iOS Widget 不显示无法添加、iOS Widget 加载网络图片
categories: [iOS]
tags: [Widget,iOS小组件]
sticky:  #9999
date: 2020-12-07
---


### [Intent Widget 开发](https://www.jianshu.com/p/029c85bdf16b)
### [Static Widget 开发](https://www.jianshu.com/p/84c180963ac6)

### [Demo下载](https://github.com/xxxIxxxx/WidgetDemo)

# Widget 在添加时找不到
 出现这种情况，可能是只配置了可编辑的 `Widget`。
导致`NSExtensionPointIdentifier`只有这一种类型 `com.apple.intents-service` 会被识别为 Siri 扩展。
### 解决方法
再添加一个不可编辑的 `Widget` 即可。不需要展示出，在 `@main`方法里不添加就好。
确定新添加的`NSExtensionPointIdentifier`类型为 `com.apple.widgetkit-extension` 。

![plist](https://upload-images.jianshu.io/upload_images/2331323-7fe44d27ed6af214.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
# Widget 是不能做动画也不能异步刷新的，所以图片加载必须同步
```

/// 同步下载图片，Widget 不能异步刷新

funcgetImage(_imgUrlString:String) ->UIImage? {

 guardletdata =try?Data(contentsOf:URL(string: imgUrlString)!)else{

        print("图片下载失败")

 returnnil}

    print("图片下载成功")

 returnUIImage(data: data)

}

//使用

Image(uiImage:getImage(entry.imageUrlStr) ??UIImage(named:"aaaa")!)

                        .resizable()

                        .frame(width:60,

                               height:60,

                               alignment: .center)

```
