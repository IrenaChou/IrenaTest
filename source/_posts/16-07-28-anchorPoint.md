title: anchorPoint锚点
date: 2016-07-28 16:22:44
tags:
---
anchorpoint（锚点）**默认值是(0.5,0.5)**

与CGAffineTransform连用，通过**anchorpoint**改变旋转点

      view.layer.anchorPoint = CGPointMake(0.5, 1);
    
![图片说明](http://7xrirn.com1.z0.glb.clouddn.com/anchorPoint.png)  

**anchorPoint必须在frame前设置，否则会影响frame的位置而来，【frame是根据center,anchorPoint,bounds等值计算而来】**  

<!-- more -->
通过查看API发现,在像CGAffineTransformRotate，CGAffineTransform..的函数最后都会调用CGAffineTransform函数；

通过如下方法，我们使用CGAffineTransform函数实现一个旋转  
  
![图片说明](http://7xrirn.com1.z0.glb.clouddn.com/CGAffineTransform.png)  

```
/**
   *  通过CGAffineTransform  api算旋转45度
   */
  CGFloat radians = M_PI_4;
  CGFloat a = cosf(radians);
  CGFloat b = sinf(radians);
  CGFloat c = -cosf(radians);
  CGFloat d = cosf(radians);
  //    旋转45度
  self.blueView.transform = CGAffineTransformMake(a, b, c, d, 0, 0);
```


