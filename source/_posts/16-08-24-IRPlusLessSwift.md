title: 加减控件IRPlusLessSwift
date: 2016-08-24 09:52:16
tags: Swift
---
**[Demo下载](https://github.com/IrenaChou/blogIRPlusLessSwift1.1.zip)**


效果展示
---
![要实现的效果](http://7xrirn.com1.z0.glb.clouddn.com/plusLess.gif)  

<!-- more -->
使用代码
---

```
import UIKit
class ViewController: UIViewController {    
    /// 定义属性
    var plusLessView : IRPlusLessView?
    override func viewDidLoad() {
        super.viewDidLoad()
        plusLessView = IRPlusLessView(frame: CGRect(x: 100,y: 100,width: 200,height: 50))
        plusLessView!.maxNum = 3
        plusLessView!.styleColor = UIColor.greenColor()
        self.view.addSubview(plusLessView!)
    }
```

*具体代码请下载Demo*