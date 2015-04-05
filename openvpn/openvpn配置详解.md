
### --server network netmask ['nopool']
	这个地方配置服务器需要分配给客户端的ip的范围,其中 参数要求 (network & netmask)==network,也就是说 
	server 172.20.128.0 255.255.128.0 是正确的,服务器占用 172.20.128.1 这个地址.
	server 172.20.129.0 255.255.128.0 是错误的
	此处配置错误会导致服务器无法启动.
	服务器自己会占用 .1 这个地址,可以在上面搭建dns什么的.

### --auth-user-pass [file]
	这个选项写在客户端上,用于输入账号密码.不填,会弹窗要求账号密码,填了会读取那个文件,然后从文件里面登陆,需要有特殊的编译选项,才可以读取账号密码文件.
	这个东西没有找到可以直接塞到 .ovpn 文件里面的办法.(已经确定不行)
	使用这个会大幅度增加用户使用成本(考虑不要使用)

### --management-client-auth
	服务器要求使用账号密码登陆,如果没有账号密码就不能登陆进来.这个密码在 management 接口上发送,并且需要在 management上面使用client-auth-nt 把用户认证进去.

### client-connect cmd
	所有需要的信息都在环境变量里面,主要是common_name这个变量管用
	可以返回 非0 返回值来表示阻止用户登陆.
	script_type=client-connect

### client-disconnect cmd
	所有需要的信息都在环境变量里面,主要是common_name这个变量管用
	script_type=client-disconnect
	script_context=init

### 注意事项
	回调的bash记住加 #!/bin/bash 否则无法执行

### 参考
	https://community.openvpn.net/openvpn/wiki/Openvpn23ManPage	