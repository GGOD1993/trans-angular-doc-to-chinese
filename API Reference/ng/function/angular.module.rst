angular.module
angular.module是一个创建，注册，检测Angular模块的全局空间。所有模块（angular核心库或者第三方库）都必须用这个机制进行注册。
当传递两个以上的参数的时候，一个新的模块会被建立。如果只传递一个参数////

Module:
一个模块是一个关于服务，管理，控制，过滤器和配置信息的集合。angular.module是用来配置$injector(注册器)的。

// 创建一个新的模块
var myModule = angular.module('myModule', []);

// 注册一个新的服务
myModule.value('appName', 'MyCoolApp');

// 设置内部已经出现的服务并且初始化块。
myModule.config(['$locationProvider', function($locationProvider) {
  // 设置已经出现的支持
  $locationProvider.hashPrefix('!');
}]);

然后你可以像这样创建一个注册器并载入你的模块：

var injector = angular.injector(['ng', 'myModule'])

然而，你可能会倾向于用ngApp或 angular.bootstrap来使得这个过程变得简单。

用法：
angular.module(name, [requires], [configFn]);

参数：
appName		字符串	需要被创建或者检测的模块的名字。
requires(optional)	!Array.<string>=	如果被指定那么一个新的模块会被建立。如果未被指定，那么模块会被检索以适应即将到来的设置。
configFn(optional)	Function=	可选的为这个模块设置函数。和Module#config()是一样的。

返回值：
module 	一个伴随着angular.Module api的模块。