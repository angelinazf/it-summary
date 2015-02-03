### 第一步,在命令行上,使用tcpdump在命令行劫包
##### 对外网卡
```
sudo tcpdump -i eth0 -s 65535 -w 1.tcpdump
```


如果觉得,获取到足够的信息,在命令行上面按ctrl+c,结束本次劫包

### 第二步,在桌面上,使用wireshark打开这个1.tcpdump
### 截取全部网卡
```
sudo tcpdump -i any -s 65535 -w 1.tcpdump
```

### 不截取ssh流量
```
sudo tcpdump -i any -s 65535 -w 1.tcpdump port not 22
```

### 远程截取,并且实时下载到本地(DD-WRT),不需要服务器有硬盘空间
```
ssh root@192.168.1.1 "tcpdump -w - -i any port not 22" > mypackets.pcap
```