title: 问题记录
date: 2016-03-01 14:09:39
tags:
---

如下错误是没有rootViewController，我平时并不这么写   
```
- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  // Override point for customization after application launch.
  self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
  [self.window addSubview:controller.view];
  [self.window makeKeyAndVisible];
  return YES;
}
```
错误：
```
*** Assertion failure in -[UIApplication _runWithMainScene:transitionContext:completion:], /BuildRoot/Library/Caches/com.apple.xbs/Sources/UIKit/UIKit-3512.30.14/UIApplication.m:3315
*** Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'Application windows are expected to have a root view controller at the end of application launch'
*** First throw call stack:
(0x1821c5900 0x181833f80 0x1821c57d0 0x182b3899c 0x187160ac0 0x18715d5c0 0x18377b790 0x18377bb10 0x18217cefc 0x18217c990 0x18217a690 0x1820a9680 0x186f26580 0x186f20d90 0x1000de108 0x181c4a8b8)
libc++abi.dylib: terminating with uncaught exception of type NSException
```

解决方法：  
---------
设置rootViewController  
```
[self.window setRootViewController:[UIViewController new]];
```