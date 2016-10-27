title: AngularJS标签
date: 2016-10-27 14:32:36
tags: AngularJS
---

通过 script 标签添加到网页中：
```
<script src="http://cdn.static.runoob.com/libs/angular.js/1.4.6/angular.min.js"></script>
```

ng-app指令
---
定义一个 AngularJS 应用程序HTML 文档中只允许有一个ng-app指令，如果有多个 ng-app 指令，则只有第一个会被使用，**ng-app** 指令用于告诉 AngularJS 应用当前这个元素是根元素。
指令在网页加载完毕时会自动引导（自动初始化）应用程序。


<!-- more -->

ng-model指令
---
ng-model 指令 绑定 HTML 元素 到应用程序数据。
把元素值（比如输入域的值）绑定到应用程序。
绑定输入框的值到scope变量中，**input, select, textarea** 标签支持该指令  

ng-model 指令也可以：
*	为应用程序数据提供类型验证（number、email、required）。
*	为应用程序数据提供状态（invalid、dirty、touched、error）。
*	为 HTML 元素提供 CSS 类。
*	绑定 HTML 元素到 HTML 表单。
     
     
```
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name" required>
    <h1>{{ name }}</h1>
</div>
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```

ng-bind指令
---
把应用程序数据绑定到 HTML 视图。
绑定 **标签p** 内的 innerHTML 到变量 myText: *具体看如下代码*

```
<div ng-app="" ng-init="myText='Hello World!'">
	<p ng-bind="myText"></p>
</div>
```

**属性**以 **ng-** 开头，但是您可以使用 **data-ng-** 来让网页对 **HTML5** 有效。
**表达式**写在双大括号内。

```
<!-- 直接输出表达式的值 -->
eg: {{5+5}}
<!--  -->
```

ng-controller指令
---
用于为你的应用添加控制器。
在控制器中，你可以编写代码，制作函数和变量，并使用 scope 对象来访问。  
      
```
<div ng-app="myApp" ng-controller="myCtrl">
	Full Name: {{firstName + " " + lastName}}
</div>
<script>
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope) {
        $scope.firstName = "John";
        $scope.lastName = "Doe";
    });
</script>
```

ng-init指令
---
ng-init 指令为 AngularJS 应用程序定义了 **初始值**。
通常情况下，**不使用 ng-init。您将使用一个控制器或模块来代替它。**


ng-repeat指令【循环】
---
re-repeat指令对于集合中(数组中)的每个项目会**克隆一次HTML元素**

**例子如下:**
```
	<!-- 循环对象 -->
	<div ng-app="" ng-init="names=[
			{name:'Jani',country:'Norway'},
			{name:'Kege',country:'Swden'},
			{name:'Kai',country:'Denmark'}
		]">
		<p>循环对象：</p>
		<ul>
			<li ng-repeat="x in names">
				{{ x.name + ',' + x.country}}
			</li>
		</ul>
	</div>
	<!-- -->
```

创建自定义的指令
---

```
	<!-- 自定义指令 --><!-- -->
	//元素名
	<runoob-directive></runoob-directive>
	//属性
	<div runoob-directive></div>
	//类名
	<div class="runoob-directive"></div>
	//注释
	<!-- directive: runoob-directive --><!-- -->
	<script>
		var app = angular.module("myApp",[]);
		app.directive("runoobDirective",function(){
			return{
				template : "<h1>自定义指令</h1>"
			};
		});
	</script>
```

**你可以通过以下方式来调用指令，也可以通过restrict的值限制使用：**
*	E作为元素名使用
*	A作为属性使用
*	C作为类名使用
*	M作为注释使用

限制使用
---

```
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        restrict : "A",
        template : "<h1>自定义指令!</h1>"
    };
});
```
**restrict 默认值为 EA, 即可以通过元素名和属性名来调用指令。**