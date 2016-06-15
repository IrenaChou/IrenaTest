title: 图片压缩
date: 2016-05-02 20:02:22
tags:
---

**可以将如下两个方法写在分类中,方便不同项目的重复使用**

```
//压缩图片质量
+ (UIImage*)reduceImage:(UIImage*)image percent:(float)percent {
  NSData* imageData = UIImageJPEGRepresentation(image, percent);
  UIImage* newImage = [UIImage imageWithData:imageData];
  return newImage;
}
```

<!-- more -->


```
//压缩图片尺寸
+ (UIImage*)imageWithImageSimple:(UIImage*)image scaledToSize:(CGSize)newSize {
  // Create a graphics image context
  UIGraphicsBeginImageContext(newSize);
  // new size
  [image drawInRect:CGRectMake(0, 0, newSize.width, newSize.height)];
  // Get the new image from the context
  UIImage* newImage = UIGraphicsGetImageFromCurrentImageContext();
  // End the context
  UIGraphicsEndImageContext();
  // Return the new image.
  return newImage;
}

```