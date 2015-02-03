注意把后面的10.1.1.5 修改为服务器的ip地址
```
# ca证书
ipsec pki --gen --outform pem > caKey.pem
ipsec pki --self --in caKey.pem --dn "C=CN, O=strongSwan, CN=strongSwan CA" --ca --outform pem > caCert.pem
# server证书
ipsec pki --gen --outform pem > serverKey.pem
ipsec pki --pub --in serverKey.pem | ipsec pki --issue --cacert caCert.pem --cakey caKey.pem --dn "C=CN, O=strongSwan, CN=10.1.1.5" --san="10.1.1.5" --flag serverAuth --flag ikeIntermediate --outform pem > serverCert.pem
# 客户端证书
ipsec pki --gen --outform pem > clientKey.pem
ipsec pki --pub --in clientKey.pem | ipsec pki --issue --cacert caCert.pem --cakey caKey.pem --dn "C=CN, O=strongSwan, CN=client" --outform pem > clientCert.pem

# p12格式
openssl pkcs12 -export -inkey clientKey.pem -in clientCert.pem -name "client" -certfile caCert.pem -caname "strongSwan CA" -out clientCert.p12

# 安装证书
cp caCert.pem /usr/local/etc/ipsec.d/cacerts/
cp serverCert.pem /usr/local/etc/ipsec.d/certs/
cp serverKey.pem /usr/local/etc/ipsec.d/private/
```

/etc/ipsec.conf
```
config setup
    strictcrlpolicy=no
    uniqueids=no #允许多设备同时在线
conn windowsphone
    keyexchange=ikev2
    ike=aes256-sha1-modp1024!
    esp=aes256-sha1!
    dpdaction=clear
    dpddelay=300s
    rekey=no
    left=%defaultroute
    leftsubnet=0.0.0.0/0
    leftauth=pubkey
    leftcert=serverCert.pem
    leftid="C=CN, O=strongSwan, CN=X.X.X.X" #C=国家，CN=自己vps的公网ip
    right=%any
    rightsourceip=10.11.1.0/24 #为客户端分配的虚拟地址池
    rightauth=eap-mschapv2
    rightsendcert=never
    eap_identity=%any
    auto=add
```

/etc/ipsec.secrets
```
: RSA serverKey.pem
: EAP "123"
```

/etc/strongswan.conf
```
charon {
    dns1 = 8.8.8.8
    dns2 = 208.67.222.222
}
```

配置iptables
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -s 10.11.1.0/24 -o eth0 -j MASQUERADE  #地址与上面地址池对应
```
