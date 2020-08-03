# strings包的使用

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	s1 := "hello"
	//是否包含指定内容
	//检查第2个子字符串是否在第1个字符串里面
	fmt.Println(strings.Contains(s1, "llo"))
	fmt.Println(strings.Contains(s1, "h"))
	fmt.Println(strings.Contains(s1, "e"))
	//只要第2个参数中有一个字符出现在第1个里面就返回True
	//是否包含chars中的任意一个字符即可
	fmt.Println(strings.ContainsAny(s1, "abcd"))

	//统计substr在s中出现的次数
	fmt.Println(strings.Count(s1, "llo"))


	//字符串以...开头
	s2 := "20190912课堂笔记.md"
	if strings.HasPrefix(s2, "2019") {
		fmt.Println("这是2019年的笔记")
	}
	//字符串以...结尾
	if strings.HasSuffix(s2, ".md") {
		fmt.Println("字符串以.md结尾")
	}

	//substr返回第一次出现的下标索引位置，如果没有就返回-1
	fmt.Println(strings.Index(s2, "019"))
	//返回第2个参数中的任意字符出现在第1个字符串里面的位置
	fmt.Println(strings.IndexAny(s2, "123456"))
	//查找最后一次出现时的下标位置
	fmt.Println(strings.LastIndex(s2, "12"))
	//字符串的拼接
	ss1 := []string{"abc", "world", "hello", "ruby"}
	s3 := strings.Join(ss1, "-")  //通过-拼接
	fmt.Println(s3)

	//字符串的切割
	s4 := "123+234+445+23"
	ss2 := strings.Split(s4, "+")
	fmt.Println(ss2)

	//重复
	s5 := strings.Repeat("123", 2)
	fmt.Println(s5)

	//替换, 第1个参数表示替换哪个字符串，第2个参数表示替换字符串中的那个子字符串
	//第3个参数表示替换字符串中的哪个字符串。第4个参数表示替换几次。如果为-1就表示全部替换
	s6 := strings.Replace(s1, "l", "*", 2)
	fmt.Println(s6)

	s7 := "helloWORLD"
	//变小写
	fmt.Println(strings.ToLower(s7))
	//变大写
	fmt.Println(strings.ToUpper(s7))

	//截取子串，使用切片进行截取。指定一个起始下标和结束下标
	fmt.Println(s7[2:5])



}

```

