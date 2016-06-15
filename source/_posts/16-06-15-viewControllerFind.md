title: 查找离自己最近的vc
date: 2016-06-15 16:46:54
tags:
---
```
/**
 *  查找离自己最近的一个父类vc(viewController)
 *
 *  @return 找到的vc
 */
- (UIViewController *)viewController {
  for (UIView *next = self.view.superview; next; next = next.superview) {
    UIResponder *nextResponder = [next nextResponder];
    if ([nextResponder isKindOfClass:[UIViewController class]]) {
      return (UIViewController *)nextResponder;
    }
  }
  return nil;
}
```