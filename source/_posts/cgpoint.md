title: CGPoint
date: 2016-04-12 18:06:06
tags:
---

CGPoint表示一个二维坐标系中的点
CGPoint通过x和y坐标定义，可使用CGPointMake(x，y)创建点。

    可以将它们与字符串进行相互转换，可用如下函数：NSStringFromCGPoint()、CGPointFromString().
    主要说CGPointFromString方法

下面是CGPoint的定义
```
/* Points. */
struct CGPoint {
    CGFloat x;
    CGFloat y;
};
typedef struct CGPoint CGPoint;
```

stringWithFormat从String转换为point的方法中，所需的string格式是**{x,y}**,下面是例子
```
  NSString *str = @"0.111, 1.22";
  str = [NSString stringWithFormat:@"{%@}", str];
  CGPoint initPath = CGPointFromString(str);
  NSLog(@"%@", NSStringFromCGPoint(initPath));
```
