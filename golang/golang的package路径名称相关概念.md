golang的package路径名称相关概念:
* PkgName 
	* 包的名字.
	* 某个go文件上面写的package名称.
	* 正常情况: PkgName和PkgPath的最后一部分一致.并且所有go文件里面必须使用同一个PkgName.
	* 测试特殊情况: 某个目录下最多可以有2个PkgName,一个叫 xxx ,另一个可以叫 xxx_test
	* main特殊情况: PkgName可以叫main,此时PkgImportPath也要是main,但是PkgPath仍然是目录名称
	* 别名特殊情况: 某个目录下的PkgName不需要和PkgPath的最后一部分一致.
	* 不同编译平台特殊情况: 当多组编译选项不同时,可以出现一个目录里面包含多个package的情况.
	* 含义和作用: 用于import的时候,写 os.Chdir 里面的 "os" 部分.
* PkgPath 
	* 包的文件路径.
	* 从某个 GOPATH/src 开始的目录名称,但是不包含src.
	* 含义和作用: 用于寻找某个package实际包含的文件路径.
* PkgImportPath
	* 包的引入路径.
	* 正常情况: 值和PkgPath一致
	* main特殊情况: 在 PkgName 是main的情况下,该名称为 main
	* 含义和作用: 用于比较某个对象是否在同一个package里面,生成import的时候,可以使用这个值.