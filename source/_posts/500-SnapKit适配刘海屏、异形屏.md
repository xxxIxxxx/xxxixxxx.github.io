---
title: SnapKit适配刘海屏、异形屏
categories: [iOS]
tags: [SnapKit,适配]
sticky:  #9999
date: 2020-11-20
---


### 🌰 适配底部安全距离
在 ViewController 的 view 中使用
```
make.bottom.equalTo(view.snp.bottomMargin)
make.top.equalTo(view.snp.topMargin)
make.left.equalTo(view.snp.leftMargin)
make.right.equalTo(view.snp.rightMargin)
```

如果 view 的 superView 没有适配，那么 view 布局需要通过上面的写法适配
如果 view 的 superView 已经适配，那么 view 布局也会自动适配



### 完整🌰
```
override func viewDidLoad() {
        super.viewDidLoad()
        
        let redView = UIView()
        redView.backgroundColor = .red
        view.addSubview(redView)
        redView.snp.makeConstraints { make in
            
//            make.bottomMargin.equalToSuperview()  //没适配
//            make.bottom.equalToSuperview()    //没适配
            make.bottom.equalTo(view.snp.bottomMargin)    //适配
            
//            make.topMargin.equalToSuperview()   //没适配导航栏高度
//            make.top.equalToSuperview()   //没适配导航栏高度
            make.top.equalTo(view.snp.topMargin)    //适配导航栏高度
            
            
//            make.leftMargin.equalToSuperview()   //没适配
//            make.left.equalToSuperview()   //没适配
                      make.left.equalTo(view.snp.leftMargin)    //适配
            
//            make.rightMargin.equalToSuperview()   //没适配
//            make.right.equalToSuperview()   //没适配
                      make.right.equalTo(view.snp.rightMargin)    //适配
        }
  
/// 如果 redView 已经适配   那么下边的都会适配
/// 如果 redView 没适配   那么只有最后一个会适配
        let blackView = UIView()
        blackView.backgroundColor = .black
        redView.addSubview(blackView)
        blackView.snp.makeConstraints { make in
            make.left.right.equalToSuperview()
            make.height.equalTo(150)
//            make.bottomMargin.equalToSuperview()  //适配
//            make.bottom.equalTo(view.snp.bottomMargin)    //适配
            make.bottom.equalToSuperview()    //没适配
        }
        
    }

```
