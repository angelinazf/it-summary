参考资料: http://www.g-loaded.eu/2005/11/10/be-your-own-ca/

### 概念及步骤
* 先自己创建一个CA
  * 创建CA的公钥ca.crt,私钥ca.key,
  * 创建序列号(下一张证书的序列号)
* 配置openssl
* 创建某个域名的服务器证书
  * 创建 证书请求 xxx.com.csr 和私钥 xxx.com.key
  * 用CA签 证书请求得到证书 xxx.com.crt
* 分发ca.crt给客户端(浏览器)
* 使用xxx.com.crt和xxx.com.key在apache2中创建https服务器(虚拟主机)

### 其他事务:
  * 创建PEM文件(有私钥,也有证书)
```
cat certs/xxx.com.crt private/xxx.com.key > private/server-key-cert.pem
```
  * 吊销某个域名的服务器证书
    * 吊销信息会被写入ca.crl文件

  
