目前观测到udp的write有下列错误信息:
	* write udp 10.1.0.11:60979-\u003e120.24.249.92:31004: write: can't assign requested address (mac关掉wifi 设备.)
	* write udp 10.1.0.42:40833-\u003e120.24.249.92:31004: write: no such device (android关掉wifi,然后又打开wifi,之后的报错)
	* write udp 10.1.0.42:40833-\u003e120.24.249.92:31004: write: invalid argument (android 关掉 wifi 之后的报错.)

已知原因:
	* 本机的网络设备断开 (mac上)
	* 本机ip和连接udp的时候的ip不一样 (待确认)
	* wifi变成 3g 或 3g 变成wifi (待确认)

根据已有现象判断:
	udp write失败,100%表示

客户端反复重连实现:
1.ClientManager 设定希望的状态
2.出现错误后,把希望状态改为close,并且关闭vpn连接
3.当出现网络设备问题时,每秒尝试重新建立一遍,共尝试30秒,如果超过30秒仍然解决不了,就断开连接.