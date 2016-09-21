title: 去除图片渲染效果【使tabBarItem及navigation显示原图片】
date: 2016-09-21 16:48:35
tags:
---



```
ctrl.tabBarItem.selectedImage = [[UIImage imageNamed:selImageName]
    imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
```
**效果如下图：**
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/blogImagerenderOriginal.png)  



在为tabBarItem及navigation设置图片的时候会有一层蒙版遮盖，imageWithRenderingMode方法就是为了解决这个问题，去除遮盖显示原图片，**遮盖的颜色可以修改self.tabBar.tintColor进行更改**


<!-- more -->



![未使用方法的效果](http://7xrirn.com1.z0.glb.clouddn.com/blogImageoriginalImage.png)
**效果如下图：**
```
ctrl.tabBarItem.selectedImage = [UIImage imageNamed:selImageName];
```


**下面提供一个category，实现如下方法**
[Category下载](http://7xrirn.com1.z0.glb.clouddn.com/UIImage+Ex.zip)  

