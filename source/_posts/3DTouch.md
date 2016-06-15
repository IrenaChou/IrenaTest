title: iOS 3D Touch
date: 2016-04-11 18:05:15
tags:
---
3D Touch说明
---

**轻压和重压(Peek and Pop)
主屏幕快捷操作(Home Screen Quick Actions)**  

3D Touch 给 iOS 9 用户提供了一个新的交互维度。在所支持3DTouch的设备上，人们可以通过按压应用的图标去快速选择应用定制的操作。在应用内，人们可以使用多种按压操作去获取一个项目的预览，可以在独立的视图里打开一个项获取相关操作。(了解更多在你的代码中如何添加3D Touch支持，参阅 [Adopting 3D Touch on iPhone .](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/Adopting3DTouchOniPhone/index.html#//apple_ref/doc/uid/TP40016543))  

系统会自动安排图标在快速操作列表中的位置是在左侧或者在右侧，这依赖于你的应用的图标在用户主屏幕的位置。(摒除图标在列表中的位置，在自左向右的语言中文字总是左对齐。)这里有主屏快捷操作的多种展现方式的例子。  

**使用主屏幕快捷操作去开启引人注目的、高价值的任务。**例如，Maps可以让用户不需要打开Maps，通过在当前位置附近搜索就可以获得回家的方向。一个应用至少需要把一个有用的任务放在主屏幕快捷操作里；你可以提供最多四个快捷操作


![1](http://7xrirn.com1.z0.glb.clouddn.com/13.png)
**使用3D Touch必须要有6s或6s plus**

 3D Touch的三大模块
 ---
**home screen quick aactions**
1. 静态菜单［不需要写代码，在info.plist中配制］
2. 动态菜单［代码实现］
3. 菜单跳转

**peek and pop**
1. 轻度按压预览页面-peek
2. 大力按压跳转页面-pop
3. peek过程中的自定义操作

**force propertiesp**

  <!-- more -->
  
**home screen quick aactions**
1、静态菜单设置
---
[下载Demo](http://pan.baidu.com/s/1c1B13X2)
下图中带“＊”号的，key必须设置，值可以没有，如果没有设置，设置菜单的当前cell将不会被显示出来
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch1.png)
UIApplicationShortcutItems:
1.  **副标题**   保持标题的简洁不会被切断从而帮助用户快速理解操作是非常重要的。如果你提供的副标题一行显示不全，系统会截断；如果你没有副标题，系统会把一行展示不完全的长标题以两行展现。
2.  **图标**  UIApplicationShortcutItemIconType 显示的
    iconType可以参考如下链接和下图**(如需swfit去下面链接中查看)**
    [iconType](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIApplicationShortcutIcon_Class/index.html#//apple_ref/c/tdef/UIApplicationShortcutIconType)
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch2.png)
    **当UIApplicationShortcutItemIconType和UIApplicationShortcutItemIconFile两个都设置的时候
    UIApplicationShortcutItemIconFile的优先级高于UIApplicationShortcutItemIconType**




 在项目中的info.plist中的配制示例如下图
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch3.png) 
效果如下图
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch4.png) 

2､动态菜单及跳转
---
[下载Demo](http://pan.baidu.com/s/1c1B13X2)
代码如下
```
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  /**
   *  3D Touch 动态菜单
   *  其中一个item就是一个菜单项
   */
  UIApplicationShortcutItem *shortcutItem1 =
      [[UIApplicationShortcutItem alloc] initWithType:@"type1"
                                       localizedTitle:@"列表"];
  //使用系统图标
  //  UIApplicationShortcutIcon *icon2 = [UIApplicationShortcutIcon
  //      iconWithType:UIApplicationShortcutIconTypeHome];
  //使用自定义图标
  //  UIApplicationShortcutIcon *icon2 =
  //      [UIApplicationShortcutIcon iconWithTemplateImageName:@""];
  /**
   不设置icon,Title默认靠右
   */
  UIApplicationShortcutItem *shortcutItem2 = [[UIApplicationShortcutItem alloc]
           initWithType:@"type2"
         localizedTitle:@"force touch"
      localizedSubtitle:@"subtitle 2subtitle 2"
                   icon:[UIApplicationShortcutIcon
                            iconWithTemplateImageName:@""]
               userInfo:nil];
 //  /**
  //   让title默认靠左，但不显示icon
  //   只要在一个cell中设置其它的title都会靠左显示
  //   */
  //  UIApplicationShortcutItem *shortcutItem3 = [[UIApplicationShortcutItem
  //  alloc]
  //           initWithType:@""
  //         localizedTitle:@"force touch"
  //      localizedSubtitle:@"subtitle 2subtitle 2"
  //                   icon:[UIApplicationShortcutIcon
  //                            iconWithTemplateImageName:@""]
  //               userInfo:nil];
  [UIApplication sharedApplication].shortcutItems =
      @[ shortcutItem1, shortcutItem2 ];  //, shortcutItem3
  return YES;
}
```
```
//点击3D Touch 跳到指定的控制器
/**
 *  点击item菜单会调用此方法
 *
 *  @param application
 *  @param shortcutItem      被点击的item
 *  @param completionHandler
 */
- (void)application:(UIApplication *)application
    performActionForShortcutItem:(UIApplicationShortcutItem *)shortcutItem
               completionHandler:(void (^)(BOOL))completionHandler {
  //第一个启动的storyboard所指向的是window的根控制器
  //获取tabbarctrl
  UITabBarController *tabBarCtrl =
      (UITabBarController *)application.keyWindow.rootViewController;
  if ([shortcutItem.type isEqualToString:@"type1"]) {
    //点击了列表
    tabBarCtrl.selectedIndex = 1;
  } else if ([shortcutItem.type isEqualToString:@"type2"]) {
    //点击froce
    tabBarCtrl.selectedIndex = 0;
  }
}
```
两种显示效果如下图
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch5.png)
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch6.png)

**peek and pop**
---
[下载Demo](http://pan.baidu.com/s/1hsnmYPm)
**peek代码**
注意点:
1. ndexPathForRowAtPoint获取到的是以当前cell为0,0点的位置，而不是以tableview为0,0点
2. 此处的方法一定要看清楚，不是convertPoint:toView:是convertPoint:fromView:  
```
首先要实现UIViewControllerPreviewingDelegate协议
/**
 *  peek
 *
 *  @param previewingContext 包含被选中对象的所有信息
 *  @param location          被选中对象手指所在的location
 */
- (nullable UIViewController *)
        previewingContext:(id<UIViewControllerPreviewing>)previewingContext
viewControllerForLocation:(CGPoint)location {
  // indexPathForRowAtPoint获取到的是以当前cell为0,0点的位置
  //我们需要的是从tableview顶部为0,0点的位置，才可以获取到当前被选中的cell
  //获取以cell为0,0点的坐标
  //  NSIndexPath *indexPath = [self.tableView indexPathForRowAtPoint:location];
  //转化坐标
  //  此处的方法一定要看清楚，不是convertPoint:toView:是convertPoint:fromView:
  //  location = [self.tableView convertPoint:location
  //                                   toView:[previewingContext sourceView]];
  location = [self.tableView convertPoint:location
                                 fromView:[previewingContext sourceView]];
  NSIndexPath *indexPath = [self.tableView indexPathForRowAtPoint:location];
  //根据cell获取数组中的数据
  id abc = self.items[indexPath.row];
  IrenaPre *pre = [[IrenaPre alloc] init];
  pre.item = abc;
  return pre;
}
```
**自定义peek代码**
---

```
//peek 过程中的自定义操作
- (NSArray<id<UIPreviewActionItem>> *)previewActionItems {
  //创建点赞操作
  UIPreviewAction *item1 = [UIPreviewAction
      actionWithTitle:@"赞"
                style:UIPreviewActionStyleDefault
              handler:^(UIPreviewAction *_Nonnull action,
                        UIViewController *_Nonnull previewViewController) {
                NSLog(@"赞了");
              }];
  //创建点赞操作
  UIPreviewAction *item2 = [UIPreviewAction
      actionWithTitle:@"举报"
                style:UIPreviewActionStyleDestructive
              handler:^(UIPreviewAction *_Nonnull action,
                        UIViewController *_Nonnull previewViewController) {
                NSLog(@"举报了");
              }];
   //
   //添加group的效果可运行看看
  //
  UIPreviewActionGroup *group =
      [UIPreviewActionGroup actionGroupWithTitle:@"group"
                                           style:UIPreviewActionStyleDefault
                                         actions:@[ item1, item2 ]];
  //  return @[ group ];
  return @[ item1, item2 ];
}

```
**自定义peek后的**
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch8.png)
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch9.png)
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch10.png)

pop
---
**pop是在点出peek后在用力按压一下屏幕后出现的**
```
/**
 *  pop
 *
 *  @param previewingContext      包含被选中对象的所有信息
 *  @param viewControllerToCommit peek返回的controller
 */
- (void)previewingContext:(id<UIViewControllerPreviewing>)previewingContext
     commitViewController:(UIViewController *)viewControllerToCommit {
  //跳转到peek的controller
  // animated在pop时无效
  [self.navigationController pushViewController:viewControllerToCommit
                                       animated:YES];
}
```

效果如下图
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch11.png)

**force**
---
[下载Demo](http://pan.baidu.com/s/1hsnmYPm)
按压力度，值范围［0-6.666667］
代码主要在demo中的IrenaForce.h/.m类
**代码如下**
```
#import "IrenaForce.h"
@interface IrenaForce ()
@property(nonatomic, strong) UIBezierPath *path;
@end
@implementation IrenaForce
- (void)drawRect:(CGRect)rect {
  [[UIColor orangeColor] set];
  [self.path fill];
}
- (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
  //获取触摸对象
  UITouch *touch = [touches anyObject];
  NSLog(@"%lf", touch.force);
  //创建路径
  //根据压力*系数 手指的位置为圆心画圆
  UIBezierPath *path = [[UIBezierPath alloc] init];
  [path addArcWithCenter:[touch locationInView:self]
                  radius:touch.force * 20
              startAngle:0
                endAngle:2 * M_PI
               clockwise:YES];
  self.path = path;
  //重绘
  [self setNeedsDisplay];
}
@end
```

效果如下
![1](http://7xrirn.com1.z0.glb.clouddn.com/3D Touch12.png)

