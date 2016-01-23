### 在入口处下断点:
```
> sudo gdb ./bin/simpleC
(gdb) info files
    ...
    Entry point: 0x80000000
    ...
(gdb) break *0x80000000
(gdb) run
```
http://stackoverflow.com/a/10483702

### 查看堆栈信息(先断点下来)
64位上,每8个字节显示一条数据.
```
(gdb) bt
```

### 查看寄存器信息(先断点下来)
```
(gdb) info all-registers
```

### 查看某个寄存器的信息
```
(gdb) print $rbp
```

### 单步汇编指令 (先断点下来)
```
(gdb) stepi
```

### 查看附近的汇编指令 (先断点下来)
打开:
```
(gdb) layout asm
```
关闭: `Ctrl+x a`

### 查看某个地方的内存的值 
```
x/8 0x7fff5fbff9b0
```
