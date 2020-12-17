---
title: WKWebView 加载 html
categories: [iOS]
tags: [WKWebView]
---
# 本文主要是针对后台返回数据是 html 标签的数据加载
# 异步加载 html 标签内的 img 标签，给 img 标签添加点击事件
---
# 例如返回的数据格式如下
```
<div>
  一、《望天门山》 作者：唐代李白 1、原文
  天门中断楚江开，碧水东流至此回。两岸青山相对出，孤帆一bai片日边来。 2、译文
  天门山从中间断裂是楚江把它冲开，碧水向东浩然奔流到这里折回。
  两岸高耸的青山隔着长江相峙而立，江面上一叶孤舟像从日边驶来。
  <img
    src="https://wx2.sinaimg.cn/large/006CHHsBly1gkxrs7785ej31402eoe84.jpg"
  />
</div>

或者

完整的 html 标签数据
```
 这些数据一般都是使用了富文本编辑器编辑的内容，而且各种标签样式都有可能使用到，所以最好还是使用 WKWebView 来加载！
 但是如果内容含有 img 标签的话就会等待所有的图片加载完才会展示出整体的样式，这样比较影响体验。
 所以应该考虑异步加载图片，而不影响文字等标签样式的展示。


# [Demo下载](https://github.com/xxxIxxxx/XXXWebView)


#### 1.先将图片链接中的 scheme 替换为自定义的 scheme
```
- (void)changeImageScheme {
    self.htmlString = [self.htmlString stringByReplacingOccurrencesOfString:self.oriImageUrl withString:self.xxxCustomImageUrl];
}
```

#### 2.在 html 标签中添加函数
```
- (void)addJsScript {
    
    NSString *htmlLab = @"</html>";
    NSString *scriptLab1 = @"</script>";
    
    NSString *jsFunctionString = @"function xxxGetAllImg() { return document.getElementsByTagName(\"img\"); }\
    function xxxUpdateImage(url, imgData) {  var list = Array.from(xxxGetAllImg()); for (let item of list) {  if ((item.src == url)) { item.src = imgData;   break; } } }        ";

    
    if (![self.htmlString containsString:htmlLab]) {
        [self addHtmlLab];
    }
    
    
    if ([self.htmlString containsString:scriptLab1]) {
     
        NSString *scriptString = [NSString stringWithFormat:@"%@%@",jsFunctionString,scriptLab1];
        self.htmlString = [self.htmlString stringByReplacingOccurrencesOfString:scriptLab1 withString:scriptString];
        
    }else {
        NSString *scriptLab0 = @"<script>";
        NSString *scriptString = [NSString stringWithFormat:@"%@%@%@%@",scriptLab0,jsFunctionString,scriptLab1,htmlLab];
        self.htmlString = [self.htmlString stringByReplacingOccurrencesOfString:htmlLab withString:scriptString];
    }
}

```

#### 3.定义一个实现 WKURLSchemeHandler 协议的类
```
@interface XXXCustomSchemeHanlder : NSObject <WKURLSchemeHandler>

@property (nonatomic, copy) NSString *oriImageUrl;
@property (nonatomic, copy) NSString *oriImageScheme;
@property (nonatomic, strong) UIImage *placeholderImage;
@property (nonatomic, copy) void(^updateImageBlock)(void);

@end

```


#### 4.实现协议方法 用于拦截图片加载
```

- (void)webView:(nonnull WKWebView *)webView startURLSchemeTask:(nonnull id<WKURLSchemeTask>)urlSchemeTask {


    UIImage *image = self.placeholderImage;
    NSData *data = UIImageJPEGRepresentation(image, 1.0);
    NSURLResponse *response = [[NSURLResponse alloc] initWithURL:urlSchemeTask.request.URL MIMEType:@"image/jpeg" expectedContentLength:data.length textEncodingName:nil];
    [urlSchemeTask didReceiveResponse:response];
    [urlSchemeTask didReceiveData:data];
    [urlSchemeTask didFinish];
    
    
    if (self.updateImageBlock) {
        self.updateImageBlock();
    }
    
    NSString *htmlImageUrlStr = [NSString stringWithFormat:@"%@",urlSchemeTask.request.URL];
    NSString *dloadImageUrlStr = [htmlImageUrlStr stringByReplacingOccurrencesOfString:XXXCustomImageScheme withString:self.oriImageScheme];
    
    
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(0.5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
        
        [self readImageForKey:dloadImageUrlStr htmlImageUrlStr:htmlImageUrlStr webView:webView];
    });
}




- (void)readImageForKey:(NSString *)dloadImageUrlStr htmlImageUrlStr:(NSString *)htmlImageUrlStr webView:(WKWebView *)webView {
    
    __weak typeof(self) weakSelf = self;
    NSURL *url = [NSURL URLWithString:dloadImageUrlStr];
    [[SDWebImageManager sharedManager] loadImageWithURL:url options:SDWebImageRetryFailed progress:nil completed:^(UIImage * _Nullable image, NSData * _Nullable data, NSError * _Nullable error, SDImageCacheType cacheType, BOOL finished, NSURL * _Nullable imageURL) {
        if (image || data) {
            NSData *imgData = data;
            if (!imgData) {
                imgData = UIImageJPEGRepresentation(image, 1);
            }
            
            dispatch_async(dispatch_get_main_queue(), ^{
                [weakSelf callJsUpdateImage:webView imageData:imgData htmlImageUrlStr:htmlImageUrlStr];
            });
            
        }
        if (error) {

        }
    }];
}




- (void)callJsUpdateImage:(WKWebView *)webView imageData:(NSData *)imageData htmlImageUrlStr:(NSString *)imageUrlString {
    
    __weak typeof(self) weakSelf = self;
    NSString *imageDataStr = [NSString stringWithFormat:@"data:image/png;base64,%@",[imageData base64EncodedString]];
    NSString *func = [NSString stringWithFormat:@"xxxUpdateImage('%@','%@')",imageUrlString,imageDataStr];
    [webView evaluateJavaScript:func completionHandler:^(id _Nullable response, NSError * _Nullable error) {
        if (weakSelf.updateImageBlock && !error) {
            weakSelf.updateImageBlock();
        }
    }];
    
}

```

#### 5.初始化 WKWebView 并配置拦截信息
```
WKWebViewConfiguration *config = [[WKWebViewConfiguration alloc] init];
XXXCustomSchemeHanlder *schemeHandler = XXXCustomSchemeHanlder.new;

schemeHandler.oriImageScheme = self.oriImageScheme;
schemeHandler.oriImageUrl = self.oriImageUrl;
schemeHandler.placeholderImage = self.placeholderImage;

__weak typeof(self) weakSelf = self;
schemeHandler.updateImageBlock = ^ {
    [weakSelf updateHeight];
};
[config setURLSchemeHandler:schemeHandler forURLScheme:XXXCustomImageScheme];


WKWebView  *webView = [[WKWebView alloc]initWithFrame:CGRectMake(0, 0, self.width, self.height) configuration:config];
```

#### 6. 更新高度
```

- (void)updateHeight {
    [self nowUpdateHeight];
    [self delayUpdateHeight];
}

- (void)nowUpdateHeight {
    
    __weak typeof(self) weakSelf = self;
    [self.webView evaluateJavaScript:@"document.body.offsetHeight" completionHandler:^(id _Nullable result,NSError * _Nullable error) {
        
        // 高度会有一点少 ，手动补上 20
        CGFloat height = [result floatValue] + 20.0;
        weakSelf.webView.height = height;
        weakSelf.height = height;
        if (weakSelf.loadOverHeight) {
            weakSelf.loadOverHeight(height);
        }
    }];
}

- (void)delayUpdateHeight {
    
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, DelayTime * NSEC_PER_SEC), dispatch_get_main_queue(), ^{
        [self nowUpdateHeight];
    });
}
```
# [Demo下载](https://github.com/xxxIxxxx/XXXWebView)
