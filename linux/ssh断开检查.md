### 问题
* ssh总是会卡住,而不是自动检测它挂掉了.

### 解决方法
在客户机器的 /etc/ssh/ssh_config 加上
```
ServerAliveInterval 10
ServerAliveCountMax 3
```
表示每隔10秒发一个keepalive的包,如果发了3个包都没有收到返回的包,则掐断这个连接
