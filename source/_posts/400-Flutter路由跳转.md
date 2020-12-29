---
title: Flutter 路由跳转
date: 2020-12-29 10:43
categories: [Flutter]
tags: []
sticky:  #9999
---

# 基本路由跳转  加传值
```
Navigator.of(context).push(MaterialPageRoute(
                builder: (context) => MyRouterPage(title: '首页'),
              ));
```

# 返回
```
Navigator.of(context).pop();
```