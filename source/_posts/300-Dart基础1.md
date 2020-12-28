---
title: Dart 基础之 类、set、get、构造函数、方法
date: 2020-12-27 11:30
categories: [Dart]
tags: []
sticky:  #9999
---



# 类、属性、方法
```
class Person {
  String name;
  int age;
  getInfo() {
    print('名字:$name 年龄:$age');
  }
}
```
# 默认构造函数、初始化列表
> 存在初始化列表就不能存在默认构造函数
```
class Person {
  //默认构造函数 简写
  Person(this.name, this.age);

  //默认构造函数 全写
  Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

// 初始化列表
  Person()
      : name = '李华',
        age = 22 {
    print(this.name);
  }
}

```

# 匿名构造函数
```
class Person {
  Person.newPeople() {
    name = "李四";
    age = 33;
  }
// 带参数匿名构造函数
  Person.new2(String name, int age) {
    this.name = name;
    this.age = age;
  }
}
```

# 私有属性、私有方法、set方法、get方法
> 私有属性、私有方法  这个类必须单独在一个文件
```
class Person {
  var _money = 999999;

//MARK:set 方法
  set gongzi(int value) {
    _money = _money + value;
    _printMoney();
  }

//MARK:get方法
  int get money {
    return _money;
  }

//MARK:   私有方法 这个类必须单独在一个文件
  _printMoney() {
    print(money);
  }
}
  
```