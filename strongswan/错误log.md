此处是所有曾经遇到过的错误,及其解决方案:

### 客户端log IDir '10.xxx.xxx.xxx' does not match to '121.xxx.xxx.143'
	* 出现错误时使用ikev1-xauth-psk
	* 这个是因为客户端没有写rightid,服务端没有写leftid,并且服务端处于nat状态下(本地ip和公网ip不一致)
	* 在客户端上写上 rightid=%any解决问题

### 客户端log XAuth authentication of 'xxx' (myself) failed
	* 出现错误时使用ikev1-xauth-psk
	* 原因不明
	* 删除leftauth leftauth2 rightauth rightauth2 解决问题

### 客户端log received INVALID_ID_INFORMATION error notify
	* 出现错误时使用ikev1-xauth-psk
	* 客户端没有配置虚拟ip
	* 在客户端写上     leftsourceip=%config 解决问题