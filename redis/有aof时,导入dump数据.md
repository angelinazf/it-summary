1.修改配置 关闭aof
2.关闭redis
3.cp dump.rdb /var/lib/redis/dump.rdb
4.开启redis
5.redis-cli config set appendonly yes
6.修改配置打开aof
完毕

### 参考
* http://serverfault.com/a/692934/282459