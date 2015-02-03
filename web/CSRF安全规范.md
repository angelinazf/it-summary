CSRF攻击方法:
* 在域名A站(域名不同,是跨站请求).对域名B站,发起ajax请求,可能是GET,可能是POST,由于同源限制无法获取到服务器返回的数据.但是请求被服务器执行了.

### 全浏览器 Referer Header 解决方案(简单,兼容所有浏览器,安全,少数代理或浏览器用户会无法使用应用.)
* 所有"写"数据都使用POST方法
* 验证所有POST,ajax请求有Referer header,并且值的url的协议,域名,端口和当前协议,域名,端口一致.

### 高版本浏览器Origin头解决方案(简单,如果浏览器支持,安全,可用性高)
* 所有"写"数据都使用POST方法
* 验证所有POST,ajax请求有Origin header,并且和当前协议,域名,端口一致
* 浏览器支持版本 IE8+(部分) IE10(全面) firefox 28+  chrome 31+ safari 5.1+ 所有手机浏览器
* 参考https://wiki.mozilla.org/Security/Origin http://caniuse.com/#search=CORS

### 全浏览器解决方案(复杂度很高,兼容所有浏览器,安全,可用性高)
* 在session中储存token,并且在3小时后过期,使用一个新的token.
* 在表单 POST提交中加入token字段
* 在ajax POST提交中加入token字段
* 在服务器中验证token字段是否和session中的token字段是否一致.



### 是否遵守csrf安全规范
* 本安全规范,在html封装的很简单,或者没有封装时,实现会产生很多重复代码.导致代码不易维护,产生较多bug.
* 如果用户恶意写数据,不会产生严重后果,没有必要加入csrf
  * 如给留言板添加留言.并且留言会审核. 恶意写数据仅会产生很多垃圾数据而已,不重要, 但是如果写数据可以删除留言,或审核通过留言,就会导致很严重的问题了.
  * 一个安全的cms后台必须遵守csrf安全规范.

### 框架已有解决方案:
* Thinkphp 有csrf模块
* ci 有csrf模块
* phpcms 后台有pc_hash参数

### 攻击限制
* 攻击者不能从当前用户获得任何数据,只能发起请求
  * 只需要防护"写"数据,不需要防护"读"数据.
  
### 备注:
* csrf的token放在url里面(GET参数)不能阻止csrf
* https不能阻止csrf
* 神秘的cookie值不能阻止csrf
* 写数据全部用POST不能阻止csrf
* 多步事务执行 不能阻止csrf


### 在浏览器console中工具的方案
```
var xhrObj = new XMLHttpRequest();
xhrObj.open('GET', 'https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js', false);
xhrObj.send('');
var se = document.createElement('script');
se.type = "text/javascript";
se.text = xhrObj.responseText;
document.getElementsByTagName('head')[0].appendChild(se);

$.ajax({
  'url':'http://test.xxxx/admin.php/Index/loginAction',
  'data':{"keyword":"xxxx"},
  'type':'POST',
});
```
