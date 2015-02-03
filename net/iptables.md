### 查看已有规则
```
iptables -L -v
iptables-save
```

### 屏蔽单个ip
```
iptables -A INPUT -s 10.10.10.10 -j DROP
```

### 屏蔽一组ip
```
iptables -A INPUT -s 10.10.10.0/24 -j DROP
iptables -A INPUT -s 10.10.10.0/255.255.255.0 -j DROP
```

### 屏蔽某个ip的某个端口
```
iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -j DROP
```

### 屏蔽某个端口
```
iptables -A INPUT -p tcp --dport ssh -j DROP
```

### TProxy流量代理
```
iptables -t mangle -A PREROUTING -s 172.19.254.0/24 -p tcp -j TPROXY --on-ip 127.0.0.1 --on-port 23498 --tproxy-mark 0x1/0x1
```

### vpn客户端全局流量
要先开net.ipv4.ip_forward=1
```
iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth0 -j MASQUERADE
iptables -A FORWARD -p tcp --syn -s 192.168.0.0/24 -j TCPMSS --set-mss 1356
```

iptables -t nat -A POSTROUTING -s 172.19.254.0/24 -p udp -o eth0 -j MASQUERADE
iptables -A FORWARD -p tcp --syn -s 172.19.254.0/24 -j TCPMSS --set-mss 1356
