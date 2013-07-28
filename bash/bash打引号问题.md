### 使用here doc 
转义问题终极解决方案 -> 完全不转义

#### 在某个命令的参数处使用
```
echo "$(cat <<'SQLEOF'
xxx''xxx'xxx'xx  123123    123123
abc'asdf"
$(dont-execute-this)
foo"bar"''
SQLEOF
)"
```


### 赋值
```
VAR="$(cat <<'VAREOF'
abc'asdf"
$(dont-execute-this)
foo"bar"''
VAREOF
)"
```

### bash打引号问题

参考资料: http://www.grymoire.com/Unix/Quote.html

### 使用\处理一个字符的转义问题
```
echo Are you sure you want to remove these files\?
```
```
echo This could be \
a very \
long line\!
```

### 使用单引号'处理转义问题
最强的引号,只有'不能转义
```
echo 'What the *heck* is a $ doing here???'
```

### 使用双引号"
未完待续
