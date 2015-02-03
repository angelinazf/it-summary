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

  
### https客户端服务端双证书bash代码
```
mkdir -p /var/cert/alumnixyt
cd /var/cert/alumnixyt
cp /etc/ssl/openssl.cnf ./
touch index.txt
echo '01' > serial
openssl req -config openssl.cnf -new -x509 -extensions v3_ca -keyout ca.key -out ca.crt -days 18250 # 生成ca
```
改配置文件 
```
dir     = .                # <--CHANGE THIS
certificate = $dir/ca.crt   # <--CHANGE THIS
private_key = $dir/ca.key    # <--CHANGE THIS
new_certs_dir   = $dir/     # default place for new certs.
default_days    = 3650          # how long to certify for
```

继续执行脚本
```
openssl req -config openssl.cnf -new -nodes -keyout server.key -out csr.csr -days 18250 # 生成服务器端的csr
openssl ca -config openssl.cnf -policy policy_anything -out server.crt -infiles csr.csr # 使用ca签刚才的csr
cat server.crt server.key > server.pem # 打包服务器端证书
openssl req -config openssl.cnf -new -nodes -keyout client.key -out csr.csr -days 18250 # 生成客户端证书
openssl ca -config openssl.cnf -policy policy_anything -out client.crt -infiles csr.csr 
openssl pkcs12 -export -inkey client.key -in client.crt -out client.pfx # 生成pfx格式的客户端证书
```

### 注意事项
* ca的密码必须设置,至少4位
* 在命令执行的过程,中会出现大量要求填信息的地方,如实填写即可,此处所有填的信息会明文发送
* CommonName是服务器域名,可以使用 *.xxx.com 这样的泛域名,填的和实际域名不匹配,浏览器会报错,但是可以跳过.不要填端口,该域名的任何端口都可以用这张证书