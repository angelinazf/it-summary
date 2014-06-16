XSS问题核心: 你以为这个数据被当作字符串这个含义处理,但实际上被当作其他含义处理.而其他含义有更高权限.

Xss解决:
* 在模板上的html上下文对所有输出变量使用htmlspecialchar进行转义.
* 在模板上的js上下文对所有输出变量使用json_encode方法进行转义.
* 不要过滤输入数据,总是会漏掉一些情况.
* 不要在存入数据库的时候进行转义,再取出来进行处理的时候,很麻烦
* 如果储存的字段是html类型的,需要在存入数据库时使用库进行过滤.(尚不确定最佳方案)

### html上下文
使用下列函数,转义字符串
function h($str){
    return htmlspecialchars($str,ENT_QUOTES,'UTF-8');
}

### json上下文
##### 使用下列函数,转义数据(未测试)
function j($data){
    return strreplace('<','\u003c',json_encode($data));
}


### 解决方案详细解释:
https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet

### 注释
* 在模板的所有地方使用htmlspecialchars不能阻止XSS