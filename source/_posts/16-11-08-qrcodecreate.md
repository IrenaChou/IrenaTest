title: 生成二维码图片
date: 2016-11-08 17:18:45
tags:
---


条码样式显示
---

![条形码](http://7xrirn.com1.z0.glb.clouddn.com/blogQRCodeCICode128BarcodeGenerator.png)



![PDF417二维码](http://7xrirn.com1.z0.glb.clouddn.com/blogQRCodeCIPDF417BarcodeGenerator.png)



![Aztec码](http://7xrirn.com1.z0.glb.clouddn.com/blogQRCodeCIAztecCodeGenerator.png)



![二维码](http://7xrirn.com1.z0.glb.clouddn.com/blogQRCodeCIQRCodeGenerator.png)



<!-- more -->


使用【返回一个image】
---

```
[self createQRCodeImageWithQRCode:@"http://irenachou.github.io/"];
```




创建【通过二维码字符串生成一个二维码图片】
---



```
+ (UIImage *)createQRCodeImageWithQRCode:(NSString *)qrcode {
  // 1.创建滤镜
  //filterWithName后name的值，选择不同的值创建不同类型的条码
  // CIAztecCodeGenerator
        //Aztec码是一种类型的二维条码所发明安德鲁朗埃克，小罗伯特·赫西于1995年[1]的代码被发布的AIM，公司在1997年虽然阿兹特克代码的专利，[1]该专利被正式公开领域。[2]阿兹特克代码也发布为ISO / IEC 24778：2008标准。中央取景器图案的相似性的得名阿兹特克金字塔，阿兹特克码具有使用较少的空间比其它的矩阵条形码，因为它不要求一个周边空白“静区”的潜力。
  // CIPDF417BarcodeGenerator：
        //PDF417条码是二维码的一种。PDF417条码是一种高密度、高信息含量的便携式数据文件，是实现证件及卡片等大容量、高可靠性信息自动存储、携带并可用机器自动识读的理想手段
  // CICode128BarcodeGenerator：条形码
  // CIQRCodeGenerator：二维码

  //普通二维码
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

