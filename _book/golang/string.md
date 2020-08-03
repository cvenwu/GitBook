# 字符串

字符串是基本数据类型，字符串其实是一个字节的切片，也就是字节的集合。理解为一个字符的序列。
定义字符串：**`字符串`**或者通过 **``**

Golang中采用utf-8编码，是一种变长的编码，中文占3个字节。也就是每3个字节才是一个中文字符。因此汉字不能按照字节遍历
`len()`返回字符串的字节数

```go
package main

import "fmt"

func main() {
	//1. 定义字符串
	s1 := "hello"
	s2 := `helloworld`
	s3 := "111你好中国"
	fmt.Println(s1, s2)

	//2. 字符串的长度：返回字节的个数
	fmt.Println(len(s1))
	fmt.Println(len(s2))

	//3. 获取某个字节
	fmt.Println(s2[0]) //获取字符串中的第一个字节,打印的是对应的编码值
	fmt.Printf("%c %c\n", s2[0], s2[1])  //打印对应的字符而不是编码值

	//4. 字符串的遍历
	for i:=0; i < len(s1); i++ {
		fmt.Printf("%c ", s1[i])
	}
	fmt.Println()
	for _, v := range s1 {
		fmt.Printf("%c ", v)
	}
	//遍历带有中文的
	for i:=0; i < len(s3); i++ {
		fmt.Printf("%c ", s3[i])
	}
	fmt.Println()
	for _, v := range s3 {
		fmt.Printf("%c ", v)
	}

	fmt.Println()
	//5. 字符串是字节的集合
	slice1 := []byte{65,66,67,68}
	s4 := string(slice1)  //根据一个字节切片转换成字符串
	fmt.Println(s4)

	s5 := "abcdef"
	slice2 := []byte(s5)  //根据字符串获取对应的字节切片
	fmt.Println(slice2)

	//6.字符串不能修改
	fmt.Println(s4)
	s4[2] = 'B'  //报错，./demo.go:49:8: cannot assign to s4[2]


}

```