---
title: iOS mask 遮罩，彩色文本
categories: [iOS]
date: 2020-11-20
---
# iOS渐变彩色文字、iOS mask 遮罩


![效果图](https://upload-images.jianshu.io/upload_images/2331323-2f3e46c5908444fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
[使用到了YYCategories](https://github.com/ibireme/YYCategories)


### 彩色文字

```
UIView *colorBgView = [UIView new];
    [self.view addSubview:colorBgView];
    colorBgView.frame = CGRectMake(0, 300, UIScreen.mainScreen.bounds.size.width, 40);
        
//这里用了YYCategories
    UIBezierPath *colorTextPath = [UIBezierPath bezierPathWithText:@"哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈" font:[UIFont systemFontOfSize:28]];
    CAShapeLayer *colorTextLayer = [CAShapeLayer layer];
    colorTextLayer.path = colorTextPath.CGPath;
    colorTextLayer.frame = CGRectMake(0, 0, UIScreen.mainScreen.bounds.size.width, 30);
    colorBgView.layer.mask = colorTextLayer;
    
    CAGradientLayer *colorLayer = CAGradientLayer.new;
    colorLayer.colors = @[(__bridge id)UIColor.redColor.CGColor,
                          (__bridge id)UIColor.orangeColor.CGColor,
                          (__bridge id)UIColor.greenColor.CGColor,
                          (__bridge id)UIColor.blueColor.CGColor,
                          (__bridge id)UIColor.yellowColor.CGColor,
                          (__bridge id)UIColor.purpleColor.CGColor,
                          (__bridge id)UIColor.blackColor.CGColor,];
    colorLayer.startPoint = CGPointMake(0, 0.5);
    colorLayer.endPoint = CGPointMake(1, 0.5);
    colorLayer.frame = CGRectMake(0, 0, UIScreen.mainScreen.bounds.size.width, 40);
    [colorBgView.layer addSublayer:colorLayer];

```

### 过渡遮罩
```

 ///黑色背景view
    UIView *indicatorView = [UIView new];
    [self.view addSubview:indicatorView];
    indicatorView.backgroundColor = UIColor.blackColor;
    indicatorView.layer.cornerRadius = 20;
    indicatorView.layer.masksToBounds = YES;
    indicatorView.frame = CGRectMake(0, 195, 100, 40);
    self.indicatorView = indicatorView;
    
  //这里用了YYCategories
    UIBezierPath *textPath = [UIBezierPath bezierPathWithText:@"哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈" font:[UIFont systemFontOfSize:28]];
    CAShapeLayer *textLayer = [CAShapeLayer layer];
    textLayer.path = textPath.CGPath;
    textLayer.frame = CGRectMake(0, 0, UIScreen.mainScreen.bounds.size.width, 30);
    
    
    UIView *darkView = [UIView new];
    [self.view addSubview:darkView];
    darkView.backgroundColor = UIColor.darkGrayColor;
    darkView.frame = CGRectMake(0, 200, UIScreen.mainScreen.bounds.size.width, 30);
    darkView.layer.mask = textLayer;
    
    
    UIView *whiteView = [UIView new];
    [darkView addSubview:whiteView];
    whiteView.backgroundColor = UIColor.whiteColor;
    whiteView.layer.cornerRadius = 20;
    whiteView.layer.masksToBounds = YES;
    whiteView.frame = CGRectMake(0, -5, 100, 40);
    self.whiteView = whiteView;
    
    //也可以使用layer
//    CALayer *darkLayer = CALayer.new;
//    [self.view.layer addSublayer:darkLayer];
//    darkLayer.backgroundColor = UIColor.darkGrayColor.CGColor;
//    darkLayer.frame = CGRectMake(0, 200, UIScreen.mainScreen.bounds.size.width, 30);
//    darkLayer.mask = textLayer;
//
//    CAShapeLayer *whiteLayer = CAShapeLayer.new;
//    [darkLayer addSublayer:whiteLayer];
//    whiteLayer.backgroundColor = UIColor.whiteColor.CGColor;
//    whiteLayer.fillColor = UIColor.whiteColor.CGColor;
//    whiteLayer.strokeColor = UIColor.whiteColor.CGColor;
//    whiteLayer.borderColor = UIColor.whiteColor.CGColor;
//    whiteLayer.cornerRadius = 20;
//    whiteLayer.masksToBounds = YES;
//    whiteLayer.frame = CGRectMake(0, -5, 100, 40);
//    self.whiteLayer = whiteLayer;
    
    UISlider *slider = UISlider.new;
    [self.view addSubview:slider];
    [slider addTarget:self action:@selector(changeFrame:) forControlEvents:UIControlEventValueChanged];
    slider.frame = CGRectMake(0, 260, UIScreen.mainScreen.bounds.size.width, 30);
    
    
----------

- (void)changeFrame:(UISlider *)slider {
 
    CGFloat x = UIScreen.mainScreen.bounds.size.width *slider.value;
    self.indicatorView.frame = CGRectMake(x, 195, 100, 40);
    self.whiteView.frame = CGRectMake(x, -5, 100, 40);
    self.whiteLayer.frame = CGRectMake(x, -5, 100, 40);
    
}

```
