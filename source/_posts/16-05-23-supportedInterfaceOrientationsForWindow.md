title: iOS 大部分页面竖屏显示，个别页面横屏显示
date: 2016-05-23 15:23:20
tags:
---
**我将横屏显示的controller显示了statusBar将将背景色显示成透明**
**效果如下图**
![效果显示](http://7xrirn.com1.z0.glb.clouddn.com/InterfaceOrientationsForWindow.gif)


**[Demo下载](http://pan.baidu.com/s/1pLhBdmN)**
---

<!-- more -->
**在AppDelegate中添加需要横屏显示的代码**
---
```
/**
 *  横竖屏幕切换
 *  NaviViewController为我设置的根控制器
 *  controller需要横屏显示的控制器
 */
- (UIInterfaceOrientationMask)application:(UIApplication *)application
  supportedInterfaceOrientationsForWindow:(UIWindow *)window {
  __block UIInterfaceOrientationMask mask = 0;
  for (UIWindow *subWindow in [UIApplication sharedApplication].windows) {
    // NaviViewController为我设置的根控制器
    if ([subWindow.rootViewController
            isKindOfClass:NSClassFromString(@"NaviViewController")]) {
      NSArray *arrays = [subWindow.rootViewController childViewControllers];
      [arrays enumerateObjectsUsingBlock:^(
                  UIViewController *obj, NSUInteger idx, BOOL *_Nonnull stop) {
        //需要横屏显示的controller
        if ([obj isKindOfClass:NSClassFromString(@"ViewController11")]) {
          mask = UIInterfaceOrientationMaskAll;
          return;
        } else {
          mask = UIInterfaceOrientationMaskPortrait;
          return;
        }
      }];
    }
  }
  return mask;
}
```

**需要横屏或旋转显示的页面**
---
```
  /**
   *  使用此句代码，会调用delegate里面的supportedInterfaceOrientationsForWindow方法
   *  默认显示numberWithInteger后的类型
   */
  [[UIDevice currentDevice]
      setValue:[NSNumber numberWithInteger:UIDeviceOrientationLandscapeRight]
        forKey:@"orientation"];
```