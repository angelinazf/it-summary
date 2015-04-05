### 命令 -- bytecount
使用 bytecount n 开始查看流量使用情况,其中n是间隔秒数,openvpn会在当前命令行中每过n秒之后发出一个BYTECOUNT_CLI消息
实际使用样例
```
bytecount 10                           #输入
SUCCESS: bytecount interval changed    #openvpn返回数据
```

### 命令 -- version
实际使用样例
```
version                               
OpenVPN Version: OpenVPN 2.3.2 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [EPOLL] [PKCS11] [eurephia] [MH] [IPv6] built on Dec  1 2014
Management Version: 1
END
```

### 命令 -- status
```
status
TITLE,OpenVPN 2.3.2 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [EPOLL] [PKCS11] [eurephia] [MH] [IPv6] built on Dec  1 2014
TIME,Sun Mar 29 23:01:00 2015,1427641260
HEADER,CLIENT_LIST,Common Name,Real Address,Virtual Address,Bytes Received,Bytes Sent,Connected Since,Connected Since (time_t),Username
CLIENT_LIST,54a10d5f8ddf870f8167463b,xxx.xxx.xxx.222:24321,172.20.128.4,429663,1646854,Sun Mar 29 22:26:53 2015,1427639213,UNDEF
HEADER,ROUTING_TABLE,Virtual Address,Common Name,Real Address,Last Ref,Last Ref (time_t)
ROUTING_TABLE,172.20.128.4,54a10d5f8ddf870f8167463b,xxx.xxx.xxx.222:24321,Sun Mar 29 23:00:59 2015,1427641259
GLOBAL_STATS,Max bcast/mcast queue length,0
END
```

### 消息 -- CLIENT
当使用--management-client-auth的时候会出现:
	>CLIENT:DISCONNECT,3
	>CLIENT:ADDRESS,4,172.20.128.2,1
	>CLIENT:CONNECT,4,0
	>CLIENT:ESTABLISHED,2
当不使用--management-client-auth时,只有
	>CLIENT:ESTABLISHED,2
	已经确认,连断开连接的请求都不发.估计要定时自行拉取状态
实际数据样例
```
>CLIENT:ESTABLISHED,2
>CLIENT:ENV,n_clients=3
>CLIENT:ENV,time_unix=1427639213
>CLIENT:ENV,time_ascii=Sun Mar 29 22:26:53 2015
>CLIENT:ENV,ifconfig_pool_netmask=255.255.128.0
>CLIENT:ENV,ifconfig_pool_remote_ip=172.20.128.4
>CLIENT:ENV,trusted_port=24321
>CLIENT:ENV,trusted_ip=xxx.xxx.xxx.222
>CLIENT:ENV,common_name=54a10d5f8ddf870f8167463b
>CLIENT:ENV,untrusted_port=24321
>CLIENT:ENV,untrusted_ip=xxx.xxx.xxx.222
>CLIENT:ENV,tls_serial_0=1
>CLIENT:ENV,tls_digest_0=fc:fe:6b:46:10:f1:21:8a:a0:da:a8:d2:03:52:c2:c7:6d:61:86:2e
>CLIENT:ENV,tls_id_0=O=54a10d5a8ddf870f81674631, CN=54a10d5f8ddf870f8167463b
>CLIENT:ENV,X509_0_CN=54a10d5f8ddf870f8167463b
>CLIENT:ENV,X509_0_O=54a10d5a8ddf870f81674631
>CLIENT:ENV,tls_serial_1=1
>CLIENT:ENV,tls_digest_1=4a:c4:3e:2d:ff:bc:a1:42:fc:23:16:a5:62:44:49:6b:1c:5b:f9:2f
>CLIENT:ENV,tls_id_1=O=54a10d5a8ddf870f81674631, CN=54a10d5a8ddf870f81674632
>CLIENT:ENV,X509_1_CN=54a10d5a8ddf870f81674632
>CLIENT:ENV,X509_1_O=54a10d5a8ddf870f81674631
>CLIENT:ENV,remote_port_1=14521
>CLIENT:ENV,local_port_1=14521
>CLIENT:ENV,proto_1=udp
>CLIENT:ENV,daemon_pid=15266
>CLIENT:ENV,daemon_start_time=1427638692
>CLIENT:ENV,daemon_log_redirect=0
>CLIENT:ENV,daemon=1
>CLIENT:ENV,verb=1
>CLIENT:ENV,config=/etc/openvpn/server.conf
>CLIENT:ENV,ifconfig_local=172.20.128.1
>CLIENT:ENV,ifconfig_netmask=255.255.128.0
>CLIENT:ENV,ifconfig_broadcast=172.20.255.255
>CLIENT:ENV,script_context=init
>CLIENT:ENV,tun_mtu=1500
>CLIENT:ENV,link_mtu=1558
>CLIENT:ENV,dev=tun0
>CLIENT:ENV,dev_type=tun
>CLIENT:ENV,redirect_gateway=0
```

### 命令 client-auth-nt {CID} {KID}
必须开账号密码模式
CID和KID来自 >CLIENT:CONNECT
认证通过 某个用户

### 命令 client-deny {CID} {KID} "reason-text" ["client-reason-text"]
必须开账号密码模式
认证失败 某个用户

### 注意事项
* openvpn的management是一对一的. 即使openvpn的managment处于监听状态,也只能有一个客户端可以连接进去,其他客户端的连接都会被挂起.前一个用户端口,后一个用户就可以连接进去了.

### 认证方式总结
* 密码认证,用户使用比较麻烦,用户使用最简单的方法仍然需要导入两个文件.(应该是可以使用的,不会是什么严重的问题.)
* 证书认证,应该只有客户端证书的common_name可以传递出数据来,会明文传输.
	缺点在于生成证书的过程比较麻烦,而且消耗服务器时间.
	managment里面 只能在ESTABLISHED之后才可以kill用户(刚看到用户)
	可以使用 client-connect 回调来验证用户是否存在,并且还有流量
	可以使用 client-disconnect 回调来表示用户已经离线了. 还可以看到消耗的流量





