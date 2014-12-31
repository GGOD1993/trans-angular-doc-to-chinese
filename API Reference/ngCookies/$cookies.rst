$cookies

提供浏览器cookies的读写途径。

只提供一个简单的对象作为接口，可以向这个对象添加或者删除属性，新的cookies会在当前的$eval结束的时候被创建或者删除。这个对象的属性只能是字符串。

需要ngCookies模块被载入进来。

例子：
angular.module('cookiesExample', ['ngCookies'])
.controller('ExampleController', ['$cookies', function($cookies) {
  // 检索一个cookie
  var favoriteCookie = $cookies.myFavorite;
  // 设置一个cookie
  $cookies.myFavorite = 'oatmeal';
}]);