title: Golang 快速入门 基础 包 变量 函数 
date: 2015-07-01 10:10:05
categories:
- Golang
tags:
- Golang

---

Golang 快速入门 基础 包 变量 函数 

内容来自[https://tour.golang.org/]()

格式说明:
>// 正常注释  
//-----依赖关系  
//-->关联关系  

{% codeblock lang:golang %}
// 包
package main

// 导入方式1
import "fmt"

// 导入方式2
import (
	"math"
	"math/cmplx"
)

// 多值返回
func swap(lastname string, firstname string) (string, string) {
	return firstname, lastname
}

// 命名返回值
func split(sum int) (x, y, sm int) {
	sm = sum
	x = sum * 4 / 9
	y = sum - x
	return
}

// 变量
var c, python, java bool
var x int

// 初始化变量
var v, u int = 2, 1

// 变量组
var (
	// Go 基本数据类型
	// bool, string, int, int8, int16, int32, int64,
	// uint, uint8, uint16, uint32, uint64, uintptr,
	// byte(unit8的别名), rune(int32的别名，代表一个Unicode码)
	// float32, float64
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)

// 常量(常量不能使用 := 语法定义)
const Pi = 3.14

//-----
//数值常量(数值常量是高精度的值)
const (
	Big   = 1 << 100
	Small = Big >> 99
)

func needInt(x int) int {
	return x*10 + 1
}

func needFloat(x float64) float64 {
	return x * 0.1
}

//-----

func main() {
	//-->多值返回&命名返回值
	lastname, firstname := swap("建", "廖新")
	fmt.Println(lastname, firstname)
	fmt.Println(split(100))

	//-->变量
	var i int
	var y int
	fmt.Println(i, c, python, java, x, y)
	fmt.Println(v, u)

	// 短声明变量，只能在函数内使用，函数外的必须以关键字var, func 等等开头
	k := 100
	fmt.Println(k)
	//-->Go基本数据类型
	fmt.Println(ToBe, MaxInt, z)

	//零值
	var q int
	var f float64
	var w bool
	var s string
	fmt.Printf("%v %v %v %q\n", q, f, w, s)

	// 类型转换
	var x, g int = 3, 4
	var r float64 = math.Sqrt(float64(x*x + g*g))
	var z int = int(r)
	fmt.Println(x, g, z)

	// 类型推导
	v := 42
	fmt.Printf("v的类型是%T\n", v)

	//-->常量
	const World = "世界"
	fmt.Println("你好", World)
	fmt.Println("原周率Pi=", Pi)
	const Truth = true
	fmt.Println("Go rules?", Truth)

	//-->数值常量
	fmt.Println(needInt(Small))
	fmt.Println(needFloat(Small))
	fmt.Println(needFloat(Big))
}
{% endcodeblock %}