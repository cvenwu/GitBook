# 深拷贝和浅拷贝

浅拷贝：拷贝数据存放的地址，会使得多个变量指向同一块内存。引用类型默认都是浅拷贝，
深拷贝：拷贝的都是数据本身。值类型默认都是深拷贝

> golang中提供了内置函数copy(dst, src)用于切片的深拷贝

dst或src可以为切片的一部分，但是注意会将src中的元素拷贝之后粘贴到dst指定的位置，会覆盖掉之前的值。


```go

package main

import "fmt"

func main() {
	nums := []int{1, 2, 3, 4}
	s1 := make([]int, 0)
	//自己实现深拷贝
	for _, v := range nums{
		s1 = append(s1, v)
	}

	fmt.Println(s1)

	s1[0] = 100
	fmt.Println(s1, nums)

	//也可以使用Golang提供的copy专门进行切片拷贝
	s3 := []int{7, 8, 9}
	fmt.Println(s3)

	//将s3中的元素拷贝到s2中
	//copy(s1, s3)  //拷贝s3所有元素后，从s1的第1个位置上开始粘贴，也就是会覆盖前面的值
	//fmt.Println(s1)

	copy(s3, s1)
	fmt.Println(s3)		//如果第2个切片长度大，则只拷贝第1个切片大小的元素到第1个切片中

	//也可以只拷贝一部分数据
	copy(s3, s1[2:])
	fmt.Println(s3)

	//也可以拷贝到的目标切片的一部分
	copy(s3[1:], s1)
	fmt.Println(s3)
}
```