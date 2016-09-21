title: scrollView添加子控件向下偏移automaticallyAdjustsScrollViewInsets
date: 2016-07-05 10:36:07
tags:
---

**self.automaticallyAdjustsScrollViewInsets = NO;**
此属性默认为YES，**UIViewController下如果只有一个UIScollView或者其子类**，那么会自动留出空白，让scollview滚动不会被各种bar盖住。**但是每个UIViewController只能有唯一一个UIScollView或者其子类，如果超过一个，需要将此属性设置为NO**,自己去控制留白以及坐标问题。

**我将scrollView的坐标避开各种bar，就会看到automaticallyAdjustsScrollViewInsets属性的效果**
![结构图](http://7xrirn.com1.z0.glb.clouddn.com/scrollViewstructure.png)  
<!-- more -->
![效果图](http://7xrirn.com1.z0.glb.clouddn.com/scrollVieweffect.gif)  
**通过如上两张图片已经很能说明automaticallyAdjustsScrollViewInsets = YES时的效果了**

*如果将scrollView的frame设置和屏幕大小相同，就不会出现我模拟的问题*
解决如上留白效果：
  1.  将scrollView的frame设置与主屏幕frame相同
  2.  将self.automaticallyAdjustsScrollViewInsets = YES;



关键代码
---
1.代码如下
```
#define kScreenWidth [UIScreen mainScreen].bounds.size.width
#define kScreenHeight [UIScreen mainScreen].bounds.size.height
  UIScrollView *scrollHomeView = [[UIScrollView alloc]
      initWithFrame:CGRectMake(0, 0, kScreenWidth, kScreenHeight)];
```

2.代码如下
```
self.edgesForExtendedLayout = UIRectEdgeNone;
self.automaticallyAdjustsScrollViewInsets = YES ; // 其中的self是控制器
```