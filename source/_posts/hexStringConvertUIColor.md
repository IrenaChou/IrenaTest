title: 十六进制颜色转换成UIColor 
date: 2016-02-24 13:41:53
tags:
---

[原文出自](http://wonderzl.iteye.com/blog/1569123)


interface
---
```
@interface UIColor (hex)
  + (UIColor *)colorWithHexString:(NSString *)stringToConvert;
@end
```

implementation
---

```
#import <QuartzCore/QuartzCore.h>
#define DEFAULT_VOID_COLOR [UIColor whiteColor]
@implementation UIColor (hex)
+ (UIColor *)colorWithHexString:(NSString *)stringToConvert {
  NSString *cString = [[stringToConvert
      stringByTrimmingCharactersInSet:[NSCharacterSet
                                          whitespaceAndNewlineCharacterSet]]
      uppercaseString];
  if ([cString length] < 6)
    return DEFAULT_VOID_COLOR;
  if ([cString hasPrefix:@"#"])
    cString = [cString substringFromIndex:1];
  if ([cString length] != 6)
    return DEFAULT_VOID_COLOR;
```
<!-- more -->

```
  NSRange range;
  range.location = 0;
  range.length = 2;
  NSString *rString = [cString substringWithRange:range];
  range.location = 2;
  NSString *gString = [cString substringWithRange:range];
  range.location = 4;
  NSString *bString = [cString substringWithRange:range];
  unsigned int r, g, b;
  [[NSScanner scannerWithString:rString] scanHexInt:&r];
  [[NSScanner scannerWithString:gString] scanHexInt:&g];
  [[NSScanner scannerWithString:bString] scanHexInt:&b];
  return [UIColor colorWithRed:((float)r / 255.0f)
                         green:((float)g / 255.0f)
                          blue:((float)b / 255.0f)
                         alpha:1.0f];
}
@end
```

使用
---
```
[UIColor colorWithHexString:@"4fc2e9"]
```