##### XSS解决方案
### 规则0
* 只能在后面的 规则1,规则2,规则3,规则5 描述的位置上放 不信任的数据 ,不要在其他任何位置放 不信任的数据
* 不要运行不信任的代码

### 规则1 - 标签内容
* 可以把不信任的数据放置在HTML的内容部分,需要进行转义 php函数: h转义 eh转义并显示
* 放置位置例示:
```
<body>...ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE...</body>
<div>...ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE...</div>
```

### 规则2 - 标签属性值
* 可以把不信任的数据放在HTML的标签的属性的值的部分,需要进行转义 php函数: h转义 eh转义并显示
* 此时必须使用引号把属性值括起来
* 放置位置例示:
```
<div attr='...ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE...'>content</div>   inside single quoted attribute
 
<div attr="...ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE...">content</div>   inside double quoted attribute
<input type="text" name="fname" value="ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE">
```

### 规则3 - json数据
* 可以把不信任的数据json_encode后放置在script标签里面,需要进行转义(不仅仅是json_encode) php函数: ejson转义并显示
* 放置位置例示:
```
<script>
     var initData = ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE;
</script>
```

### 规则5 - url参数
* 可以把数据放在url的query的参数值部分 ,需要进行转义 php函数: urlv转义 eurlv转义并显示
```
<a href="http://www.somesite.com?test=...ESCAPE UNTRUSTED DATA BEFORE PUTTING HERE...">link</a >    
```
### 规则6 - html插入
* 使用专门的html过滤库 过滤用户输入的html
* 放置位置示例:
```
<div>UNTRUSTED HTML</div>
```

### 注意事项:
* 如果是模板上写死的信息,只要符合html标准,怎么写都可以.
* 返回json数据时,保证Content-Type是application/json,而不是text/html,避免被Xss攻击
* 禁止直接插入不信任的url.
* 本解决方案参考 https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet

### 禁止放置数据的地方
原因:
* 放在下列位置不知道如何安全转义
* 没有需求,或者可以由其他方式传递数据
```
<div attr=...UNTRUSTED DATA...>content</div>           没有引号的属性值
<div style="width: UNTRUSTED DATA;">Selection</div>    css的任何地方
<script>var currentValue='UNTRUSTED DATA';</script>    js字符串
<script>someFunction('UNTRUSTED DATA');</script>       在函数里面的js字符串
<script>...NEVER PUT UNTRUSTED DATA HERE...</script>   js的某个地方
<!--...NEVER PUT UNTRUSTED DATA HERE...-->             html注释的某个地方
<div ...NEVER PUT UNTRUSTED DATA HERE...=test />       属性名
<NEVER PUT UNTRUSTED DATA HERE... href="/test" />      标签名
<style>...NEVER PUT UNTRUSTED DATA HERE...</style>     css的任何地方
```


### 攻击方法
  你以为这个数据被当作字符串(或数据)含义处理,但实际上被当作其他含义处理.而其他含义有可执行权限.
例如:
使用`index.php?name=guest<script>alert('attacked')</script>`访问下列php脚本
```
<?php
$name = $_GET['name'];      //获得 $name 这个字符串
echo "Welcome $name<br>";   //$name被转换成了html字符串类型,可以被浏览器执行.
echo "<a href="http://xssattackexamples.com/">Click to Download</a>";
?>
```

* 你以为$name是一个字符串,却被当作html的含义处理,html具有可执行权限,被浏览器执行.



### TODO:
* 上传图片的url的XSS处理(解决上传安全问题时解决)