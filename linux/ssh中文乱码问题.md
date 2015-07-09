在输入ssh的登陆的机器上给 /etc/profile 后面加上
```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

### 注意事项
* 在bash里面输入上述两条命令,本bash马上有效.
* 在 /etc/profile 里面加上,重启bash后有效.
