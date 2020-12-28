---
title: Flutter 组件 Image
date: 2020-12-28 14:20 
categories: [Flutter]
tags: []
sticky:  #9999
---
# Image 本地图片
```
Image(
        image: Assets.images.cat,
      )
```

# Image.network 显示网络图片 
```
Image.network(
      '图片url',
      //充满不变形
      fit: BoxFit.cover,
      alignment: Alignment.center,
      color: Colors.blueGrey,
      colorBlendMode: BlendMode.difference,
    )
```

# 结合 ClipOval 组件 展示圆图
```
ClipOval(
      clipBehavior: Clip.antiAliasWithSaveLayer,
      child: Image.network(
        imageUrl,
        // width: 200,
        // height: 200,ß
        fit: BoxFit.cover,
      ),
    );
```

# Container BoxDecoration 属性生成 圆图
```
Container(
      // child: networkImage,
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(150),
        image: DecorationImage(
          image: NetworkImage(imageUrl),
          fit: BoxFit.cover,
        ),
      ),
      width: 300,
      height: 300,
    );
```