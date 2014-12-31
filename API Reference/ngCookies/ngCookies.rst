ngCookies

ngCookies
ngCookies对于读写浏览器cookies提供了一个非常方便的包装模块。
参考 $cookies和$cookieStore来知晓用法。

初始化：
首先在你的HTML里包含入angular-cookies.js
<script src="angular.js">
<script src="angular-cookies.js">
你可以从以下站点来获取这个文件：
Google CDN
e.g. //ajax.googleapis.com/ajax/libs/angularjs/X.Y.Z/angular-cookies.js
Bower
e.g.
bower install angular-cookies@X.Y.Z
code.angularjs.org
e.g.
"//code.angularjs.org/X.Y.Z/angular-cookies.js"
X.Y.Z的地方是你运行的AngularJS的版本。
然后通过在你的应用中将其添加为一个注入模块来加载它：
angular.module('app', ['ngCookies']);
这样你就可以开始了。

模块组件：
服务：
$cookies 	提供了读写浏览器cookies的途径。

$cookieStore 	提供了一个kv(字符串-对象)存储，这个由cookies所支持。////