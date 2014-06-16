```
#监听某个端口,默认80已经在其他配置里面监听过了
listen 28840
NameVirtualHost *:28840
#禁止某个目录显示文件列表
<Directory /var/www/>
    Options -Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
# 没有写在列表里面的域名都出404(某个端口的第一个出现的配置,会被当作该端口默认配置)
<VirtualHost *:80>
    RewriteEngine On
    RewriteRule .* - [R=404,L]
</VirtualHost>
#某个网站
<VirtualHost *:80>
    ServerName lqv.ca
    DocumentRoot /var/lqv.ca
</VirtualHost>
```