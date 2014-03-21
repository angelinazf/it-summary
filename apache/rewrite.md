### ubunut打开rewrite
```
sudo a2enmod rewrite
```

### rewrite log 查看时处理
```
:%s/\([^\]]*\]\)\{4\}//g
```

### apache rewrite内部处理流程：
大概代码:
```
while(1){
  for (x in file.lines){ //每一行都执行
    isContinue = doMatch();
    if (!isContinue) continue; //可以用L退出本轮
  }
  if (!isNextIteration()) break; //在某些规则下会退出循环
}
```
### 用RewriteCond做判断
* 用RewriteRule做匹配。每一行匹配都都会执行，除非使用L或S等标志位
* 全部匹配完毕后，还会从开头开始，重新进入下一轮(iteration)匹配。
* 目前了解到有几种情况会停止匹配：（http://stackoverflow.com/a/6800150）
  * 本轮没有任何规则被匹配到。最常见。
  * 仅匹配到这种东西。RewriteRule .* -（经实验表明如果前面也匹配到其他东西，是会还会进入下一轮的）
  * （据说）本轮匹配的输入url和输出url一模一样。
* 加标志位L，如果匹配到会放弃后面的匹配，直接进入下一轮匹配
* 加标志位S=num，如果匹配到会跳过后面的num个规则，

### Fix for infinite loops
* 不进行下一轮匹配
* 一般用于阻止匹配死循环(加上一般不会有问题.)
* rewrite很神秘,不要乱改
```
RewriteCond %{ENV:REDIRECT_STATUS} 200
RewriteRule .* - [L]
```
### 把当前目录rewrite到另一个子目录(与直接把apache2虚拟主机根目录指到那个地方是一样的效果)
```
RewriteRule    ^$ app/webroot/    [L]
RewriteRule    (.*) app/webroot/$1 [L]
```
### 把当前目录的所有无法访问的请求rewrite到一个php文件上去(前端控制器)
```
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^(.*)$ index.php/$1 [QSA,PT,L]
```
### 允许某文件被访问
```
RewriteRule \.(jpeg|jpg|png|gif)$ - [L]
```
### 不允许某目录(文件)被访问
```
RewriteRule ^data/ - [R=404,L]
```
## rewrite文件框架
先阻止下一轮,然后先允许,后不允许,按顺序匹配
### 禁止某些扩展名的文件被访问
```
<FilesMatch "\.(bak|inc|lib|sh|lbi|dwt)$">
    order deny,allow
    deny from all
</FilesMatch>
```
### 关闭apache2默认的列出目录
```
Options -Indexes
```
### 打开rewrite
```
RewriteEngine On
RewriteBase /
```
### 只进行一轮匹配
```
RewriteCond %{ENV:REDIRECT_STATUS} 200
RewriteRule .* - [L]
```
### 允许访问的文件
```
RewriteRule \.(jpeg|jpg|png|gif)$ - [L]
```
### 禁止访问的目录
```
RewriteRule ^data/ - [R=404]
RewriteRule ^includes/(!fckeditor) - [R=404]
```
### 禁止用未知域名访问服务器,只要是用配置里面没有写过的域名去访问服务器就跳404
在http.conf的最前面写上
```
<VirtualHost *:80>
    RewriteEngine On
    RewriteRule .* - [R=404,L]
</VirtualHost>
```
