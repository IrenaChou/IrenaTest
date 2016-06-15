title: iOS在程序中控制系统的屏幕亮度 
date: 2016-03-01 09:51:51
tags:
---

[参考原文](http://blog.sina.com.cn/s/blog_9693f61a0102uymd.html)

```
// 0 .. 1.0, where 1.0 is maximum brightness. Only supported by main screen.
@property(nonatomic) CGFloat brightness NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;        
```

```
 //获取系统屏幕当前的亮度值
 CGFloat value = [UIScreen mainScreen].brightness;
 //设置系统屏幕亮度值
 value += 0.8;
 [[UIScreen mainScreen] setBrightness:value];
```

