```
vim /etc/network/interface
```
# loopback回环
修改`/etc/network/interface`
```
auto lo
iface lo inet loopback
```

# 静态ip
修改`/etc/network/interface`
```
auto eth0
iface eth0 inet static
    address 192.168.1.5
    netmask 255.255.255.0
    network 192.168.1.0
    broadcast 192.168.1.255
    gateway 192.168.1.1
    # dns-* options are implemented by the resolvconf package, if installed
    dns-nameservers 192.168.1.1
    dns-search dashu.us
```

# 使配置生效
在bash里面运行
```
sudo /etc/init.d/networking restart
```