---
title: Flutter 组件 ListView
date: 2020-12-28 14:35
categories: [Flutter]
tags: []
sticky:  #9999
---

# ListView

```
ListView(
      padding: EdgeInsets.fromLTRB(18, 20, 18, 50),
      // 滑动方向
      scrollDirection: Axis.horizontal,
      children: [
        ListTile(
          leading: Icon(
            Icons.tv,
            color: Colors.amberAccent,
          ),
          trailing: Icon(Icons.ac_unit),
          title: Text('标题'),
          subtitle: Text('二级标题啦啦啦啦啦'),
        ),
      ],
    )
```

# ListView.builder

```
List<Widget> _getData() {
    List<Widget> widgetList = List();
    for (var i = 0; i < 30; i++) {
      widgetList.add(Text(
        '$i 哈哈哈哈哈',
        style: TextStyle(fontSize: 30),
      ));
    }

    return widgetList;
  }


  ListView.builder(
      itemCount: _getData().length,
      itemBuilder: (BuildContext context, int index) {
        return _getData()[index];
      },
    );


```