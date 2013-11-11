* 下列操作均需要登录进入mysql,并执行sql

### 修改密码
```
SET PASSWORD For 'mysqlUser'@'%' = PASSWORD('xxx');
```

### 添加用户,并给予管理员权限
```
CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
```