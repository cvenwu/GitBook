# 切片

> 切片同数组类似，也叫做变长数组或动态数组。
**切片是一个引用类型的容器，因为切片本身不存储数据，是底层数组存取数据，因此指向了一个底层数组**。可以使用`fmt.Printf("%p",切片名)`查看切片指向的地址



切片即使元素个数超过cap也是可以的，因为会进行扩容。一旦扩容就会指向一个新的底层数组。同时每次扩容都会成倍增长。3->6->12->24->48

扩容过程：首先创建一个新的数组，将原来数组的内容拷贝到新的数组，然后添加新元素到新的数组

## 切片创建




> 使用make或者直接使用初始元素创建
func make(t Type, size ...IntergeType) Type
    第一个参数：类型
    第二个参数：长度len，切片实际存储的元素个数
    第三个参数：容量cap，最多能够存储元素的个数
```go
nums := make([]int, 4, 8)
nums := []int {1, 2, 3, 4, 5}
```

## 从已有数组创建切片

此时切片指向该数组的一部分，此时修改数组或者修改切片都会造成另一方的修改。

```go
nums := [10]int{1,2,3,4,5,6,7,8,9,10}
//从头开始切片到底5个元素
s1 := nums[:5]  //包含头不包含尾相当于从0取到5。，头不写则说明从头开始
fmt.Println("我们需要一个世界欢迎你但是我们需啊")
s2 := nums[6:]  //如果取到最后则最后可以不写

s3 := s2  //s2存储的是nums[6]的地址，因此会将这个地址赋值一份给s3
```

案例代码：
```go
package main

import "fmt"

func main() {

	//创建数组
	nums := [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

	//创建切片，切片指向的地址与数组的地址一致
	s1 := nums[:5]  //如果包含数组的头部则开始可以省略
	s2 := nums[3:8]
	s3 := nums[5:]
	s4 := nums[:]

	fmt.Printf("s1 = %p, s2 = %p, s3 = %p, s4 = %p, nums = %p\n", s1, s2, s3, s4, &nums)
	fmt.Println()

	//长度和容量
	fmt.Println(len(nums), cap(nums))
	fmt.Println(len(s1), cap(s1))
	fmt.Println(len(s2), cap(s2))
	fmt.Println(len(s3), cap(s3))
	fmt.Println(len(s4), cap(s4))

	//修改数组中的一个元素,切片也会进行修改
	nums[4] = 1000
	fmt.Println(nums)
	fmt.Println(s1)
	fmt.Println(s2)
	fmt.Println(s3)
	fmt.Println(s4)

	//向s1添加元素
	s1 = append(s1, 1, 1, 1, 1)  //其实会修改数组后面的内容
	fmt.Println(nums)
	fmt.Println(s1)
	fmt.Println(s2)
	fmt.Println(s3)

	//添加元素引起扩容,扩容会创建一个新的底层数组
	s1 = append(s1, 99, 22, 33, 44)
	fmt.Println(nums)
	fmt.Println(s1)
	fmt.Println(s2)
	fmt.Println(s3)


}

```

打印结果：
```
s1 = 0xc00001e050, s2 = 0xc00001e068, s3 = 0xc00001e078, s4 = 0xc00001e050, nums = 0xc00001e050

10 10
5 10
5 7
5 5
10 10
[1 2 3 4 1000 6 7 8 9 10]
[1 2 3 4 1000]
[4 1000 6 7 8]
[6 7 8 9 10]
[1 2 3 4 1000 6 7 8 9 10]
[1 2 3 4 1000 1 1 1 1 10]
[1 2 3 4 1000 1 1 1 1]
[4 1000 1 1 1]
[1 1 1 1 10]
[1 2 3 4 1000 1 1 1 1 10]
[1 2 3 4 1000 1 1 1 1 99 22 33 44]
[4 1000 1 1 1]
[1 1 1 1 10]

```

## 切片尾部添加元素
> 如果要对长度以外的索引赋值需要使用内置函数append()添加，如果在长度以内的直接使用切片名[索引]赋值
**由于append()添加后可能引起扩容，会返回一个切片的新地址，因此我们必须用原切片接收**

方式1：append()后面可以加多个元素，将多个元素添加到切片中
方式2：append()后面可以加一个切片，将后面切片中的所有元素加入到切片中，并返回

```go
nums = append(nums, 2, 3, 4)
nums = append(nums2, nums...)
```

## 切片遍历


```go
package main

import "fmt"

func main() {
	//定义一个切片
	nums := []int{99, 18, 239, 109, 11, 3, 45}

	//遍历切片
	//第一种方式遍历切片
	for i := 0; i < len(nums); i++ {
		fmt.Printf("%d\t", nums[i])
	}
	fmt.Println()

	//第二种方式遍历切片
	for i, val := range nums{
		fmt.Printf("%d------>%d\n", i, val)
	}
}
```