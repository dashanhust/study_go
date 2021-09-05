if 语句中的变量，只在当前condition中有效，出了这个if和else的condition之后，将无效。例如：
```golang
if n := 1, n < 0 {
	// ...
} else if n > 0 {
	// ...
} else {
	fmt.Println(n)  // n存在if-else的整个命名空间中
}

fmt.Println(n)  // 报错，n没有被定义
```