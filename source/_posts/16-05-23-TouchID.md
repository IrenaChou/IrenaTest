title: iOS Touch ID
date: 2016-05-23 18:10:30
tags:
---
**Touch ID**指纹识别作为iPhone 5s上的“杀手级”功能早已为人们所熟知，iphone SE、iPhone 6、iPhone 6Puls、iPhone 6s、iPhone 6s Plus、iPad Pro、iPad mini 4、iPad mini 3和iPad air 2也使用了Touch ID。  苹果把用户的指纹数据存放在处理器的安全区域（Secure Enclave）中，充分保护用户的数据安全。除此之外，苹果还有另外一道指纹数据安全防线，以一种前所未有的硬件技术实现了对用户数据的保护。

效果展示
---
* ![效果显示](http://7xrirn.com1.z0.glb.clouddn.com/TouchID.png)


[Demo下载](http://pan.baidu.com/s/1o8eVpNG)
---


<!-- more -->

具体实现
---
```
先导入LocalAuthentication.framework
#import <LocalAuthentication/LocalAuthentication.h>
- (void)authenticateUser {
  //初始化上下文对象
  LAContext *context = [[LAContext alloc] init];
  //错误对象
  NSError *error = nil;
  //使用canEvaluatePolicy 判断设备支持状态
  if ([context canEvaluatePolicy:LAPolicyDeviceOwnerAuthenticationWithBiometrics
                           error:&error]) {
    //支持指纹验证
    [context
         evaluatePolicy:LAPolicyDeviceOwnerAuthenticationWithBiometrics
        localizedReason:@"TouchID 测试"  //显示的文本
                  reply:^(BOOL success, NSError *error) {
                    if (success) {
                      NSLog(@"验证成功，主线程处理UI");
                    } else {
                      NSLog(@"%@", error.localizedDescription);
                      switch (error.code) {
                        case LAErrorSystemCancel: {
                          NSLog(@"切换到其他APP，系统取消验证Touch "
                                @"ID");
                          //切换到其他APP，系统取消验证Touch ID
                          break;
                        }
                        case LAErrorUserCancel: {
                          //用户取消验证Touch ID
                          NSLog(@"用户取消验证Touch ID");
                          break;
                        }
                        case LAErrorUserFallback: {
                          NSLog(
                              @"用"
                              @"户选择输入密码，切换主线程处理");
                          [[NSOperationQueue mainQueue] addOperationWithBlock:^{
                            NSLog(
                                @"用"
                                @"户"
                                @"选择输入密码，切换主线程处理");
                          }];
                          break;
                        }
                        default: {
                          [[NSOperationQueue mainQueue] addOperationWithBlock:^{
                            NSLog(@"其他情况，切换主线程处理");
                          }];
                          break;
                        }
                      }
                    }
                  }];
  } else {
    //不支持指纹识别，LOG出错误详情
    switch (error.code) {
      case LAErrorTouchIDNotEnrolled: {
        NSLog(@"设备Touch ID不可用，用户未录入");
        break;
      }
      case LAErrorPasscodeNotSet: {
        NSLog(@"系统未设置密码");
        break;
      }
      default: {
        NSLog(@"TouchID不可用");
        break;
      }
    }
    NSLog(@"%@", error.localizedDescription);
  }
}
```



错误失败信息：
---
1.  连续三次指纹识别错误：
    **Aplication retry limit exceeded**
2.  Touch ID功能被锁定，下一次需要输入系统密码：
    **Biometry is locked out**
3.  用户在Touch ID对话框中点击了取消按钮
    **Canceled by user**
4.  在Touch ID对话框显示过程中，背系统取消，例如按下电源键：
    **UI canceled by system**
5.  用户在Touch ID对话框中点击输入密码按钮：
    **Fallback authentication mechanism selected**
6.  目标设备不支持指纹识别
    **Biometry is not available on this device** //真机
    **Simulator is not supported**               //模拟器



