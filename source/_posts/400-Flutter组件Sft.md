---
title: Flutter 组件 StatefulWidget
date: 2020-12-29 10:37
categories: [Flutter]
tags: []
sticky:  #9999
---
# StatefulWidget
> 动态组件，页面可变化 使用  setState(() {});
            
```
class MyStfWidget extends StatefulWidget implements PageRouterProtocol {
  @override
  final Map arguments;
  MyStfWidget({Key key, this.arguments}) : super(key: key);

  @override
  _MyStfWidgetState createState() => _MyStfWidgetState(arguments);
}

class _MyStfWidgetState extends State<MyStfWidget> {
  final Map arguments;

  List dataList = [];

  _MyStfWidgetState(this.arguments);
  addData() {
    List singleList = List();
    for (var i = 0; i < 20; i++) {
      singleList.add('增加数据了');
    }

    this.dataList.addAll(singleList);
  }

  @override
  Widget build(BuildContext context) {
    RaisedButton addBtn = RaisedButton(
        child: Text('加载更多'),
        onPressed: () {
          setState(() {
            this.addData();
          });
        });

    return Scaffold(
      appBar: AppBar(
        title: Text(arguments['title'] ?? '默认标题'),
      ),
      body: ListView.builder(
        itemCount: dataList.length + 1,
        itemBuilder: (BuildContext context, int index) {
          if (index == 0) {
            return addBtn;
          }

          return Text('data  $index');
        },
      ),
    );
  }
}

```