## 定义样式
### 单行
下面是空格最少版本, ;号必有
```
function f1 { echo 1;echo 2;}
```

### 多行
```
function f1 {
echo 1
}
```
## 调用样例
```
f1
f1 arg1 arg2
```

## 使用参数
```
function f1 { echo $1;}
f1 arg1
```

## 注意
必须先定义,后调用
