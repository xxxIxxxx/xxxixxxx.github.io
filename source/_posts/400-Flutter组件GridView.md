---
title: Flutter 组件 GridView
date: 2020-12-29 10:11
categories: [Flutter]
tags: []
sticky:  #9999
---

```

 List<Widget> _getData() {
    var widgetList = List<Widget>();
    for (var i = 0; i < 30; i++) {
      var c = Container(
        // alignment: Alignment.topCenter,
        color: Colors.green[100],
        child: Column(
          children: [
            Image(image: Assets.images.cat),
            SizedBox(
              height: 12,
            ),
            Text(
              '哈哈哈 $i',
              textAlign: TextAlign.center,
              style: TextStyle(fontSize: 24),
            ),
          ],
        ),
      );
      widgetList.add(c);
    }
    return widgetList;
  }
```

# GridView.count
```
GridView.count(
      scrollDirection: Axis.vertical,
      padding: EdgeInsets.fromLTRB(16, 20, 16, 20),
      crossAxisCount: 2,
      crossAxisSpacing: 8,
      mainAxisSpacing: 10,
      childAspectRatio: 0.8,
      children: this._getData(),
    );
```

# GridView.builder
```
GridView.builder(
      padding: EdgeInsets.all(10),
      itemCount: _getData().length,
      itemBuilder: (context, index) {
        return _getData()[index];
      },
      gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
        crossAxisCount: 2,
        childAspectRatio: 0.8,
        mainAxisSpacing: 10,
        crossAxisSpacing: 10,
      ),
    );
```