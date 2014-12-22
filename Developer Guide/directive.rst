创建通常的Directives

注意：这个教程是面向已经熟悉基础的AngularJS的开发者的。如果你只是一个新手，我们推荐你先浏览tutorial。如果你在寻找directives API,我们最近把它放到了$compile里面。

这个文档解释了当你想要在AngularJS应用里面创建你自己的directives,并且如何实现它们。

什么是Directives?

形象地说，directives是一个DOM元素的标志物()，它可以告诉Angular 
JS的HTML编译器来让确定的行为附加到DOM元素上甚至转换DOM元素和它的子元素。

Angular有很多内建的指令，像ngBind, ngModel,和ngClass.和你创建Controllers和Services很像，你在Angular里面创建你自己的指令来进行使用。当Angular引导你的应用程序的时候，HTML编译器遍历整个DOM来使指令和DOM元素匹配。

“编译”一个HTML模板是什么意思？对于AngularJS来说，"编译"的意思是把事件监听器附加到HTML界面来使它可以互动。////

匹配Directives
在我们可以写一个directive之前，我们需要知道当我们给出一个directive的时候Angular的HTML编译器是如何工作的。

在下面的例子里面，我们说<input>元素匹配ngModel指令。
<input ng-model="foo">
