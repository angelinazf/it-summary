### 简要例子
```
// +build windows

package main

import (
    "fmt"
)

func main() {
    fmt.Println("This is windows")
}
```
* // +build xx 后面一定要空一行.


### 可以在windows和linux下面使用
```
// +build windows linux
```

### 在除了windows和linux以外的所有平台
```
// +build !linux,!windows
```

### reference
* https://golang.org/pkg/go/build/