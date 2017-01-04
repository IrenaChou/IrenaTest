title: iOS制作framework
date: 2017-01-04 15:11:03
tags:
---

生成和使用framework

<!-- more -->






制作framework
---
本文使用：**Xcode Version 8.2.1**，**macOS Sierra 10.12.2**

**创建framework文件步骤如下图**：

​	此framework主要有一个打印的测试方法

![创建framework](http://7xrirn.com1.z0.glb.clouddn.com/blogImagemakeFramework.gif)

**把真机的framework与模拟器的framework合并**【_文件本文只生成debug使用的framework_】：

![合并framework](http://7xrirn.com1.z0.glb.clouddn.com/blogImagemakeFramework02.gif)	






使用framework
---
![使用framework](http://7xrirn.com1.z0.glb.clouddn.com/blogImagemakeFramework03.gif)	

如上图使用会出现如下错误：

```
dyld: Library not loaded: @rpath/IRMakeAPIFramework.framework/IRMakeAPIFramework
  Referenced from: /var/containers/Bundle/Application/FF92ED2C-8C1B-4CD2-BE8E-583A9DC1B5BC/IRTestAPIFramework.app/IRTestAPIFramework
  Reason: image not found
```
解决办法有两个
*	  一是修改生成framework程序后在重新生成framework
     *  ![使用framework](http://7xrirn.com1.z0.glb.clouddn.com/blogImagemakeFramework04.png)	
     *  另一个生成framework文件使用**Dynamic Libary**，使用的时候需修改
     *  ![使用framework](http://7xrirn.com1.z0.glb.clouddn.com/blogImagemakeFramework05.png)