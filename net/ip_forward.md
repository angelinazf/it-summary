### 查看是否开启
```
cat /proc/sys/net/ipv4/ip_forward
```
返回1表示开启,返回0表示不开启

### 开启
```
echo 1 > /proc/sys/net/ipv4/ip_forward				# 在本次启动开启这个选项.
echo 'net.ipv4.ip_forward = 1' >> /etc/sysctl.conf  # 下次启动后开启这个选项.
```

### 注意事项
* 此命令开启后,当前机器的所有进程有效(没有bash的session问题.)
* 此开启命令,重启后有效
* 多次多次对配置进行写入不会出现问题.