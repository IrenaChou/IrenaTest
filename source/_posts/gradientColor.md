title: iOS渐变颜色可设置渐变方向
date: 2016-03-01 10:23:25
tags:
---

[参考原文](http://blog.csdn.net/caryaliu/article/details/49283419)


```
#import <UIKit/UIKit.h>
//渐变方向
typedef NS_ENUM(NSUInteger, GradientType) {
  GradientTypeTopToBottom = 0,      //从上到小
  GradientTypeLeftToRight = 1,      //从左到右
  GradientTypeUpleftToLowright = 2, //左上到右下
  GradientTypeUprightToLowleft = 3, //右上到左下
};
@interface UIImage (GradientColor)
+ (UIImage *)gradientColorImageFromColors:(NSArray *)colors
                             gradientType:(GradientType)gradientType
                                  imgSize:(CGSize)imgSize;
@end
```
<!-- more -->

```
#import "UIImage+GradientColor.h"
@implementation UIImage (GradientColor)
+ (UIImage *)gradientColorImageFromColors:(NSArray *)colors
                             gradientType:(GradientType)gradientType
                                  imgSize:(CGSize)imgSize {
  NSMutableArray *colorsArray = [NSMutableArray array];
  for (UIColor *color in colors) {
    [colorsArray addObject:(id)color.CGColor];
  }
  UIGraphicsBeginImageContextWithOptions(imgSize, YES, 1);
  CGContextRef context = UIGraphicsGetCurrentContext();
  CGContextSaveGState(context);
  CGColorSpaceRef colorSpace =
      CGColorGetColorSpace([[colors lastObject] CGColor]);
  CGGradientRef gradient =
      CGGradientCreateWithColors(colorSpace, (CFArrayRef)colorsArray, NULL);
  CGPoint start;
  CGPoint end;
  switch (gradientType) {
  case GradientTypeTopToBottom:
    start = CGPointMake(0.0, 0.0);
    end = CGPointMake(0.0, imgSize.height);
    break;
  case GradientTypeLeftToRight:
    start = CGPointMake(0.0, 0.0);
    end = CGPointMake(imgSize.width, 0.0);
    break;
  case GradientTypeUpleftToLowright:
    start = CGPointMake(0.0, 0.0);
    end = CGPointMake(imgSize.width, imgSize.height);
    break;
  case GradientTypeUprightToLowleft:
    start = CGPointMake(imgSize.width, 0.0);
    end = CGPointMake(0.0, imgSize.height);
    break;
  default:
    break;
  }
  CGContextDrawLinearGradient(context, gradient, start, end,
                              kCGGradientDrawsBeforeStartLocation |
                                  kCGGradientDrawsAfterEndLocation);
  UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
  CGGradientRelease(gradient);
  CGContextRestoreGState(context);
  CGColorSpaceRelease(colorSpace);
  UIGraphicsEndImageContext();
  return image;
}
@end
```

使用
---
```
  UIColor *topleftColor = [UIColor colorWithHexString:@"4fc2e9"];
  UIColor *bottomrightColor = [UIColor colorWithHexString:@"0379b2"];
  UIImage *bgImg =
      [UIImage gradientColorImageFromColors:@[ topleftColor, bottomrightColor ]
                               gradientType:GradientTypeLeftToRight
                                    imgSize:kScreenSize];
  [UITabBar appearance].barTintColor = [UIColor colorWithPatternImage:bgImg];
```