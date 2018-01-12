---
title: iOS调用系统打电话
date: 2018-01-12 16:34:10
tags:
---

iOS调用系统打电话的方式有多种，此文主要说一下在iOS10以上弹出框变慢的问题

这是以前笔者习惯使用的方法，笔者并不经常使用调起系统打电话功能，前一阵发现在iOS11上弹出框变的很慢，找到解决方法后记录一下
```
UIWebView *callWebview = [[UIWebView alloc] init];
NSMutableString *urlStr = [[NSMutableString alloc] initWithFormat:@"tel:%@",@"10010"];
[callWebview loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:urlStr]]];
[self.view addSubview:callWebview];
```

<!-- more -->

解决办法【换成如下的代码】：
```
NSString *callPhone = [NSString stringWithFormat:@"telprompt://%@", @"10010"];
[[UIApplication sharedApplication] openURL:[NSURL URLWithString:callPhone] options:@{} completionHandler:nil];
```
