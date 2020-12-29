---
title: Flutter 组件 Row、Column、Expanded
date: 2020-12-29 10:20
categories: [Flutter]
tags: []
sticky:  #9999
---

# Row
> 水平布局
```
ow(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          MyIconWidget(Icons.tv, color: Colors.redAccent),
          MyIconWidget(Icons.ac_unit, color: Colors.blueAccent),
          MyIconWidget(Icons.access_alarms, color: Colors.orangeAccent)
        ],
      ),
```
# Column
> 垂直布局
```
Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: [
          MyIconWidget(Icons.tv, color: Colors.redAccent),
          MyIconWidget(Icons.ac_unit, color: Colors.blueAccent),
          MyIconWidget(Icons.access_alarms, color: Colors.orangeAccent)
        ],
      ),
```
# Expanded
> 扩展组件 比例分配
```
Expanded(
          child: MyIconWidget(Icons.games, color: Colors.blueGrey),
        ),



 Row(
      children: [
        Expanded(
          flex: 2,
          child: MyIconWidget(Icons.ac_unit, color: Colors.red),
        ),
        Expanded(
          flex: 1,
          child: MyIconWidget(Icons.ac_unit, color: Colors.amberAccent),
        ),
        Expanded(
          flex: 2,
          child: MyIconWidget(Icons.ac_unit, color: Colors.red),
        ),
      ],
    );
```