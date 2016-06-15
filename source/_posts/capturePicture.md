title: capturePicture 截取scrollView和屏幕显示的图片
date: 2016-02-16 14:22:45
tags:
---
一、获取当前屏幕显示的图片
--

```
  UIGraphicsBeginImageContextWithOptions(_scrollView.contentSize, YES, 1);
  [_scrollView.layer renderInContext:UIGraphicsGetCurrentContext()];
  UIImage *uiImage = UIGraphicsGetImageFromCurrentImageContext();
  UIGraphicsEndImageContext();
```

二、获取scrollView的contentSize包含的图片
--
<!-- more -->

```
- (UIImage *)captureScrollView:(UIScrollView *)scrollView {
  UIImage *image = nil;
  UIGraphicsBeginImageContext(scrollView.contentSize);
  {
    CGPoint savedContentOffset = scrollView.contentOffset;
    CGRect savedFrame = scrollView.frame;
    scrollView.contentOffset = CGPointZero;
    scrollView.frame = CGRectMake(0, 0, scrollView.contentSize.width,
    scrollView.contentSize.height);
    [scrollView.layer renderInContext:UIGraphicsGetCurrentContext()];
    image = UIGraphicsGetImageFromCurrentImageContext();
    scrollView.contentOffset = savedContentOffset;
    scrollView.frame = savedFrame;
  }
  UIGraphicsEndImageContext();
  if (image != nil) {
    return image;
  }
  return nil;
}
```



