### 构造注入 可以混入setter注入
```
services:
  di_name:
    class: 'Xxx\xxx\ClassName'   # 注意:前面没有\
    arguments:           # 构造函数注入
      - {xxx:xxx}        #直接传入一个数组,(里面可以引用parameter)
      - abc              #传入一个字符串
      - %xxxx%           #引用parameter,不存在时,编译时报错
      - @tbf_serializer  #引用service,不存在时,编译时报错
      - @?tbf_serializer #引用service,不存在时,传入null
    calls:               # 构造完了,在函数上进行调用注入
      - [setMailer, ["@my_mailer"]]  
      - [setEmailFormatter, ["@my_email_formatter"]]
    tags:
      - {name:tag_name,attr1:val1,attr2:val2} 
    abstract:  true      #抽象service,可以被继承,不可以被实例化
    parent: xxx.service_id   #继承另一个service
    lazy: true           # 懒加载(需要安装ocramius/proxy-manager才有效果)
    configurator: ["@email_configurator", configure] # 传入另一个service里面进行配置
    public: false        # 私有service
    file: "%kernel.root_dir%/src/xxx" # 在实例化这个service的时候加载一个文件
    properties:          # 属性注入(只能是公开属性)
      mailer: "@my_mailer" 
```

### 工厂注入 调用类静态函数
```
services:
  di_name:
    class: 'Xxx\Xxx'
    factory_class: Dwoo_Compiler
    factory_method: compilerFactory
    arguments:              # 可选,向这个工厂传参数
      - "@templating"
```

### 工厂注入 调用service上的方法
```
services:
  di_name:
    class: 'Xxx\Xxx'
    factory_service: tbf_serializer
    factory_method: compilerFactory
    arguments:             # 可选,向这个工厂传参数
      - "@templating"
```

### service别名
给某个service另一个名字
```
services:
   foo:
     class: Example\Foo
   bar:
     alias: foo
```

### 合成的service
在container编译好之后,运行时传入的service
```
services:
    request:
        synthetic: true
```