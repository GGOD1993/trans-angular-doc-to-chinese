finished by GGOD1993

ngClick

ngClick指令允许元素在被点击的时候执行自定义的动作。

指令信息：

这个指令的执行优先级是第0级。

用法：

作为属性：

<ANY
  ng-click = "">
...
</ANY>

参数：

ngClick  表达式  点击后触发的函数。（事件对象可以通过$event调用）

例子：

index.html:

<button ng-click="count = count + 1" ng-init="count=0">
  Increment
</button>
<span>
  count: {{count}}
</span>

protractor.js:

it('should check ng-click', function() {
  expect(element(by.binding('count')).getText()).toMatch('0');
  element(by.css('button')).click();
  expect(element(by.binding('count')).getText()).toMatch('1');
});