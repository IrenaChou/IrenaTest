---
title: iOS开发之模拟接口返回数据[转]
date: 2017-12-27 17:06:43
tags:
---

原文连接：https://www.ianisme.com/ios/2533.html

适用场景
----

我们在iOS开发的过程中，往往后端和前端都是并行的，后端一般都先给出接口文档，后续在进行实现维护，前端等到后台的数据是一个漫长的过程，当接口比较多的情况下，将测试全部放到后期是相对紧张的。

<!-- more -->
方法
---
下面我们以如下的JSON字段进行一下说明
```
{
  "code": 0,
  "message": "成功",
  "data": {
    "website":"https://www.ianisme.com",
    "list": [
      {
        "day": "30",
        "month": "10",
        "year": "2017"
      }
    ]
  }
}
```

搭建后台假数据
---
我们可以本地用搭建一个网站环境或者使用远程服务器去请求。
我会保存一个json文件，然后用一个php文件去调用。
```
<?php
header("Content-type: text/html; charset=utf-8");
$test = $_POST["s"];
$json_string = file_get_contents($test . '.json');
echo $json_string;
```
![图片说明](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception1.png)
![图片说明1](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception2.png)

这种情况下，我们可以直接把app端的网络请求代码全部写好，就相当于模仿后台的接口一样，到时候切换后台接口我们只需要更换下接口地址就行了。

代理拦截网络请求
---
这个是比较推荐的方案，不需要修改app端代码。一切无损对接后台。
这就是利用代理软件的 Map Local 功能，将请求转换为请求电脑本地的静态json文件。
我们以Charles为例，我们把本地的接口写好之后，我们使用Charles抓一下这个接口的请求，此时肯定是失败的。
如图：
![图片说明2](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception4.png)

我们去 Map Local 指向电脑中的一个json文件。
![图片说明3](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception5.png)
![图片说明4](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception6.png)
![图片说明5](https://www.ianisme.com/wp-content/uploads/2017/11/networkInterception7.png)
这样我们就将此接口指向了电脑本地的一个json文件，我们可以用此方法，将所有的接口都分别指向本地的各自的 json 文件，当后台接口完毕后，我们就可以关闭 Map Local 无缝衔接到真正的后台。

根据接口文档Mock数据
---

可以根据接口文档进行mock数据，相对来说还是方便些的
http://rap.taobao.org/
