在项目目录下面建立一个名叫Makefile的文件:
写入下列内容:
```
test:
	./vendor/bin/phpunit
```

然后就可以使用`make test` 执行需要的功能了.

### 注意事项
* 解析器限制 缩进要用tab ,不能用空格