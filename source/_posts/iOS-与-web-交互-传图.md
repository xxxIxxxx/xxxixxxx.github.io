---
title: iOS 与 web 交互传图
categories: [iOS]
tags: 
---
web 端将图片 base64 编码后传给 iOS 端，会在 base64 编码前加上 `data:image/png;base64,` 需要先把这一串给去掉后进行解码，然后转 data 再转为 image 
