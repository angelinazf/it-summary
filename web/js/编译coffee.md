编译某个目录下面的所有coffee文件到对应的js文件
```
find -name '*.coffee' -print0 | xargs -0 coffee -c -b
```