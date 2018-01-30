---
title: js跳转原生iOSAPP与iOSAPP应用间跳转
date: 2018-01-29 17:36:35
tags: 'JavaScript'
---

iOS APP应用间跳转
---
原生APP应用间跳转需要在打开与被打开的APP都做处理

*这里将首先打开的APP称为【 APP2 】，将跳转到的APP称为【 APP1 】*

步骤如下：
* 【APP1】需要维护自身的 **URL Schemes**
* 【APP2】需要将APP1的 **URL Schemes** 添加到自身的APP中
*  做完上面两个步骤后，在需要跳转的位置添加如下代码

```
[[UIApplication sharedApplication]openURL:[NSURL URLWithString:@"APP1 的 URL Schemes:"] options:@{} completionHandler:nil ];
```

如果需要在APP1中对其处理，需要在 **UIApplicationDelegate** 中的 **openURL** 方法中进行处理

<!-- more -->

js跳转原生iOS APP
---
js代码如下，APP需要设置url schemes

如果需要在APP1中对其处理，需要在 **UIApplicationDelegate** 中的 **openURL** 方法中进行处理
```
window.location.href = 'APP的URL Schemes://';
```

微信跳转原生iOS APP
---
经过笔者的亲测【 *将含有跳转原生APP的html文件链接以发送到微信，在从微信打开链接的形式，是不能跳转到原生APP的，但是可以选择以浏览器的形式打开此链接，以浏览器的形式打开链接是可以跳转到原生APP的* 】

经百度搜索得出：微信小程序支持跳转APP了【未进行过测试】
