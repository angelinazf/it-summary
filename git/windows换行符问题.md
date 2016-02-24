### 在windows上,要求git使用linux的换行符.
```
git config --global core.eol lf
git config --global core.autocrlf input
```

### 如果windows已经出现换行符错误,执行下列操作,让git重新折腾一遍换行符
* 请先把已有信息commit保存起来.
```
git rm -rf -cached .
git reset —hard HEAD
```