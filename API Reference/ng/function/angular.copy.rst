finished by GGOD1993

angular.copy

对source进行一个深度的复制，这个source应该是一个对象或者数组。
如果没有提供destination,对于数组或者对象的复制将会被创建。
如果destination被提供，它的所有元素（对数组来说）或者所有属性（对对象来说）会被删除然后来自source的所有元素/属性会被复制过去。
如果source不是一个对象或者数组（inc. null and undefined）.source会被返回。
如果source和destination是相同的，一个错误会被抛出。

用法：

angular.copy(source, [destination]);

参数:

source 	*	source会被用来制作其副本。可以是任何类型的，包括primitives,null和undefined.

destination(optional)	Object/Array	destination用来存储source的拷贝内容，如果提供了，那么必须和source的类型是一样的。

返回值：

source的副本或更新过的destination.如果destination被指定的话。

例子：

<div ng-controller="ExampleController">
<form novalidate class="simple-form">
Name: <input type="text" ng-model="user.name" /><br />
E-mail: <input type="email" ng-model="user.email" /><br />
Gender: <input type="radio" ng-model="user.gender" value="male" />male
<input type="radio" ng-model="user.gender" value="female" />female<br />
<button ng-click="reset()">RESET</button>
<button ng-click="update(user)">SAVE</button>
</form>
<pre>form = {{user | json}}</pre>
<pre>master = {{master | json}}</pre>
</div>

<script>
 angular.module('copyExample', [])
   .controller('ExampleController', ['$scope', function($scope) {
     $scope.master= {};

     $scope.update = function(user) {
       // Example with 1 argument
       $scope.master= angular.copy(user);
     };

     $scope.reset = function() {
       // Example with 2 arguments
       angular.copy($scope.master, $scope.user);
     };
   }]);
</script>