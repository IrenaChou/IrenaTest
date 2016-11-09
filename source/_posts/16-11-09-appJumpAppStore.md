title: App应用内跳转AppStore与iTunesStore
date: 2016-11-09 10:39:54
tags:
---

1.  先找到app在itunes.apple.com下的链接【此文的itunes链接是按如下方法找的】
    ![此文查找链接的方法](http://7xrirn.com1.z0.glb.clouddn.com/blogitunes.png) 
2.  这里以QQ为例：
    itunes下的链接：https://itunes.apple.com/cn/app/id444934666?mt=8
    如果要跳转到AppStore，将协议https改成itms-apps：*itms-apps://itunes.apple.com/cn/app/id444934666?mt=8*
    如果要跳转到iTunesStore，将协议https改成itms：*itms://itunes.apple.com/cn/app/id444934666?mt=8*

<!-- more -->
具体代码如下【以QQ跳转到AppStore为例】：
---
```
  NSString *url = @"itms://itunes.apple.com/cn/app/id444934666?mt=8";
  [[UIApplication sharedApplication] openURL:[NSURL URLWithString:url]];
```

效果如下：
---
![AppStore](http://7xrirn.com1.z0.glb.clouddn.com/blogAppStore.png) 
![iTunesStore](http://7xrirn.com1.z0.glb.clouddn.com/blogiTunesStore.png) 

