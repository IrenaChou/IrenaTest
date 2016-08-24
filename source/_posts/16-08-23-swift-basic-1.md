title: Swift基础1
date: 2016-08-23 17:44:47
tags: Swift
---

**Swift中取余运算符可用于浮点型**
**Swift3 取消了'++'，'--'**


第一个问题：
---
        Property 'self.test' not initialized at super.init call

![问题](http://7xrirn.com1.z0.glb.clouddn.com/blog_photoswift_base_error1.png)

<!-- more -->  

解答：
---
**Swift中定义的属性必须要满足以下两者之一，如果没有满足以下二者之一，就会报如下错误
  **一：可以为空  **
  ```
  private var test : Int?
  ```
  
  **二：有初使值**
  ```
  internal var test : Int = 5
  ```



第二个问题：
---
        为UIButton添加点击事件时，func转selector问题

解答：
---
```
let testBtn = UIButton.init()
testBtn.addTarget(self, action:#selector(ViewController.test(_:)), forControlEvents: UIControlEvents.TouchUpInside)
/**
按钮点击调用函数
- parameter sender: 被点击的按钮
 */
@objc
private func test(sender:UIButton) {
    print("aaa")
}
```