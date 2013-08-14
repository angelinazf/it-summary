* 下面的一些命令仅仅是起到帮助记忆的作用.
* 具体参数含义请用git help commit之类的命令查看官方文档.
* 具体操作流程和基本概念请去官方网站http://git-scm.com/ 看文档

# 基本流程
## 新建
* 配置用户名和邮箱
* 新建一个或者克隆一个项目
* 创建一个.gitignore把项目的临时目录,log目录,编辑器的临时文件忽略掉
* 写代码,或者从别处复制一些代码
* 使用git status查看修改.
* 使用git add 添加文件
* 使用git commit提交修改到本地
* 将提交push到某个远程服务器
* 后面开始修改流程

## 修改
* 使用git pull获取服务器的修改(别人的修改)
* 写代码,复制图片,复制代码,xxx
* 使用git status查看修改
* 使用git add 添加文件
* 使用git commit提交修改到本地
* 使用git push到远程服务器
* 回到git pull继续


# 基本操作
能用!!!
### 配置自己的用户名和邮箱(不配置总是会报错)
```
git config --global user.name "用户名"
git config --global user.email "abc@gmail.com"
```
### 新建本地普通项目
```
git init
```
### 克隆一个已有项目
```
git clone git@gits:~/alumni ./
```
### 添加文件
```
git add ./some_file.txt
```
### 添加全部修改
```
git add -A
```
### 删除文件
```
git rm ./some_file.txt
```
### 仅将文件脱离git控制
```
git rm --cached ./some_file.txt
```
### 查看项目文件状态
```
git status
```
### 提交修改(将文件修改交给git控制)
```
git commit -m"some comment of this commit"
```
### 取出服务器上面的提交(commit),并merge到本分支
```
git pull origin master
```
### 将提交(commit)上传给服务器,(这个不会产生merge动作)(默认只能push到裸项目)
```
git push origin master
```
### 查看本分支的提交历史
```
git log
git log --stat
```
### 比较不同版本之间的区别(可以是一个文件,也可以是多个文件)
```
git diff --stat HEAD^1
git diff --stat origin/master
git diff --stat dev product
git diff d8ab84c5cabfb1c8d6dd102cf3e290ea871b32a8 ./some_file.txt
```
那一串16进制的东西来自git log

# 高级操作
减少工作量!!!
## 新建项目
### 项目镜像(会生成一个裸项目),可以用于做缓存,做fork
```
git clone --mirror git@gits:~/alumni
```
### 新建git服务器(就是裸项目,然后就可以从别处git clone git push 了)
```
git init --bare
```
## 版本控制
此处的命令不太清楚含义,官方文档有些概念不懂!下面的命令经过验证在大部分情况下可以使用,但是出现过一些奇怪的情况.
### merge 对另一个分支进行3方merge
```
git merge dev
```
3方为:自己的当前位置,另一分支的当前位置,共同祖先.
* merge存在方向(自己是谁,另一分支是谁)
* 正确的merge需要有正确的共同祖先
* 将其他分支或历史上的某一个位置的文件复制到当前分支,然后提交,再merge,会出现回档情况.(可能是需要的,也可能是不需要的.)

### 撤销某个文件或者一个目录 修改回到上一次commit
```
git checkout ./some_file.txt
```
### 撤销某个文件或者一个目录 修改回到某一次commit
```
git checkout d8ab84c5cabfb1c8d6dd102cf3e290ea871b32a8  ./some_file.txt
```
### 撤销几次commit到某个版本(危险!)
```
git reset d8ab84c5cabfb1c8d6dd102cf3e290ea871b32a8
git rebase d8ab84c5cabfb1c8d6dd102cf3e290ea871b32a8
```
同时使用这两行一定可以把commit退回到某个版本,但是目前不明白含义,必要可以git checkout撤销当前修改
### 从项目的所有历史中删除文件(节约git的空间)
```
git filter-branch --index-filter 'git rm --cached --ignore-unmatch ./vendor/' --prune-empty --tag-name-filter cat -- --all
```
#### 备注:
此处部分概念不懂,可能会出现奇怪的状态.在奇怪的状态下,只要把当前文件的修改到正确的状态,然后提交就 可以工作了.(可能会破坏历史信息)

## 同步数据
### 镜像裸项目强制更新至某个远程项目
```
git remote update --prune origin
```
### 只拉服务器的数据,不merge
```
git fetch origin
```
## 设置信息
### 设置远程分支的url
```
git remote set-url origin git@gits:~/alumni
```
## 查看信息
### 当前项目的git目录的位置
```
git rev-parse --git-dir
```
会返回相对目录或绝对目录
普通项目返回xxx/.git,裸项目返回xxx/
### 当前项目是否是裸项目
```
git config --get core.bare
```
返回true或false
### 获取当前项目的某个远程分支的url
```
git remote show -n origin
```
会返回很多信息,需要用正则 /Fetch URL:(.*)/ 取出远程分支的url
## 玩分支
### 新建空分支(当前文件不会变化,只是新分支里面没有东西)
```
git checkout --orphan branch_name
```
### 新拉出一个分支(当前文件不变,新分支和当前分支指向同一个地方)
```
git checkout -b branch_name
```
### 切换分支(git有可能会不允许切换分支!)
```
git checkout branch_name
```
### 列出当前项目存在的分支
```
git branch
```
### 列出远程分支
```
git branch --remotes
```
这个只是当前git已经知道远程存在的分支,必要可以用git fetch获取远程分支信息

# 注意事项
## 回档
### 已知下面一些情况会产生回档:
* merge方向错误
* 将其他分支或历史上的某一个位置的文件复制(包括git checkout)到当前分支,然后提交,再merge.
* 使用git rebase

## window
使用github的window客户端,可以输入中文...
