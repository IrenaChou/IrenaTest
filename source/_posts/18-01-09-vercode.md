---
title: 【转】iOS 短信验证码倒计时按钮的实现
date: 2018-01-09 15:44:41
tags:
---

实现思路:
---
* 创建按钮, 添加点击方法;
* 用NSTimer定时器, 每秒执行一次, 定时改变Button的title,改变Button的样式, 设置Button不可点击;
* 若倒计时结束, 定时器关闭, 并改变Button的样式, 可以点击;

<!-- more -->

代码如下:
---
在按钮的点击事件里调用该方法.

```
// 开启倒计时效果
-(void)openCountdown:(UIButton*)sender{

    __block NSInteger time = 59; //倒计时时间

    dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
    dispatch_source_t _timer = dispatch_source_create(DISPATCH_SOURCE_TYPE_TIMER, 0, 0, queue);

    dispatch_source_set_timer(_timer,dispatch_walltime(NULL, 0),1.0*NSEC_PER_SEC, 0); //每秒执行

    dispatch_source_set_event_handler(_timer, ^{

        if(time <= 0){ //倒计时结束，关闭

            dispatch_source_cancel(_timer);
            dispatch_async(dispatch_get_main_queue(), ^{

                //设置按钮的样式
                [sender setTitle:@"重新发送" forState:UIControlStateNormal];
                [sender setTitleColor:[UIColor colorFromHexCode:@"FB8557"] forState:UIControlStateNormal];
                sender.userInteractionEnabled = YES;
            });

        }else{

            int seconds = time % 60;
            dispatch_async(dispatch_get_main_queue(), ^{

                //设置按钮显示读秒效果
                [sender setTitle:[NSString stringWithFormat:@"重新发送(%.2d)", seconds] forState:UIControlStateNormal];
                [sender setTitleColor:[UIColor colorFromHexCode:@"979797"] forState:UIControlStateNormal];
                sender.userInteractionEnabled = NO;
            });
            time--;
        }
    });
    dispatch_resume(_timer);
}
```

作者：Li_Cheng
链接：https://www.jianshu.com/p/2104865e7dba
來源：简书
