finished by GGOD1993

a

修改了html中a标签的默认行为，所以当href属性是空的时候默认行为是被禁止的。

这个改变允许使用ngClick指令创建简单的动作链接而不会改变位置或者使界面重新载入，

例如：

<a href = "" ng-click = "list.addItem()">Add Item</a>

指令信息：

这个指令在执行时它的优先级是0.

用法：

作为元素：

<a>
...
</a>