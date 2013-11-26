# !!!注意!!!
* 参考文档: http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html
* 不能省任何空格...
* 不要想当然..bash的语法非常奇葩...

# 格式问题
## 单行if
```
if test 1 ; then echo 1; fi
if false ; then echo 1; fi
if true; then echo 1; fi
if [ -f 1.txt ] ; then echo 1; fi
```
## else
```
if [ -f index.htm ];then echo 1;else echo 2;fi
```
## elif
```
if [ -f index.htm ];then echo 1
elif [ -f index.html ]; then echo 2
fi
```

## 空格问题
### 下面是空格最少的写法...
```
if [ -f index.html ];then echo 1;fi
```

### 可以换行1
```
if [ -f index.html ]
then echo 1
fi
```

### 可以换行2
```
if [ -f index.html ];then
echo 1
fi
```

## 总结
使用;号的地方也可以用换行

# 带else的版本
```
if [ -f index.htm ];then echo 1;else echo 2;fi
```

# if 条件语法

那个地方填的是一个命令,test false true [ 都是命令...

#常见条件
后面已经使用了空格最少版本,不要减少里面任何一个空格!!!

## 文件存在
```
if [ -f 1.txt ];then echo 1;fi
```

## 文件不存在
```
if [ ! -f 1.txt ];then echo 1;fi
```

## 目录存在
```
if [ -d 1.txt ];then echo 1;fi
```

## 测试字符串相等,里面涉及的$a不必存在
注意:
* 缺少==号两边的空格会导致条件一直为真!!!
* 缺少""号 会导致变量没有定义时报错

```
a=1
if [ "$a" == 2 ];then echo 1;fi
if [ "$1" == test ];then echo 1;fi
```

## 字符串不相等
```
if [ "$a" != test ];then echo 1;fi
```

## 变量长度为0,可能是没有定义,可能是定义了,长度为0
```
if [ -z $VAR ]; then echo VAR is not set at all or is set but empty; fi
```

## 变量是否定义
```
if [ -z "${VAR+xxx}" ]; then echo VAR is not set at all; fi
```

## 变量定义了,但是长度为0
```
if [ -z "$VAR" ] && [ "${VAR+xxx}" = "xxx" ]; then echo VAR is set but empty; fi
```
