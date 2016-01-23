* 先去`https://www.namecheap.com/` 登陆
* 去页面`https://www.namecheap.com/security/ssl-certificates/single-domain.aspx` 购买证书
* 付款后去`https://ap.www.namecheap.com/ProductList/SslCertificates`激活证书的内容.
* 创建一个目录如 `mkdir -p doc/cert/xxxyourdomain.com` 注意将 xxxyourdomain.com 替换为您正在生成https的域名.
* 使用命令 `openssl req -out domain.csr -new -newkey rsa:2048 -nodes -keyout domain.key -subj '/C=US/ST=US/L=US/O=US/OU=US/CN=xxxyourdomain.com/'` 生成一个证书
* 把domain.csr的内容拷贝到网站上. ServerType选 nginx
* 购买证书,生成csr时,记录url上面的数字id.
* 一路next
* Company Contacts 里面信息随意填 ,ZIP code 要填 999077,邮箱填一个有效的,要接收证书.
* 去点两次邮件验证: 标题类似于 `IMMEDIATE VERIFICATION required for xxxyourdomain.com`, `ORDER #187123571 - Domain Control Validation for xxxyourdomain.com`
* 去邮箱里面,下载标题类似于 `ORDER #187123571 - Your PositiveSSL Certificate for xxxyourdomain.com` 里面的附件.
* https key 的内容为 domain.key
* https cert 的内容为 附件里面 xxxyourdomain_com.crt 接上 xxxyourdomain_com.ca-bundle (cat起来.)
* 如果页面丢失,去 `https://ap.www.namecheap.com/domains/SSL/ProductPage/17184/apps`,把前面那个url里面的数字id替换为之前记录的url上面的数字id.

### 注意事项:
* 对于$9 这种便宜证书,生成csr时,除了CN,CN必须为需要签名的域名的字符串 其他的可以随意填写,这些信息会出现在浏览器的证书上.网站上要求附加信息时,也可以随意填写.
* 对于绿标证书,需要正确填写信息,别人能找到你填写的这家公司.
* 购买证书时如果证书页面丢失,去 `https://ap.www.namecheap.com/dashboard` 里面寻找,或者使用之前记录的数字id构造url进入.
