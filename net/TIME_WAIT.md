##### 超时时间
目前没有找到可以在linux上修改这个超时时间的办法.
```
echo 1 > /proc/sys/net/ipv4/tcp_tw_recycle
```

### 注意
* 参考http://www.stolk.org/debian/timewait.html
* 已经使用ubuntu 1404测试过 `net.ipv4.netfilter.ip_conntrack_tcp_timeout_time_wait = 1` 没有效果