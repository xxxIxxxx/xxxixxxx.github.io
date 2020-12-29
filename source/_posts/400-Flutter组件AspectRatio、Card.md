---
title: Flutter 组件 AspectRatio、Card
date: 2020-12-29 10:30
categories: [Flutter]
tags: []
sticky:  #9999
---


# AspectRatio
> 设置自身比例
```
AspectRatio(
        aspectRatio: 5.0 / 1.0,
        child: Container(
          child: Text(
            'AspectRatio 宽高比 5/1',
            textAlign: TextAlign.center,
            style: TextStyle(fontSize: 30),
          ),
          color: Colors.greenAccent,
        ),
      ),
```

# Card
> 卡片样式
```
Card(
      margin: EdgeInsets.all(10),
      shape: RoundedRectangleBorder(
          side: BorderSide(color: Colors.orange, width: 2),
          borderRadius: BorderRadius.circular(10)),
      child: Column(
        children: [
          AspectRatio(
            aspectRatio: 16 / 9,
            child: Image.network(
              randomImgSrc(),
              fit: BoxFit.cover,
            ),
          ),
          Padding(
            padding: EdgeInsets.all(12),
            child: Row(
              crossAxisAlignment: CrossAxisAlignment.baseline,
              children: [
                ClipOval(
                  child: Image.network(randomImgSrc(),
                      width: 60, fit: BoxFit.cover),
                ),
                Container(
                  padding: EdgeInsets.fromLTRB(10, 0, 0, 0),
                  height: 60,
                  child: Stack(
                    children: [
                      Align(
                        alignment: Alignment.topLeft,
                        child: Text(
                          '我是一只大猫',
                          style: TextStyle(
                              fontWeight: FontWeight.bold, fontSize: 22),
                        ),
                      ),
                      Align(
                        alignment: Alignment.bottomLeft,
                        child: Text('啦啦啦啦啦啦啦啦啦啦啦啦啦啦啦'),
                      )
                    ],
                  ),
                ),
                CircleAvatar(
                  backgroundImage: NetworkImage(randomImgSrc()),
                ),
              ],
            ),
          ),
        ],
      ),
    );
``