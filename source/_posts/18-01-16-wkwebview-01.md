---
title: WKWebView加载h5调用原生相册相机问题
date: 2018-01-16 16:09:05
tags:
---

需求说明
---
tabbar上面有一个按钮，点击跳转html5页面【这种在第一级页面上笔者选择了modal **presentViewController** 的方式弹出】,
笔者使用WKWebView加载h5


<!-- more -->

问题
---
正常加载是没有问题的，当h5发起调原生的相册【选择相片】、相机，modal出来的h5显示控制器就会被关掉，控制台会打印如下日志
```
Warning: Attempt to present <UIImagePickerController: 0x102112400> on <WebViewController: 0x100ec5840> whose view is not in the window hierarchy!
```
如果h5调起的原生相册选择相片，用户点击取消时，会出现白屏现象

**但是**
自己在modal出来的controller中添加一个按钮，点击按钮去modal一个controller是没问题的

问题分析
---
*忘记了是从哪里看到的问题剖析，还是自己脑子突然开窍了，也是猜测，问题是解决了*

因为h5页面是modal出来的，所以当h5调用原生相机时，先将h5页面dismiss了，所以在去present的时候是找不到WebViewController的，控制台就会报出如下错误

问题解决
---
我的解决方法是改变了h5控制器的打开方式
**一：** 将h5控制器变成rootViewController
**二：** 使用Push的方法打开h5控制器
