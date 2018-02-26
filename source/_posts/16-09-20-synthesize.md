title: oc-synthesize和dynamic
date: 2016-09-20 16:43:26
tags:
---

@property有两个对应的词，一个是 @synthesize，一个是 @dynamic。如果@synthesize和@dynamic都没写，那么默认的就是@syntheszie var = *_var*;

@synthesize
---

* @synthesize语法来指定实例变量的名字，@synthesize 声明的属性=实例变量【一般以下划线开头后面跟属性名，eg: *@synthesize 属性名 = _属性名*】
* @synthesize表示如果属性没有手动实现setter和getter方法，那么编译器会自动加上这两个方法。
* 如果@synthesize和 @dynamic都没写，那么默认的就是 *@syntheszie var = _var*;


@dynamic
---
* @dynamic告诉编译器：属性的 setter 与 getter 方法由用户自己实现，不自动生成。
* 当然对于 readonly 的属性只需提供 getter 即可
* 假如一个属性被声明为@dynamic var，而且你没有提供@setter方法和@getter 方法，编译的时候没问题，运行中如果发现有使用到setter或getter方法，就会导致崩溃
