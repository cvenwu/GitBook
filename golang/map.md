# Map
> map是引用类型
## 注意事项

1. **map是无序的**，每次打印出来map都会不一样，它不能通过index获取，而必须通过key获取
2. **map长度不固定**并且和slice一样也是引用类型。
3. map的len函数会返回map的key的数量
4. map的key可以是所有比较的类型，如布尔型，字符串，整数型，浮点型

引用类型的默认值是nil。切片如果没有初始化，但也是有底层数组的，可以直接使用，但是空的map不可以使用。

当key值不存在时，我们通过`map名字[key]`不会报错，而是返回value对应类型的默认值，如果使用map[key]将会获取值对应的这个类型对应的默认值,也就是该类型对应的零值。因此我们可以使用ok-idiom模式判断key是否存在，如果key存在，则返回true，否则返回false。`if v,ok:=m["d"];ok{存在}` 使用ok-idiom模式判断key是否存在


## map的三种语法

1. 创建map `var map1 map[key类型]value类型` 只是声明map并没有创建，是nil map，无法直接使用。这个只有声明，没有初始化，是一个nil map。这种属于连盘子都没有
2. 通过make函数创建 `var map2 = make(map[key类型]value类型)`，只是一个弄了一个空盘子
3. `var map3 = map[key类型]value类型{key:value, key1:value1....}`，不仅弄了一个盘子，还加了饺子在里面。





```go


package main

import "fmt"

func main() {
	//创建map
	var map1 map[int]string		//只有声明，没有初始化，是一个nil map。第一种属于连盘子都没有
	var map2 = make(map[int]string)  //make本身就是创建，有盘子，但盘子为空
	var map3 = map[string]int{"go": 21, "python": 99, "html": 33}  //创建并初始化，既有盘子又有饺子
	fmt.Println(map1)
	fmt.Println(map2)
	fmt.Println(map3)

	//如何判断是否为nil map呢
	fmt.Println(map1 == nil)
	fmt.Println(map2 == nil)
	fmt.Println(map3 == nil)

	//因此我们首先要判断map是否为空
	if map1 == nil {
		map1 = make(map[int]string)
		fmt.Println(map1 == nil)
	}
 }

```


## map的操作


- 添加数据 `map名字[key] = value`
- 删除数据 `delete(map名字, key值)` 根据key删除数据
- 修改数据 `map名字[key] = value` 修改数据
- 获取数据 `value, ok = map[key]` 如果ok为true说明键存在，value为对应的值，否则为false，value为对应类型的默认值。
- 长度：len()



如果想要有序获取map的数据，思路如下
1. 获取所有的key, 将其存放切片或数组
2. 进行排序，使用排序算法或者sort包下的函数
3. 遍历key，-----》map[key]