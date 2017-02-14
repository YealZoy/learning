# 单一职责
+ 一个文件只定义一个组件
```javascript
/* avoid */    
angular
.module('app', ['ngRoute'])
.controller('SomeController', SomeController)
.factory('someFactory', someFactory);

function SomeController() { }

function someFactory() { }
```

推荐以下面的方式来做，把上面相同的组件分成单独的文件
```javascript
/* recommended */

// app.module.js
angular
  .module('app', ['ngRoute']);
```

```javascript
/* recommended */

// someController.js
angular
    .module('app')
    .controller('SomeController', SomeController);

function SomeController() { }
```

```javascript
/* recommended */
// someFactory.js
angular
    .module('app')
    .factory('someFactory', someFactory);

function someFactory() { }
```

# IIFE
+ 把Angular组件包装到一个立即调用函数表达式中（IIFE）。
*为什么？*：把变量从全局作用域中删除了，这有助于防止变量和函数声明比预期在全局作用域中有更长的生命周期，也有助于避免变量冲突。
*为什么？*：当你的代码为了发布而压缩了并且被合并到同一个文件中时，可能会有很多变量发生冲突，使用了IIFE（给每个文件提供了一个独立的作用域），你就不用担心这个了。
```javascript
/* avoid */
// logger.js
angular
  .module('app')
  .factory('logger', logger);

// logger function会被当作一个全局变量  
function logger() { }

// storage.js
angular
  .module('app')
  .factory('storage', storage);

// storage function会被当作一个全局变量    
function storage() { }
```

```javascript
/**
* recommended 
*
* 再也不存在全局变量了 
*/

// logger.js
(function() {
  'use strict';

  angular
      .module('app')
      .factory('logger', logger);

  function logger() { }
})();

// storage.js
(function() {
  'use strict';

  angular
      .module('app')
      .factory('storage', storage);

  function storage() { }
})();
```

# Modules
## 避免命名冲突
+ 每一个独立子模块使用唯一的命名约定。
*为什么*：避免冲突，每个模块也可以方便定义子模块。

## 定义(aka Setters)
+ 不使用任何一个使用了setter语法的变量来定义modules。
*为什么?*：在一个文件只有一个组件的条件下，完全不需要为一个模块引入一个变量。

```javascript
/* avoid */
var app = angular.module('app', [
  'ngAnimate',
  'ngRoute',
  'app.shared',
  'app.dashboard'
]);
```

你只需要用简单的setter语法来代替。
```javascript
/* recommended */
angular
    .module('app', [
    'ngAnimate',
    'ngRoute',
    'app.shared',
    'app.dashboard'
]);
```

## Getters
+ 使用module的时候，避免直接用一个变量，而是使用getter的链式语法。
*为什么？*：这将产生更加易读的代码，并且可以避免变量冲突和泄漏。
```javascript
/* avoid */
var app = angular.module('app');
app.controller('SomeController', SomeController);

function SomeController() { }
```

```javascript
/* recommended */
angular
  .module('app')
  .controller('SomeController', SomeController);

function SomeController() { }
```

## Setting vs Getting
+ 只能设置一次。
*为什么？*：一个module只能被创建一次，创建之后才能被检索到。
++ 设置module，`angular.module('app', []);`。
++ 获取module，`angular.module('app');`。

## 命名函数 vs 匿名函数
+ 回调函数使用命名函数，不要用匿名函数。
*为什么？*：易读，方便调试，减少嵌套回调函数的数量。
```javascript
/* avoid */
angular
  .module('app')
  .controller('Dashboard', function() { })
  .factory('logger', function() { });
```

```javascript
/* recommended */

// dashboard.js
angular
  .module('app')
  .controller('Dashboard', Dashboard);

function Dashboard () { }
```

```javascript
// logger.js
angular
  .module('app')
  .factory('logger', logger);

function logger () { }
```

# Controllers
## controllerAs在View中的语法
+ 使用controllerAs 语法代替直接用经典的$scope定义的controller的方式。
*为什么？*：congtroller被构建的时候，就会有一个新的实例，controllerAs 的语法比经典的$scope语法更接近JavaScript构造函数。

*为什么？*：这促进在View中对绑定到“有修饰”的对象的使用（例如用customer.name 代替name），这将更有语境、更容易阅读，也避免了任何没有“修饰”而产生的引用问题。

*为什么？*：有助于避免在有嵌套的controllers的Views中调用 $parent。

```html
<!-- avoid -->
<div ng-controller="Customer">
{{ name }}
</div>
```

```html
<!-- recommended -->
<div ng-controller="Customer as customer">
{{ customer.name }}
</div>
```

## controllerAs在controller中的语法
+ 使用 `controllerAs` 语法代替 经典的`$scope`语法 语法。

+ 使用`controllerAs` 时，controller中的`$scope`被绑定到了`this`上。

*为什么？*：`controllerAs` 是`$scope`的语法修饰，你仍然可以绑定到View上并且访问 `$scope`的方法。

*为什么？*：避免在controller中使用 `$scope`，最好不用它们或是把它们移到一个factory中。factory中可以考虑使用`$scope`，controller中只在需要时候才使用`$scope`，例如当使用`$emit`， `$broadcast`，或者 `$on`来发布和订阅事件时，可以考虑把这些调用挪到factory当中，并从controller中调用。
```javascript
/* avoid */
function Customer ($scope) {
  $scope.name = {};
  $scope.sendMessage = function() { };
}
```

```javascript
/* recommended - but see next section */
function Customer () {
  this.name = {};
  this.sendMessage = function() { };
}
```

+ 注：你可以参照下面的做法来避免 jshint的警告。但是构造函数（函数名首字母大写）是不需要这个的.
```javascript
/* jshint validthis: true */
var vm = this;
```

+ 注：在controller中用`controller as`创建了一个watch时，可以用下面的语法监测`vm.*`的成员。（创建watch时要谨慎，因为它会增加更多的负载）
```html
<input ng-model="vm.title"/>
```

```javascript
function SomeController($scope, $log) {
  var vm = this;
  vm.title = 'Some Title';

  $scope.$watch('vm.title', function(current, original) {
      $log.info('vm.title was %s', original);
      $log.info('vm.title is now %s', current);
  });
}
```

## 可绑定成员放到顶部
+ 把可绑定的成员放到controller的顶部，按字母排序，并且不要通过controller的代码传播。
*为什么？*：易读，可以让你立即识别controller中的哪些成员可以在View中绑定和使用。

*为什么？*：虽然设置单行匿名函数很容易，但是当这些函数的代码超过一行时，这将极大降低代码的可读性。在可绑定成员下面定义函数（这些函数被提出来），把具体的实现细节放到下面，可绑定成员放到顶部，这会提高代码的可读性。

```javascript
/* avoid */
function Sessions() {
  var vm = this;

  vm.gotoSession = function() {
    /* ... */
  };
  vm.refresh = function() {
    /* ... */
  };
  vm.search = function() {
    /* ... */
  };
  vm.sessions = [];
  vm.title = 'Sessions';
}
```

```javascript
/* recommended */
function Sessions() {
  var vm = this;

  vm.gotoSession = gotoSession;
  vm.refresh = refresh;
  vm.search = search;
  vm.sessions = [];
  vm.title = 'Sessions';

  ////////////

  function gotoSession() {
    /* */
  }

  function refresh() {
    /* */
  }

  function search() {
    /* */
  }
}
```

注：如果一个函数就是一行，那么只要不影响可读性就把它放到顶部。
```javascript
/* avoid */
function Sessions(data) {
  var vm = this;

  vm.gotoSession = gotoSession;
  vm.refresh = function() {
      /** 
       * lines 
       * of
       * code
       * affects
       * readability
       */
  };
  vm.search = search;
  vm.sessions = [];
  vm.title = 'Sessions';
}
```

```javascript
/* recommended */
function Sessions(dataservice) {
  var vm = this;

  vm.gotoSession = gotoSession;
  vm.refresh = dataservice.refresh; // 1 liner is OK
  vm.search = search;
  vm.sessions = [];
  vm.title = 'Sessions';
}
```

## 函数声明隐藏实现细节
+ 使用函数声明来隐藏实现细节，把绑定成员放到顶部，当你需要在controller中绑定一个函数时，把它指向一个在文件的后面会出现函数声明。更多详情请看这里。

*为什么？*：易读，易识别哪些成员可以在View中绑定和使用。

*为什么？*：把函数的实现细节放到后面，你可以更清楚地看到重要的东西。

*为什么？*：由于函数声明会被提到顶部，所以没有必要担心在声明它之前就使用函数的问题。

*为什么？*：你再也不用担心当 a依赖于 b时，把var a放到var b之前会中断你的代码的函数声明问题。

*为什么？*：函数表达式中顺序是至关重要的。
```javascript
/** 
* avoid 
* Using function expressions.
*/
function Avengers(dataservice, logger) {
  var vm = this;
  vm.avengers = [];
  vm.title = 'Avengers';

  var activate = function() {
      return getAvengers().then(function() {
          logger.info('Activated Avengers View');
      });
  }

  var getAvengers = function() {
      return dataservice.getAvengers().then(function(data) {
          vm.avengers = data;
          return vm.avengers;
      });
  }

  vm.getAvengers = getAvengers;

  activate();
}
```

注意这里重要的代码分散在前面的例子中。 下面的示例中，可以看到重要的代码都放到了顶部。实现的详细细节都在下方，显然这样的代码更易读。

```javascript
/*
* recommend
* Using function declarations
* and bindable members up top.
*/
function Avengers(dataservice, logger) {
  var vm = this;
  vm.avengers = [];
  vm.getAvengers = getAvengers;
  vm.title = 'Avengers';

  activate();

  function activate() {
      return getAvengers().then(function() {
          logger.info('Activated Avengers View');
      });
  }

  function getAvengers() {
      return dataservice.getAvengers().then(function(data) {
          vm.avengers = data;
          return vm.avengers;
      });
  }
}
```


## 把Controller中的逻辑延迟到Service中
+ 通过委派到service和factory中来延迟controller中的逻辑。
*为什么？*：把逻辑放到service中，并通过一个function暴露，就可以被多个controller重用。

*为什么？*：把逻辑放到service中将会使单元测试的时候更加容易地把它们分离，相反，如果在controller中调用逻辑就显得很二了。

*为什么？*：保持controller的简洁。

*为什么？*：从controller中删除依赖关系并且隐藏实现细节。
```javascript
/* avoid */
function Order($http, $q, config, userInfo) {
  var vm = this;
  vm.checkCredit = checkCredit;
  vm.isCreditOk;
  vm.total = 0;

  function checkCredit () { 
      var settings = {};
      // Get the credit service base URL from config
      // Set credit service required headers
      // Prepare URL query string or data object with request data
      // Add user-identifying info so service gets the right credit limit for this user.
      // Use JSONP for this browser if it doesn't support CORS
      return $http.get(settings)
          .then(function(data) {
             // Unpack JSON data in the response object
             // to find maxRemainingAmount
             vm.isCreditOk = vm.total <= maxRemainingAmount
          })
          .catch(function(error) {
             // Interpret error
             // Cope w/ timeout? retry? try alternate service?
             // Re-reject with appropriate error for a user to see
          });
  };
}
```

```javascript
/* recommended */
function Order (creditService) {
  var vm = this;
  vm.checkCredit = checkCredit;
  vm.isCreditOk;
  vm.total = 0;

  function checkCredit () { 
      return creditService.isOrderTotalOk(vm.total)
        .then(function(isOk) { vm.isCreditOk = isOk; })
        .catch(showServiceError);
  };
}
```

## 保持Controller的专一性
+ 一个view定义一个controller，尽量不要在其它view中使用这个controller。把可重用的逻辑放到factory中，保证controller只服务于当前视图。

*为什么？*：不同的view用同一个controller是非常不科学的，良好的端对端测试覆盖率对于保证大型应用稳定性是必需的。


## 分配Controller
+ 当一个controller必须匹配一个view时或者任何一个组件可能被其它controller或是view重用时，连同controller的route一起定义。

注：如果一个view是通过route外的其它形式加载的，那么就用`ng-controller="Avengers as vm"`语法。

*为什么？*：在route中匹配controller允许不同的路由调用不同的相匹配的controller和view，当在view中通过ng-controller分配controller时，这个view总是和相同的controller相关联。

```javascript
/* avoid - when using with a route and dynamic pairing is desired */

// route-config.js
angular
  .module('app')
  .config(config);

function config ($routeProvider) {
  $routeProvider
      .when('/avengers', {
          templateUrl: 'avengers.html'
      });
}
```

```html
<!-- avengers.html -->
<div ng-controller="Avengers as vm">
</div>
```

```javascript
/* recommended */

// route-config.js
angular
  .module('app')
  .config(config);

function config ($routeProvider) {
  $routeProvider
      .when('/avengers', {
          templateUrl: 'avengers.html',
          controller: 'Avengers',
          controllerAs: 'vm'
      });
}
```

```html
<!-- avengers.html -->
<div>
</div>
```

# Services
## 单例
+ 用`new`实例化`service`，用`this`实例化公共方法和变量，由于这和factory是类似的，所以为了保持统一，推荐用facotry来代替。

注意：所有的Angular services都是单例，这意味着每个injector都只有一个实例化的service。

```javascript
// service
angular
  .module('app')
  .service('logger', logger);

function logger () {
  this.logError = function(msg) {
    /* */
  };
}
```

```javascript
// factory
angular
  .module('app')
  .factory('logger', logger);

function logger () {
  return {
      logError: function(msg) {
        /* */
      }
  };
}
```

# Factories
## 单一职责
+ factory应该是单一职责，这是由其上下文进行封装的。一旦一个factory将要处理超过单一的目的时，就应该创建一个新的factory。

## 单例
+ facotry是一个单例，它返回一个包含service成员的对象。
注：所有的Angular services都是单例，这意味着每个injector都只有一个实例化的service。

## 可访问的成员放到顶部
+ 使用从显露模块模式派生出来的技术把service（它的接口）中可调用的成员暴露到顶部，

*为什么？*：易读，并且让你可以立即识别service中的哪些成员可以被调用，哪些成员必须进行单元测试（或者被别人嘲笑）。

*为什么？*：当文件内容很长时，这可以避免需要滚动才能看到暴露了哪些东西。

*为什么？*：虽然你可以随意写一个函数，但当函数代码超过一行时就会降低可读性并造成滚动。通过把实现细节放下面、可调用接口放到顶部的返回service的方式来定义可调用的接口，从而使代码更加易读。

```javascript
/* avoid */
function dataService () {
  var someValue = '';
  function save () {
    /* */
  };
  function validate () { 
    /* */
  };

  return {
      save: save,
      someValue: someValue,
      validate: validate
  };
}
```

```javascript
/* recommended */
function dataService () {
  var someValue = '';
  var service = {
      save: save,
      someValue: someValue,
      validate: validate
  };
  return service;

  ////////////

  function save () { 
    /* */
  };

  function validate () { 
    /* */
  };
}
```

## 函数声明隐藏实现细节
+ 函数声明隐藏实现细节，把绑定成员放到顶部，当你需要在controller中绑定一个函数时，把它指向一个函数声明，这个函数声明在文件的后面会出现。

*为什么？*：易读，易识别哪些成员可以在View中绑定和使用。

*为什么？*：把函数的实现细节放到后面，你可以更清楚地看到重要的东西。

*为什么？*：由于函数声明会被提到顶部，所以没有必要担心在声明它之前就使用函数的问题。

*为什么？*：你再也不用担心当 a依赖于 b时，把var a放到var b之前会中断你的代码的函数声明问题。

*为什么？*：函数表达式中顺序是至关重要的。

```javascript
/**
* avoid
* Using function expressions
*/
function dataservice($http, $location, $q, exception, logger) {
  var isPrimed = false;
  var primePromise;

  var getAvengers = function() {
    // implementation details go here
  };

  var getAvengerCount = function() {
    // implementation details go here
  };

  var getAvengersCast = function() {
    // implementation details go here
  };

  var prime = function() {
    // implementation details go here
  };

  var ready = function(nextPromises) {
    // implementation details go here
  };

  var service = {
      getAvengersCast: getAvengersCast,
      getAvengerCount: getAvengerCount,
      getAvengers: getAvengers,
      ready: ready
  };

  return service;
}
```

```javascript
/**
* recommended
* Using function declarations
* and accessible members up top.
*/
function dataservice($http, $location, $q, exception, logger) {
  var isPrimed = false;
  var primePromise;

  var service = {
      getAvengersCast: getAvengersCast,
      getAvengerCount: getAvengerCount,
      getAvengers: getAvengers,
      ready: ready
  };

  return service;

  ////////////

  function getAvengers() {
    // implementation details go here
  }

  function getAvengerCount() {
    // implementation details go here
  }

  function getAvengersCast() {
    // implementation details go here
  }

  function prime() {
    // implementation details go here
  }

  function ready(nextPromises) {
    // implementation details go here
  }
}
```

# Data Services
## 独立的数据调用
+ 把进行数据操作和数据交互的逻辑放到factory中，数据服务负责XHR请求、本地存储、内存存储和其它任何数据操作。

*为什么？*：controller的作用是查看视图和收集视图的信息，它不应该关心如何取得数据，只需要知道哪里需要用到数据。把取数据的逻辑放到数据服务中能够让controller更简单、更专注于对view的控制。

*为什么？*：方便测试。

*为什么？*：数据服务的实现可能有非常明确的代码来处理数据仓库，这可能包含headers、如何与数据交互或是其它service，例如$http。把逻辑封装到单独的数据服务中，这隐藏了外部调用者（例如controller）对数据的直接操作，这样更加容易执行变更。

```javascript
/* recommended */

// dataservice factory
angular
  .module('app.core')
  .factory('dataservice', dataservice);

dataservice.$inject = ['$http', 'logger'];

function dataservice($http, logger) {
  return {
      getAvengers: getAvengers
  };

  function getAvengers() {
      return $http.get('/api/maa')
          .then(getAvengersComplete)
          .catch(getAvengersFailed);

      function getAvengersComplete(response) {
          return response.data.results;
      }

      function getAvengersFailed(error) {
          logger.error('XHR Failed for getAvengers.' + error.data);
      }
  }
}
```

注意：数据服务被调用时（例如controller），隐藏调用的直接行为，如下所示。

```javascript
/* recommended */

// controller calling the dataservice factory
angular
  .module('app.avengers')
  .controller('Avengers', Avengers);

Avengers.$inject = ['dataservice', 'logger'];

function Avengers(dataservice, logger) {
  var vm = this;
  vm.avengers = [];

  activate();

  function activate() {
      return getAvengers().then(function() {
          logger.info('Activated Avengers View');
      });
  }

  function getAvengers() {
      return dataservice.getAvengers()
        .then(function(data) {
            vm.avengers = data;
            return vm.avengers;
        });
  }
}      
```

## 数据调用返回一个Promise
+ 就像$http一样，调用数据时返回一个promise，在你的调用函数中也返回一个promise。

*为什么？*：你可以把promise链接到一起，在数据调用完成并且resolve或是reject这个promise后采取进一步的行为。
```javascript
/* recommended */

activate();

function activate() {
  /**
   * Step 1
   * Ask the getAvengers function for the
   * avenger data and wait for the promise
   */
  return getAvengers().then(function() {
    /**
     * Step 4
     * Perform an action on resolve of final promise
     */
    logger.info('Activated Avengers View');
  });
}

function getAvengers() {
  /**
   * Step 2
   * Ask the data service for the data and wait
   * for the promise
   */
  return dataservice.getAvengers()
    .then(function(data) {
        /**
         * Step 3
         * set the data and resolve the promise
         */
        vm.avengers = data;
        return vm.avengers;
    });
}
```


# Directives
## 一个dirctive一个文件
+ 一个文件中只创建一个directive，并依照directive来命名文件。
*为什么？*：虽然把所有directive放到一个文件中很简单，但是当一些directive是跨应用的，一些是跨模块的，一些仅仅在一个模块中使用时，想把它们独立出来就非常困难了。

*为什么？*：一个文件一个directive也更加容易维护。

>注： "最佳实践：Angular文档中有提过，directive应该自动回收，当directive被移除后，你可以使用element.on('$destroy', ...)或者scope.$on('$destroy', ...)来执行一个clearn-up函数。"

```javascript
/* avoid */
/* directives.js */

angular
  .module('app.widgets')

  /* order directive仅仅会被order module用到 */
  .directive('orderCalendarRange', orderCalendarRange)

  /* sales directive可以在sales app的任意地方使用 */
  .directive('salesCustomerInfo', salesCustomerInfo)

  /* spinner directive可以在任意apps中使用 */
  .directive('sharedSpinner', sharedSpinner);

function orderCalendarRange() {
  /* implementation details */
}

function salesCustomerInfo() {
  /* implementation details */
}

function sharedSpinner() {
  /* implementation details */
}
```

```javascript
/* recommended */
/* calendarRange.directive.js */

/**
* @desc order directive that is specific to the order module at a company named Acme
* @example <div acme-order-calendar-range></div>
*/
angular
  .module('sales.order')
  .directive('acmeOrderCalendarRange', orderCalendarRange);

function orderCalendarRange() {
  /* implementation details */
}
```

```javascript
/* recommended */
/* customerInfo.directive.js */

/**
* @desc sales directive that can be used anywhere across the sales app at a company named Acme
* @example <div acme-sales-customer-info></div>
*/    
angular
  .module('sales.widgets')
  .directive('acmeSalesCustomerInfo', salesCustomerInfo);

function salesCustomerInfo() {
  /* implementation details */
}
```

```javascript
/* recommended */
/* spinner.directive.js */

/**
* @desc spinner directive that can be used anywhere across apps at a company named Acme
* @example <div acme-shared-spinner></div>
*/
angular
  .module('shared.widgets')
  .directive('acmeSharedSpinner', sharedSpinner);

function sharedSpinner() {
  /* implementation details */
}
```

注：由于directive使用条件比较广，所以命名就存在很多的选项。选择一个让directive和它的文件名都清楚分明的名字。下面有一些例子，不过更多的建议去看命名章节。

## 在directive中操作DOM

+ 当需要直接操作DOM的时候，使用directive。如果有替代方法可以使用，例如：使用CSS来设置样式、animation services、Angular模板、ngShow或者ngHide，那么就直接用这些即可。例如，如果一个directive只是想控制显示和隐藏，用ngHide/ngShow即可。

*为什么？*：DOM操作的测试和调试是很困难的，通常会有更好的方法（CSS、animations、templates）。


## 提供一个唯一的Directive前缀
+ 提供一个短小、唯一、具有描述性的directive前缀，例如acmeSalesCustomerInfo在HTML中声明为`acme-sales-customer-info`。

*为什么？*：方便快速识别directive的内容和起源，例如`acme-`可能预示着这个directive是服务于Acme company。

注：避免使用`ng-`为前缀，研究一下其它广泛使用的directive避免命名冲突，例如Ionic Framework的`ion-`。

## 限制元素和属性
+ 当创建一个directive需要作为一个独立元素时，restrict值设置为`E`（自定义元素），也可以设置可选值`A`（自定义属性）。一般来说，如果它就是为了独立存在，用E是合适的做法。一般原则是允许`EA`，但是当它是独立的时候这更倾向于作为一个元素来实施，当它是为了增强已存在的DOM元素时则更倾向于作为一个属性来实施。

*为什么？*：这很有意义！

*为什么？*：虽然我们允许directive被当作一个class来使用，但如果这个directive的行为确实像一个元素的话，那么把directive当作元素或者属性是更有意义的。

```html
<!-- avoid -->
<div class="my-calendar-range"></div>
```

```javascript
/* avoid */
angular
  .module('app.widgets')
  .directive('myCalendarRange', myCalendarRange);

function myCalendarRange () {
  var directive = {
      link: link,
      templateUrl: '/template/is/located/here.html',
      restrict: 'C'
  };
  return directive;

  function link(scope, element, attrs) {
    /* */
  }
}
```

```html
<!-- recommended -->
<my-calendar-range></my-calendar-range>
<div my-calendar-range></div>
```

```javascript
/* recommended */
angular
  .module('app.widgets')
  .directive('myCalendarRange', myCalendarRange);

function myCalendarRange () {
  var directive = {
      link: link,
      templateUrl: '/template/is/located/here.html',
      restrict: 'EA'
  };
  return directive;

  function link(scope, element, attrs) {
    /* */
  }
}
```

## Directives和ControllerAs
+ directive使用controller as语法，和view使用controller as保持一致。

*为什么？*：因为不难且有必要这样做。

注意：下面的directive演示了一些你可以在link和directive控制器中使用scope的方法，用controllerAs。这里把template放在行内是为了在一个地方写出这些代码。

注意：关于依赖注入的内容，请看手动依赖注入。

注意：directive的控制器是在directive外部的，这种风格避免了由于注入造成的`return`之后的代码无法访问的情况。

```html
<div my-example max="77"></div>
```

```javascript
angular
  .module('app')
  .directive('myExample', myExample);

function myExample() {
  var directive = {
      restrict: 'EA',
      templateUrl: 'app/feature/example.directive.html',
      scope: {
          max: '='
      },
      link: linkFunc,
      controller : ExampleController,
      controllerAs: 'vm',
      bindToController: true // because the scope is isolated
  };

  return directive;

  function linkFunc(scope, el, attr, ctrl) {
      console.log('LINK: scope.min = %s *** should be undefined', scope.min);
      console.log('LINK: scope.max = %s *** should be undefined', scope.max);
      console.log('LINK: scope.vm.min = %s', scope.vm.min);
      console.log('LINK: scope.vm.max = %s', scope.vm.max);
  }
}

ExampleController.$inject = ['$scope'];

function ExampleController($scope) {
  // Injecting $scope just for comparison
  var vm = this;

  vm.min = 3;

  console.log('CTRL: $scope.vm.min = %s', $scope.vm.min);
  console.log('CTRL: $scope.vm.max = %s', $scope.vm.max);
  console.log('CTRL: vm.min = %s', vm.min);
  console.log('CTRL: vm.max = %s', vm.max);
}
```

```html
<!-- example.directive.html -->
<div>hello world</div>
<div>max={{vm.max}}<input ng-model={vm.max"/></div>
<div>min={{vm.min}}<input ng-model={vm.min"/></div>
```

注意：当你把controller注入到link的函数或可访问的directive的attributes时，你可以把它命名为控制器的属性。
```javascript
// Alternative to above example
function linkFunc(scope, el, attr, vm) { // 和上面例子的区别在于把vm直接传递进来
console.log('LINK: scope.min = %s *** should be undefined', scope.min);
console.log('LINK: scope.max = %s *** should be undefined', scope.max);
console.log('LINK: vm.min = %s', vm.min);
console.log('LINK: vm.max = %s', vm.max);
}
```

+ 当directive中使用了controller as语法时，如果你想把父级作用域绑定到directive的controller作用域时，使用bindToController = true。

*为什么？*：这使得把外部作用域绑定到directive controller中变得更加简单。

注意：Angular 1.3.0才介绍了bindToController。

```html
<div my-example max="77"></div>
```

```javascript
angular
  .module('app')
  .directive('myExample', myExample);

function myExample() {
  var directive = {
      restrict: 'EA',
      templateUrl: 'app/feature/example.directive.html',
      scope: {
          max: '='
      },
      controller: ExampleController,
      controllerAs: 'vm',
      bindToController: true
    };

  return directive;
}

function ExampleController() {
  var vm = this;
  vm.min = 3;
  console.log('CTRL: vm.min = %s', vm.min);
  console.log('CTRL: vm.max = %s', vm.max);
}
```


```html
<!-- example.directive.html -->
<div>hello world</div>
<div>max={{vm.max}}<input ng-model="vm.max"/></div>
<div>min={{vm.min}}<input ng-model="vm.min"/></div>
```


## 解决Controller的Promises

+ 在activate函数中解决controller的启动逻辑。

*为什么？*：把启动逻辑放在一个controller中固定的位置可以方便定位、有利于保持测试的一致性，并能够避免controller中到处都是激活逻辑。

*为什么？*：`activate`这个controller使得重用刷新视图的逻辑变得很方便，把所有的逻辑都放到了一起，可以让用户更快地看到视图，可以很轻松地对`ng-view` 或 `ui-view`使用动画，用户体验更好。

注意：如果你需要在开始使用controller之前有条件地取消路由，那么就用route resolve来代替。

```javascript
/* avoid */
function Avengers(dataservice) {
  var vm = this;
  vm.avengers = [];
  vm.title = 'Avengers';

  dataservice.getAvengers().then(function(data) {
      vm.avengers = data;
      return vm.avengers;
  });
}
```

```javascript
/* recommended */
function Avengers(dataservice) {
  var vm = this;
  vm.avengers = [];
  vm.title = 'Avengers';

  activate();

  ////////////

  function activate() {
      return dataservice.getAvengers().then(function(data) {
          vm.avengers = data;
          return vm.avengers;
      });
  }
}
```


## Route Resolve Promises
+ 当一个controller在激活之前，需要依赖一个promise的完成时，那么就在controller的逻辑执行之前在$routeProvider中解决这些依赖。如果你需要在controller被激活之前有条件地取消一个路由，那么就用route resolver。

+ 你决定在过渡到视图之前取消路由时，使用route resolve。

*为什么？*：controller在加载前可能需要一些数据，这些数据可能是从一个通过自定义factory或是$http的promise而来的。route resolve允许promise在controller的逻辑执行之前解决，因此它可能对从promise中来的数据做一些处理。

*为什么？*：这段代码将在路由后的controller的激活函数中执行，视图立即加载，promise resolve的时候将会开始进行数据绑定，可以（通过`ng-view`或`ui-view`）在视图的过渡之间加个loading状态的动画。

注意：这段代码将在路由之前通过一个promise来执行，拒绝了承诺就会取消路由，接受了就会等待路由跳转到新视图。如果你想更快地进入视图，并且无需验证是否可以进入视图，你可以考虑用控制器 `activate` 技术。

```javascript
/* avoid */
angular
  .module('app')
  .controller('Avengers', Avengers);

function Avengers (movieService) {
  var vm = this;
  // unresolved
  vm.movies;
  // resolved asynchronously
  movieService.getMovies().then(function(response) {
      vm.movies = response.movies;
  });
}
```

```javascript
/* better */

// route-config.js
angular
  .module('app')
  .config(config);

function config ($routeProvider) {
  $routeProvider
      .when('/avengers', {
          templateUrl: 'avengers.html',
          controller: 'Avengers',
          controllerAs: 'vm',
          resolve: {
              moviesPrepService: function(movieService) {
                  return movieService.getMovies();
              }
          }
      });
}

// avengers.js
angular
  .module('app')
  .controller('Avengers', Avengers);

Avengers.$inject = ['moviesPrepService'];
function Avengers (moviesPrepService) {
  var vm = this;
  vm.movies = moviesPrepService.movies;
}
```

注意：下面这个例子展示了命名函数的路由解决，这种方式对于调试和处理依赖注入更加方便。

```javascript
/* even better */

// route-config.js
angular
  .module('app')
  .config(config);

function config($routeProvider) {
  $routeProvider
      .when('/avengers', {
          templateUrl: 'avengers.html',
          controller: 'Avengers',
          controllerAs: 'vm',
          resolve: {
              moviesPrepService: moviesPrepService
          }
      });
}

function moviePrepService(movieService) {
  return movieService.getMovies();
}

// avengers.js
angular
  .module('app')
  .controller('Avengers', Avengers);

Avengers.$inject = ['moviesPrepService'];
function Avengers(moviesPrepService) {
    var vm = this;
    vm.movies = moviesPrepService.movies;
}
```

注意：示例代码中的`movieService`不符合安全压缩的做法，可以到手动依赖注入和压缩和注释部分学习如何安全压缩。

# 手动依赖注入
## 压缩的不安全性

+ 声明依赖时避免使用缩写语法。

*为什么？*：组件的参数（例如controller、factory等等）将会被转换成各种乱七八糟错误的变量。例如，common和dataservice可能会变成a或者b，但是这些转换后的变量在Angular中是找不到的。

```javascript
/* avoid - not minification-safe*/
angular
  .module('app')
  .controller('Dashboard', Dashboard);

function Dashboard(common, dataservice) {
}
```

这一段代码在压缩时会产生错误的变量，因此在运行时就会报错。
```javascript
/* avoid - not minification-safe*/
angular.module('app').controller('Dashboard', d);function d(a, b) { }
```

## 手动添加依赖
+ 用$inject手动添加Angular组件所需的依赖。

*为什么？*：这种技术反映了使用`ng-annotate`的技术，这就是我推荐的对依赖关系进行自动化创建安全压缩的方式，如果`ng-annotate`检测到已经有了注入，那么它就不会再次重复执行。

*为什么？*：可以避免依赖变成其它Angular找不到的变量，例如，`common`和`dataservice`可能会变成a或者b。

*为什么？*：避免创建内嵌的依赖，因为一个数组太长不利于阅读，此外，内嵌的方式也会让人感到困惑，比如数组是一系列的字符串，但是最后一个却是组件的function。

```javascript
/* avoid */
angular
  .module('app')
  .controller('Dashboard', 
      ['$location', '$routeParams', 'common', 'dataservice', 
          function Dashboard($location, $routeParams, common, dataservice) {}
      ]);      
```

```javascript
/* avoid */
angular
  .module('app')
  .controller('Dashboard', 
    ['$location', '$routeParams', 'common', 'dataservice', Dashboard]);

function Dashboard($location, $routeParams, common, dataservice) {
}
```

```javascript
/* recommended */
angular
  .module('app')
  .controller('Dashboard', Dashboard);

Dashboard.$inject = ['$location', '$routeParams', 'common', 'dataservice'];

function Dashboard($location, $routeParams, common, dataservice) {
}
```

注意：当你的函数处于return语句后面，那么$inject是无法访问的（这会在directive中发生），你可以通过把Controller移到directive外面来解决这个问题。
```javascript
function outer() {
  var ddo = {
      controller: DashboardPanelController,
      controllerAs: 'vm'
  };
  return ddo;

  DashboardPanelController.$inject = ['logger']; // Unreachable
  function DashboardPanelController(logger) {
  }
}
```

```javascript
/* recommended */
// outside a directive definition
function outer() {
  var ddo = {
      controller: DashboardPanelController,
      controllerAs: 'vm'
  };
  return ddo;
}

DashboardPanelController.$inject = ['logger'];
function DashboardPanelController(logger) {
}
```

## 手动确定路由解析器依赖
+ 用$inject手动给Angular组件添加路由解析器依赖。

*为什么？*：这种技术打破了路由解析的匿名函数的形式，易读。

*为什么？*：$inject语句可以让任何依赖都可以安全压缩。
```javascript
/* recommended */
function config ($routeProvider) {
  $routeProvider
      .when('/avengers', {
          templateUrl: 'avengers.html',
          controller: 'AvengersController',
          controllerAs: 'vm',
          resolve: {
              moviesPrepService: moviePrepService
          }
      });
}

moviePrepService.$inject =  ['movieService'];
function moviePrepService(movieService) {
  return movieService.getMovies();
}
```

## 压缩和注释
+ 在Gulp或Grunt中使用ng-annotate，用/** @ngInject */对需要自动依赖注入的function进行注释。

*为什么？*：可以避免代码中的依赖使用到任何不安全的写法。

*为什么？*：不推荐用ng-min。

下面的代码没有注入依赖，显然压缩是不安全的。
```javascript
angular
    .module('app')
    .controller('Avengers', Avengers);

/* @ngInject */
function Avengers (storageService, avengerService) {
    var vm = this;
    vm.heroSearch = '';
    vm.storeHero = storeHero;

    function storeHero(){
      var hero = avengerService.find(vm.heroSearch);
      storageService.save(hero.name, hero);
    }
}
```

当上面的代码通过`ng-annotate`运行时，就会产生如下的带有$inject注释的输出结果，这样的话压缩就会安全了。
```javascript
angular
    .module('app')
    .controller('Avengers', Avengers);

/* @ngInject */
function Avengers (storageService, avengerService) {
    var vm = this;
    vm.heroSearch = '';
    vm.storeHero = storeHero;

    function storeHero(){
      var hero = avengerService.find(vm.heroSearch);
      storageService.save(hero.name, hero);
    }
}

Avengers.$inject = ['storageService', 'avengerService'];
```

注意：如果ng-annotate检测到已经有注入了（例如发现了@ngInject），就不会重复生成$inject代码了。

注意：路由的函数前面也可以用/* @ngInject */
```javascript
// Using @ngInject annotations
function config($routeProvider) {
    $routeProvider
        .when('/avengers', {
            templateUrl: 'avengers.html',
            controller: 'Avengers',
            controllerAs: 'vm',
            resolve: { /* @ngInject */
                moviesPrepService: function(movieService) {
                    return movieService.getMovies();
                }
            }
        });
}
```

## 使用Gulp或Grunt结合ng-annotate
+ 在自动化任务中使用gulp-ng-annotate或grunt-ng-annotate，把/* @ngInject */注入到任何有依赖关系函数的前面。

为什么？：ng-annotate会捕获大部分的依赖关系，但是有时候需要借助于/* @ngInject */语法提示。

下面的代码是gulp任务使用ngAnnotate的例子。

```javascript
gulp.task('js', ['jshint'], function() {
    var source = pkg.paths.js;

    return gulp.src(source)
        .pipe(sourcemaps.init())
        .pipe(concat('all.min.js', {newLine: ';'}))
        // Annotate before uglify so the code get's min'd properly.
        .pipe(ngAnnotate({
            // true helps add where @ngInject is not used. It infers.
            // Doesn't work with resolve, so we must be explicit there
            add: true
        }))
        .pipe(bytediff.start())
        .pipe(uglify({mangle: true}))
        .pipe(bytediff.stop())
        .pipe(sourcemaps.write('./'))
        .pipe(gulp.dest(pkg.paths.dev));
});
```

# 异常处理
+ 使用一个decorator，在配置的时候用$provide服务，当发生异常时，在$exceptionHandler服务中执行自定义的处理方法。

*为什么？*：在开发时和运行时提供了一种统一的方式来处理未被捕获的Angular异常。

注：另一个选项是用来覆盖service的，这个可以代替decorator，这是一个非常nice的选项，但是如果你想保持默认行为，那么推荐你扩展一个decorator。
```javascript
/* recommended */
angular
    .module('blocks.exception')
    .config(exceptionConfig);

exceptionConfig.$inject = ['$provide'];

function exceptionConfig($provide) {
    $provide.decorator('$exceptionHandler', extendExceptionHandler);
}

extendExceptionHandler.$inject = ['$delegate', 'toastr'];

function extendExceptionHandler($delegate, toastr) {
    return function(exception, cause) {
        $delegate(exception, cause);
        var errorData = { 
          exception: exception, 
          cause: cause 
        };
        /**
         * Could add the error to a service's collection,
         * add errors to $rootScope, log errors to remote web server,
         * or log locally. Or throw hard. It is entirely up to you.
         * throw exception;
         */
        toastr.error(exception.msg, errorData);
    };
}
```

## 异常捕获器
+ 创建一个暴露了一个接口的factory来捕获异常并以合适方式处理异常。

*为什么？*：提供了一个统一的方法来捕获代码中抛出的异常。

注：异常捕获器对特殊异常的捕获和反应是非常友好的，例如，使用XHR从远程服务获取数据时，你想要捕获所有异常并做出不同的反应。
```javascript
/* recommended */
angular
    .module('blocks.exception')
    .factory('exception', exception);

exception.$inject = ['logger'];

function exception(logger) {
    var service = {
        catcher: catcher
    };
    return service;

    function catcher(message) {
        return function(reason) {
            logger.error(message, reason);
        };
    }
}
```

## 路由错误

+ 用`$routeChangeError`来处理并打印出所有的路由错误信息。

*为什么？*：提供一个统一的方式来处理所有的路由错误。

*为什么？*：当一个路由发生错误的时候，可以给展示一个提示信息，提高用户体验。
```javascript
/* recommended */
var handlingRouteChangeError = false;

function handleRoutingErrors() {
    /**
     * Route cancellation:
     * On routing error, go to the dashboard.
     * Provide an exit clause if it tries to do it twice.
     */
    $rootScope.$on('$routeChangeError',
        function(event, current, previous, rejection) {
            if (handlingRouteChangeError) { return; }
            handlingRouteChangeError = true;
            var destination = (current && (current.title ||
                current.name || current.loadedTemplateUrl)) ||
                'unknown target';
            var msg = 'Error routing to ' + destination + '. ' +
                (rejection.msg || '');

            /**
             * Optionally log using a custom service or $log.
             * (Don't forget to inject custom service)
             */
            logger.warning(msg, [current]);

            /**
             * On routing error, go to another route/state.
             */
            $location.path('/');

        }
    );
}
```

# 命名
## 命名原则
+ 遵循以描述组件功能，然后是类型（可选）的方式来给所有的组件提供统一的命名，我推荐的做法是feature.type.js。大多数文件都有2个名字。

文件名 (avengers.controller.js)
带有Angular的注册组件名 (AvengersController)
*为什么？*：命名约定有助于为一目了然地找到内容提供一个统一的方式，在项目中和团队中保持统一性是非常重要的，保持统一性对于跨公司来说提供了巨大的效率。

*为什么？*：命名约定应该只为代码的检索和沟通提供方便。

## 功能文件命名
+ 遵循以“描述组件功能.类型（可选）”的方式来给所有的组件提供统一的命名，我推荐的做法是feature.type.js。

*为什么？*：为快速识别组件提供了统一的方式。

*为什么？*：为任何自动化的任务提供模式匹配。

```
/**
 * common options 
 */

// Controllers
avengers.js
avengers.controller.js
avengersController.js

// Services/Factories
logger.js
logger.service.js
loggerService.js
```

```
/**
 * recommended
 */

// controllers
avengers.controller.js
avengers.controller.spec.js

// services/factories
logger.service.js
logger.service.spec.js

// constants
constants.js

// module definition
avengers.module.js

// routes
avengers.routes.js
avengers.routes.spec.js

// configuration
avengers.config.js

// directives
avenger-profile.directive.js
avenger-profile.directive.spec.js
```

## 测试文件命名

+ 和组件命名差不多，带上一个spec后缀。

*为什么？*：为快速识别组件提供统一的方式。

*为什么？*：为karma或是其它测试运行器提供模式匹配。
```
/**
 * recommended
 */
avengers.controller.spec.js
logger.service.spec.js
avengers.routes.spec.js
avenger-profile.directive.spec.js
```

## Controller命名

+ 为所有controller提供统一的名称，先特征后名字，鉴于controller是构造函数，所以要采用UpperCamelCase（每个单词首字母大写）的方式。

*为什么？*：为快速识别和引用controller提供统一的方式。

*为什么？*：UpperCamelCase是常规的识别一个可以用构造函数来实例化的对象的方式。
```javascript
/**
 * recommended
 */

// avengers.controller.js
angular
    .module
    .controller('HeroAvengersController', HeroAvengersController);

function HeroAvengers(){ }    
```

## Controller命名后缀

+ 使用Controller。

*为什么？*：Controller使用更广泛、更明确、更具有描述性。
```javascript
/**
 * recommended
 */

// avengers.controller.js
angular
    .module
    .controller('AvengersController', AvengersController);

function AvengersController(){ }
```

## Factory命名

+ 一样要统一，对service和factory使用camel-casing（驼峰式，第一个单词首字母小写，后面单词首字母大写）方式。避免使用`$`前缀。

*为什么？*：可以快速识别和引用factory。

*为什么？*：避免与内部使用`$`前缀的服务发生冲突。
```javascript
/**
 * recommended
 */

// logger.service.js
angular
    .module
    .factory('logger', logger);

function logger(){ }
```

## Directive组件命名
+ 使用camel-case方式，用一个短的前缀来描述directive在哪个区域使用（一些例子中是使用公司前缀或是项目前缀）。

*为什么？*：可以快速识别和引用controller。
```javascript
/**
 * recommended
 */

// avenger-profile.directive.js    
angular
    .module
    .directive('xxAvengerProfile', xxAvengerProfile);

// usage is <xx-avenger-profile> </xx-avenger-profile>

function xxAvengerProfile(){ }
```

## 模块
+ 当有很多的模块时，主模块文件命名成`app.module.js`，其它依赖模块以它们代表的内容来命名。例如，一个管理员模块命名成`admin.module.js`，它们各自的注册模块名字就是`app`和`admin`。

*为什么？*：给多模块的应用提供统一的方式，这也是为了扩展大型应用。

*为什么？*：对使用任务来自动化加载所有模块的定义（先）和其它所有的angular文件（后）提供了一种简单的方式。

## 配置

+ 把一个模块的配置独立到它自己的文件中，以这个模块为基础命名。app模块的配置文件命名成`app.config.js`（或是config.js），`admin.module.js`的配置文件命名成admin.config.js。

*为什么？*：把配置从模块定义、组件和活跃代码中分离出来。

*为什么？*：为设置模块的配置提供了一个可识别的地方。

## 路由
+ 把路由的配置独立到单独的文件。主模块的路由可能是app.route.js，admin模块的路由可能是admin.route.js。即使是在很小的应用中，我也喜欢把路由的配置从其余的配置中分离出来。