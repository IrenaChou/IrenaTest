---
title: url百分号转义
date: 2018-01-17 10:23:51
tags:
---

百分号转义就是将一些特殊字符以 **%25** 类似这种的形式标识

转义
---
在iOS中，笔者一般在进行加载url显示之前，会以如下代码进行转义一下
```
// urlString 为原始的url字符串，需要通过一个字符串来接受转义后的url字符串
NSString *requestURL = [urlString stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding]
```

<!-- more -->
恢复
---
近期笔者突然发现，后台传给我的url有转义过的情况，如果我在将这串url进行转义，那拿去加载的字符串就会有问题了，所以笔者先将后台传给我的url移除转义，在进行转义【因为后台穿过来的链接是有的转义了，有的没转义】

```
// urlString是后台传过来的url，去除转义后需要接收
urlString = [urlString stringByRemovingPercentEncoding];
```
