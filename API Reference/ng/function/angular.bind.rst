finished by GGOD1993

angular.bind

返回一个将fn和self绑定的函数(self变成了fn中的this).你可以提供可选的args来对函数进行预绑定。这个特性被大家称为偏函数，和函数加里化一样为人们熟知。

用法：

angular.bind(self, fn, args);

参数：

self  Object	fn应该进行赋值的对象。

fn	function()	绑定的函数

args	*    可选的与fn函数进行预绑定的参数。

返回值：

function()	一个包装了fn所有指定的绑定的函数。