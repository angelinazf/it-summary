设置永久环境变量
=================
### 修改/etc/profile
* bash语法可用
* 以普通用户ssh登录可用
* 以sudo调用命令不可用
* 进入sudo bash不可用
* 不会立刻修改当前bash的环境变量

### 修改/etc/environment
* 修改时使用XXX="xxx",bash语法不可用
* 以普通用户ssh登录可用
* 以sudo调用命令不可用
* 进入sudo bash不可用
* 不会立刻修改当前bash的环境变量,重新登录ssh生效

### 修改/etc/bash.bashrc
* 重新登录ssh生效
* 以普通用户ssh登录可用
* 以sudo调用命令不可用
* 进入sudo bash,sudo -i可用

### 使永久环境变量生效
* 重新登录ssh
* 重新进入tmux无效

### ubuntu 下sudo调用命令的$PATH问题
* 似乎/etc/sudoers可以修改这个PATH (没有尝试)
* 默认配置下,没有任何办法修改这个$PATH, http://stackoverflow.com/questions/257616/sudo-changes-path-why

当前bash设置环境变量
=================