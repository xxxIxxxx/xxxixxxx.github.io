---
title: iOS 修改状态栏的颜色 preferredStatusBarStyle
categories: [iOS]
tags: [UI]
---
### ⚠️⚠️⚠️首先要在项目的 Info.plist 文件里设置 View controller-based status bar appearance 为 YES，如果没有就不用添加⚠️ ⚠️⚠️
```
/*
1. 重写 UINavigationController 的 childViewControllerForStatusBarStyle
可以写在基类的 UINavigationController 中，也可以使用Category
*/
- (UIViewController *)childViewControllerForStatusBarStyle {
    return self.topViewController;
}

///Swift 
override var childForStatusBarStyle: UIViewController? {
        return topViewController
}

/*
2.  在需要改变状态栏颜色的 UIViewController 中实现 preferredStatusBarStyle
*/
- (UIStatusBarStyle)preferredStatusBarStyle {
   return UIStatusBarStyleLightContent;
   // return UIStatusBarStyleDefault;
}

///Swift
override var preferredStatusBarStyle: UIStatusBarStyle {
      return .lightContent
}

/*
3. 当触发某个条件需要改变状态栏颜色时在 UIViewController 中调用
然后在 - (UIStatusBarStyle)preferredStatusBarStyle; 中判断你的条件是否满足改变颜色
*/
[self setNeedsStatusBarAppearanceUpdate];

///Swift
setNeedsStatusBarAppearanceUpdate()

```

iOS修改状态栏颜色 
OC 修改状态栏颜色 
Swift修改状态栏颜色
