```
#监听某个端口,默认80已经在其他配置里面监听过了
listen 28840
NameVirtualHost *:28840
#禁止某个目录显示文件列表
<Directory /var/www/>
    Options -Indexes
</Directory>
#某个网站
<VirtualHost *:80>
    ServerName lqv.ca
    DocumentRoot /var/lqv.ca
</VirtualHost>
```