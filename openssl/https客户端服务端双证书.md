##### ubuntu bash使用方法
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
把ca.crt和client.pfx发给用户,用户导入证书就可以了.
服务器端 从安全上考虑,下列文件内容需要保密: server.key ca.key
客户端 从安全上考虑,下列文件内容需要保密: client.pfx

### 注意事项
* ca的密码必须设置,至少4位
* 在命令执行的过程,中会出现大量要求填信息的地方,如实填写即可,此处所有填的信息会明文发送
* CommonName是服务器域名,可以使用 *.xxx.com 这样的泛域名,填的和实际域名不匹配,浏览器会报错,但是可以跳过.不要填端口,该域名的任何端口都可以用这张证书
* mac上导入客户端证书必须在pfx上使用密码

##### apache2配置
```
listen 28841
<VirtualHost *:28841>
    ServerName www.xxx.com
    DocumentRoot /var/xxx/adminWeb
    SSLEngine on
    SSLCertificateFile /var/cert/xxx/server.crt
    SSLCertificateKeyFile /var/cert/xxx/server.key
    SSLVerifyClient require
    SSLVerifyDepth 1
    SSLCACertificateFile /var/cert/xxx/ca.crt
</VirtualHost>
```
