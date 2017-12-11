---
title: 解决UIWebView自动缓存导致页面不可刷新问题
date: 2017-12-11 13:32:35
tags:
---
问题描述
---
**用UIWebView加载h5页面，后台h5页面更改后，APP端并没有刷新/加载显示成最新页面**


UIWebview会自动缓存之前的CSS样式，这就导致了更改过webview的页面样式之后，
我们APP端再打开这个webView页面，发现页面的样式没有加载最新的。

```
//清除webView的缓存
[[NSURLCache sharedURLCache] removeAllCachedResponses];
```
<!-- more -->

我把上面的方法写到了页面将要消失的时候，清除UIWebview缓存的东西，
然后让H5开发更改了页面样式，重新打开页面并没有变化，关闭APP然后重启，
变了，不过也是不行啊这样的效果，然后我找到了下面的方法：

```
//清除请求
[[NSURLCache sharedURLCache] removeCachedResponseForRequest:self.request];
```

```
//清除cookies
NSHTTPCookie *cookie;
NSHTTPCookieStorage *storage = [NSHTTPCookieStorage sharedHTTPCookieStorage];
for (cookie in [storage cookies]) {
   [storage deleteCookie:cookie];
}
```

上面的方法写过之后也是没有任何的改进了，还是需要重启才有效果；（也就是上面所有的方法都没有解决问题）


具体描述和问题解决
---

**我在加载URL的时候，用的方法是：**
```
self.request = [[NSURLRequest alloc] initWithURL:[NSURL URLWithString:htmlString]];
```

**就是这个问题所在，导致了自动缓存，更改无效。**
**将创建NSURLRequest替换成如下方法即可：**

```
//加载请求的时候忽略缓存
self.request = [NSURLRequest requestWithURL:[NSURL URLWithString:htmlString] cachePolicy:NSURLRequestReloadIgnoringLocalCacheData timeoutInterval:5.0];
```


参考原文
---

作者：First灬DKS
链接：http://www.jianshu.com/p/f3019d511f36
來源：简书
