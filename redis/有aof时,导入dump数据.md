
4.修改配置 关闭aof
2.关闭redis
3.cp dump.rdb /var/lib/redis/dump.rdb
4.开启redis
4.redis-cli config set appendonly yes
6.完毕