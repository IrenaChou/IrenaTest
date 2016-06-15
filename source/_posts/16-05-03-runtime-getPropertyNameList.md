title: 获取当前类所有属性
date: 2016-05-03 17:18:31
tags:
---


    **class_copyPropertyList**： 返回对象类的属性(@property声明的属性)
    **class_copyIvarList**：返回类的所有属性和变量(包括在@interface大括号中声明的变量)


    通过runtime获取当前类@property声明的属性列表

```
#import <objc/runtime.h>
@implementation PayModel
- (NSArray *)getPropertyNameList {
  unsigned int count;
  //  返回对象类的属性(@property声明的属性)
  objc_property_t *properties = class_copyPropertyList([self class], &count);
  //存储属性列表
  NSMutableArray *propertyNameList = [NSMutableArray array];
  for (int i = 0; i < count; i++) {
    objc_property_t property = properties[i];
    // property_getName返回一个CString
    // 将CString转换为NSString
    NSString *str = [NSString stringWithCString:property_getName(property)
                                       encoding:NSUTF8StringEncoding];
    [propertyNameList addObject:str];
  }
  free(properties);
  return [propertyNameList copy];
}
@end
```
