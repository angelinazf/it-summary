# sed
## 文本替换
* 默认只会替换每一行的第一个

### 从文件old里面替换字符串day为night,保存为文件new
```
sed s/day/night/ <old >new
```
```
sed s/day/night/ old >new
```

### 换一种分隔符
```
sed 's_/usr/local/bin_/common/bin_' <old >new
```

### /g整行替换
```
sed s/day/night/g <old >new
```