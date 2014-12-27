ngShow

ngShow指令根据提供给ngShow属性的表达式来决定是否展示或者隐藏HTML元素。通过在元素上添加.ng-hide CSS class来决定是否展示或者隐藏元素。.ng-hide CSS class在AngularJS中预定义的，将展示的风格设置为空(使用!important 标记)。至于CSP模式请添加angular-csp.css到你的html文件中。

<!-- when $scope.myValue is truthy (element is visible) -->
<div ng-show="myValue"></div>

<!-- when $scope.myValue is falsy (element is hidden) -->
<div ng-show="myValue" class="ng-hide"></div>
////////

为什么用!important?
你也许想知道为什么!important要用于.ng-hide CSS class.这是因为.ng-hide选择器很容易被更高的选择器覆盖。例如，只是简单得改变HTML所展示出的style就会使得隐藏起来的元素又变得可见。这在运用CSS框架进行处理的时候会是一个更大的问题。


