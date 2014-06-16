当某个log文件体积特别大的时候,可以使用logrotate,让系统自动把log变小
```
logrotate -f /etc/logrotate.conf
```