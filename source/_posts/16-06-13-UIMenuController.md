title: UIMenuController UITextField 的功能(复制，剪切...)菜单
date: 2016-06-13 16:18:46
tags:
---
[参考原文](http://www.jianshu.com/p/ddd59867909a)
**苹果自带的UIMenuController功能扩展**


**下面实现的效果如下图 **
![自定义textField的MenuController](http://7xrirn.com1.z0.glb.clouddn.com/menuController-1.gif)

**下面代码是自定义UITextField类的.m文件，.h中为空，如用Category会影响到全文**
```
#import "menuController.h"
@implementation menuController
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender {
  UIMenuController *menuController = [UIMenuController sharedMenuController];
  UIMenuItem *item1 =
      [[UIMenuItem alloc] initWithTitle:@"你好" action:@selector(abc)];
  menuController.menuItems = @[ item1 ];
  NSLog(@"%@", NSStringFromSelector(action));
  if (action == @selector(cut:) || action == @selector(copy:) ||
      action == @selector(paste:) || action == @selector(abc) ||
      action == @selector(select:)) {
    return YES;
  }
  return NO;
}
- (void)cut:(nullable id)sender {
  NSLog(@"%s", __func__);
}
/**
 *  UIMenuItem 点击
 */
- (void)abc {
  self.text = [NSString stringWithFormat:@"%@你好", self.text];
}
@end
```
<!-- more -->
一、UIMenuController认识
---
  * 默认情况下，UITextView / UITextFiled / UIWebView 都有苹果自带的有UIMenuController功能
  * UITextFiled 的弹出菜单效果是系统自带的
  
二、UIMenuController基本使用
---
* ![自定义textField的MenuController](http://7xrirn.com1.z0.glb.clouddn.com/menuController-2.png)
* 如为指定控件添加该功能；我们可以自定义；
* 通过sharedMenuController获取单例对象；
* 必须手动设置弹窗菜单可见；
* 指定弹窗相对哪个View的哪个位置显示;
* 指定其显示方向（上下左右）；
* 指定Item多个（数组）；
* 
* 而且可以指定menuFrame；不仅如此，系统也提供了可以监听menu的通知（即将显示/完全显示、即将隐藏/完全隐藏、menu的frame改变）  

具体实现如下：
1. 获得菜单 menu
      UIMenuController *menu = [UIMenuController sharedMenuController];
2. 设置菜单最终显示的位置
  ```
   // 菜单最终显示的位置
  CGRect rect = CGRectMake(100, 100, 100, 100);
  [menu setTargetRect:rect inView:self.label];
  //
  // targetRect：menuController指向的矩形框
  //targetView：targetRect以targetView的左上角为坐标原点
  ```
3. 手动设置需要，显示菜单
      [menu setMenuVisible:YES animated:YES];
4. 必须要得通过第一响应者，来告诉MenuController它内部应该显示什么内容
  a.  让第一响应者，实现下面方法，来告诉显示内容，监听哪些操作action

```
/**
* 通过这个方法告诉UIMenuController它内部应该显示什么内容
* 返回YES，就代表支持action这个操作
*/
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender
{
  NSLog(@"%@", NSStringFromSelector(action));
   if (action == @selector(cut:)
      || action == @selector(copy:)
      || action == @selector(paste:)) {
      return YES; // YES ->  代表我们只监听 cut: / copy: / paste:方法
  }
  return NO; // 除了上面的操作，都不支持
}
// 打印如下：
2015-7-28 10:06:25.578 UIMenuController[4735:388013] cut:
2015-7-28 10:06:25.581 UIMenuController[4735:388013] copy:
2015-7-28 10:06:25.581 UIMenuController[4735:388013] select:
2015-7-28 10:06:25.582 UIMenuController[4735:388013] selectAll:
2015-7-28 10:06:25.582 UIMenuController[4735:388013] paste:
2015-7-28 10:06:25.582 UIMenuController[4735:388013] delete:
2015-7-28 10:06:25.582 UIMenuController[4735:388013] _promptForReplace:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _transliterateChinese:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _showTextStyleOptions:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _define:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _addShortcut:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _accessibilitySpeak:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _accessibilitySpeakLanguageSelection:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _accessibilityPauseSpeaking:
2015-7-28 10:06:25.583 UIMenuController[4735:388013] _share:
2015-7-28 10:06:25.584 UIMenuController[4735:388013] makeTextWritingDirectionRightToLeft:
2015-7-28 10:06:25.584 UIMenuController[4735:388013] makeTextWritingDirectionLeftToRight:
```
5. 设置第一响应者
  a.  前提是：必须要有第一响应者，让第一响应者，实现上面方法，告诉显示什么内容。实现下面方法，可以让某个视图或者控制器，成为第一响应者： **canBecomeFirstResponder**方法。

```
/**
* 说明控制器可以成为第一响应者
*/
- (BOOL)canBecomeFirstResponder
{
  return YES;
}
```

实现监听菜单内容的对应的action方法
```
 - (void)cut:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
- (void)copy:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
- (void)paste:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
```
监听到menu菜单的显示与隐藏与frame改变的通知
如下：监听menu即将显示的通知

1.注册通知监听
// 注册监听 菜单即将显示 通知
```
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(show:) name:UIMenuControllerWillShowMenuNotification object:nil];
```
2.实现监听到menu菜单显示调用方法
```
- (void)dealloc{
  // 移除监听通知
  [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```
3.dealloc方法中，移除通知监听
```
- (void)dealloc{
   // 移除监听通知
  [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```
设置menu支持中文，显示中文 ->修改软件应用支持中文
* ![自定义textField的MenuController](http://7xrirn.com1.z0.glb.clouddn.com/menuController-3.png)
* 解决方案：查看UIMenuController的头文件，我们发现有个属性menuItems数组，通过它我们可以增加额外的菜单项,自定义meun显示自己定义的文字

注意：
---
* 创建只能通过[UIMenuController sharedMenuController];单例方式获取，不能通过init方式创建，否则报如下错误
  **获得菜单 -> 回报如下错误**
      UIMenuController *menu = [[UIMenuController alloc] init]; 

      Terminating app due to uncaught exception 'NSInternalInconsistencyException',
      reason: 'There can only be one UIMenuController instance.'
      
三、应用
---
1. 如何给Label添加UIMenuController功能
  1.设置UILabel允许交互
  2.给UILabel添加手势，
  3.在UILabel手势监听方法中，创建UIMenuController-》menu
  4.设置menu位置，利用UIMenuController的对象方法setTargetRect: inView:方法来设置menu显示在在那个控件的那个位置
  6.显示menu, -》 menu setMenuVisible: animation:
  7.设置menu显示内容
  注意：得通过第一响应者，来告诉menu它内部显示什么内容。如果显示中文标题，就需要手动设置APP支持中文
  实现：
  7.1让label成为第一响应者（注意：不一定第一响应者必须是控制器）
  7.2设置menu显示menuItem，告诉menu可以显示什么内容。


```
#import "JPLabel.h"
@implementation JPLabel
- (void)awakeFromNib
{
   // 给Label添加手势
   [self addGestureRecognizer:[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(labelClick)]];
}
-  (void)initWithFrame:(CGRect)rect{
   if(self = [super initWithFrame:rect]){
      // 给Label添加手势 
      [self addGestureRecognizer:[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(labelClick)]];
   }
}
- (void)labelClick
{
    // 让label成为第一响应者
    [self becomeFirstResponder];
    // 获得菜单
    UIMenuController *menu = [UIMenuController sharedMenuController];
    // 设置菜单内容，显示中文，所以要手动设置app支持中文
    menu.menuItems = @[
                       [[UIMenuItem alloc] initWithTitle:@"顶" action:@selector(ding:)],
                       [[UIMenuItem alloc] initWithTitle:@"回复" action:@selector(reply:)],
                       [[UIMenuItem alloc] initWithTitle:@"举报" action:@selector(warn:)]
                       ];
    // 菜单最终显示的位置
    [menu setTargetRect:self.bounds inView:self];
    // 显示菜单
    [menu setMenuVisible:YES animated:YES];
}
#pragma mark - UIMenuController相关
/**
 * 让Label具备成为第一响应者的资格
 */
- (BOOL)canBecomeFirstResponder
{
    return YES;
}
/**
 * 通过第一响应者的这个方法告诉UIMenuController可以显示什么内容
 */
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender
{
    if ( (action == @selector(copy:) && self.text) // 需要有文字才能支持复制
        || (action == @selector(cut:) && self.text) // 需要有文字才能支持剪切
        || action == @selector(paste:)
        || action == @selector(ding:)
        || action == @selector(reply:)
        || action == @selector(warn:)) return YES;
    return NO;
}
#pragma mark - 监听MenuItem的点击事件
- (void)cut:(UIMenuController *)menu
{
    // 将label的文字存储到粘贴板
    [UIPasteboard generalPasteboard].string = self.text;
    // 清空文字
    self.text = nil;
}
- (void)copy:(UIMenuController *)menu
{
    // 将label的文字存储到粘贴板
    [UIPasteboard generalPasteboard].string = self.text;
}
- (void)paste:(UIMenuController *)menu
{
    // 将粘贴板的文字赋值给label
    self.text = [UIPasteboard generalPasteboard].string;
}
- (void)ding:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
- (void)reply:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
- (void)warn:(UIMenuController *)menu
{
    NSLog(@"%s %@", __func__, menu);
}
@end
```


