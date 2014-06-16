### 表现
* 在后台文章列表处,修改排序的值,刷新页面后,后台排序没有变化,前台使用了listorder desc,排序有变化

### 解决方案
* 修改文件`phpcms/modules/content/content.php`
下面这一行
```
$datas = $this->db->listinfo($where,'id desc',$_GET['page']);
```
为
```
$datas = $this->db->listinfo($where,'listorder desc,inputtime desc',$_GET['page']);
```
