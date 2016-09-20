title: oc-synthesize
date: 2016-09-20 16:43:26
tags:
---

在Xcode4版本之前@property和@synthesize的功能是独立开来的：

.h中的代码

```
//@property的作用是：自动的生成成员变量setter/getter方法的声明：
  @property int carName;  //它的作用和下面两行代码的作用相同
  - (void)setCarName:(int)carName;
  - (int)carName;
```
**注意：属性名称不要加前缀_ 否则生成的setter/getter方法中也会有下划线**
<!-- more -->

.m中的代码
```
  //@synthesize的作用是实现@property定义的方法代码如：
  @synthesize carName
  //将@propertys中定义的属性自动生成setter/getter的实现方法而且默认访问成员变量carName
```

```
 如果指定访问成员变量_carName：
 @synthesize carName = _carName；
 就是说 实现@property中声明的carName成员变量生成setter/getter方法，并且在实现方法内部访问_carName这个成员变量，也就意味着给成员 _carName 赋值
```




如果在.h文件中没有定义_carName成员变量的话，就会在.m文件中自动生成@private类型的成员变量_carName
 

**在Xcode4以后@property会实现以上所有功能,可以不用在.m文件中写@synthesize**