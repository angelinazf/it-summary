### 第一步,在命令行上,使用tcpdump在命令行劫包
```
sudo tcpdump -i eth0 -s 65535 -w 1.tcpdump
```
如果觉得,获取到足够的信息,在命令行上面按ctrl+c,结束本次劫包

### 第二步,在桌面上,使用wireshark打开这个1.tcpdump