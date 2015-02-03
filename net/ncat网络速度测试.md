### udp网络速度测试
在机器A上 需要可以监听udp端口
```
cat /dev/zero | pv -L 1M -B 1024 | ncat -u -l 80
```

在机器B上 不需要监听端口,需要可以
