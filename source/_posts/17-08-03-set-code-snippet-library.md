---
title: 设置代码片断
date: 2017-08-03 13:51:59
tags: 'objc'
---

*本文就要是记录下设置代码片段*
*设置代码片段，就是通过一个标识去将一段代码整合越来吧，方便多次使用代码重复输入的问题*
*Xcode也给我们提供了很多代码片段，就像enum定义enumdef*
**enumdef**
```
typedef enum : NSUInteger {
    <#MyEnumValueA#>,
    <#MyEnumValueB#>,
    <#MyEnumValueC#>,
} <#MyEnum#>;
```

<!-- more -->
自己创建的代码片段图标上是有 **User标识的** ，可以进行修改和删除
Xcode帮我们创建的代码片段是没有标识的，不可以修改和删除

这里我们就拿创建 **创建属性** 来说一下，这个也是非常常用的了

创建
---
![创建和使用](http://7xrirn.com1.z0.glb.clouddn.com/blogcode_snippet.gif)

**步骤**：
1.  将要设置代码块的代码 **选中----> 拖拽** 到右下角的 **Show the Code Snippet libary【一对大括号的图标】** 当出现蓝色框松开鼠标
2.  为设置的代码片段设置标题描述，**completion scopes** 等，需要在使用时设置的参数，需要用 **<#参数#>** 标识，其中 **completion shortcut** 参数比较重要，使用的时候通过此参数调用。

例如：
```
@property (nonatomic, copy) NSString* <#name#>;
```

使用
---
直接在相应 **completion scopes** 的位置输入设置的 **completion shortcut** 即可


编辑【修改】
---
如果发现标题或是其他觉得不舒服或弄错了，直接在  **Show the Code Snippet libary【一对大括号的图标】** 位置，在下面的 ```Filter``` 中输入你要修改代码片段的  **completion shortcut**
找到后 **双击鼠标左键** 点击左下角的 **Edit** 修改完点击 **Done** 就可以了

删除
---
删除直接在 **Show the Code Snippet libary【一对大括号的图标】** 位置，点击键盘的 **Delete** 按键，在弹出的框中选择  **Delete** 就ok了
