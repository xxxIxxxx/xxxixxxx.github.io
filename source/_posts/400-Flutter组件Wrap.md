---
title: Flutter 组件 Wrap
date: 2020-12-29 10:35
categories: [Flutter]
tags: []
sticky:  #9999
---

# Wrap
> 流式布局
```
Wrap(
      spacing: 10,
      runSpacing: 10,
      alignment: WrapAlignment.end,
      children: [
        MyButton('哈哈哈'),
        MyButton('阿斯顿萨达撒'),
        MyButton('苏打水萨达撒'),
        MyButton('阿瑟'),
        MyButton('萨发送个人舒服舒服当发送的'),
        MyButton('title'),
        //MARK:       MaterialButton
        MaterialButton(
          child: Text('MaterialButton 风格 btn'),
          shape: CircleBorder(side: BorderSide(width: 100)),
          color: Colors.orange,
          onPressed: () {
            print('object');
          },
        ),
        //MARK:IconButton
        IconButton(icon: Icon(Icons.ac_unit), onPressed: null),
        //MARK: FlatButton
        FlatButton(onPressed: () {}, child: Text('扁平化按钮')),
        FloatingActionButton(
          onPressed: () {},
          child: Text('FloatingActionButton'),
        )
      ],
    );
```
