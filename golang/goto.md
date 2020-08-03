# goto语句

> 程序正常执行时会进入贴上标签的代码，并执行

语法：`goto 标签`


给代码贴上标签：`标签: 代码`



```go
	a := 10
	loop: 
		for a < 20 {
			if a == 15 {
				a += 1
				goto loop
			}
			fmt.Println(a)
			a++
		}
	a += 1
	fmt.Print("123")
	breakHere:		//这里会按照顺序正常执行
		return
	fmt.Print("123")

	fmt.Print(23)
	goto breakHere
```

打印结果如下：

```
10
11
12
13
14
16
17
18
19
123
```

## 应用场景
> goto语句应用：统一错误处理


```go
	err := firstCheckError()
	if err != nil {
		goto onExit
	}

	err := secondCheckError()
	if err != nil {
		goto onExit
	}

	fmt.Println("done")
	return

	onExit:
		fmt.Println(err)
		exitProcess()
```