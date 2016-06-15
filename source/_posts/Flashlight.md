title: 手电筒
date: 2016-03-28 14:06:15
tags:
---


[原码下载](http://pan.baidu.com/s/1gfIwpmb)

```
#import "ViewController.h"
#import <AVFoundation/AVFoundation.h>
@interface ViewController ()
@property(nonatomic, strong) AVCaptureDevice *device;
@property(nonatomic) AVCaptureTorchMode torchModeMe;
@property(weak, nonatomic) IBOutlet UISwitch *controlSwitch;
@end
```

```
@implementation ViewController
/**
 *  开关手电桶
 */
- (IBAction)onOrOff:(id)sender {
  // AVCaptureDevice代表抽象的硬件设备
  // 返回用于捕获给定媒体类型的数据的默认设备
  _device = [AVCaptureDevice defaultDeviceWithMediaType:AVMediaTypeVideo];
  //检查设备是否支持手电筒
  if (![_device hasTorch]) {
    NSLog(@"设备不支持手电筒");
    return;
  }
  if ([sender isOn]) {
    [self.view setBackgroundColor:[UIColor whiteColor]];
    _torchModeMe = AVCaptureTorchModeOn;
  } else {
    [self.view setBackgroundColor:[UIColor blackColor]];
    _torchModeMe = AVCaptureTorchModeOff;
  }
  // lockForConfiguration 来尝试在捕获设备上获取锁
  [_device lockForConfiguration:nil];
  [_device setTorchMode:_torchModeMe];
  //来放弃锁定
  [_device unlockForConfiguration];
}
- (void)viewDidLoad {
  [super viewDidLoad];
  [self onOrOff:_controlSwitch];
}
@end
```