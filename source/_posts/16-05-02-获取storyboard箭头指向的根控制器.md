title: 获取storyboard箭头指向的根控制器
date: 2016-05-02 19:56:16
tags:
---
```
/**
 *  通过名称获取storyboard箭头指向的根控制器
 *
 *  @param sbName storyboard名字
 *
 *  @return storyboard instantiateInitialViewController
 */
- (id)viewControllerWithSBName:(NSString*)sbName {
//获取程序的名字
  NSDictionary* info = [[NSBundle mainBundle] infoDictionary];
  NSString* prodName = [info objectForKey:@"CFBundleExecutable"];
  NSString* sbPath = [NSString stringWithFormat:@"%@/%@/", prodName, sbName];
  //  NSLog(@"%@", [[UIStoryboard
  //                   storyboardWithName:sbName
  //                               bundle:[[NSBundle alloc]
  //                               initWithPath:sbPath]]
  //                   instantiateInitialViewController]);
  return
      [[UIStoryboard storyboardWithName:sbName
                                 bundle:[[NSBundle alloc] initWithPath:sbPath]]
          instantiateInitialViewController];
}
```