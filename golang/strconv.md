# 字符串和基本数据类型的转换



Golang中 `+`操作符连接的两个变量只能是同类型，而不可以像java中这样写："213" + 123 将会得到"213123"。Golang要求必须是同类型，因此当我们进行字符串拼接的时候，务必要将其他类型转换成字符串。



字符串转整数：`i1, err := strconv.Atoi("123")`

整数转字符串：`ss := strconv.Itoa(123)`

字符串转为其他类型都是使用Parse一系列函数进行解析，都会返回两个值，第1个值是解析后的基本数据，第2个是错误。

`b, err := strconv.ParseBool("true")`

`f, err := strconv.ParseFloat("3.1415", 64)`

`i, err := strconv.ParseInt("-42", 10, 64)`

`u, err := strconv.ParseUint("42", 10, 64)`



基本数据类型转字符串类型，可以使用Format的一系列函数



`s := strconv.FormatBool(true)`

`s := strconv.FormatBool(3.1415, 'E', -1, 64)`

`s := strconv.FormatInt(-42, 16)`

`s := strconv.FormatUint(42, 16)`



```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	//bool类型
	s1 := "bool"
	b1, err := strconv.ParseBool(s1)
	if err != nil {
		fmt.Printf("%T %t\n", b1, b1)
		return
	}
	fmt.Println(b1)
	
}

```

