title: 加减控件IRPlusLessView
date: 2016-08-19 10:29:40
tags:
---


**[Demo下载](https://github.com/IrenaChou/IRPlusLessView.git)**
  

效果展示
---
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/plusLess.gif)  

<!-- more -->
使用代码
---
```
#import "IRPlusLessView.h"
  IRPlusLessView *plusLessView =
      [[IRPlusLessView alloc] initWithFrame:CGRectMake(100, 100, 150, 50)];
  _plusLessView = plusLessView;
  plusLessView.maxNum = 3;
  //  plusLessView.colorStyle = [UIColor greenColor];
  [self.view addSubview:plusLessView];
```

*具体代码请下载Demo*