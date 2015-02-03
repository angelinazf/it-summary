### 生成私钥 PKCS1格式
```
openssl genrsa -out key.pem 2048
```
其中private_key.pem是输出的私钥

### 私钥转成公钥 PKIX格式
```
openssl rsa -in key.pem -pubout -out pubkey.pem
```

### 私钥 从PKCS1格式转成 pkcs8 格式
```
openssl pkcs8 -topk8 -inform PEM -in key.pem -outform PEM -nocrypt > key_pkcs8.pem
```



### 使用私钥签名
```
openssl rsautl -sign -in file -inkey in.key -out sig
```
其中in.key是rsa私钥,file是输入数据,sig是输出数据存放位置

### 使用公钥验证签名
```
```

### 使用公钥加密
```
openssl rsautl -encrypt -in file -pubin -inkey in.pub -out sig
```

### 文档查看
```
man genrsa
man rsautl
man rsa
```