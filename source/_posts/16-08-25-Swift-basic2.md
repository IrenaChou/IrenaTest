title: Swift基本语法2
date: 2016-08-25 15:38:08
tags: Swift
---
**Swift中如果使用十进制表示指数，需使用e/E表示幂e2表示10^2**

```
let num = 2e2    //输出打印num = 200.0
let num1 = 2e-2  //输出打印num = 0.2
```

<!-- more -->

**用十六进制表示指数，需用p/P表示幂，p2表示2^2**
```
let num = 0xAp2     // 40.0
let num1 = 0xAp-2   //2.5
```

**Swift中数字比较大的整数可以用‘_’分割，其实际意义不变**
```
let num = 2_234_500     //2234500
```

**将整数、浮点数等其它数据类型与字符串拼接可用'\()'**
```
let num = 3
let total = "\(num) 加 10 等于 \(num + 10)"
```

**switch条件表达式可以使用整数、浮点数、字符、字符串和元组等类型，
      case分支不需要显示地添加break语句，分支执行完成就会跳出case
      case可以是闭区间'...'和半闭区间'..'运算符
**
**元组switch**
```
  var student = (id:"1001",name:"李四",age:32)  
  switch student {
  case (_,_,let age) where age >= 32:     //case中使用where语句，进行条件过滤，类似SQL中的where
      if (age>30) {
          print("a")
      }else{
          print("b")
      }
  default:
      print("")
  }
```

**跳转语句**
**continue**同break使用相似，也可选择是否使用标签
**break**可选择是否带标签，如break,break label
默认情况下break只会跳出最近的内循环，带标签break会直接跳出指定标签的循环
```
        abc: for _ in 0  ..< 10 {
            for i in 0  ..< 10 {
                print(i)
                if i == 3 {
                    break abc
                }
            }
        }
```


**fallthrough**：是贯通语句，只能使用在switch语句中。
switch中的case默认不支持贯通，只有case中添加**fallthrough**的才可以贯通
```
  var j = 1
  switch j {
  case 1:
      j += 1
      print("1")
      fallthrough
  default:
      j += 1
      print("4")
  }
```

**数组：有序，可重复，不可变数组在访问效率上比可变数组高**
```
  var studentList1 : Array<String>   //<String>此数组是一个泛型数组，其中只能放字符串
  studentList1 = ["aa","bb"]         //初始化数组
  studentList1 += ["abc","aab"]      //数组可以使用+=添加数组
  studentList1.append("cc")          //想数组中添加单个元素，元素添加到数组最后一个元素的后面
  //移除数组中的元素
  studentList1.removeLast()
  studentList1.insert("a0", atIndex: 0)  //添加元素到制定下标
  studentList1.removeAtIndex(1)          //移除指定下标的元素
```

**字典：键不要重复，值可重复，键值无序，Swift中的集合都是结构体类型**
```
  let studentDictionary : Dictionary<Int,String> = [101:"aa",102:"bb"]
  //遍历
  for (stuId ,stuName) in studentDictionary {
      print("stuId: \(stuId) == stuName:\(stuName)")
  }
```


**函数的定义语法，函数可以重载**
    //**Swift中函数的返回值是用这种格式来的**
```
 private func testFunc()->CGPathRef{
    //函数体，函数的具体实现
    return xx.CGPath 
 }
 private :  函数的作用域
 func    :  函数的修饰符
 testFunc:  函数名
 ()      :  函数名后的这对小括号中间的为函数的参数列表【多个参数用'**,**'分割】
 //如果没有返回值，下面两个省略
 ->CGPathRef：  函数的返回值类型【返回值可以是单个或多个，多个用元组】
 return ：  函数的返回值，类型要和返回值类型一致
```
**函数的嵌套和函数作为返回值**
```
func calculate(opr:String) -> (Int,Int)->Int {
    func add(a:Int,b:Int)->Int{
        return a+b
    }
    var result : (Int,Int)->Int
    result = add
    return result
}
```

**闭包：**
```
var result : (Int,Int)->Int
  result = {$0 + $1}
  result = {(a:Int, b:Int)->Int in
      return a + b
  }
```


