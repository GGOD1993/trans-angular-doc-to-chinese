finished by GGOD1993

Services

Angular服务是通过依赖注入连接在一起的可替代对象。你可以用services来组织和分享你的应用程序中的代码。

Angualr services是：

	惰性实例化：Angular只有当应用程序的某个组件依赖于它的时候才会实例化一个service.
	单一的：每个组件只依赖于一个服务，从一个单一的服务内取得参数。

Angular提供很多有用的服务（像$http），但是对于大部分的应用程序来说，你也想创造你自己的服务。
注意：就像其他核心Angular指令集，内建的服务通常以$打头（例如：$http）。

使用一个服务：

要想使用Angular service，你应该把它作为一个需要service作为依靠的组件的依赖项。Angular的依赖注入的这一子功能会进行余下的任务。

index.html:

<div id="simple" ng-controller="MyController">
  <p>Let's try this simple notify service, injected into the controller...</p>
  <input ng-init="message='test'" ng-model="message" >
  <button ng-click="callNotify(message);">NOTIFY</button>
  <p>(you have to click 3 times to see an alert)</p>
</div>

script.js:

angular.
module('myServiceModule', []).
 controller('MyController', ['$scope','notify', function ($scope, notify) {
   $scope.callNotify = function(msg) {
     notify(msg);
   };
 }]).
factory('notify', ['$window', function(win) {
   var msgs = [];
   return function(msg) {
     msgs.push(msg);
     if (msgs.length == 3) {
       win.alert(msgs.join("\n"));
       msgs = [];
     }
   };
 }])

 protractor.js:

 it('should test service', function() {
  expect(element(by.id('simple')).element(by.model('message')).getAttribute('value'))
      .toEqual('test');
});

创建Services:

应用程序开发者可以通过注册服务名和服务的工厂函数来定义它们自己的服务，通过Angular的模式。服务工厂函数生成一个代表应用程序的剩下的服务的单例对象或者函数。这个由service返回的对象或者函数是注册在service里面指定为依赖项的任何一个组件。

注册Services:

Service通过Module API注册服务。通常你使用Module#API来注册一个Service:
var myModule = angular.module('myModule', []);
myModule.factory('serviceId', function() {
  var shinyNewServiceInstance;
  // factory function body that constructs shinyNewServiceInstance
  return shinyNewServiceInstance;
});
注意你注册的不是一个service实例，而是一个工厂函数，当你呼叫它的时候你才能创建这个实例。

依赖项：

Services可以有自己的依赖项。就像在controller里面声明一个依赖项一样，你可以通过在一个services的工厂函数指出依赖项来声明它们。

想了解更多关于依赖项的内容，参考依赖注入文档。

下面这个例子模块有两个service，每个有很多个依赖项。

var batchModule = angular.module('batchModule', []);

/**
 * The `batchLog` service allows for messages to be queued in memory and flushed
 * to the console.log every 50 seconds.
 *
 * @param {*} message Message to be logged.
 */
batchModule.factory('batchLog', ['$interval', '$log', function($interval, $log) {
  var messageQueue = [];

  function log() {
    if (messageQueue.length) {
      $log.log('batchLog messages: ', messageQueue);
      messageQueue = [];
    }
  }

  // start periodic checking
  $interval(log, 50000);

  return function(message) {
    messageQueue.push(message);
  }
}]);

/**
 * `routeTemplateMonitor` monitors each `$route` change and logs the current
 * template via the `batchLog` service.
 */
batchModule.factory('routeTemplateMonitor', ['$route', 'batchLog', '$rootScope',
  function($route, batchLog, $rootScope) {
    $rootScope.$on('$routeChangeSuccess', function() {
      batchLog($route.current ? $route.current.template : null);
    });
  }]);

在这个例子里面，注意：

batchLog这个服务依赖于内建服务指令$interval和$log。
routeTemplateMonitor服务依赖于内建指令$route和我们自定义的服务指令batchLog.

所有服务都用数组符号来声明它们的依赖项。

数组中标识符的顺序和在工厂函数中参数名的顺序是一样的。

注册一个带有$provide的Service:
你也可以在一个模块的配置函数里面通过$provide注册一个函数。
angular.module('myModule', []).config(['$provide', function($provide) {
  $provide.factory('serviceId', function() {
    var shinyNewServiceInstance;
    // factory function body that constructs shinyNewServiceInstance
    return shinyNewServiceInstance;
  });
}]);
这个技术经常用在测试单元来模拟出一个服务的依赖项。

测试单元：

下面是一个关于上面如何创建Angular Services的测试单元。这个单元使用了一种Jasmine spy(模仿)的方法，而不是浏览器警告。

var mock, notify;

beforeEach(function() {
  mock = {alert: jasmine.createSpy()};

  module(function($provide) {
    $provide.value('$window', mock);
  });

  inject(function($injector) {
    notify = $injector.get('notify');
  });
});

it('should not alert first two notifications', function() {
  notify('one');
  notify('two');

  expect(mock.alert).not.toHaveBeenCalled();
});

it('should alert all after third notification', function() {
  notify('one');
  notify('two');
  notify('three');

  expect(mock.alert).toHaveBeenCalledWith("one\ntwo\nthree");
});

it('should clear messages after alert', function() {
  notify('one');
  notify('two');
  notify('third');
  notify('more');
  notify('two');
  notify('third');

  expect(mock.alert.callCount).toEqual(2);
  expect(mock.alert.mostRecentCall.args).toEqual(["more\ntwo\nthird"]);
});

相关的主题：

AngularJS中的依赖注入。

相关的API:

Angular Service API
Injector API
