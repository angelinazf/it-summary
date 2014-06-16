TODO 重构此规范


### controller接口规范
* 每一个接口是一个api,处理某件事情,尽量不要在api内部继续划分处理事务
* 不要区分POST参数和GET参数,使用$_REQUEST,实际传入时POST参数名和GET参数名不要重复
* 区分页面Page,提交Action,文件上传FileUpload,图片输出Image等不同api类型
* 例子:
  * CategoryListPage   栏目列表页
  * CategoryAddPage    栏目添加页面(添加栏目显示的那个页面)
  * CategoryAddAction  栏目添加动作(提交的那个请求)
  * CategoryEditPage   栏目编辑页面
  * CategoryEditAction 栏目编辑动作
* 在ci这种框架里面可以使用controller的类名做命名空间,函数名做api的后边一部分的名称如:
  /Category/ListPage
  /Category/AddPage
* 首页问题
  * 除了网站入口,不要使用某模块入口(文档化比较差)
  * 根据不同框架的不同方法,在首页处,跳转至对应api,或引用对应api.

### controller接口目标
  * 更清晰的文档
    * 一个api处理一件事情.不要通过GET和POST请求方法来分辨不同的事务.
    * api不应该根据某些数据变化而无限增加
    * 不要隐含规则,如url第3段是页面 或者第3段是文章id ...
  * 减少这个地方的编程复杂度.
    * 让浏览器和框架去处理数据的序列化和反序列化问题.(POST和GET参数)
    * 不要在逻辑里面解析字符串.
    * 不要写正则解析url
    * 不要让用户去写url,用户才不在乎url呢.
  
### POST-Redirect-GET设计模式
* 例如:
  * 用户修改了自己的密码,点击保存按钮,此时发送一个POST请求包含用户id和密码,后端处理成功后redirect到用户列表.
  * 用户添加了一个管理员,点击保存按钮,浏览器发送一个POST请求,后端处理成功后redirect到用户列表
* 优势:
  * 用户点击浏览器的后退按钮不会,提示是否重新提交表单.
  * 减少后端重复代码.
  
注意事项:
* 所有地方均使用utf-8编码(数据库,html,php文件)
* 避免使用类似'/channel/index/id/2'的url, 尽量使用类似 '/?n=ContentListPage&CatId=15'的url构造,以降低代码复杂度.
* 减少controller和model之间的重复封装,如果某个功能仅出现过一次,直接写在controller里面,model仅用来封装重复代码.以降低代码复杂度.
* 避免使用iframe划分显示区域
* 避免form表单嵌套
* 避免使用绝对路径,避免使用域名,以减少迁移复杂度
* 后台可以仅兼容chrome
* 不要考虑可能会出现的需求,以当前需求为准
* 很多东西有较高学习成本,在时间紧张时,以完成功能为先.
* 为快速实现,多用form表单提交,少用ajax
* 建议添加与编辑写到一个模板里面,减少代码重复.
* 同一件事务,请在整个项目的所有地方使用完全一样的拼写,不要有大小写区别,不要有下划线分隔区别.便于理解和代码搜索.