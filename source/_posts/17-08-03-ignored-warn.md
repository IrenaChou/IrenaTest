---
title: Xcode忽略Bulidtime警告
date: 2017-08-03 13:23:31
tags:
---
*本文主要是忽略Xcode警告，让Xcode不提示，参考原文已经写的很好了，这里自己记录一下*
*忽略前，要先看清是否是关键的警告在决定是要忽略---还是修复他*

获取警告标识
---
可以说警告是分类型的， **Issue navigator** 中可以通过文件或是类型查看警告
![按类型查看警告](http://7xrirn.com1.z0.glb.clouddn.com/blogchooseType.png)

<!-- more -->

**单击右键** ，选择了 **View by Type** 后，警告会通过类型来区分
*下面是我项目中的警告，我只有几个警告是选择忽略的，其它根据警告做处理*
![按类型查看警告](http://7xrirn.com1.z0.glb.clouddn.com/blogwarnTypes.png)

同一类警告下面会有多个警告，警告标识大部分是相同的
可以打开一类警告看描述，相同的就不用重复获取了，相对来说还是会方便一些的
![警告类型](http://7xrirn.com1.z0.glb.clouddn.com/blogissue.png)

如下图，在某一个警告行上单击右键，获取警告标识
![获取警告标识](http://7xrirn.com1.z0.glb.clouddn.com/blogissue1.png)

如下图，下图中红色框中的就是我们本文要用的警告标识了
![具体警告标识](http://7xrirn.com1.z0.glb.clouddn.com/blogissue2.png)

忽略源文件中单个警告
---
```
#pragma clang diagnostic push
#pragma clang diagnostic ignored "警告标识符"
报警告的代码
#pragma clang diagnostic pop
```

一般我会将下面代码存成一个代码片断，以便重复使用
设置代码片断参考[创建代码片断](http://irenachou.github.io/2017/08/03/17-08-03-set-code-snippet-library/)

```
#pragma clang diagnostic push
#pragma clang diagnostic ignored "<#-Wunused-variable#>"
#pragma clang diagnostic pop
```


在 Build Settings 中项目全局忽略警告
---
在项目的 **Build Settings** 中也可以设置忽略某种或多种类型的警告，不过在这设置的影响范围就是整个项目的了，要三思而后行。

如下图，在 **Build Settings** 中找到 **Custom Compiler Flags**，双击 **Other Warning Flags**（可以配置 Debug 和 Release 环境），填入 **-Wno-unused-variable** ，完成后，编译项目，项目中所有的此类型警告都没有了。

下图我是采用搜索的方式查找的，就是在右上角的搜索框中输入相应的搜索关键字，回车就ok
![忽略全局警告](http://7xrirn.com1.z0.glb.clouddn.com/blogissue3.png)

这里所填写的内容规则，在警告标识中的 **W** 字母后面加上  **no-** 就可以了。
例如：警告标识是 **-Wunused-variable**
     这里要填写的就是 **-Wno-unused-variable**


忽略CocoaPods导入第三方库的警告
---
通过 CocoaPods 给项目导入了一些第三方库，这些库里面或多或少会有些警告，想消除这些警告，很简单，只需在 Podfile 中加上这一句 **inhibit_all_warnings!**，所有通过 CocoaPods 安装的第三库的警告就没有了。



原文[参考自](http://www.jianshu.com/p/327078fda8dc)
