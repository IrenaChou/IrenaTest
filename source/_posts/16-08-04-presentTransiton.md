title: iOS自定义Present转场动画
date: 2016-08-04 16:49:01
tags:
---
每一个界面切换到另一个界面，都是不同场景之前的转换,场景的转换用的就是转场动画
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/transitioning.gif)  
<!-- more -->
自定义转场：
1.  设置自定义转场
        playerVC.modalPresentationStyle = UIModalPresentationCustom;
  ```
   /**
   系统转场效果
   *
   当从A场景过度到B场景，A场景消失，B场景会加到一个容器View中(UITransitionView)
   */
  // （设置系统自带转场）修改转场动画的动画效果
  playerVC.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
  ```
  
  ```
    /**
   *  自定义转场效果
   *    当从A场景过度到B场景，A场景不消失，B场景会加到一个容器View中(UITransitionView)
   *   如果设置了自定义转场，未实现转场效果，还会使用系统默认的转场动画
   */
  //    设置自定义转场动画
  playerVC.modalPresentationStyle = UIModalPresentationCustom;
  ```
2.  通过代理设置如何进行自定义转场
        playerVC.transitioningDelegate = self;
        [self presentViewController:playerVC animated:YES completion:nil];
3.  实现代理方法
         <UIViewControllerTransitioningDelegate>的代理方法，代码中会详细说明  
  
**UIViewControllerTransitioningDelegate**
```
/**
 *  弹出时执行的动画
 *  当A控制器转场到B控制器时，弹出
 *  @param presented  A控制器
 *  @param presenting B控制器
 *
 *  @return 当view呈现的时候，要通过哪个对象来执行方法
 */
- (nullable id<UIViewControllerAnimatedTransitioning>)
animationControllerForPresentedController:(UIViewController *)presented
                     presentingController:(UIViewController *)presenting
                         sourceController:(UIViewController *)source {
  //    返回一个对象
  IRAnimationPresentedProxy *presentedProxy =
      [[IRAnimationPresentedProxy alloc] init];
  return presentedProxy;
}
/**
 *  消失时执行的动画
 *  当B控制器消失时，消失
 *  @param dismissed B控制器
 *
 *  @return 控制器在dismiss时，要通过哪个对象来执行转场动画
 */
- (nullable id<UIViewControllerAnimatedTransitioning>)
animationControllerForDismissedController:(UIViewController *)dismissed {
  //    返回一个对象
  IRAnimationDismissedProxy *dismissedProxy =
      [[IRAnimationDismissedProxy alloc] init];
  return dismissedProxy;
}
  ```
**其他代码在Demo中提现，需要注意如下几点：**
  * B控制器旋转出来时anchorPoint必须在设置frame之前设置
  * 当转场动画方法执行完之后，必须调用此方法**[transitionContext completeTransition:YES];**，否则B控制器将无法监听任何事件
  * 其他具体代码看Demo
  
  
[Demo下载](http://7xrirn.com1.z0.glb.clouddn.com/codeIRTransitionAnimation.zip)