伪submodule是: 
	在某个git项目下面,有一个子项目里面还有一个.git目录,如果使用git add,这个子项目会编程submodule,有一种方法即保留子目录里面的.git目录,也使整个目录在父目录里面进行版本控制,这个就是 伪submodule.

分两种情况:
1.已经是submodule了, 使用git rm —cached  ./xxx/project/ 从git里面删除这个东西 ,然后走第2种情况
2.还没加入控制.使用 git add ./xxx/project/xxxfile 向git加入这个子项目里面的一个文件,然后就得到了 伪submodule 的效果.