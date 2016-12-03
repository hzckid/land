# land
test github
作为public 类应该和文件名一致 源文件中公关类名要与文件名相同

why system.out？ 
//		Properties properties=System.getProperties();//获取全部属性
//		properties.list(System.out);//system.out 是printscream流

		String  valueString=System.getProperty("os.name");//获取指定属性
		System.out.println("当前系统："+valueString);

ctrl+shift+/  添加多行注释
ctrl+shift+\  取消多行注释

java中无论数组或者集合，指针一般指向最后一个元素在后面一个位置，所以（from2，to3）这样一个参数里面只有一个值index==2的值。


StringBuilder是一个容器。添加使用append。


字符串实现了Comparable接口，可以通过字符串的comparaTo方法比较。

SimpleDataFormat 对时间处理   parse()  转换时间。






eclipse的基本使用：
alt+/  内容补全

ctrl+1 快速修复

alt+ 上下方向键  移动代码

tab 向右移动代码
alt+tab 向左移动代码

ctrl+/  单行注释
ctrl+\  取消单行注释

ctrl+shift+/  多行注释
ctrl+shift+\  取消多行注释

ctrl+shift+F  代码格式化

ctrl+shift+o  快速导包

ctrl+D   删除当前行


构造函数，set get函数快捷键：自定义
	keys->constructor using field->ctrl+q  有参构造函数
	keys->constructor from superclass->任意快捷键     无参构造函数

	keys->getter->ctrl+E   set与get快捷键


ctrl+shift+T  快速查找与查看源代码

ctrl+shift+X  更改为大写
ctrl+shift+Y  更改为小写

断点调试：可以让程序停留在指定的地方，然后观察目前程序的数据，分析问题的原因。
	step over 跳过本行代码
	step into 进入方法内部
	step return 结束方法，返回数据。

全体改名  右击refactor +rename



凡是数组内存地址的都是以中括号[开头的。
