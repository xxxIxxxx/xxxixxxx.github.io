---
title: Flutter 开发错误 StatefulWidget createState must return a subtype of State
categories: [Flutter]
tags: []
sticky:  #9999
date: 2020-12-01
---

报错如下:

StatefulWidget.createState must return a subtype of State

The createState function for XXXX2 returned a state of type _XXXXState, which is not a subtype of State<XXXX2>, violating the contract for createState.

错误分析：
其实就是返回的 Widget 类型不对，
大意了，修改正确即可。

![错误图](https://upload-images.jianshu.io/upload_images/2331323-a44eecc36a9468ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

