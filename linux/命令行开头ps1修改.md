### 命令行开头ps1修改
修改后会得到如下效果:
```
~/work/xxx/src/github.com/bronze1man/kmg > vim ~/.bash_history
```

### 修改方法:
* 在当前bash里面输入 PS1='\w > ',当前bash有效
* 在/etc/bashrc 里面加上 PS1='\w > ',重启bash后有效.