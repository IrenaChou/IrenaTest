title: 空值判断
date: 2016-03-11 13:19:36
tags:
---
```
//空值判断
BOOL isNotNULL(id object);
```

```
BOOL isNotNULL(id object) {
  if ([object isKindOfClass:[NSNull class]]) {
    return NO;
  } else if ([object isKindOfClass:[NSString class]]) {
    if ([object isEqualToString:@"(null)"]) {
      return NO;
    }
  } else if (!object) {
    return NO;
  }
  return YES;
}
```