### 在本地A监听,转发所有请求给远程某机器B
要求远程机器可以接受tcp连接
```
ncat --sh-exec 'ncat www.google.cn 80' -l 8081
```