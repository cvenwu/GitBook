# type关键字的使用

作用：定义一些新类型或者给类型起别名。也可以使用type定义函数类型

`type 类型名 Type` 定义一个新类型

`type 类型名 = Type` 给类型起别名

![Dr2i3b](https://gitee.com/yirufeng/images/raw/master/uPic/Dr2i3b.png)

## 定义类型

### 定义结构体

![ul3vUY](https://gitee.com/yirufeng/images/raw/master/uPic/ul3vUY.png)

### 定义接口

![t2qM9I](https://gitee.com/yirufeng/images/raw/master/uPic/t2qM9I.png)

### 定义其他的新类型

![kbGbmG](https://gitee.com/yirufeng/images/raw/master/uPic/kbGbmG.png)

type自定义的类型和其对应的类型语法上不能通用

`type myint int` 例如定义myint类型其实就是int,但是语法上不能通用



```go
package main

import (
	"fmt"
	"strconv"
)

//定义一个新的类型
type myint int
type mystr string

func main() {
	//自定义一个新类型
	var i1 myint
	var i2 = 100
	i1 = 200
	fmt.Println(i1, i2)

	var name mystr
	name = "王二狗"
	var s1 string
	s1 = "李小花"
	fmt.Println(name, s1)

	fmt.Printf("%T %T %T %T\n", i1, i2, name, s1) //main.myint int main.mystr string

	//i3 := 299
	//i1 = i3 //报错：不能使用int作为myint
	//fmt.Println(i1)

	fmt.Println("----------------------------")
}

```



### 定义函数的类型

![lcS6c7](https://gitee.com/yirufeng/images/raw/master/uPic/lcS6c7.png)

```go
package main

import (
	"fmt"
	"strconv"
)


//定义函数类型
type myfun func(int, int) string //参数为两个int,返回string
func fun1() myfun {
	fun := func(a, b int) string {
		s := strconv.Itoa(a) + strconv.Itoa(b)
		return s
	}
	return fun

}
func main() {
	//i3 := 299
	//i1 = i3 //报错：不能使用int作为myint
	//fmt.Println(i1)

	fmt.Println("----------------------------")
	res := fun1()  //返回另一个函数,res指向fun1的内层函数
	fmt.Println(res(1, 2))


}

```

## 类型别名

语法：`type 别名 = Type` 到时将Type类型的变量赋值给别名对应的变量不会报错。如果对于一样的方法名，接收者一个是Type一个是别名，调用时将会报错，因为其实是一样的。

![AhJYIY](https://gitee.com/yirufeng/images/raw/master/uPic/AhJYIY.png)

## 非本地类型不能定义方法

![fSdu9J](https://gitee.com/yirufeng/images/raw/master/uPic/fSdu9J.png)

## 在结构体成员嵌入时使用别名

如果对于一样的方法名，接收者一个是Type一个是别名，调用时将会报错，因为其实是一样的。

```go
package main

import "fmt"

type Person struct {
	name string
}

type People = Person

type Student struct {
	Person
	People
}

func (p Person) show() {
	fmt.Println(p.name)
}

func (p People) show2() {
	fmt.Println(p.name)
}

func main() {
	var s Student
	//s.name = "你好"  //报错：ambiguous selector s.name
	s.Person.name = "王二狗"
	//s.show()  //报错 ambiguous selector s.show
	s.Person.show()

	s.People.name = "李小花"
	//s.show()  // ambiguous selector s.show
	s.People.show2()
	s.Person.show()



}

```

