angular.toJson
将一个输入序列化为一个JSON格式的字符串。从angular使用这个字符表示开始，以$$开头的属性字符会剥离。

用法：
angular.toJson(obj.pretty);

参数：
obj		对象，数组，日期，字符串，数字		输入被用来序列化为JSON字符串。

pretty		布尔，数字		////

返回值：
string		代表obj的JSON格式的字符串。