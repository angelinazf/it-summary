```
mysql -uroot -p -e "SET PASSWORD For 'root'@'localhost' = PASSWORD('')"
```

### 注意事项
* 使用空密码后,可以直接使用 `mysql -uroot` 登入mysql查看信息.
* 使用空密码后,为了安全起见,请监听127.0.0.1 避免mysql被人访问到.