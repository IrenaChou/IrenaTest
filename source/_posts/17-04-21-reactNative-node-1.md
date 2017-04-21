---
title: ReactNativeNode
date: 2017-04-21 17:09:14
tags: 'ReactNative'
---

node1
---
**问题描述：**

在终端执行如下命令时
*npm install --save react-redux/npm install --save redux-thunk*

报如下错误：
**UNMET PEER DEPENDENCY redux@^2.0.0 || ^3.0.0**

**问题解决：**
---
*这只是缺少依懒模块*
```
npm install --save redux-logger
npm install --save redux-thunk
```
<!-- more -->
**问题参考链接：**
http://stackoverflow.com/questions/41505664/getting-error-on-implementing-react-native-with-react-redux



node2
----
**问题描述：**
执行 **npm install --save redux-logger**
 *└── UNMET PEER DEPENDENCY react@^0.13.0 || ^0.14.0 || ^15.0.0*  


**问题解决：**
*版本过底，使用如下信不信*
```
npm install npm -g
```

**问题参考链接：**
http://stackoverflow.com/questions/32985495/react-router-peerdependencies-error


node3
---
**问题描述：**
在通过react-native run-ios运行reactnative运行项目的时候报如下错误
![问题详情](http://7xrirn.com1.z0.glb.clouddn.com
/reactnativenode3.png)

**No bundle URL present
Make sure you’re running a packager server or have included a .jsbundle file in your application bundle**

**问题解决：**
*关掉翻墙软件*
我是使用shadowocks，将全局代理必成自动代理。
我是可以的，如果还是不行关掉shadowocks

**问题参考链接：**
http://www.crifan.com/react_native_ios_run_again_error_no_bundle_url_present/
