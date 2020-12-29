---
title: Flutter 组件 Stack、Align、Positioned
date: 2020-12-29 10:25
categories: [Flutter]
tags: []
sticky:  #9999
---

# Stack
```
Stack(
      // alignment: Alignment(-1,-1),
      alignment: Alignment.bottomLeft,
      children: [
        Container(color: Colors.orange, height: 100),
        Text('单独 Stack 布局只有两个组件',
            style: TextStyle(color: Colors.white, fontSize: 20)),
      ],
    );
```

# Stack 结合 Align 布局
```
Stack(
        children: [
          Align(
            alignment: Alignment.center,
            child: Text(
              'Stack 结合 Align 布局',
              style: TextStyle(color: Colors.white, fontSize: 30),
            ),
          ),
          Align(
            alignment: Alignment.topLeft,
            child: Icon(Icons.ac_unit),
          ),
          Align(
            alignment: Alignment.bottomLeft,
            child: Icon(Icons.ac_unit),
          ),
        ],
      ),
```

# Stack 结合 Positioned 布局

```
Stack(
        children: [
          Positioned(
              top: 16,
              left: 16,
              child: Text(
                ' Stack 结合 Positioned 布局',
                style: TextStyle(color: Colors.white, fontSize: 30),
              )),
          Positioned(
              bottom: 10,
              right: 10,
              width: 100,
              height: 100,
              child: Container(
                color: Colors.red,
                child: Icon(Icons.tv),
              ))
        ],
      ),

```