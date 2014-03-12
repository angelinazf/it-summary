### 解决方案思想:
* 所有html输出均进行正确转移,即使被攻击也会显示出用户输入的信息,而不管用户输入什么信息
* 用户可以输入html的地方,需要进行html过滤

### php代码
```
function h($str){
    return htmlspecialchars($string, ENT_QUOTES | ENT_SUBSTITUTE, 'utf-8');
}
```