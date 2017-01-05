title: Swift-extension【扩展】
date: 2017-01-05 15:43:53
tags: Swift
---



## Swift-extension【扩展】

**扩展能够向已有的类、结构体，枚举或协议类型添加新的功能。这包括在没有权限获取原始代码的情况下扩展类型的能力【即逆向建模】。扩展类似于Objective-C中的分类【categories】，与Objective-C分类不同的是，Swift的extension没有名称，Objective-C中的Category只能扩展类(类别)**

*extension中的private方法不能被已有实现类调用*


Swift中的extension可以实现如下的所示的功能：

- 添加计算型属性和计算静态属性
- 定义实例方法和类型方法
- 提供新的构造器器
- 定义下标
- 定义和使用新的嵌套类型
- 使一个已有类型符合某个协议

<!-- more -->

## 计算型属性

*距离转换*

```swift
class IRTestController: UIViewController {
	override func viewDidLoad() {
		super.viewDidLoad()
		let aMarathon = 25.5.mm + 1.2.m
         print("A marathon is \(aMarathon) meters long")
	}
}
extension Double{
    var m : Double { return self }
    var mm : Double { return self / 1_000.0 }
}
```

在上述代码中，计算属性的含义是把一个Double型的值看作是某单位下的长度值，实现距离转换



## 构造器

扩展能向类中添加新的便利构造器，**不能向类中添加新的指定的构造器或析构造函数**。指定构造器和析构造函数必须由原始类实现提供

```swift
class IRTestController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        let rect = CGRect(center: CGPoint(x: 4.0,y: 4.0), size: CGSize(width: 3,height: 3))
        print(rect)
    }
}
extension CGRect {
    init(center: CGPoint,size: CGSize) {
        let originX = center.x - size.width * 0.5
        let originY = center.y - size.height * 0.5
        self.init( origin: CGPoint( x: originX, y: originY ) ,size: size 		)
    }
}
```

## 扩展方法

可以向已有类型添加新的实例方法和类型方法。

扩展增加的实例方法可以修改实例本身。结构体和枚举类型中的方法如果想要修改实例本身或者属性的话需要用`mutating`来修饰方法，所以扩展这样的方法也需要加`mutating`。

*向Int类型中添加一个名为repetions的新实例方法*

```swift
class IRTestController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        var num = 2
        num.repetions {
            print("irena")
        }
        num.square()
        print("\(num) square is \(num)")
    }
}
extension Int {
    /// 参数是一个单类型的闭包，没有参数，没有返回值的闭包 ()-()
    func repetions(task: () -> ()) {
        for _ in 1...self {
            task()
        }
    }
    /// 要修改self，就需要是可改类型方法，需要加上关键字mutating
    mutating func square() {
        self = self * self
    }
}
```

## 下标

扩展可以向一个已有类型添加新下标

*如果位数不足返回0*

```swift
class IRTestController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        print("\(289435733[3])")  //return 5
        print("\(2[3])")          //return 0
    }
}
extension Int {
    /// 下标[n]会返回十进制数字从右向左第n个数字
    subscript(index: Int) -> Int{
        var decimalBase = 1
        if index > 0 {
            for _ in 1...index {
                decimalBase *= 10
            }
        }
        return (self / decimalBase) % 10
    }
}
```

## 嵌套类型

```swift
class IRTestController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        printIntegerKinds([3, 19, -27, 0, -6, 0, 7])   // return  + + - 0 - 0 + 
    }
    func printIntegerKinds(_ numbers: [Int]) {
        for number in numbers {
            switch number.kind {
            case .negative:
                print("- ", terminator: "")
            case .zero:
                print("0 ", terminator: "")
            case .positive:
                print("+ ", terminator: "")
            }
        }
        print("")
    }
}
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}
```

