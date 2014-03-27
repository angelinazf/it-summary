url
========
完整样例:http://pass@user:example.com/path1/path2.php?a=1&b=2#xxx
一般使用:http://example.com/path1/path2.php?a=1&b=2

method http方法
========
### GET
缺点: 
* 传输数据有限(某些gateway限制url不能超过10k)
* 不能上传文件
* 会被缓存

### POST
缺点:
* 用来显示html,用户刷新会弹"是否重新提交"
* 不会被缓存(少数gateway会缓存...)

### 其他方法
缺点:
* 某些gateway不支持


Content-Type
=============
### 上传文件的协议
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryiUiybIV44BXASZOR

### html form 提交协议
Content-Type:application/x-www-form-urlencoded