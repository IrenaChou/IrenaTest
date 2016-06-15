title: iOS判断NSString是否为纯数字
date: 2016-04-15 11:44:40
tags:
---
```
//判断是否为整形
- (BOOL)stringIsPureNumber:(NSString*)string {
  NSScanner* scan = [NSScanner scannerWithString:string];
  int val;
  return [scan scanInt:&val] && [scan isAtEnd];
}
```
<!-- more -->
```
 //判断是否为浮点型
- (BOOL)floatIsPureFloat:(NSString*)string {
  NSScanner* scan = [NSScanner scannerWithString:string];
  float val;
  return [scan scanFloat:&val] && [scan isAtEnd];
}
```

