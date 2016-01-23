函数变量:
	* 完成相同功能,代码量最小.
	* 只能包含一个函数接口.

interface:
	* 当使用struct做interface的实现的时候,可以使用json进行序列化.此种情况下,代码复杂度仍然要高于函数变量 (golang里面的json不支持自动interface序列化.)
	* 一个interface可以包含多个函数接口.

函数变量的struct:
	* 数据与代码分离比较差.
	* 需要做序列化时,需要再写一个struct.
	* 当作为函数的request可以多传入一个字段.

class继承:
	* 代码量比interface稍多.
	* 一个class只能继承一个父类.
	* 父类可以使用抽象方法调用子类.

结论:
	* 当一个接口只有一个函数,请使用函数变量.
	* 当一个接口有一个函数时,可以使用interface.