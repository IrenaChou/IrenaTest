title: UIView Clip Subviews
date: 2016-06-14 17:58:01
tags:
---

最终效果  
---
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/clipSubviews-1.png)  
<!-- more -->
用代码实现如下
---
```
[self.baseView setClipsToBounds:YES];
```
用storyBoard或xib操作步骤：
--- 
  * 为**父类**勾选如下图红框中的选项
  * ![要设置的属性](http://7xrirn.com1.z0.glb.clouddn.com/clipSubviews-3.png)  
  * 未勾选的效果如下
  * ![设置此属性前的效果](http://7xrirn.com1.z0.glb.clouddn.com/clipSubviews-2.png)  

[Demo下载](http://pan.baidu.com/s/1eSG0yYm)
---

*本文使用iOS9.3  Xcode7.3*

