### 方法1
* 修改 `/etc/hostname` 把这个文件的内容修改为你想要修改的主机名
* 修改 `/etc/hosts` 把127.0.0.1 old-name 修改为你想要修改的主机名
* 运行 `service hostname restart` ,从此开始后,你新开的bash窗口可以看到新的名字

### 注意事项
* `hostname your-new-name` 修改只对本次运行有作用,下次就不见了.
* 没有找到修改已经打开的bash的窗口的主机名的方法

### 参考
http://askubuntu.com/a/16443/389557