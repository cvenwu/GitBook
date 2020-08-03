# 随机数
> 生成随机数需要设置不一样的种子，当我们种子不一样时就会产生不同的随机数，因此如果种子一样生成的随机数也会一样


通过`rand.Seed(time.Now().Unix())`设置随机数


```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	//因为随机数是根据种子生成的
	rand.Seed(time.Now().Unix())
	//种子固定以后就可以生成随机出
	//生成[0, 31]的随机数
	for i := 0; i < 10; i++ {
		fmt.Println(rand.Intn(32))
	}

}
```