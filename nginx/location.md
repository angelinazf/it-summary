### location优先级问题
* `location = /upload ` 精确location
* `location ~ /upload ` 正则location 按照出现在配置文件中的顺序进行匹配
* `location /upload` 前缀location 最长的匹配想会被选中

* 正则优先级 比 前缀高
* 前缀location可以用`^~` 提高优先级(但是也要是最长匹配)

