$cookieStore
提供一个kv(字符串-对象)存储，这个由cookies所支持.////
需要ngCookies模块被加载进入。

依赖:
$cookies

方法：
get(key);
返回指定的cookie键值的值

参数：
key 	字符串 		用来查找的Id.

返回值：
Object 	反序列化的cookie值.

put(key, value);
设定指定的cookie键值的值

参数:
key 	字符串 		value的Id.
value 	Object 		需要被存储的值。

remove(key);
移除给出的cookie

参数：
key 	字符串 		需要删除的kv值对的Id.

例子:

angular.module('cookieStoreExample', ['ngCookies'])
.controller('ExampleController', ['$cookieStore', function($cookieStore) {
  // 设置cookie
  $cookieStore.put('myFavorite','oatmeal');
  // 取得cookie
  var favoriteCookie = $cookieStore.get('myFavorite');
  // 移除一个cookie
  $cookieStore.remove('myFavorite');
}]);