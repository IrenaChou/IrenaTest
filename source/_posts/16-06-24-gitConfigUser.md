title: git 用户名配制
date: 2016-06-24 17:27:07
tags:
---
设置单个仓库用户名和邮箱
``` bash
$  git config user.name "xxx@xxx.com"
$  git config user.email "xxx@xxx.com"
```

设置全局用户名和邮箱
``` bash
$  git config --global user.email "xxx@gmail.com"
$  git config --global user.name "xxx"
```

<!-- more -->
写这篇文章主要是为了记录前两天遇到的问题，当时博客是放在github上的，使用的用户名和邮箱与公司仓库的用户名与邮箱不同，使我陷入了申请SSH公钥的困惑中（我测试的结果是最终有效的SSH公钥只能是最后申请的SSH，导致我不能同时使用博客和公司代码仓库）。

**我的解决办法：**
我博客使用SSH，配置这个仓库的用户名和邮箱（不使用全局用户名，邮箱）  
公司仓库使用HTTP协议，无需申请SSH公钥，使用全局用户名和邮箱，或是单独配置都可以