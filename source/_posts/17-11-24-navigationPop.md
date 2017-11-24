---
title: navigationPop效果
date: 2017-11-24 13:07:11
tags:
---

效果：
----

![效果](http://7xrirn.com1.z0.glb.clouddn.com/blogpopNaigationBar.gif)

<!-- more -->

关键代码：
---
```
-(void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];
    [self.navigationController setNavigationBarHidden:YES animated:animated];
}
-(void)viewWillDisappear:(BOOL)animated{
    [super viewWillDisappear:animated];
    [self.navigationController setNavigationBarHidden:NO animated:animated];
}
```
  Demo下载
  ---

  [Demo下载](http://7xrirn.com1.z0.glb.clouddn.com/blogNavigationPushDemo.zip)
