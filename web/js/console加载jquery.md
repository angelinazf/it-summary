### 异步加载
* 无跨域问题
* 要等一会加载好了才能用,直接在后面写的代码不能直接用
```
newScript = document.createElement('script');
newScript.src = 'https://code.jquery.com/jquery-1.7.2.js';
document.getElementsByTagName('head')[0].appendChild(newScript);
```

### 同步加载 
* 有跨域问题
* 直接在后面写的代码就可以用
* xhrObj的创建方法不同浏览器不同
```
var xhrObj = new XMLHttpRequest();
xhrObj.open('GET', 'https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js', false);
xhrObj.send('');
var se = document.createElement('script');
se.type = "text/javascript";
se.text = xhrObj.responseText;
document.getElementsByTagName('head')[0].appendChild(se);
```

### 如果有jquery
```
$.getScript("http://code.jquery.com/jquery-1.11.0.js");
```

### 各大cdn的url样例
* 不能跨域 https://code.jquery.com/jquery-1.7.2.js
* 可以跨域 https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.js
* 可以跨域 http://cdn.staticfile.org/jquery/2.1.1/jquery.js