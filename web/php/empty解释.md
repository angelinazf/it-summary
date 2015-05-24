* isset()：仅当null和未定义，返回false；
* empty()：""、0、"0"、NULL、FALSE、array(),未定义，均返回false；
* is_null()：仅判断是否为null，未定义 报警告；
* 变量本身作为参数，与empty()一致，但接受未定义变量时，报警告；