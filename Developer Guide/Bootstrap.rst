finished by GGOD1993

Bootstrap

这个页面解释了Angular的初始化过程和早必要的情况下如何手动初始化Angular.

Angular <script>标签。

这个例子展示了通常情况下我们是如何自动初始化Angular的。

<!doctype html>
<html xmlns:ng="http://angularjs.org" ng-app>
  <body>
    ...
    <script src="angular.js"></script>
  </body>
</html>

1.把script标签放在页面的底部。把脚本标签放在一个页面的底部提高了应用程序的加载速度，因为HTML的加载过程没有被angular.js脚本打断。你可以从http://code.angularjs.org。请不要把你的开发代码链接到这个URL,这会使你的站点暴露出安全漏洞。对于测试性的开发可以链接到我们的网站。
	选择: angular-[版本].js 是一个人类可读的文件，适合拿来开发或者debugging.
	选择：angular-[版本].min.js 是一个压缩整合过的文件，适合拿来发布产品。

2.请把 ng-app 放在你的应用程序的根下，例如在<html>标签，如果你希望angular来自动引导你的应用程序。

3.如果你选择用句法旧一点的指令 ng:需要把 xml-命名空间包含进html来让IE支持它。（这是由于一个历史原因，而且我们也不推荐使用ng:）

自动初始化

////在这个时候Angular查找ng-app指令在你的应用程序根目录中所指定的部分。如果ng-app指令被找到的话，那么Angular会进行以下工作：
	加载和指令相关的模板。
	创建应用程序的注册器。
	编译ng-app指令作为根目录的所指定的DOM事件。这个允许你让它只编译DOM的一部分来作为你的Angular应用程序。

<!doctype html>
<html ng-app="optionalModuleName">
  <body>
    I can add: {{ 1+2 }}.
    <script src="angular.js"></script>
  </body>
</html>

一个最佳的练习是考虑和ng-app同一个元素的地方添加一个ng-strict-di指令:

<!doctype html>
<html ng-app="optionalModuleName" ng-strict-di>
  <body>
    I can add: {{ 1+2 }}.
    <script src="angular.js"></script>
  </body>
</html>

这个可以确保在你的应用程序中的每一个服务都是被合适的注解过的。可以参考严格的依赖注入模式文档来获取更多的信息。

手动初始化
如果你需要在初始化的过程中进行更多的控制的话，你可以使用手动引导的方法。例如当你需要使用脚本来加载或者需要在Angular编译页面之前进行一些操作。

下面是一个关于手动初始化Angular的例子：

<!doctype html>
<html>
<body>
  <div ng-controller="MyController">
    Hello {{greetMe}}!
  </div>
  <script src="http://code.angularjs.org/snapshot/angular.js"></script>

  <script>
    angular.module('myApp', [])
      .controller('MyController', ['$scope', function ($scope) {
        $scope.greetMe = 'World';
      }]);

    angular.element(document).ready(function() {
      angular.bootstrap(document, ['myApp']);
    });
  </script>
</body>
</html>

注意我们把对应的需要加载的应用程序模块注入器作为了angular.bootstrap函数的第二个参数。注意angular.bootstrap不会凭空地创建出module你必须在你传递参数之前先创建出你的自定义模块。

注意：你在手动引导你的应用程序的时候是不能使用ng-app指令的。

下面是你的代码应该遵守的一些规则：

1.在你的页面和你的所有代码加载完成后，找出你的AngularJS应用的根元素，就是文档中很明显的根。

2.调用angular.bootstrap函数来把你的元素编译可执行的，双向绑定的元素。

递延引导

这个特性使得很多类似Batarang的程序和测试程序在angular的引导过程中无声地进行更多模块的依赖注入，////

如果window.name包含NG_DEFER_BOOTSTRAP前缀！当angular.bootstrap被调用的时候，引导过程会被暂停直到angular.resumeBootstrap()被调用。

angular.resumeBootstrap()携带一个可选的模块数组，这个模块数组要和引导过程一起被添加到原始列表。