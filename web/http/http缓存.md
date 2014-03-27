### 不缓存
在请求返回时,发送http头
```
Cache-Control:no-cache
```

### 缓存半小时,并且使用修改时间验证
先判断请求的http头里面的
```
If-Modified-Since:Thu, 15 Aug 2013 02:58:01 GMT
```

* 如果没有失效,返回一个304
* 如果请求里面没有这个header,或者已经失效,在请求返回时,发送http头

```
Cache-Control:max-age=1800, public, s-maxage=1800
Date:Thu, 15 Aug 2013 05:43:04 GMT
Expires:Thu, 15 Aug 2013 06:13:04 GMT
Last-Modified:Thu, 15 Aug 2013 02:58:01 GMT
```