---
title: iOS 用户可编辑的 Widget
categories: [iOS]
tags: [Widget]
sticky:  #9999
date: 2020-11-27
---

### 本篇是用户可编辑的 Widget
### [用户不可编辑的 Widget，点我去看](https://www.jianshu.com/p/84c180963ac6)
### [编辑屏幕 Widget 不显示，Widget 加载网络图片](https://www.jianshu.com/p/a80d59c94442)
# [Demo 下载](https://github.com/xxxIxxxx/WidgetDemo)


# 先来看效果图
![效果图](https://upload-images.jianshu.io/upload_images/2331323-196fcdf3f96e1360.JPEG?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# 建议将 demo 下载下来对照着看对应 demo 里的 AnimalWidget 文件
### 1. 新建 Widget Extension，勾选 Intent。
![1. 新建 Widget Extension，勾选 Intent](https://upload-images.jianshu.io/upload_images/2331323-4c736e922128a5f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2. 点击 AnimalWidget.intentdefinition 文件 添加可编辑的数据类型 具体操作看图吧

![2. 点击 AnimalWidget.intentdefinition 文件 具体操作看图吧](https://upload-images.jianshu.io/upload_images/2331323-e26dffe1a81d1a99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3. 为第二步新增的数据类型 设置对应的值
![image.png](https://upload-images.jianshu.io/upload_images/2331323-6c898cf25193f0c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4. 编辑 Info.plist (️是 widget extension 的 Info.plist )

```
<key>NSExtension</key>
	<dict>
		<key>IntentsSupported</key>
		<array>
			<string>AnimalWidgetConfigurationIntent</string>
		</array>
		<key>NSExtensionAttributes</key>
		<dict>
			<key>IntentsRestrictedWhileLocked</key>
			<array/>
			<key>IntentsRestrictedWhileProtectedDataUnavailable</key>
			<array/>
			<key>IntentsSupported</key>
			<array>
				<string>AnimalWidgetConfigurationIntent</string>
			</array>
		</dict>
		<key>NSExtensionPointIdentifier</key>
		<string>com.apple.intents-service</string>
		<key>NSExtensionPrincipalClass</key>
		<string>$(PRODUCT_MODULE_NAME).IntentHandler</string>
	</dict>
```
![4. 编辑 Info.plist (️是 widget extension 的 Info.plist )](https://upload-images.jianshu.io/upload_images/2331323-8bb6ff14aab5c9eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5. 创建 IntentHandler.swift 添加一下代码 (可能会报错 找不到 AnimalWidgetConfigurationIntentHandling 、AnimalWidgetConfigurationIntent  先不管先把别的配置好)
```
import Intents

/// 自己创建的文件
class IntentHandler: INExtension, AnimalWidgetConfigurationIntentHandling { // AnimalWidgetConfigurationIntentHandling 是第二步的名字 加上 IntentHandling 后缀
    
    
    /// 配置给用户可选的列表                    AnimalWidgetConfigurationIntent 是第二步的名字 加上 Intent 后缀
    func provideAnimalOptionsCollection(for intent: AnimalWidgetConfigurationIntent, searchTerm: String?, with completion: @escaping (INObjectCollection<Animal>?, Error?) -> Void) {
        
        /// 这里可以去请求网络拿数据
        
        ///搜索词 searchTerm 搜索cat
        if searchTerm == "cat" {
            completion(INObjectCollection(items: [Animal(identifier: "cat", display: "cat")]), nil)
        }
        
        let animals: [Animal] = XXXAnimal.zoo.map { (xxxAnimal) in
            return Animal(identifier: xxxAnimal.id, display: xxxAnimal.name)
        }
        completion(INObjectCollection(items: animals), nil)
        
    }
    
    override func handler(for intent: INIntent) -> Any {
        return self
    }
}

```

### 6. 修改 AnimalWidget.swift 内容
```
如果你的工程已经存在了一个 Widget 将 @main 去掉
使用下面

//我的这部分代码在 XXXWidget.swift
@main
struct AllWidget: WidgetBundle {
    
    @WidgetBundleBuilder
    var body: some Widget {
        XXXWidget()
        AnimalWidget()
    }
}

```
---
#### 修改 TimelineEntry
```

struct SimpleEntry: TimelineEntry {
    let date: Date
    let configuration: ConfigurationIntent
}
--------------原️----新️-----------------
/// 重新命名 去掉 let configuration: ConfigurationIntent  （也可以保留但类型是 AnimalWidgetConfigurationIntent）
///增加自己需要的参数
struct AnimalSimpleEntry: TimelineEntry {
    let date: Date
    /// 新加自己需要的参数
    let animal: XXXAnimal
}

```

---
#### 修改 IntentTimelineProvider  
#### **️ 涉及到 AnimalWidgetConfigurationIntent 可能会报错 先不管 ️**
```

struct Provider: IntentTimelineProvider {
    func placeholder(in context: Context) -> SimpleEntry {
        SimpleEntry(date: Date(), configuration: ConfigurationIntent())
    }

    func getSnapshot(for configuration: ConfigurationIntent, in context: Context, completion: @escaping (SimpleEntry) -> ()) {
        let entry = SimpleEntry(date: Date(), configuration: configuration)
        completion(entry)
    }

    func getTimeline(for configuration: ConfigurationIntent, in context: Context, completion: @escaping (Timeline<Entry>) -> ()) {
        var entries: [SimpleEntry] = []

        // Generate a timeline consisting of five entries an hour apart, starting from the current date.
        let currentDate = Date()
        for hourOffset in 0 ..< 5 {
            let entryDate = Calendar.current.date(byAdding: .hour, value: hourOffset, to: currentDate)!
            let entry = SimpleEntry(date: entryDate, configuration: configuration)
            entries.append(entry)
        }

        let timeline = Timeline(entries: entries, policy: .atEnd)
        completion(timeline)
    }
}

--------------原️----新️-----------------

// 重新命名
struct AnimalProvider: IntentTimelineProvider {
    
// 按照要求增加  Entry 和 Intent
    typealias Entry = AnimalSimpleEntry
    typealias Intent = AnimalWidgetConfigurationIntent
    
    
    func placeholder(in context: Context) -> AnimalSimpleEntry {
        AnimalSimpleEntry(date: Date(), animal: .lion)
    }

    func getSnapshot(for configuration: AnimalWidgetConfigurationIntent, in context: Context, completion: @escaping (AnimalSimpleEntry) -> ()) {
        let entry = AnimalSimpleEntry(date: Date(), animal: .lion)
        completion(entry)
    }

    
    func getTimeline(for configuration: AnimalWidgetConfigurationIntent, in context: Context, completion: @escaping (Timeline<Entry>) -> ()) {
        
        let currentDate = Date()
        
        guard let id = configuration.animal?.identifier, let entryDate = Calendar.current.date(byAdding: .minute, value: 1, to: currentDate) else {
            let timeline = Timeline(entries: [AnimalSimpleEntry(date: currentDate, animal: .lion)], policy: .atEnd)
            completion(timeline)
            return
        }
        
        let entry = AnimalSimpleEntry(date: entryDate, animal: XXXAnimal.animal(id, color: configuration.color))
        
        let timeline = Timeline(entries: [entry], policy: .atEnd)
        completion(timeline)
    }
}

```

## 其他地方对照 demo 修改就可以了
# ️如果有  Cannot find type 'AnimalWidgetConfigurationIntent' in scope 报错 尝试多 build 几次或者 重启 Xcode️
![其他注意](https://upload-images.jianshu.io/upload_images/2331323-194231fd2ac108f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
