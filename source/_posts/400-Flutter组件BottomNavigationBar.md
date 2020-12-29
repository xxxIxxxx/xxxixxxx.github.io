---
title: Flutter 组件 BottomNavigationBar
date: 2020-12-29 10:41
categories: [Flutter]
tags: []
sticky:  #9999
---

```
  int index = 0;
  var pages = [HomePage(), SearchPage(), SetPage()];
  var titls = [Text('首页'), Text('搜索'), Text('设置')];
```


# BottomNavigationBar

```

BottomNavigationBar(
        selectedItemColor: Colors.orangeAccent,
        iconSize: 34,
        // type: BottomNavigationBarType.shifting,
        unselectedItemColor: Colors.grey,
        // showSelectedLabels: false,
        // showUnselectedLabels: false,
        currentIndex: index,
        onTap: (index) {
          setState(() {
            this.index = index;
          });
        },
        items: [
          BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: '首页',
              activeIcon: Icon(
                Icons.home,
                color: Colors.orangeAccent,
              )),
          BottomNavigationBarItem(
              icon: Icon(Icons.search),
              label: '搜索',
              activeIcon: Icon(
                Icons.search,
                color: Colors.orangeAccent,
              )),
          BottomNavigationBarItem(
              icon: Icon(Icons.settings),
              label: '设置',
              activeIcon: Icon(
                Icons.settings,
                color: Colors.orangeAccent,
              )),
        ],
      ),
```