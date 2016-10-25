title: 自定义简单倒计时
date: 2016-10-25 15:33:00
tags:
---

**效果如下图：**
*如不输入倒计时数字，默认60秒
输入倒计时数字后点击键盘的return链确认*

![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/blogcountDown.gif)  

<!-- more -->

关键代码如下【具体代码看Demo】：
---

```
/**
 *  开始倒计时
 */
- (IBAction)tapped:(id)sender {
  [sender setEnabled:NO];
  self.targetTimeNum.enabled = NO;
  self.leftNum = [self.currentNum.text integerValue];
  self.timer = [NSTimer timerWithTimeInterval:1
                                       target:self
                                     selector:@selector(tickDown)
                                     userInfo:nil
                                      repeats:YES];
  [[NSRunLoop mainRunLoop] addTimer:self.timer forMode:NSRunLoopCommonModes];
}
/**
 *  更新当前显示的数字
 */
- (void)tickDown {
  self.leftNum -= 1;
  [self.currentNum setText:[NSString stringWithFormat:@"%zd", self.leftNum]];
  /**
   *  放大
   */
  //创建一个CABasicAnimation对象
  CABasicAnimation *animation =
      [CABasicAnimation animationWithKeyPath:@"transform.scale"];
  self.currentNum.layer.anchorPoint = CGPointMake(.5, .5);
  animation.fromValue = @0.0f;
  animation.toValue = @1.0f;
  //动画时间
  animation.duration = 0.5;
  //是否反转变为原来的属性值
  animation.autoreverses = YES;
  //把animation添加到图层的layer中，便可以播放动画了。forKey指定要应用此动画的属性
  [self.currentNum.layer addAnimation:animation forKey:@"scale"];
  if (self.leftNum <= 0) {
    [self systemSound];
    [self systemVibrate];
    self.targetTimeNum.enabled = YES;
    [self.starBtn setEnabled:YES];
    [self.timer invalidate];
  }
}
```



[点击Demo下载](http://7xrirn.com1.z0.glb.clouddn.com/blogCodeIRCountdown.zip)
---




