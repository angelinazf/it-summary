### 打开ssl功能
```
sudo a2enmod ssl
```

### 编辑/etc/apache/httpd.conf
```
listen 28841
<VirtualHost *:28841>
    ServerName 1.xyh03.lqv.ca
    DocumentRoot /var/www/phpmyadmin
    SSLEngine on
    SSLCertificateFile /home/bronze1man/tmp/mysitename.crt
    SSLCertificateKeyFile /home/bronze1man/tmp/mysitename.key
</VirtualHost>
```