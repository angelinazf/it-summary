If map entries that have not yet been reached are removed during iteration, the corresponding iteration values will not be produced. If map entries are created during iteration, that entry may be produced during the iteration or may be skipped.

循环到某个key时,删除当前key没有问题,删除没有循环到的key,也没有问题,向map中添加key,可能会循环到,也可能不会循环到
