* 使用symfony作为入口
* 修改配置,使用symfony的配置(减少配置复杂度)
* 一切自动化
* 程序会修改的文件 需要被忽略 ,如果有bootstrap问题,请使用自动化build方案...
* 使用symlink

# 前端控制器问题
* 使用symfony作为入口

# 统一检查和生成配置问题
* 使用symfony的dic

# 目录权限,和git文件管理问题
* 三类目录 cache data log
* 程序会修改的文件 需要被忽略 ,
* 如果有bootstrap问题,请使用自动化build方案...
* 使用symlink

# 全局变量问题
* 可以在前端控制器(顶层php脚本入口) 引入第三方php框架

# 测试问题
* 使用api测试

# url路由问题
* 目前没有成熟解决方案

# 错误处理问题
* 使用symfony的错误处理方案