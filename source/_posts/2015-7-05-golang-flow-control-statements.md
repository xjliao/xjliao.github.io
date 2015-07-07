title: Golang 快速入门 流程控制语句 
date: 2015-07-05 15:10:05
categories:
- Golang
tags:
- Golang

---

##Golang 快速入门 流程控制语句

内容来自[https://tour.golang.org/]()

格式说明:
>// 正常注释  
//-----依赖关系  
//-->关联关系  

{% codeblock lang:golang %}
package main

import (
	"fmt"
	"math"
	"runtime"
	"time"
)

func sqrt(x float64) string {
	// if
	if x < 0 {
		return sqrt(-x) + "i"
	} else {
		fmt.Printf("x < 0")
	}

	return fmt.Sprint(math.Sqrt(x))
}

// if 便捷语句
func pow(x, n, lim float64) float64 {
	if v := math.Pow(x, n); v < lim {
		return v
	}

	return lim
}

func main() {
	// for
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)

	// for 续
	sumb := 1
	for sumb < 1000 {
		sumb += sumb
	}
	fmt.Println(sumb)

	// while 用for表示， 所以没有while了
	sumc := 1
	for sumc < 1000 {
		sumc += sumc
	}
	fmt.Println(sumc)

	// 无限循环 这里先注释掉， 要不然后面无法执行
	//for {
	//
	//}

	//-->if else
	fmt.Println(sqrt(2))

	//-->if 便捷语句
	fmt.Println(pow(3, 2, 10))

	// switch 当符合
	// fallthrough  这个关键字的作用和java的switch 不加break的
	// 执行顺序有上而下，匹配成功停止
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
	case "linux":
		fmt.Println("Linux.")
	case "darwin":
		fmt.Println("OS X")
		// 当进入这里时，使用fallthrough，还会执行defluat
		fallthrough
	default:
		// freebsd, openbsd,
		fmt.Println("%s", os)
	}

	// 没有条件的switch
	// 和 switch true {
	//case:
	//default:
	//}
	// 一样
	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning.")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}

	// defer 延迟函数的执行直到上层函数返回
	// 延迟调用的参数会立刻生成，但是在上层函数返回前函数都不会被调用
	defer World()
	fmt.Println("hello")
	// defer 栈
	fmt.Println("counting.....")
	for i := 0; i < 100; i++ {
		defer fmt.Println(i)
	}
	fmt.Println("done")
}

func World() {
	fmt.Println("world")
}
{% endcodeblock %}