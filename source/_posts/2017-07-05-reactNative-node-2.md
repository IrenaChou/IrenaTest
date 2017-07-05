---
title: ReactNativeNode
date: 2017-07-05 14:05:08
tags: 'ReactNative'
---

Print: Entry, ":CFBundleIdentifier", Does Not Exist
---
在终端执行如下命令时：
*react-native run-ios*

报如下错误：
```
Failed to install the requested application
An application bundle was not found at the provided path.
Provide a valid path to the desired application bundle.
Print: Entry, ":CFBundleIdentifier", Does Not Exist

Command failed: /usr/libexec/PlistBuddy -c Print:CFBundleIdentifier build/Build/Products/Debug-iphonesimulator/ReactNativexx.app/Info.plist
Print: Entry, ":CFBundleIdentifier", Does Not Exist
```

**问题解决：**
这是经过各种尝试后得出的结果了，查看的下面的链接，给出的前几个方法结过测试都不能解决我的问题，只有下面的的方法是可以的

**解决步骤**：
1.  首先删除node_modules  
2.  修改package.json中react-native的版本为0.44.3 react为16.0.0-alpha.6
3.  react-native run-ios 就可以了

问题参考链接：
http://www.jianshu.com/p/98c8f2a970eb
