title: 设置statusBar背景色 
date: 2016-05-13 16:54:21
tags:
---


本文使用iOS9.3

* ![效果显示](http://7xrirn.com1.z0.glb.clouddn.com/statusBarstatusBarColorChange.gif)

*本人写的这个有一个侧滑，开始只在navigationController中将状态栏设置成了light，发现不行，后来将侧滑的控制器也设置成了白色，才可以*

设置statusBar背景颜色
---
```
 [[UINavigationBar appearance] setTintColor:[UIColor whiteColor]];
  UIView *statusBarView =
      [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 20)];
  statusBarView.backgroundColor = [UIColor blackColor];
  [self.view addSubview:statusBarView];
```

<!-- more -->
设置statusBar文字及电池的颜色
---
```
- (UIStatusBarStyle)preferredStatusBarStyle {
  return UIStatusBarStyleLightContent;
}
```