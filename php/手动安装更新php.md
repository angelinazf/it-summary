未完待续
### 安装方法
```
sudo apt-get update
sudo apt-get install apache2-prefork-dev # 如果这个装不上 apt-get里面的某些包的版本有问题...
sudo apt-get install libxml2-dev make autoconf
wget http://www.php.net/distributions/php-5.5.1.tar.xz # 官网上的连接,如果失效,上官网自己找去...
tar -xf php-5.5.1.tar.xz
cd php-5.5.1
./configure --with-apxs2=/usr/bin/apxs2 --with-mysql --enable-mbstring --enable-intl
make
sudo make install
pecl install apc
```

### 配置参数
#### 开发(能开的就开,不要过时的扩展)
```
sudo apt-get install libxml2-dev make autoconf libicu-dev g++ libcurl4-openssl-dev libbz2-dev libgd2-xpm-dev libreadline-dev g++ libfreetype6-dev
./configure --with-apxs2=/usr/bin/apxs2 --with-mysql --enable-mbstring --enable-intl \
 --with-openssl --with-zlib --enable-bcmath --with-bz2 --with-curl --enable-ftp --with-gd \
 --with-mysqli --with-pdo-mysql --with-readline --enable-shmop --enable-soap --enable-sockets \
 --enable-sysvmsg --enable-sysvsem --enable-sysvshm --enable-zip --enable-mysqlnd --with-pear \
 --enable-opcache --enable-gd-native-ttf --enable-gd-jis-conv \
 --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include
```
#### 最小
```
sudo apt-get install libxml2-dev make autoconf
./configure --with-apxs2=/usr/bin/apxs2 --with-mysql --with-pdo-mysql
```

#### symfony
```
sudo apt-get install libxml2-dev make autoconf libicu-dev g++
./configure --with-apxs2=/usr/bin/apxs2 --with-mysql --enable-mbstring --enable-intl
```


### 分析安装方法
* 搞到apt-get安装的apache2的apxs文件路径

```
sudo apt-get install apt-file
sudo apt-file update
sudo apt-file list apache2 | grep apx
```
* 这个地方有2个包,php的安装说明里面建议不要用threaded MPM,就选择 apache2-prefork-dev: /usr/bin/apxs2
/usr/bin/apxs2

### 已遇到的问题
#### 更新配置
```
./configure xxx
make clean
make 
make install
service apache2 restart
```

#### apc问题(2013-8-1)
* php5.4 5.3可以安装apc, php5.5不可以安装

#### gd问题(2013-8-1)
##### imagettftext() 函数 
* `--with-freetype-dir=/usr/include/freetype2`
* 依赖 `libfreetype6-dev`

##### imagejpeg() 函数
* `--with-jpeg-dir=/usr/include`
* 依赖 `libjpeg-dev`



### configure参数含义表
#### --with-apxs2
编译成apache2的一个模块,可以是threaded MPM也可以是prefork MPM

#### --with-mysql
* php的mysql模块,包含函数 
* mysql_connect()
* 被官方废弃的模块

#### --enable-mbstring
操作各种编码字符串的模块,mb_strlen() symfony需要这个东西

#### --enable-intl
* 国家化模块,转换各种国际化日期,大小写 
* symfony需要这个东西
* 依赖ubuntu的libicu-dev g++

#### --with-openssl
* 密码学加密解密模块, 
* openssl_random_pseudo_bytes() 
* 依赖libcurl4-openssl-dev

#### --with-zlib
* 压缩模块

#### --enable-bcmath
* 大整数数学运算

#### --with-bz2
* 压缩模块,打开修改bz2文件用
* 依赖 libbz2-dev

#### --enable-calendar
* 日历模块

#### --with-curl
* http客户端(发http请求)

#### --with-enchant
* 拼写检查库
* 没有安装成功

#### --enable-exif
* 读取图片的exif的meta信息

#### --enable-ftp
* ftp客户端

#### --with-gd
* 图片操作模块
* 依赖libgd2-xpm-dev

#### --with-gettext
* 国际化翻译模块

#### --with-gmp
* 大整数数学运算
* 依赖libgmp-dev

#### --with-mhash
* hash模块
* 被官方废弃的模块,直接使用hash()就可以了

#### --with-imap
* 邮件imap协议模块 支持IMAP NNTP POP3 查看本地邮件
* 没有安装测试

#### --with-kerberos
* 和openssl有关,用处不明
* 没有安装测试

#### --with-imap-ssl
* 邮件imap协议带ssl支持
* 没有安装测试

#### --with-interbase
* Firebird/InterBase数据库客户端
* 没有安装测试

#### --with-ldap
* ldap数据库客户端
* 没有安装测试

#### --with-mcrypt
* 加密解密模块
* 依赖libmcrypt-dev

#### --with-mysqli
* mysql数据库mysqli客户端
* 没有安装测试

#### --with-empress
* empress数据库??
* 没有安装测试

#### --with-birdstep
* birdstep数据库??
* 没有安装测试

#### --enable-pcntl
* 进程控制模块
* pcntl_fork() pcntl_exec()

#### --enable-opcache
* 字节码缓存模块
* 5.5.0开始有

#### --with-pdo-mysql
* mysql数据库pdo客户端

#### --with-readline
* 命令行readline模块,用处不明
* 依赖libreadline-dev

#### --with-recode
* 编码转换
* 依赖librecode-dev

#### --with-mm
* 将session保存在共享内存中?
* 依赖libmm-dev

#### --enable-shmop
* 共享内存模块
* shmop_open()

#### --with-snmp
* 用snmp协议管理远程设备?
* 没有安装测试

#### --enable-soap
* soap的rpc协议客户端和服务器端
* 非常垃圾的rpc协议...

#### --enable-sockets
* socket协议函数,客户端和服务器端
* socket_accpet()

#### --enable-sysvmsg --enable-sysvsem --enable-sysvshm
* 共享内存,锁 模块
* Semaphore, Shared Memory and IPC

#### --with-tidy
* html操控
* 依赖libtidy-dev

#### --enable-wddx
* wddx数据序列化协议,基于xml

#### --with-xmlrpc
* xml-rpc协议的服务器端和客户端

#### --with-xsl
* xsl变换,从一种xml文档,用xsl信息,变换成另一种xml文档
* 依赖libxslt1-dev

#### --enable-zip
* 读写zip压缩文件

#### --enable-mysqlnd
* 某种mysql扩展模块

#### --with-pear
* pear:php组件管理系统