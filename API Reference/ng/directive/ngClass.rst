ngClass

ngClass指令允许你通过对需要添加的CSS进行一个代表其表达式的数据绑定使你能够动态地设置HTML元素的CSS属性。

这个指令通过三种不同的方法进行操作，这取决于表达式具体属于那种形态。

1.如果表达式是一个字符串的话，字符串中的class的名字之间应该有多余一个的空格。

2.如果表达式是一个数组，数组中的每一个元素都应该class名字之间多余一个的空格所构成的字符串。

3.如果表达式是一个对象，对于对象中的每一组kv值，相应的key值都应该是一个class的名字。

指令不会添加重复的class,如果一个指定的class已经被设定了。

当一个表达式发生改变的时候，之前添加的class会被移除掉，在这之后新的class才会被添加进去。

指令信息：

这个指令执行时的优先级是0.

用法：

作为一个属性:

<ANY
  ng-class="">
...
</ANY>

作为一个CSS class:

<ANY class="ng-class: ;"> ... </ANY>

动画：
添加事件发生在class应用于元素之前，移除事件发生在class从元素移除之前。

参数：
ngClass 	表达式	需要解析的表达式。////

例子：
通过ngClass指令演示基础的绑定的例子。
index.html:
<p ng-class="{strike: deleted, bold: important, red: error}">Map Syntax Example</p>
<input type="checkbox" ng-model="deleted"> deleted (apply "strike" class)<br>
<input type="checkbox" ng-model="important"> important (apply "bold" class)<br>
<input type="checkbox" ng-model="error"> error (apply "red" class)
<hr>
<p ng-class="style">Using String Syntax</p>
<input type="text" ng-model="style" placeholder="Type: bold strike red">
<hr>
<p ng-class="[style1, style2, style3]">Using Array Syntax</p>
<input ng-model="style1" placeholder="Type: bold, strike or red"><br>
<input ng-model="style2" placeholder="Type: bold, strike or red"><br>
<input ng-model="style3" placeholder="Type: bold, strike or red"><br>

style.css
.strike {
  text-decoration: line-through;
}
.bold {
    font-weight: bold;
}
.red {
    color: red;
}

protractor.js:
var ps = element.all(by.css('p'));

it('should let you toggle the class', function() {

  expect(ps.first().getAttribute('class')).not.toMatch(/bold/);
  expect(ps.first().getAttribute('class')).not.toMatch(/red/);

  element(by.model('important')).click();
  expect(ps.first().getAttribute('class')).toMatch(/bold/);

  element(by.model('error')).click();
  expect(ps.first().getAttribute('class')).toMatch(/red/);
});

it('should let you toggle string example', function() {
  expect(ps.get(1).getAttribute('class')).toBe('');
  element(by.model('style')).clear();
  element(by.model('style')).sendKeys('red');
  expect(ps.get(1).getAttribute('class')).toBe('red');
});

it('array example should have 3 classes', function() {
  expect(ps.last().getAttribute('class')).toBe('');
  element(by.model('style1')).sendKeys('bold');
  element(by.model('style2')).sendKeys('strike');
  element(by.model('style3')).sendKeys('red');
  expect(ps.last().getAttribute('class')).toBe('bold strike red');
});

动画：
下面的例子展示了怎样使用ngClass来演示动画。
index.html:

<input id="setbtn" type="button" value="set" ng-click="myVar='my-class'">
<input id="clearbtn" type="button" value="clear" ng-click="myVar=''">
<br>
<span class="base-class" ng-class="myVar">Sample Text</span>

style.css:
.base-class {
  -webkit-transition:all cubic-bezier(0.250, 0.460, 0.450, 0.940) 0.5s;
  transition:all cubic-bezier(0.250, 0.460, 0.450, 0.940) 0.5s;
}

.base-class.my-class {
  color: red;
  font-size:3em;
}

protractor.js:
it('should check ng-class', function() {
  expect(element(by.css('.base-class')).getAttribute('class')).not.
    toMatch(/my-class/);

  element(by.id('setbtn')).click();

  expect(element(by.css('.base-class')).getAttribute('class')).
    toMatch(/my-class/);

  element(by.id('clearbtn')).click();

  expect(element(by.css('.base-class')).getAttribute('class')).not.
    toMatch(/my-class/);
});

ngClass和现有的CSS3的动画：

ngClass指令依然支持CSS3动画，尽管他们并不遵守ngAnimate CSS的命名结构。////