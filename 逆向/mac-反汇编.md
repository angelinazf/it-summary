### otool
```
otool -tV ./bin/simpleC
```

### go objdump
只能反汇编go生成的文件,其他东西生成的文件无法使用.
```
go tool objdump ./bin/simpleC
```

### gobjdump
安装
```
brew install binutils
```
使用
```
gobjdump -d ./bin/simpleC
```