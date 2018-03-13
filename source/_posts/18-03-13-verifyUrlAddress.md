---
title: 验证http(s)url链接的合法性
date: 2018-03-13 15:40:25
tags:
---

**通过正则来验证http(s)url的合法性，下面代码放在NSString的category中**


方法定义
---
```
-(BOOL)isUrlAddress;
```
<!-- more -->

方法实现
---
```
-(BOOL)isUrlAddress{
    NSString *reg = @"^http(s)?:\\/\\/([\\w-]+\\.)+[\\w-]+(\\/[\\w- ./?%&=]*)?$";
    NSPredicate *urlPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", reg];
    return [urlPredicate evaluateWithObject:self];
}
```


*此文档只做记录使用*
