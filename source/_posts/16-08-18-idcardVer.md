title: 身份证号合法性验证
date: 2016-08-18 15:28:23
tags:
---
*此方法主要验证身份证号的合法性*

方法定义
---

```
#import <Foundation/Foundation.h>
@interface NSString (Extension)
/**
 *  身份证识别
 *
 *  @param cardNo 身份证号
 *
 *  @return 是否正确
 */
+ (BOOL)checkIdentityCardNo:(NSString *)cardNo;
@end
```


<!-- more -->
方法实现
---
```
#import "NSString+Extension.h"

@implementation NSString (Extension)
#pragma mark - 身份证识别
/**
 *  身份证合法性验证
 *
 *  @param cardNo 身份证号
 *
 *  @return 是否合法【1-合法，0-不合法】
 */
+ (BOOL)checkIdentityCardNo:(NSString *)cardNo {
  if (cardNo.length != 18) {
    return NO;
  }
  NSArray *codeArray = [NSArray
      arrayWithObjects:@"7", @"9", @"10", @"5", @"8", @"4", @"2", @"1", @"6",
                       @"3", @"7", @"9", @"10", @"5", @"8", @"4", @"2", nil];
  NSDictionary *checkCodeDic = [NSDictionary
      dictionaryWithObjects:[NSArray arrayWithObjects:@"1", @"0", @"X", @"9",
                                                      @"8", @"7", @"6", @"5",
                                                      @"4", @"3", @"2", nil]
                    forKeys:[NSArray arrayWithObjects:@"0", @"1", @"2", @"3",
                                                      @"4", @"5", @"6", @"7",
                                                      @"8", @"9", @"10", nil]];
  NSScanner *scan = [NSScanner scannerWithString:[cardNo substringToIndex:17]];
  int val;
  BOOL isNum = [scan scanInt:&val] && [scan isAtEnd];
  if (!isNum) {
    return NO;
  }
  int sumValue = 0;
  for (int i = 0; i < 17; i++) {
    sumValue += [[cardNo substringWithRange:NSMakeRange(i, 1)] intValue] *
                [[codeArray objectAtIndex:i] intValue];
  }
  NSString *strlast = [checkCodeDic
      objectForKey:[NSString stringWithFormat:@"%d", sumValue % 11]];
  if ([strlast isEqualToString:[[cardNo substringWithRange:NSMakeRange(17, 1)]
                                   uppercaseString]]) {
    return YES;
  }
  return NO;
}
```