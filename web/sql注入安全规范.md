sql注入问题核心: 你以为这个数据被当作字符串这个含义处理,但实际上被当作其他含义处理.而其他含义有更高权限.

sql注入解决: 分离sql字符串和数据
* sql和数据分离使用PDO::
### PDO解决方案:
```
$stmt = $pdo->prepare('SELECT * FROM employees WHERE name = :name');
$stmt->execute(array('name' => $name));
foreach ($stmt as $row) {
    // do something with $row
}
```

### mysqli解决方案:
```
$stmt = $dbConnection->prepare('SELECT * FROM employees WHERE name = ?');
$stmt->bind_param('s', $name);
$stmt->execute();
$result = $stmt->get_result();
while ($row = $result->fetch_assoc()) {
    // do something with $row
}
```

### 已知下列框架没有使用prepare方案: 
  * Thinkphp  mysql_real_escape_string转义+拼接sql字符串
  * phpcms    数据过滤+拼接sql字符串
  * ci        ??

### 对已有应用框架的完美解决方案: 
* 重新开发数据库接口部分
* 新代码使用新数据库接口
* 大量扫描旧代码

### 对已有应用的不完美解决方案:
* 使用已有框架的接口
* 对数据进行过滤
* mysql_real_escape_string转义一般出现会多次转义之类的问题.

### sql非数据参数传入问题(表名,字段名,limit)
* 使用字符白名单过滤 限制只能使用 0-9a-zA-Z_ 遇到不正确的字符,报错


### php的sql注入问题解决方案详细解释:
http://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php

### mysql_real_escape_string不能解决问题的证明
http://ilia.ws/archives/103-mysql_real_escape_string-versus-Prepared-Statements.html