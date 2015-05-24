## ssh login with cert 用证书登录ssh 可以不提供密码
* https://help.ubuntu.com/community/SSH/OpenSSH/Keys
* https://help.github.com/articles/generating-ssh-keys

### 方法
* 如果你本机没有证书,你需要在本机生成一个ssh证书,
* 将这个证书的公钥添加到某个服务器下的某个用户的ssh认证列表中.
* 这样就可以在本机上使用这个证书登录该服务器上的该用户了,不需要使用密码.


### 客户端生成证书(!!!请先检查本机是否有证书!!!)
* 如果你以前在这个机器的这个用户上生成过证书,再次生成证书,会覆盖掉上一个证书,
* 上一个证书注册的那些服务器都会失效需要重新注册

```
mkdir ~/.ssh
chmod 700 ~/.ssh
ssh-keygen -t rsa
```

### 在客户端上 上传证书到服务器
#### 方法1(需要能登录上去,需要客户端是ubuntu)
```
ssh-copy-id <username>@<host>
```

#### 方法2
##### 先把你的证书的公钥 scp 到服务器上(在客户端执行)
```
scp ~/.ssh/id_rsa.pub <username>@<host>:~/
```

##### 再把你的证书的公钥 追加到服务的某个用户的证书列表的后面(在服务器端执行)
```
cat ~/id_rsa.pub >> /home/<username>/.ssh/authorized_keys
```

##### 方法3
ssh证书一行导入.注意修改端口域名用户名
```
ssh -p 11011 bronze1man@dashi.us 'umask 077; test -d ~/.ssh || mkdir ~/.ssh ; cat >> ~/.ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```

### 注意
* 注意:一定是追加,不要把别人的证书覆盖了
* 没有权限时可以用`sudo bash`提权
