controllers
理解controllers
在angular中，一个controller是一个JavaScript结构的函数，可以用来扩展Angular Scope.

当一个控制器通过ng-controller指令附加在DOM上的时候，Angular会实例化一个新的Controller对象，使用指定的控制器的构造函数。一个新的子范围会作为控制器构造函数中的$scope注入为其参数。

使用controllers来：
	设置$scope对象的最初的状态。
	向$scope对象添加行为。

不用controllers的地方：
	操纵DOM —— Controllers应该只包含业务逻辑。把程序底层的逻辑放在Controllers里面很明显会影响它的可测试性。Angular在大多数情况下都会有数据绑定和封装手动操作DOM的指令。
	格式化输入 —— 使用angular form controls来代替。
	过滤输出 —— 用angular filters来代替。
	通过controllers来分享代码或者状态 —— 用angular services来替换。
	控制其他组件的生命周期（例如，创建服务实例）。

设置$scope对象的最初的状态

很显然，当你创建一个应用程序的时候你需要设置angular $scope对象的最初的状态。你设置$scope对象的最初的一些附加属性。包含视图模型的属性。（这个模块会通过view展示出来）。在DOM中Controller被注册的时候所有的$scope的属性对于模板来说都是可用的。

下面这个例子展示了创建一个GreetingController使得$scope的greeting属性附着一个'Hola!'字符串:

var myApp = angular.module('myApp',[]);

myApp.controller('GreetingController', ['$scope', function($scope) {
  $scope.greeting = 'Hola!';
}]);

我们在我们的应用程序中创建了一个Angular Module,myApp.然后我们添加了controller的构造函数得以使用.controller()方法。这个使得controller的构造函数剥离于全局范围。
////

我们通过ng-controller指令使我们的controller附加到DOM上。现在greeting这一属性可以和模板数据绑定了：

<div ng-controller="GreetingController">
  {{ greeting }}
</div>

向一个Scope对象添加行为
为了在view中对事件作出回应或执行计算，我们必须对作用范围提供行为。我们通过向$scope对象附加方法来向作用范围内添加行为。这些方法可以从template/view中被调用。

下面这个例子使用Controller来向作用范围内添加一个可以使数字翻倍的方法：

var myApp = angular.module('myApp',[]);

myApp.controller('DoubleController', ['$scope', function($scope) {
  $scope.double = function(value) { return value * 2; };
}]);

一旦Controller被附加在DOM上面，那么翻倍的方法就能被模板的Angular表达式调用。

<div ng-controller="DoubleController">
  Two times <input ng-model="num"> equals {{ double(num) }}
</div>

当讨论到这个指令的概念部分的时候,所有分配给作用域的对象都会成为model的属性。任何作用域内的方法在模板/视图里面都是可用的，并且可以通过Angular的表达式和ng事件句柄指令来被调用。

正确的使用Controllers
一般来说，一个Controller不应该试图处理太多。它应该只包含一个页面的业务逻辑。
使Controllers变得轻便的最常用的方法是把一些不应该属于Controller的工作封装到services里面然后通过依赖注入来在Controller里面调用这些services.相关的指南我们在依赖注入服务部分进行了详细的论述。

把Controllers和Angular作用域对象关联起来。
你可以通过ngControlle指令或者$route服务来间接地把Controllers和作用域内的对象关联起来

简单准确的控制器例子
为了进一步地说明控制器组件在Angular里面是如何工作的，让我们创建一个包含下列组件的小型的应用程序。
	一个包含两个按钮和一个简单讯息的模板。
	一个包含名为spice字符串的模块。
	一个包含两个设置spice的值的函数的Controller。

	我们模板中的信息包含一个绑定至spice的模块，默认设置为字符串"very"。根据哪个按钮被点击，spice模块被设置为chili或者jalapeño。同时讯息是通过数据绑定自动更新的。

	index.html:
	<div ng-controller="SpicyController">
 	<button ng-click="chiliSpicy()">Chili</button>
 	<button ng-click="jalapenoSpicy()">Jalapeño</button>
 	<p>The food is {{spice}} spicy!</p>
	</div>

	app.js:
	var myApp = angular.module('spicyApp1', []);

  myApp.controller('SpicyController', ['$scope', function($scope) {
    $scope.spice = 'very';

    $scope.chiliSpicy = function() {
        $scope.spice = 'chili';
    };

    $scope.jalapenoSpicy = function() {
        $scope.spice = 'jalapeño';
    };
  }]);

  上面的例子需要注意的地方是：
  ng-controller指令的作用是用来给我们的模板创建一个作用域，同时scope是由SpicyController控制器来管理的。

  SpicyController只是一个普通的JavaScript函数。作为一种命名的公约一般是由一些字母打头同时用Controller来进行结尾。
  给$scope来指定一个属性来创建一个可更新的模块。
  ////
  控制器中的方法和属性在模板里面是可用的(<div>中的元素和它的子元素).

  Spicy Arguments Example
  ////

  作用域继承的例子：
  一般情况下是把Controllers附加到不同层次的DOM上。从ng-controller指令创建了一个新的子作用域开始，我们获得了一个可以进行相互继承的作用域。每个Controlle所接收到的作用域都有可以访问不同层次的属性和方法。更多的关于作用域的继承的信息可以查看Understanding Scopes

  index.html:
  <div class="spicy">
  <div ng-controller="MainController">
    <p>Good {{timeOfDay}}, {{name}}!</p>

    <div ng-controller="ChildController">
      <p>Good {{timeOfDay}}, {{name}}!</p>

      <div ng-controller="GrandChildController">
        <p>Good {{timeOfDay}}, {{name}}!</p>
      </div>
    </div>
  </div>
</div>

app.css:
div.spicy div {
  padding: 10px;
  border: solid 2px blue;
}

app.js:

var myApp = angular.module('scopeInheritance', []);
myApp.controller('MainController', ['$scope', function($scope) {
  $scope.timeOfDay = 'morning';
  $scope.name = 'Nikki';
}]);
myApp.controller('ChildController', ['$scope', function($scope) {
  $scope.name = 'Mattie';
}]);
myApp.controller('GrandChildController', ['$scope', function($scope) {
  $scope.timeOfDay = 'evening';
  $scope.name = 'Gingerbread Baby';
}]);

注意我们在我们的模板里面嵌套了三层ng-controller指令。这使得我们的视图创建出四个作用域：

根作用域。
MainController的作用域，包含timeOfDay和name属性。
ChildController的作用域，继承了timeOfDay属性但是重写了前面的name属性。
GrandChildController作用域，重写了MainController里面的timeIfDay属性和MainController里面的name属性。

方法的继承和属性的继承是一样的。所以之前的例子里面，所有的属性都可以被替换成方法来返回一个字符串的值。

测试Controllers
虽然有很多测试Controller的方法，约定俗成的最好的方法之一，展示如下，通过注入$rootScope和$controller:
Controller定义：
var myApp = angular.module('myApp',[]);

myApp.controller('MyController', function($scope) {
  $scope.spices = [{"name":"pasilla", "spiciness":"mild"},
                   {"name":"jalapeno", "spiciness":"hot hot hot!"},
                   {"name":"habanero", "spiciness":"LAVA HOT!!"}];
  $scope.spice = "habanero";
});

Controller Test:
describe('myController function', function() {

  describe('myController', function() {
    var $scope;

    beforeEach(module('myApp'));

    beforeEach(inject(function($rootScope, $controller) {
      $scope = $rootScope.$new();
      $controller('MyController', {$scope: $scope});
    }));

    it('should create "spices" model with 3 spices', function() {
      expect($scope.spices.length).toBe(3);
    });

    it('should set the default value of spice', function() {
      expect($scope.spice).toBe('habanero');
    });
  });
});

如果你需要测试一个嵌套的Controller你需要创建一个和出现在DOM中相同作用域的层级关系：
describe('state', function() {
    var mainScope, childScope, grandChildScope;

    beforeEach(module('myApp'));

    beforeEach(inject(function($rootScope, $controller) {
        mainScope = $rootScope.$new();
        $controller('MainController', {$scope: mainScope});
        childScope = mainScope.$new();
        $controller('ChildController', {$scope: childScope});
        grandChildScope = childScope.$new();
        $controller('GrandChildController', {$scope: grandChildScope});
    }));

    it('should have over and selected', function() {
        expect(mainScope.timeOfDay).toBe('morning');
        expect(mainScope.name).toBe('Nikki');
        expect(childScope.timeOfDay).toBe('morning');
        expect(childScope.name).toBe('Mattie');
        expect(grandChildScope.timeOfDay).toBe('evening');
        expect(grandChildScope.name).toBe('Gingerbread Baby');
    });
});