title: 通过slider调整图片的大小
date: 2016-09-12 13:46:02
tags:
---

[Demo下载](http://7xrirn.com1.z0.glb.clouddn.com/blogIRSliderConvertPhotoSize.zip)  
---
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/blogsliderConvertPhotoSize.gif)  


<!-- more -->

关键代码
---

```
- (void)sliderAction:(UISlider *)sender {
  sender.value += 0.01;
  CGFloat mumValue = 0.01;
  _currentImage.transform =
      self.upValue > sender.value
          ? CGAffineTransformMakeScale(sender.value - mumValue,
                                       sender.value - mumValue)
          : _currentImage.transform;
  _currentImage.transform =
      self.upValue < sender.value
          ? _currentImage.transform = CGAffineTransformMakeScale(
                sender.value + mumValue, sender.value + mumValue)
          : _currentImage.transform;
  self.upValue = sender.value;
}
```


