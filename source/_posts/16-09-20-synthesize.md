title: oc-synthesize和dynamic
date: 2016-09-20 16:43:26
tags:
---

@property
---
**@property=ivar+getter+setter**
当我们属性定义完成后,编译器会自动生成该属性的getter和setter方法,并且还会自动向类中添加有下划线的实例变量,即 *_实例变量*

@synthesize
---
的作用就是如果你没有手动实现getter与setter方法,那么编译器就会自动为你加上这两个方法

@dynamic
---
* @dynamic告诉编译器：属性的 setter 与 getter 方法由用户自己实现，不自动生成。
* 当然对于 readonly 的属性只需提供 getter 即可
* 假如一个属性被声明为@dynamic var，而且你没有提供@setter方法和@getter 方法，编译的时候没问题，运行中如果发现有使用到setter或getter方法，就会导致崩溃
