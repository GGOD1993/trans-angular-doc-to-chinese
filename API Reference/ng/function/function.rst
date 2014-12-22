AngularJS API 文档
欢迎来到AngularJS API页面。这些页面包括了AngularJS的参考材料。
一个AngularJS应用，它的文件模板是由很多组件组成的。这些组件是directives,services,filters,providers,templates,全局API,和测试部分。
Angular前缀$和$$:用来防止和你的代码发生命名冲突，Angular前缀用$标记公共对象，用$$标记私有对象。请不要在你的代码中使用$或$$前缀。

Angular 模块。

ng(核心模块)
这个模块是默认提供的，它包含AngularJS的核心组件。

Directives:这个是你的AngularJS应用的模板中的核心指令集。例如：ngClick,ngInclude,ngRepeat,等等。。。

Services/Factories:这个是你的核心服务容器，在你的应用程序中的依赖注入中使用。例如：$compile,$http,$location,等等。。。

Filters:ng模块中的核心过滤器用于在模板数据被指令和表达式渲染前将其转换。例如：filter,date,currency,lowercase,uppercase,等等。。。

Global APIs:核心的全局API函数是附于angular对象上的。这些函数对于你的应用中的低一层次的JavaScript操作是非常有用的。例如：angular.copy,angular.equals(),angular.element(),等等。。。

ngRoute
用 ngRoute可以使 URL 路由到你的应用程序。ngRoute模板支持URL通过hashbang和HTML5 pushstate进行URL管理。
把angular-route.js文件包含进来同时把ngRoute设置成依赖使它能够在你的应用程序中工作。

Services/Factories：下面的这些服务用于路由管理：
					$routeParams是用来访问URL中出现的查询字符串的值的。
					$route是用来访问当前正在被访问的路由的详细信息的。
					$routeProvider是用来注册应用程序中的路由的。

Directives: ngView指令用于在页面中展示当前路由下的模板。

ngAnimate
用ngAnimate使你的应用程序能够使用动态特征。当ngAnimate被包含进来的时候很多的核心ng指令会在你的应用程序中提供动态挂钩。动画是用CSS转换/动态 或 JavaScript 回调。
把angular-animate.js文件包含近来同时把ngAnimate设置成依赖使它能够在你的应用程序中工作。
Services/Factories: 用$animate来在你的管理代码中触发动态操作。
CSS-based animations://////
JS-based animations://////

ngAria//////

ngResource
用ngResource模块当向一个含状态传输的API请求和发送数据的时候。
把angular-resource.js文件包含进来同时把ngResource设置成依赖使它能够在你的应用程序中工作。
Services/Factories: $resource服务用来定义和含状态传输的API交流的含状态传输的对象。

ngCookies
用ngCookies模块来处理你应用程序中cookie的管理。
把angular-cookies.js文件包含进来同时把ngCookies设置成依赖使它能够在你的应用程序中工作。
Services/Factories:下面的服务是用于cookie的管理的：
$cookie是一个用来存储浏览器cookies中简单数据的方便的包。
$cookieStore是用来序列化地存储更加复杂的数据的。

ngTouch
当对移动浏览器或设备进行开发的时候可以使用ngTouch.
把angular-touch.js文件包含进来同时把ngTouch设置成依赖使它能够在你的应用程序中工作。
Services/Factories:$swipe服务是用来注册和管理移动端的DOM事件的。
Directives：很多指令在模仿移动端的DOM事件时是可用的。

ngSanitize
用ngSanitize来对你的应用程序中的HTML数据进行安全的解析和操纵。
把angular-sanitize.js文件包含进来同时把ngSanitize设置成依赖使它能够在你的应用程序中工作。
Services/Factories: $sanitize服务可以用一种快速便捷的方法删除危险的HTML代码。
Filters:linky filter用来在提供的字符串下把URL转换成HTML的链接。

ngMock
将ngMock注入并且在你的测试单元中进行modules,factories,services和providers的测试。
Services/Factories//////