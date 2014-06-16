### SearchInts函数
在已排序的int数组里面查找一个int
```
func SearchInts(a []int, x int) int {
	return Search(len(a), func(i int) bool { return a[i] >= x })
}
```

* 返回值范围 [0,n]
* 数组a需要是从小到大排序
* 返回值含义
  * 0表示 x小于等于a里面所有的值 a里面所有的值都大于等于x
  * n表示 x大于a里面所有的值     a里面所有的值都小于x
  * 0表示 a[0]>=x && a[1]<x
  * 1表示 a[1]>=x && a[2]<x
  * 2表示 a[2]>=x && a[3]<x

### Search函数
泛型化的二分搜索
```
func Search(n int, f func(int) bool) int

Search uses binary search to find and return the smallest index i in [0, n) at which f(i) is true, assuming that on the range [0, n), f(i) == true implies f(i+1) == true.
```

* 返回值范围 [0,n]
* 函数f需要满足条件: 
  * 输入的int是在[0,n-1]范围内,
  * 满足下列3个条件之一:
    * 全部返回true
    * 全部返回false
    * 在[1,n-1]范围内的一个确定值x,在i<x时返回 false,在i=x时返回 true,在i>=x时返回 true
* 返回值含义:
  * 0表示f全部返回 true
  * n表示f全部返回 false
  * 找到前面那个x