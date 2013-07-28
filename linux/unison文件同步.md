### 以远程为准,将远程的文件强制同步到本地目录 的bash脚本
包含下列变量
* `<username>` 远程机器用户名
* `<host>` 远程机器域名/ip
* `<remote_path>` 远程机器绝对路径 如: `/home/xxx/xxx`
* `<local_path>` 本地项目路径(可以是相对路径) 如: `./xxx`

#### 模板:
```
#!/bin/bash
src='ssh://<username>@<host>/<remote_path>'
dest='<local_path>'
yes | unison ${src} ${dest} -force ${src} -auto
```

#### 样例:
```
#!/bin/bash
src='ssh://name@xxx.com//home/xxx/xxx'
dest='./xxx'
yes | unison ${src} ${dest} -auto -force ${src}
```