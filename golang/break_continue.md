# break以及continue的使用
> break 或者 continue 都只是针对于紧挨break 或 continue 的内层循环

如果想要终止外层循环或者跳过可以给外层循环加上标签，之后使用语法：`break 外层循环加的标签名` 或 `goto 外层循环加的标签名`

首先要给我们想要中断的外层循环添加标签，之后在break或continue后面加上标签
```go
    //continue和break默认结束最里层的循环
	//如果我们想要结束外层循环可以贴标签
	out:for i := 0; i < 5; i++ {
		for j := 0; j < 5; j++ {
			if j == 1 {
				break out
			}
			fmt.Println("i = ", i, " j = ", j)
		}
    }
    
	out1:for i := 0; i < 5; i++ {
		for j := 0; j < 5; j++ {
			if j == 1 {
				continue out1
			}
			fmt.Println("i = ", i, " j = ", j)
		}
	}
```
打印结果如下：
```
i =  0  j =  0
i =  0  j =  0
i =  1  j =  0
i =  2  j =  0
i =  3  j =  0
i =  4  j =  0
```