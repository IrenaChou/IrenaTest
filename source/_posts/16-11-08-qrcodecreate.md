title: 生成二维码图片
date: 2016-11-08 17:18:45
tags:
---

使用【返回一个image】
---

```
[self createQRCodeImageWithQRCode:@"http://irenachou.github.io/"];
```



创建【通过二维码字符串生成一个二维码图片】
---

<!-- more -->

```
+ (UIImage *)createQRCodeImageWithQRCode:(NSString *)qrcode {
  // 1.创建滤镜
  CIFilter *filter = [CIFilter filterWithName:@"CIQRCodeGenerator"];
  // 2.还原滤镜默认属性
  [filter setDefaults];
  // 3.设置需要生成二维码的数据到滤镜中(OC中要求设置的是一个二进制数据)
  NSData *data = [qrcode
      dataUsingEncoding:
          NSUTF8StringEncoding];  //(这里的字符串就是用来生成二维码的,可直接复制代码只需修改这里如果没有其他需求)
  [filter setValue:data forKeyPath:@"InputMessage"];
  // 4.从滤镜从取出生成好的二维码图片
  CIImage *ciImage = [filter outputImage];
  return [self createhdUIImageFormCIImage:ciImage size:300];
}
+ (UIImage *)createhdUIImageFormCIImage:(CIImage *)ciImage size:(CGFloat)size {
  CGRect wsRect = CGRectIntegral(ciImage.extent);
  CGFloat scale =
      MIN(size / CGRectGetWidth(wsRect), size / CGRectGetHeight(wsRect));
  //  1.二维码基本设置
  // 1.创建bitmap;
  size_t width = CGRectGetWidth(wsRect) * scale;
  size_t height = CGRectGetHeight(wsRect) * scale;
  CGColorSpaceRef cs = CGColorSpaceCreateDeviceGray();
  CGContextRef wsRef = CGBitmapContextCreate(nil, width, height, 8, 0, cs,
                                             (CGBitmapInfo)kCGImageAlphaNone);
  CIContext *context = [CIContext contextWithOptions:nil];
  CGImageRef wsImageRef = [context createCGImage:ciImage fromRect:wsRect];
  CGContextSetInterpolationQuality(wsRef, kCGInterpolationNone);
  CGContextScaleCTM(wsRef, scale, scale);
  CGContextDrawImage(wsRef, wsRect, wsImageRef);
  // 保存bitmap到图片
  CGImageRef scaledImage = CGBitmapContextCreateImage(wsRef);
  CGContextRelease(wsRef);
  CGImageRelease(wsImageRef);
  return [UIImage imageWithCGImage:scaledImage];
}
```

**通过二维码字符串生成二维码图片的关键代码放在如下链接的category里，需要请下载使用**

[关键代码下载](http://7xrirn.com1.z0.glb.clouddn.com/blogCode生成二维码图片.zip)
---

