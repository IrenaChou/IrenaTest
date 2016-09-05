title: 绘制虚线
date: 2016-02-24 16:25:49
tags:
---

[参考原文](http://www.tuicool.com/articles/ZruuIzv)

绘制虚线方法
---
```
/**
 ** lineView:     需要绘制成虚线的view
 ** lineLength:   虚线的宽度
 ** lineSpacing:  虚线的间距
 ** lineColor:    虚线的颜色
 **/
+ (void)drawDashLine:(UIView *)lineView
          lineLength:(int)lineLength
         lineSpacing:(int)lineSpacing
           lineColor:(UIColor *)lineColor {
  CAShapeLayer *shapeLayer = [CAShapeLayer layer];
  [shapeLayer setBounds:lineView.bounds];
  [shapeLayer setPosition:CGPointMake(CGRectGetWidth(lineView.frame) / 2,
                                      CGRectGetHeight(lineView.frame))];
  [shapeLayer setFillColor:[UIColor clearColor].CGColor];
  //  设置虚线颜色为blackColor
  [shapeLayer setStrokeColor:lineColor.CGColor];
  //  设置虚线宽度
  [shapeLayer setLineWidth:CGRectGetHeight(lineView.frame)];
  [shapeLayer setLineJoin:kCALineJoinRound];
  //  设置线宽，线间距
  [shapeLayer
      setLineDashPattern:[NSArray
                             arrayWithObjects:[NSNumber
                                                  numberWithInt:lineLength],
                                              [NSNumber
                                                  numberWithInt:lineSpacing],
                                              nil]];
  //  设置路径
  CGMutablePathRef path = CGPathCreateMutable();
  CGPathMoveToPoint(path, NULL, 0, 0);
  CGPathAddLineToPoint(path, NULL, CGRectGetWidth(lineView.frame), 0);
  [shapeLayer setPath:path];
  CGPathRelease(path);
  //  把绘制好的虚线添加上来
  [lineView.layer addSublayer:shapeLayer];
}
```

使用
---
```
  [ViewController drawDashLine:self.lineView
                    lineLength:10
                   lineSpacing:2.0
                     lineColor:[UIColor colorWithHexString:@"393939"]];
```


绘制虚线【竖线】
---

```
/**
 *  绘制虚线【竖线】
 *
 *  @param lineView    需要绘制成虚线的view
 *  @param lineLength  虚线的宽度
 *  @param lineSpacing 虚线的间距
 *  @param lineColor   虚线的颜色
 */
+ (void)drawDashVerticalLine:(UIView *)lineView
                  lineLength:(int)lineLength
                 lineSpacing:(int)lineSpacing
                   lineColor:(UIColor *)lineColor {
  CAShapeLayer *shapeLayer = [CAShapeLayer layer];
  [shapeLayer setBounds:lineView.bounds];
  [shapeLayer setPosition:CGPointMake(CGRectGetWidth(lineView.frame),
                                      CGRectGetHeight(lineView.frame) * 0.5)];
  [shapeLayer setFillColor:[UIColor clearColor].CGColor];
  //  设置虚线颜色为blackColor
  [shapeLayer setStrokeColor:lineColor.CGColor];
  //  设置虚线宽度
  [shapeLayer setLineWidth:lineLength];
  [shapeLayer setLineJoin:kCALineJoinRound];
  //  设置线宽，线间距
  [shapeLayer
      setLineDashPattern:[NSArray
                             arrayWithObjects:[NSNumber
                                                  numberWithInt:lineLength],
                                              [NSNumber
                                                  numberWithInt:lineSpacing],
                                              nil]];
  //  设置路径
  CGMutablePathRef path = CGPathCreateMutable();
  CGPathMoveToPoint(path, NULL, 0, 0);
  CGPathAddLineToPoint(path, NULL, 0, lineView.frame.size.height);
  [shapeLayer setPath:path];
  CGPathRelease(path);
  //  把绘制好的虚线添加上来
  [lineView.layer addSublayer:shapeLayer];
}
```


[category下载](http://7xrirn.com1.z0.glb.clouddn.com/blog绘制虚线.zip)