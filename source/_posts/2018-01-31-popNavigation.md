---
title: UIPopoverPresentationController实现多级跳转
date: 2018-01-31 10:46:54
tags:
---

效果：
---
![效果](http://7xrirn.com1.z0.glb.clouddn.com/blogUIPopoverPresentationController.gif)

<!-- more -->

简单介绍
---
Demo的效果如上图，由于是一个效果展示的Demo其中有一些部分写的比较随意，数据部分是写的一个本地的json文件，需要修改地方根据自身项目修改

**用UIPopoverPresentationController的好处在于，可以根据返回数据层级进行任意层级的处理**

关键代码
---
*此处只有一点比较关键的代码，具体代码看Demo*

```
UIPopoverPresentationController *popController = [navCtrl popoverPresentationController];
 popController.delegate   = self;
 popController.sourceView = self.popButton;

 CGRect btnFrame = self.popButton.frame;

 /// sourceRect的起点是从sourceView左上角
 popController.sourceRect = CGRectMake(0, btnFrame.size.height, btnFrame.size.width, 1);
```

Demo
----
[Demo](http://7xrirn.com1.z0.glb.clouddn.com/blogIRPopNavigationDemo.zip)
