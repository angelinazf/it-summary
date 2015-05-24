### 查看是否开启
```
cat /proc/sys/net/ipv4/ip_forward
```
返回1表示开启,返回0表示不开启

### 开启
```
echo 1 > /proc/sys/net/ipv4/ip_forward
echo 'net.ipv4.ip_forward = 1' >> /etc/sysctl.conf
```