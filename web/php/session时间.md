1.不靠谱的时间控制
* 发往客户端的session清理时间,这个是客户端自行控制的.
```
ini_set("session.cookie_lifetime","3600");
```
* 0表示浏览器关闭session就消失了