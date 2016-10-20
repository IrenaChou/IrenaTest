title: 提示(声音、震动)
date: 2016-10-20 16:25:32
tags:
---

声音提示
---
*  导入头文件//#import <Photos/Photos.h>

```
#import <Photos/Photos.h>
/**
 *  声音
 */
- (void)systemSound {
  AudioServicesPlaySystemSound(SOUNDID);
}
```



振动提示
---
*  导入头文件//#import <Photos/Photos.h>

```
#define SOUNDID 1109  // 1012 -iphone   1152 ipad  1109 ipad
- (void)systemVibrate {
  AudioServicesPlaySystemSound(kSystemSoundID_Vibrate);
}
```