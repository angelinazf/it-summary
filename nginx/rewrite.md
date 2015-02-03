### 下列rewrite方案可以解决 synfomy2的问题
```
        if (!-e $request_filename) {
            rewrite  ^(.*)$  /app.php/$1  last;
            break;
        }
```

### 下列rewrite方案可以解决 thinkphp的问题
实际url样式: /admin.php/Index/loginPage.html
```
            if (!-e $request_filename) {
                rewrite  ^/admin.php(.*)$  /admin.php?s=$1  last;
                break;
            }
```

### phpcms
```
        location ^~ /phpcms {return 404;}
        location ^~ /bin {return 404;}
        location ^~ /.git {return 404;}
        location ^~ /.gitignore {return 404;}
        location ^~ /html {return 404;}
        location ^~ /phpsso_server {return 404;}
        location ^~ /plugin.php {return 404;}
        location ^~ /api$ {return 404;}
        location ^~ /api/ {return 404;}
```