### 查看一个项目的submodule
```
git submodule
```

### 新下载的代码,里面包含一个submodule
```
git submodule update --recursive
```

### 原则
* 保证每个子项目有最新的代码
* 大项目 
  * 要么 用composer管理依赖,并忽略vendor(管理这个大项目简单)
  * 要么 把所有文件都加入版本控制(拉一个新项目简单...)

### 绕开submodule
* 先正常不带.git文件加入子目录.并提交,再把.git目录从其他地方搞过来就可以绕开submodule,
* 效果:
  * 外层git认为这个目录是一个正常的目录,内层git也认为这个目录是一个子项目的根.
  * 上传外层git的时候,所有文件都被保存起来一起上传了.
  * 上传内层git的时候,这个子项目也可以更新.

#### 已经是submodule但是没有mapping信息(不小心把带.git文件夹commit加入项目)
* 不需要提交
* 第一次删除submodule,
* 第二次重新加入正常目录,
* 之后可以再把.git搞回来....

```
mv target_dir b1          # 换个名字
git rm target_dir         # git删除
mv b1 target_dir          # 改回去
mv target_dir/.git ~/tmp  # 先不要有.git目录
git add ./target_dir      # 正常向git里面加入这个目录,从此处向后这个项目就不认为这个目录是submodule了
mv ~/tmp/.git target_dir  # 再加上.git目录
git commit -am"asdfasdf" # 这步可选
```

#### 目录已存在父项目的git中,加入.git文件夹
这个时候直接把子项目的.git文件搞到需要需要的目录下面即可...
```
git clone git@xxx:xxx b1
mv b1/.git target_dir
rm -rf b1
```
