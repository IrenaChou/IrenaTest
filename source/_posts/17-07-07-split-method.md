---
title: 单个数求和后拆分
date: 2017-07-07 11:19:18
tags:
---

输入一个数如38，拆分 3 + 8 = 11，1 + 1 = 2，最后2无法拆分就返回
---

这是网上看到别人回来的，时间上差不多，代码也精简的多，完胜
---
```
- (NSUInteger)test:(NSUInteger)num
{
    while (num >= 10) {
        num = num/10 + num%10;
    }
    return num;
}
```

<!-- more -->

*先拆分求每位数累加的和，在将和去重复上一步操作，主要使用递归实现*

```
@property (nonatomic, assign) NSUInteger sum;
```

```
-(NSUInteger)splitNum:(NSUInteger)num{

    self.sum += num % 10;

    if (num / 10 == 0) {
        if (self.sum / 10 != 0) {
            num = self.sum;
            self.sum = num % 10;
        }else{
            return self.sum;
        }
    }

    return [self splitNum:num / 10];

}
```
