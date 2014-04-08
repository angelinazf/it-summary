* 下列操作均需要登录进入mysql,并执行sql

### 修改密码
```
SET PASSWORD For 'mysqlUser'@'%' = PASSWORD('xxx');
```
```
SET PASSWORD For 'root'@'%' = PASSWORD('xxx');
```
```
SET PASSWORD For 'root'@'localhost' = PASSWORD('xxx');
```

### 添加用户,并给予管理员权限
```
CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
```

### 添加一个root用户,并给予管理员权限
```
CREATE USER 'root'@'%' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```

注意事项
==================
### 用户名构成
'mysqlUser'@'%' 前面是登录的用户名mysqlUser 后面的%表示那些ip的机器可以登录
* '%' 表示所有ip都可以登录
* '127.0.0.1' 表示这个ip 127.0.0.1 可以登录
