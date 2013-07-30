### 客户端发送数据样例
```
EHLO
AUTH PLAIN eHh4AHh4eAB4eHg=
MAIL FROM:<sender@example.com>
RCPT TO:<reciver@example.com>
DATA
From: "xxx" <sender@example.com>
TO: "xxx" <reciver@example.com>
Subject: Test Message

Test Body
```

#### 认证参数计算:
```php
'AUTH PLAIN '.base64_encode($username . chr(0) . $username . chr(0) . $password)
```
```python
user_name='xxx';password='xxx';
'AUTH PLAIN '+(user_name+'\0'+user_name+'\0'+password).encode('base64')
```