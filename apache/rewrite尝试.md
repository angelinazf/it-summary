apache2 rewrite 规则过度复杂,下面列举各种尝试,及其产生的效果,以此尝试逆向各种规则.
apache 版本 2.4.10

#### 结论
### 跳转
```
RewriteEngine On
RewriteRule    ^en/qrpf$ /1.php [R]
```
可以携带GET 的query信息

### 多条规则混合
```
RewriteEngine On
RewriteRule    ^en/qrpf$ /2.php [R,L]
RewriteCond %{REQUEST_FILENAME} !-f    
RewriteRule ^(.*)$ 1.php [QSA,L]
```


#### 实验
### 跳转
```
RewriteEngine On
RewriteRule    ^en/qrpf$ /1.php [R]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 会跳转到 http://127.0.0.1:23456/1.php?a=12

```
RewriteEngine On
RewriteRule    ^en/qrpf$ 1.php [R]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 会跳转到 http://127.0.0.1:23456/var/www/test1/1.php?a=12

```
RewriteEngine On
RewriteRule    ^/en/qrpf$ 1.php [R]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 404




### 跳转并且修改query参数的名字
```
RewriteEngine On
RewriteRule ^en/qrpf?a=(.*)$ /2.php?b=$1 [R,L]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 404



### 多条规则混合
```
RewriteEngine On
RewriteRule    ^en/qrpf$ /2.php [R]
RewriteCond %{REQUEST_FILENAME} !-f    
RewriteRule ^(.*)$ 1.php [QSA,L]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 302 但是没有跳转地址,却访问到了1.php文件

```
RewriteEngine On
RewriteRule    ^en/qrpf$ /2.php [R,L]
RewriteCond %{REQUEST_FILENAME} !-f    
RewriteRule ^(.*)$ 1.php [QSA,L]
```
访问 http://127.0.0.1:23456/en/qrpf?a=12 302 会跳转到 http://127.0.0.1:23456/1.php?a=12