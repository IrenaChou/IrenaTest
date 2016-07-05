title: 为navigationBar添加阴影
date: 2016-07-05 09:43:20
tags:
---
效果
---
![最终效果](http://7xrirn.com1.z0.glb.clouddn.com/navigationnavigationBarShadow.png)  

<!-- more -->
代码
---
```
 self.navigationController.navigationBar.layer.shadowColor = [UIColor blackColor].CGColor;  //shadowColor阴影颜色
 self.navigationController.navigationBar.layer.shadowOffset = CGSizeMake(2.0f, 2.0f);  // shadowOffset阴影偏移x，y向(上/下)偏移(-/+)2
 self.navigationController.navigationBar.layer.shadowOpacity = 0.3f;  //阴影透明度，默认0
 self.navigationController.navigationBar.layer.shadowRadius = 4.0f;   //阴影半径
```