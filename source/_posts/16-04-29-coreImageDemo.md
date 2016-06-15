title: coreImage图片滤镜处理
date: 2016-04-29 10:59:22
tags:
---

[参考](http://www.csdn.net/article/2015-02-13/2823961-core-image)

CoreImage 是一种图像处理和分析技术，为图片和视频图像提供近实时处理。图像数据类型从核心图形核心视频和图像的I / O框架，可使用GPU或CPU渲染路径。核心图像通过提供一个易于使用的应用程序接口（接口），隐藏低级别图形处理的细节。你不需要知道OpenGL和OpenGLES的细节，利用GPU的能力，你也不需要知道任何关于Grand Central Dispatch（GCD）得到的多核处理的效益。核心图像为你处理细节。
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage1.png)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage1.png)

**CIContext**： 所有图像处理都是在一个CIContext 中完成的，这很像是一个Core Image处理器或是OpenGL的上下文。 

**CIImage**： 这个类保存图像数据。它可以从UIImage、图像文件、或者是像素数据中构造出来。

**CIFilter**： 滤镜类包含一个字典结构，对各种滤镜定义了属于他们各自的属性。滤镜有很多种，比如鲜艳程度滤镜，色彩反转滤镜，剪裁滤镜等等。

Core Image架构
---

Core Image有一个插件架构，这意味着它允许用户编写自定义的滤镜并与系统提供的滤镜集成来扩展其功能。我们在这篇文章中不会用到Core Image的可扩展性；我提到它只是因为它影响到了框架的API。

包含了Core Image提供的图像滤镜的完整列表，以及用法示例。

无回路有向图



一个滤镜图表是一个链接在一起的滤镜网络（[无回路有向图](https://en.wikipedia.org/wiki/Directed_acyclic_graph)），使得一个滤镜的输出可以是另一个滤镜的输入。以这种方式，可以实现精心制作的效果。我们将在下面看到如何连接滤镜来创建一个复古的拍照效果。


[Core Image Filter Reference](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CoreImageFilterReference/index.html#//apple_ref/doc/filter/ci/CIColorClamp)包含了Core Image提供的图像滤镜的完整列表，以及用法示例。


**本文中的Demo使用iOS9.3测试**
Demo包含两个:
  一个是单纯的基本滤镜的处理
  另一个是照相,图片压缩和简单滤镜处理
  
[Demo代码下载](http://pan.baidu.com/s/1jIm3VD0)
<!-- more -->
**下面附上本人比较喜欢的几个滤镜的效果：**
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage2.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage3.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage4.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage5.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage6.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage7.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage8.PNG)
![1](http://7xrirn.com1.z0.glb.clouddn.com/coreImage9.PNG)


