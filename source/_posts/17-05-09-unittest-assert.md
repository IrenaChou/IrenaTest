---
title: 单元测试断言汇总
date: 2017-05-09 10:14:40
tags:
---

*本文是对XCTestAssertions.h的简单翻译并添加了自己以及收集的一些想法，如有错误，欢迎指出*

XCTFail(...)
---
```
XCTFail(@"错误，停止");
```
*描述文本参数可选*
相当于在此处放一个bug，让程序停止，提示描述文本
**任何时候都为 faile**

<!-- more -->
XCTAssertNil(expression, ...)
---
*string = @""，number = 0都是测试失败，只要不是nil都测试失败*
当表达式等于nil的时候通过，否则测试失败，提示描述文本
expression接受 **id** 类型的参数

XCTAssertNotNil(expression, ...)
---
与XCTAssertNil相反，当表达式不等于nil的时候通过，否则测试失败，提示描述文本
expression接受 **id** 类型的参数

XCTAssert(expression, ...)
---
当表达式的值为YES的时候通过，否则测试失败，提示描述文本
*空字符串 = YES*
*number = 0 = NO，number != 0 = YES*
*nil = NO*
expression接受 **BOOL** 类型的参数

XCTAssertTrue(expression, ...)
---
当表达式的值为YES时通过，否则测试失败，提示描述文本
expression接受 **BOOL** 类型的参数

XCTAssertFalse(expression, ...)
---
与XCTAssertFalse相反，当表达式的值为NO时通过，否则测试失败，提示描述文本
expression接受 **BOOL** 类型的参数

XCTAssertEqualObjects(expression1, expression2, ...)
---
```
XCTAssertEqualObjects(@(3),@(3 - 0),@"表达式1 ！= 表达式2");
```
当 **表达式1 == 表达式2** 时通过， *比较表达式地址* ，否则测试失败，提示描述文本
expression接受 **id** 类型的参数

XCTAssertNotEqualObjects(expression1, expression2, ...)
---
与XCTAssertEqualObjects相反，当 **表达式1 != 表达式2** 时通过，否则测试失败，提示描述文本
expression接受 **id** 类型的参数

XCTAssertEqual(expression1, expression2, ...)
---
当 **表达式1 == 表达式2** 时通过，否则测试失败，提示描述文本
expression接受基本类型的参数（数值、结构体之类的）
*当expression为id类型时，比较两个id类型的地址*


XCTAssertNotEqual(expression1, expression2, ...)
---
与XCTAssertEqual相反，当 **表达式1 != 表达式2** 时通过，否则测试失败，提示描述文本
expression接受基本类型的参数（数值、结构体之类的）
*当expression为id类型时，比较两个id类型的地址*


XCTAssertEqualWithAccuracy(expression1, expression2, accuracy, ...)
---
```
XCTAssertEqualWithAccuracy(1,1,0,@"error");
```
当 **表达式1 - 表达式2 <= accuracy** 时通过，否则测试失败，提示描述文本
expression，accuracy接受 **基础** 类型的参数

XCTAssertNotEqualWithAccuracy(expression1, expression2, accuracy, ...)
---
与XCTAssertEqualWithAccuracy相反
当 **表达式1 - 表达式2 > accuracy** 时通过，否则测试失败，提示描述文本
expression，accuracy接受 **基础** 类型的参数


XCTAssertGreaterThan(expression1, expression2, ...)
---
```
XCTAssertGreaterThan(2, 1, @"error");
```
当 **表达式1 > 表达式2** 时通过，否则测试失败，提示描述文本
expression接受 **基础** 类型的参数

XCTAssertGreaterThanOrEqual(expression1, expression2, ...)
---
```
XCTAssertGreaterThanOrEqual(2,1,@"error");
```
当 **表达式1 >= 表达式2** 时通过，否则测试失败，提示描述文本
expression接受 **基础** 类型的参数

XCTAssertLessThan(expression1, expression2, ...)
---
当 **表达式1 < 表达式2** 时通过，否则测试失败，提示描述文本
expression接受 **基础** 类型的参数

XCTAssertLessThanOrEqual(expression1, expression2, ...)
---
当 **表达式1 <= 表达式2** 时通过，否则测试失败，提示描述文本
expression接受 **基础** 类型的参数

XCTAssertThrows(expression, ...)
---
当表达式抛出异常时通过，否则测试失败，提示描述文本
expression为一个表达式

XCTAssertThrowsSpecific(expression, exception_class, ...)
---
当表达式没抛指定类exception_class的异常，测试失败。
expression为一个表达式
exception_class为一个指定类

XCTAssertThrowsSpecificNamed(expression, exception_class, exception_name, ...)
---
expression没抛指定类、指定名字的异常，测试失败。
expression为一个表达式
exception_class为一个指定类
exception_name为一个指定名字

XCTAssertNoThrow(expression, ...)
---
expression抛出异常时，测试失败。
expression为一个表达式

XCTAssertNoThrowSpecific(expression, exception_class, ...)
---
expression抛出指定类的异常，测试失败。
expression为一个表达式

XCTAssertNoThrowSpecificNamed(expression, exception_class, exception_name, ...)
---
expression抛出指定类、指定名字的异常，测试失败。
expression为一个表达式
exception_class为一个指定类
exception_name为一个指定名字


*后面的几个说明来自https://my.oschina.net/u/1418722/blog/340194*
