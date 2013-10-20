一般跨域
====================
### js发请求
和普通本域请求没有区别

### php返回响应
```php
        $response->headers->set('Access-Control-Allow-Origin','*');
```

### 注意事项
* 当http请求超出下列范围时,一个js的ajax的request会发送2个http请求,第一个请求是prefight请求
    * http的method只能使用 GET, HEAD, POST
    * 如果使用POST, Content-Type 只能使用 application/x-www-form-urlencoded, multipart/form-data, text/plain
    * 在request里面不能设置任何自定义的header

服务端处理prefight请求
====================
下面的代码可以通过所有prefight请求..
```php
        if ($request->headers->has('Access-Control-Request-Method')){
            $response->headers->set('Access-Control-Allow-Methods','POST, GET, HEAD');
        }
        if ($request->headers->has('Access-Control-Request-Headers')){
            $response->headers->set('Access-Control-Allow-Headers',$request->headers->get('Access-Control-Request-Headers'));
        }
        if ($request->getMethod()==='OPTIONS'){
            $response->headers->set('Access-Control-Max-Age','1728000');
        }
```

cookie跨域
====================
* 发送的请求会带访问的站的cookie
* 返回的响应可以修改访问的站的cookie

### 不做cookie跨域的效果
* 发送的请求不会带cookie
* 返回的响应的set-cookie没有效果

### js发请求
* 必须在XMLHttpRequest上设置 obj.withCredentials = true

```js
var invocation = new XMLHttpRequest();
var url = 'http://deskit.sxz.dashi.us/front/front_user/login';
invocation.open('POST', url, true);
invocation.withCredentials = true; //注意这一步.
invocation.onreadystatechange = function(){console.log(1);};
invocation.send("user_name=tt01&plain_password=a123456"); 
```


### php返回响应
* `Access-Control-Allow-Origin` 必须返回一个域名,如果使用'*'会挂掉...
* `Access-Control-Allow-Credentials` 必须返回true

```php
        if ($request->headers->has('Origin')){
            $origin = $request->headers->get('Origin');
        }else{
            $origin = '*';
        }
        $response->headers->set('Access-Control-Allow-Origin',$origin);
        $response->headers->set('Access-Control-Allow-Credentials','true');
```

### 注意事项
* 即使本域是localhost也可以使用这些东西