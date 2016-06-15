title: 设置navigationBar背景透明
date: 2016-05-20 19:40:36
tags:
---
**效果如下图红色窗体**  
* ![效果显示](http://7xrirn.com1.z0.glb.clouddn.com/navigationNavigationBarBackgroundShow.gif)  




**我将此方法放在了一个Category里面，下载请点击此链接[下载代码](http://pan.baidu.com/s/1o8u4u0a)**
---



设置NavigationBar背景为透明
---
```
  /**
   *  将navigationBar背景颜色设置为透明
   */
  [self setNavigationBarBackgroundShow:NO];
```
<!-- more -->
设置NavigationBar背景恢复不透明
---
```
 /**
   *  将navigationBar显示背景颜色
   */
  [self setNavigationBarBackgroundShow:YES];
```

方法实现
---
```
/**
 *  状态栏是否显示背景色
 *
 *  @param show yes为显示背景色，否则为透明
 */
- (void)setNavigationBarBackgroundShow:(BOOL)show {
  // 设置为半透明
  self.navigationController.navigationBar.translucent = !show;
  UIColor *color = nil;
  if (show) {
    color = [UIColor whiteColor];
  } else {
    color = [UIColor clearColor];
  }
  CGRect rect = CGRectMake(0, 0, [UIScreen mainScreen].bounds.size.height, 64);
  UIGraphicsBeginImageContext(rect.size);
  CGContextRef context = UIGraphicsGetCurrentContext();
  CGContextSetFillColorWithColor(context, [color CGColor]);
  CGContextFillRect(context, rect);
  UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
  UIGraphicsEndImageContext();
  [self.navigationController.navigationBar
      setBackgroundImage:image
           forBarMetrics:UIBarMetricsDefault];
  self.navigationController.navigationBar.clipsToBounds = !show;
}
```

*我在做这个的时候遇到过一个问题，navigationBar透明之后当前控制器的高不够，显示出的是其它控制器*
**解决：我将当前控制器的高调整成了屏幕的高**