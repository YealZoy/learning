# Angularjs 表达式
+ AngularJs表达式写在双大括号内:{{expression}}
+ AngularJs表达式把数据绑定到HTML,可以使用ng-bind(一般首个页面加载使用ng-bind，以免客户刷新时看到{{}})

## AngularJs 数字
```html
<div ng-app="" ng-init="quantity=1;cost=5">
    <p>总价： {{ quantity * cost }} </p>
</div>
```

## AngularJs 字符串
```html
<div ng-app="" ng-init="firstName='John';lastName='Doe'">
    <p>姓名： {{ firstName + " " + lastName }}</p>
</div>
```

## AngularJs 对象
```html
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">
 
<p>姓为 {{ person.lastName }}</p>
 
</div>
```

## AngularJs 数组
```html
<div ng-app="" ng-init="points=[1,15,19,2,40]">
 
<p>第三个值为 {{ points[2] }}</p>
 
</div>
```

# AngularJs 指令（带有前缀ng-）
+ ng-app  指令初始化一个 AngularJS 应用程序。
+ ng-bind 绑定 HTML 元素到应用程序数据
+ ng-init 指令初始化应用程序数据。
+ ng-model 令把元素值（比如输入域的值）绑定到应用程序。
```html
<div ng-app="" ng-init="firstName='John'">
 
     <p>在输入框中尝试输入：</p>
     <p>姓名：<input type="text" ng-model="firstName"></p>
     <p>你输入的为： {{ firstName }}</p>
 
</div>
```

## 数据绑定
```html
<div ng-app="" ng-init="quantity=1;price=5">
 
<h2>价格计算器</h2>
 
数量： <input type="number"    ng-model="quantity">
价格： <input type="number" ng-model="price">
 
<p><b>总价：</b> {{ quantity * price }}</p>
 
</div>
```

## 重复 HTML 元素
```html
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <p>使用 ng-repeat 来循环数组</p>
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```

## 创建自定义的指令
可以使用 .directive 函数来添加自定义的指令。
```html
<body ng-app="myApp">

<runoob-directive></runoob-directive>

<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "<h1>自定义指令!</h1>"
    };
});
</script>

</body>
```

可以通过以下方式来调用指令：
+ 元素名 `<runoob-directive></runoob-directive>`
+ 属性 `<div runoob-directive></div>`
+ 类名 `<div class="runoob-directive"></div>` 
+ 注释 `<!-- directive: runoob-directive -->`

限制使用(通过添加 restrict 属性)
```javascript
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        restrict : "A",
        template : "<h1>自定义指令!</h1>"
    };
});
```

restrict 值可以是以下几种:
+ E 作为元素名使用
+ A 作为属性使用
+ C 作为类名使用
+ M 作为注释使用

# AngularJs 模型
```html
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```


## 双向绑定
```html
<div ng-app="myApp" ng-controller="myCtrl">
    名字: <input ng-model="name">
    <h1>你输入了: {{name}}</h1>
</div>
```

## 验证用户输入
```html
<form ng-app="" name="myForm">
    Email:
    <input type="email" name="myAddress" ng-model="text">
    <span ng-show="myForm.myAddress.$error.email">不是一个合法的邮箱地址</span>
</form>
```

## 应用状态
ng-model 指令可以为应用数据提供状态值(invalid, dirty, touched, error):
```html
<form ng-app="" name="myForm" ng-init="myText = 'test@runoob.com'">
    Email:
    <input type="email" name="myAddress" ng-model="myText" required></p>
    <h1>状态</h1>
    {{myForm.myAddress.$valid}}
    {{myForm.myAddress.$dirty}}
    {{myForm.myAddress.$touched}}
</form>
```

## CSS 类
```html
<style>
input.ng-invalid {
    background-color: lightblue;
}
</style>
<body>

<form ng-app="" name="myForm">
    输入你的名字:
    <input name="myAddress" ng-model="text" required>
</form>
```

# AngularJs Scope(作用域)
```html
<div ng-app="myApp" ng-controller="myCtrl">
    <input ng-model="name">
    <h1>{{greeting}}</h1>
    <button ng-click='sayHello()'>点我</button>    
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "Runoob";
    $scope.sayHello = function() {
        $scope.greeting = 'Hello ' + $scope.name + '!';
    };
});
</script>
```

# 根作用域
```html
<div ng-app="myApp" ng-controller="myCtrl">

<h1>{{lastname}} 家族成员:</h1>

<ul>
    <li ng-repeat="x in names">{{x}} {{lastname}}</li>
</ul>

</div>

<script>
var app = angular.module('myApp', []);

app.controller('myCtrl', function($scope, $rootScope) {
    $scope.names = ["Emil", "Tobias", "Linus"];
    $rootScope.lastname = "Refsnes";
});
</script>
```

# AngularJS 控制器
```html
<div ng-app="myApp" ng-controller="myCtrl">

名: <input type="text" ng-model="firstName"><br>
姓: <input type="text" ng-model="lastName"><br>
<br>
姓名: {{firstName + " " + lastName}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```

应用解析：
+ AngularJS 应用程序由 ng-app 定义。应用程序在 <div> 内运行。
+ ng-controller="myCtrl" 属性是一个 AngularJS 指令。用于定义一个控制器。
+ myCtrl 函数是一个 JavaScript 函数。
+ AngularJS 使用$scope 对象来调用控制器。
+ 在 AngularJS 中， $scope 是一个应用对象(属于应用变量和函数)。
+ 控制器的 $scope （相当于作用域、控制范围）用来保存AngularJS Model(模型)的对象。
+ 控制器在作用域中创建了两个属性 (firstName 和 lastName)。
+ ng-model 指令绑定输入域到控制器的属性（firstName 和 lastName）。

# AngularJS 过滤器
+ currency    格式化数字为货币格式。
+ filter  从数组项中选择一个子集。
+ lowercase   格式化字符串为小写。
+ orderBy 根据某个表达式排列数组。
+ uppercase   格式化字符串为大写。

## 表达式中添加过滤器
过滤器可以通过一个管道字符（|）和一个过滤器添加到表达式中。
```html
<div ng-app="myApp" ng-controller="personCtrl">

<p>姓名为 {{ lastName | uppercase }}</p>

</div>
```

## 向指令添加过滤器
过滤器可以通过一个管道字符（|）和一个过滤器添加到指令中。
```html
<div ng-app="myApp" ng-controller="namesCtrl">

<ul>
  <li ng-repeat="x in names | orderBy:'country'">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>

</div>
```

## 过滤输入
输入过滤器可以通过一个管道字符（|）和一个过滤器添加到指令中，该过滤器后跟一个冒号和一个模型名称。
```html
<div ng-app="myApp" ng-controller="namesCtrl">

<p><input type="text" ng-model="test"></p>

<ul>
  <li ng-repeat="x in names | filter:test | orderBy:'country'">
    {{ (x.name | uppercase) + ', ' + x.country }}
  </li>
</ul>

</div>
```

# AngularJS 服务(Service)
在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。
AngularJS 内建了30 多个服务。
有个 $location 服务，它可以返回当前页面的 URL 地址。
```javascript
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $location) {
    $scope.myUrl = $location.absUrl();
});
```

## $http 服务
$http 是 AngularJS 应用中最常用的服务。 服务向服务器发送请求，应用响应服务器传送过来的数据。
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
    $http.get("welcome.htm").then(function (response) {
        $scope.myWelcome = response.data;
    });
});
```

## $timeout 服务
AngularJS $timeout 服务对应了 JS window.setTimeout 函数。
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
    $scope.myHeader = "Hello World!";
    $timeout(function () {
        $scope.myHeader = "How are you today?";
    }, 2000);
});
```

## $interval 服务
AngularJS $interval 服务对应了 JS window.setInterval 函数。
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
    $scope.theTime = new Date().toLocaleTimeString();
    $interval(function () {
        $scope.theTime = new Date().toLocaleTimeString();
    }, 1000);
});
```

## 创建自定义服务
你可以创建访问自定义服务，链接到你的模块中：
```javascript
app.service('hexafy', function() {
    this.myFunc = function (x) {
        return x.toString(16);
    }
});
```

```javascript
app.controller('myCtrl', function($scope, hexafy) {
    $scope.hex = hexafy.myFunc(255);
});
```

## 过滤器中，使用自定义服务
```javascript
app.filter('myFormat',['hexafy', function(hexafy) {
    return function(x) {
        return hexafy.myFunc(x);
    };
}]);
```

# AngularJS Select(选择框)
AngularJS 可以使用数组或对象创建一个下拉列表选项。
```html
<div ng-app="myApp" ng-controller="myCtrl">
 
<select ng-init="selectedName = names[0]" ng-model="selectedName" ng-options="x for x in names">
</select>
 
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.names = ["Google", "Runoob", "Taobao"];
});
</script>
```

## 数据源为对象
使用对象作为数据源, x 为键(key), y 为值(value):
```javascript
$scope.sites = {
    site01 : "Google",
    site02 : "Runoob",
    site03 : "Taobao"
};
```


```html
<select ng-model="selectedSite" ng-options="x for (x, y) in sites">
</select>

<h1>你选择的值是: {{selectedSite}}</h1>
```

# AngularJS 表格
```html
<div ng-app="myApp" ng-controller="customersCtrl"> 

    <table>
        <tr ng-repeat="x in names">
            <td>{{ $index + 1 }}</td>
            <td ng-if="$odd" style="background-color:#f1f1f1">{{ x.Name }}</td>
            <td ng-if="$even">{{ x.Name }}</td>
            <td ng-if="$odd" style="background-color:#f1f1f1">{{ x.Country }}</td>
            <td ng-if="$even">{{ x.Country }}</td>
        </tr>
    </table>

</div>

<script>
var app = angular.module('myApp', []);
app.controller('customersCtrl', function($scope, $http) {
    $http.get("/try/angularjs/data/Customers_JSON.php")
    .success(function (response) {$scope.names = response.records;});
});
</script>
```

# AngularJS HTML DOM

## ng-disabled 指令
ng-disabled 指令直接绑定应用程序数据到 HTML 的 disabled 属性。
```html
<div ng-app="" ng-init="mySwitch=true">

<p>
<button ng-disabled="mySwitch">点我!</button>
</p>

<p>
<input type="checkbox" ng-model="mySwitch">按钮
</p>

<p>
{{ mySwitch }}
</p>

</div>
```

## ng-show 指令
ng-show 指令隐藏或显示一个 HTML 元素。
```html
<div ng-app="">

<p ng-show="true">我是可见的。</p>

<p ng-show="false">我是不可见的。</p>

</div>
```

## ng-hide 指令
ng-hide 指令用于隐藏或显示 HTML 元素。
```html
<div ng-app="">

<p ng-hide="true">我是不可见的。</p>

<p ng-hide="false">我是可见的。</p>

</div>
```

# AngularJS 模块

## 创建模块
你可以通过 AngularJS 的 angular.module 函数来创建模块：
```html
<div ng-app="myApp">...</div>

<script>

var app = angular.module("myApp", []); 

</script>
```
"myApp" 参数对应执行应用的 HTML 元素。

## 添加控制器
```html
<div ng-app="myApp" ng-controller="myCtrl">
{{ firstName + " " + lastName }}
</div>

<script>

var app = angular.module("myApp", []);

app.controller("myCtrl", function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});

</script>
```

## 添加指令
```html
<div ng-app="myApp" runoob-directive></div>

<script>

var app = angular.module("myApp", []);

app.directive("runoobDirective", function() {
    return {
        template : "我在指令构造器中创建!"
    };
});
</script>

```

## AngularJS 输入验证
```html
<!DOCTYPE html>
<html>
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
<body>

<h2>Validation Example</h2>

<form  ng-app="myApp"  ng-controller="validateCtrl"
name="myForm" novalidate>

<p>用户名:<br>
  <input type="text" name="user" ng-model="user" required>
  <span style="color:red" ng-show="myForm.user.$dirty && myForm.user.$invalid">
  <span ng-show="myForm.user.$error.required">用户名是必须的。</span>
  </span>
</p>

<p>邮箱:<br>
  <input type="email" name="email" ng-model="email" required>
  <span style="color:red" ng-show="myForm.email.$dirty && myForm.email.$invalid">
  <span ng-show="myForm.email.$error.required">邮箱是必须的。</span>
  <span ng-show="myForm.email.$error.email">非法的邮箱。</span>
  </span>
</p>

<p>
  <input type="submit"
  ng-disabled="myForm.user.$dirty && myForm.user.$invalid ||
  myForm.email.$dirty && myForm.email.$invalid">
</p>

</form>

<script>
var app = angular.module('myApp', []);
app.controller('validateCtrl', function($scope) {
    $scope.user = 'John Doe';
    $scope.email = 'john.doe@gmail.com';
});
</script>

</body>
</html>
```

+ $dirty  表单有填写记录
+ $valid  字段内容合法的
+ $invalid    字段内容是非法的
+ $pristine   表单没有填写记录

# AngularJS API
## AngularJS 全局 API

API 描述
+ angular.lowercase() 转换字符串为小写
+ angular.uppercase() 转换字符串为大写
+ angular.isString()  判断给定的对象是否为字符串，如果是返回 true。
+ angular.isNumber()  判断给定的对象是否为数字，如果是返回 true。

# AngularJS 包含
```html
<body ng-app="">
 
<div ng-include="'runoob.htm'"></div>
 
</body>
```

## 跨域包含
```html
<body ng-app="myApp">
 
<div ng-include="'http://c.runoob.com/runoobtest/angular_include.php'"></div>
 
<script>
var app = angular.module('myApp', [])
app.config(function($sceDelegateProvider) {
    $sceDelegateProvider.resourceUrlWhitelist([
        'http://c.runoob.com/runoobtest/**'
    ]);
});
</script>
 
</body>
```

# AngularJS 动画
AngularJS 提供了动画效果，可以配合 CSS 使用。
AngularJS 使用动画需要引入 angular-animate.min.js 库。
```html
<body ng-app="myApp">

<h1>隐藏 DIV: <input type="checkbox" ng-model="myCheck"></h1>

<div ng-hide="myCheck"></div>

<script>
var app = angular.module('myApp', ['ngAnimate']);
</script>
```

# AngularJS 依赖注入
AngularJS 提供很好的依赖注入机制。以下5个核心组件用来作为依赖注入：
+ value
+ factory
+ service
+ provider
+ constant

## value
```javascript
// 定义一个模块
var mainApp = angular.module("mainApp", []);

// 创建 value 对象 "defaultInput" 并传递数据
mainApp.value("defaultInput", 5);
...

// 将 "defaultInput" 注入到控制器
mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
   $scope.number = defaultInput;
   $scope.result = CalcService.square($scope.number);
   
   $scope.square = function() {
      $scope.result = CalcService.square($scope.number);
   }
});
```


## factory
factory 是一个函数用于返回值。在 service 和 controller 需要时创建。
通常我们使用 factory 函数来计算或返回值。
```javascript
// 定义一个模块
var mainApp = angular.module("mainApp", []);

// 创建 factory "MathService" 用于两数的乘积 provides a method multiply to return multiplication of two numbers
mainApp.factory('MathService', function() {
   var factory = {};
   
   factory.multiply = function(a, b) {
      return a * b
   }
   return factory;
}); 

// 在 service 中注入 factory "MathService"
mainApp.service('CalcService', function(MathService){
   this.square = function(a) {
      return MathService.multiply(a,a);
   }
});
...
```

## provider
AngularJS 中通过 provider 创建一个 service、factory等(配置阶段)。
Provider 中提供了一个 factory 方法 get()，它用于返回 value/service/factory。
```javascript
// 定义一个模块
var mainApp = angular.module("mainApp", []);
...

// 使用 provider 创建 service 定义一个方法用于计算两数乘积
mainApp.config(function($provide) {
   $provide.provider('MathService', function() {
      this.$get = function() {
         var factory = {};  
         
         factory.multiply = function(a, b) {
            return a * b; 
         }
         return factory;
      };
   });
});
```

## constant
constant(常量)用来在配置阶段传递数值，注意这个常量在配置阶段是不可用的。
```javascript
mainApp.constant("configParam", "constant value");
```

```html
<html>
   
   <head>
      <meta charset="utf-8">
      <title>AngularJS  依赖注入</title>
   </head>
   
   <body>
      <h2>AngularJS 简单应用</h2>
      
      <div ng-app = "mainApp" ng-controller = "CalcController">
         <p>输入一个数字: <input type = "number" ng-model = "number" /></p>
         <button ng-click = "square()">X<sup>2</sup></button>
         <p>结果: {{result}}</p>
      </div>
      
      <script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
      
      <script>
         var mainApp = angular.module("mainApp", []);
         
         mainApp.config(function($provide) {
            $provide.provider('MathService', function() {
               this.$get = function() {
                  var factory = {};
                  
                  factory.multiply = function(a, b) {
                     return a * b;
                  }
                  return factory;
               };
            });
         });
            
         mainApp.value("defaultInput", 5);
         
         mainApp.factory('MathService', function() {
            var factory = {};
            
            factory.multiply = function(a, b) {
               return a * b;
            }
            return factory;
         });
         
         mainApp.service('CalcService', function(MathService){
            this.square = function(a) {
               return MathService.multiply(a,a);
            }
         });
         
         mainApp.controller('CalcController', function($scope, CalcService, defaultInput) {
            $scope.number = defaultInput;
            $scope.result = CalcService.square($scope.number);

            $scope.square = function() {
               $scope.result = CalcService.square($scope.number);
            }
         });
            
      </script>
      
   </body>
</html>
```

# AngularJS 路由
```html
<html>
    <head>
        <meta charset="utf-8">
        <title>AngularJS 路由实例 - 菜鸟教程</title>
    </head>
    <body ng-app='routingDemoApp'>
     
        <h2>AngularJS 路由应用</h2>
        <ul>
            <li><a href="#/">首页</a></li>
            <li><a href="#/computers">电脑</a></li>
            <li><a href="#/printers">打印机</a></li>
            <li><a href="#/blabla">其他</a></li>
        </ul>
         
        <div ng-view></div>
        <script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
        <script src="http://apps.bdimg.com/libs/angular-route/1.3.13/angular-route.js"></script>
        <script>
            angular.module('routingDemoApp',['ngRoute'])
            .config(['$routeProvider', function($routeProvider){
                $routeProvider
                .when('/',{template:'这是首页页面'})
                .when('/computers',{template:'这是电脑分类页面'})
                .when('/printers',{template:'这是打印机页面'})
                .otherwise({redirectTo:'/'});
            }]);
        </script>
     
     
    </body>
</html>
```