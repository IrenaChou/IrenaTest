title: UITouch-跟着手指走－判断point的范围
date: 2016-04-22 11:37:35
tags:
---
响应者对象  
--
    在iOS中不是任何对象都能处理事件,只有继承了UIResponder的对象才能接收并处理事件.我们称之为"响应者对象".

    UIApplication,UIViewController,UIView都继承自UIResponder,因此它们都是响应者对象,都能够接收并处理事件.

UIResponder
--
    UIResponder内部提供了方法来处理事件;
    > 触摸事件 
    一次完成的触摸过程,会经历3个状态;

UIView的触摸事件处理
--
    1、一根或多根手指开始触摸view,系统会自动调用view下面的方法:
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event;  //触摸开始
- 
    2、一根或者多根手指在view上移动，系统会自动调用view下面的方法（随着手指的移动，会持续调用该方法）:

- (void)touchesMoved:(NSSet *)touches withEvent:(UIEvent *)event;  //触摸移动
    3、一根或者多根手指离开view，系统会自动调用view下面的方法：  

- (void)touchesEnded:(NSSet *)touches withEvent:(UIEvent *)event;  //触摸结束
    4、触摸结束前，某个系统事件（例如电话呼入）会打断触摸过程，系统会自动调用view下面的方法

- (void)touchesCancelled:(NSSet *)touches withEvent:(UIEvent *)event; //触摸取消(可能会经历)
    4个触摸事件的处理方法中，都有 NSSet *touches 和 UIEvent *event 两个参数；

    1、一次完整的触摸过程，只会产生一个事件对象，4个触摸方法都是同一个event参数；

    2、如果两根手指同时触摸一个view，那么view只会调用一次 touchesBegan:withEvent: 方法，touches参数中装着两个UITouch对象；

    3、如果这两根手指一前一后分开触摸同一个view，那么view会分别调用两次 touchesBegan:withEvent:方法， 并且每次调用时的touches参数只包含一个UITouch对象；

    4、根据touches中UITouch个数可以判断出使单点触摸还是多点触摸。

    提示：touches中存放的都是UITouch对象。
    
    **下面提供一个简单的Demo，view跟着手指移动**
    [点击下载Demo](http://pan.baidu.com/s/1boOxFjh)
    
        
   ![1](http://7xrirn.com1.z0.glb.clouddn.com/ball-2.gif) 
    **下面提供一个简单的Demo，view由手指拖着走，并且不能超出屏幕范围**
    [点击下载Demo](http://pan.baidu.com/s/1i5CWzvn)    
<!-- more -->
UITouch类中包含如下成员函数：
--
当用户用一根手指触摸屏幕时，会创建一个与手指相关联的UITouch对象；一根手指对应一个UITouch对象；

UITouch的作用:
---

    保存跟手指相关的信息，比如触摸的位置、时间、阶段；

    当手指移动时，系统会更新同一个UITouch对象，使之能够一直保存该手指的触摸位置；

    当手指离开屏幕时，系统会销毁相应的UITouch对象。

    提示：iPhone开发中，要避免使用双击事件。
- (CGPoint)locationInView:(UIView *)view：函数返回一个CGPoint类型的值，表示触摸在view这个视图上的位置，这里返回的位置是针对view的坐标系的。调用时传入的view参数为空的话，返回的是触摸点在整个窗口的位置。
 
- (CGPoint)previousLocationInView:(UIView *)view：该方法记录了前一个坐标值，函数返回也是一个CGPoint类型的值， 表示触摸在view这个视图上的位置，这里返回的位置是针对view的坐标系的。调用时传入的view参数为空的话，返回的是触摸点在整个窗口的位置。

**可使用UITouch的如上两个方法判断方向**

      可使用这个方法，判断point的否在[self.ball frame]范围内
      if (CGRectContainsPoint([self.ball frame], point)){}

触摸事件的产生：
---

    1> 发生触摸事件后，系统会将该事件加入到一个由UIApplication管理的事件队列中；

    2> UIApplication会从事件队列中取出最前面的事件，并将事件分发下去以便处理，通常，先发送事件给应用程序的主窗口（keyWindow）；

    3> 主窗口会在视图层次结构中找到一个最合适的视图控件来处理触摸事件，这也是整个事件处理过程的第一步；

    4> 找到合适的视图控件后，就会调用视图控件的touches方法来做具体的事件处理。

触摸事件的传递：
---

    触摸事件的传递是从父控件传递到子控件；

    如果父控件不能接收触摸事件，那么子控件就不可能接收到触摸事件。

UIView不接收触摸事件的三种情况：
---

    1> 不接受用户交互 ：userInteractionEnable = NO;

    2> 隐藏 ：hidden = YES;

    3> 透明：alpha = 0.0 ~ 0.01
UIEvent
--
    每产生一个事件，就会产生一个UIEvent对象；
    UIEvent:称为事件对象，记录事件产生的时刻和类型。
    
<!-- more -->
![1](http://7xrirn.com1.z0.glb.clouddn.com/ball.gif)
```
#import "ViewController.h"
@interface ViewController ()
@property(weak, nonatomic) IBOutlet UIView *ball;
@end
@implementation ViewController
- (void)viewDidLoad {
  [super viewDidLoad];
  self.ball.userInteractionEnabled = NO;
}
- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
  UITouch *touch = [touches anyObject];
  CGPoint point = [touch locationInView:touch.view];
  _ball.center = point;
}
- (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
  UITouch *touch = [touches anyObject];
  CGPoint point = [touch locationInView:touch.view];
  _ball.center = point;
}
@end
```


