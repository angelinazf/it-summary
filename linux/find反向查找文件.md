### 找出所有不是.md的文件
```
find . -type f ! -name '*.md'
```

### 找出所有不是.md的文件
```
find . -type f ! -name '*.md' | xargs rm
```