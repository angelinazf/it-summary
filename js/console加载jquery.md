```
newScript = document.createElement('script');
newScript.src = 'https://code.jquery.com/jquery-1.7.2.js';
document.getElementsByTagName('head')[0].appendChild(newScript);
```

### 如果有jquery...
```
$.getScript("http://code.jquery.com/jquery-1.11.0.js");
```