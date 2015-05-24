### 添加路由项
```
ip route add 0.0.0.0/1 via 172.20.2.1 dev tun0
```

### 列出路由项
```
route -n
ip route show
```

### 删除路由项
* 后面的东西来自`ip route show`的某一行
```
ip route del 0.0.0.0/1 via 172.20.2.1 dev tun0
```
