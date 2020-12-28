---
title: Flutter UI 组件 Container、Text
date: 2020-12-28 14:10
categories: [Flutter]
tags: []
sticky:  #9999
---

> Text、Container 组件较为基础同时使用也很频繁，建议自行封装一套使用，避免每次都要输入很多属性。

# Text 文本组件
```
Text(
      '文本组件',
      textAlign: TextAlign.center,
      overflow: TextOverflow.ellipsis,
      maxLines: 2,
      style: TextStyle(
        fontSize: 20,
        color: Colors.orange,
        fontWeight: FontWeight.bold,
        fontStyle: FontStyle.italic,
        decoration: TextDecoration.underline,
        decorationColor: Colors.black,
        decorationStyle: TextDecorationStyle.dotted,
        letterSpacing: 2,
      ),
    )
```
# Container 组件
```
Container(
      child: Text('Container 组件'),
      width: 300,
      height: 300,
      decoration: BoxDecoration(
        color: Colors.redAccent,
        borderRadius: BorderRadius.all(Radius.circular(18)),
        border: Border.all(
          color: Colors.blueAccent,
          width: 7,
        ),
      ),
      //内边距
      padding: EdgeInsets.all(18),
      //外边距
      margin: EdgeInsets.fromLTRB(50, 50, 0, 0),
      // transform: Matrix4.translationValues(100, 0, 0),
      transform: Matrix4.rotationZ(0.1),
      alignment: Alignment.bottomLeft,
    )
```