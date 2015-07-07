title: Golang 快速入门 slice array map 函数闭包
categories:
- Golang
tags:
- Golang

---

Golang 快速入门 slice array map 函数闭包

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
)

// 结构体
type Vertex struct {
	X int
	Y int
}

// 字面结构体
var (
	v1 = Vertex{1, 2}
	v2 = Vertex{X: 1}
	v3 = Vertex{}
	p  = &Vertex{1, 2}
)

var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

// map
type Location struct {
	Lat, Long float64
}

var m map[string]Location

// 字面map
var mi = map[string]Location{
	"Bell Labs": {34.34499, -89.09492},
	"Google":    {34.34123, -123.34321},
}

// 字面map(续)
// 如果顶级的类型只有类型名的话，可以在文法的元素中省略键名。
// 这里的类型名是指Location
var mj = map[string]Location{
	"Bell Labs": {34.34499, -89.09494},
	"Google":    {34.34123, -123.34321},
}

func main() {
	//指针
	i, j := 42, 8000

	p := &i
	fmt.Println(p)
	*p = 21
	fmt.Println(i)
	fmt.Println(p)
	fmt.Println(&i)

	p = &j
	*p = *p / 2
	fmt.Println(j)

	//-->结构体
	fmt.Println(Vertex{1, 2})

	// 结构体字段
	v := Vertex{3, 4}
	v.X = 5
	fmt.Println(v.X)

	// 结构体指针
	q := &v
	q.X = 1000
	fmt.Println(v)

	//-->字面结构体
	fmt.Println(v1, p, v2, v3)

	// 数组
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1])
	fmt.Println(a)

	// 片
	s := []int{2, 3, 5, 7, 11, 13}
	fmt.Println("s==", s)
	for i := 0; i < len(s); i++ {
		fmt.Printf("s[%d] == %d\n", i, s[i])
	}

	// 对slice切片
	// 从下标1开始到4，但不包含4 fmt.Println("s[1:4] ==", s[1:4])
	// 省略下标从0开始到3，但不包含3
	fmt.Println("s[:3] ==", s[:3])
	// 省略上标 len(s)结束
	fmt.Println("s[4:] ==", s[4:])
	// 构造切片
	a1 := make([]int, 5)
	printSlice("a1", a1)
	b := make([]int, 0, 5)
	printSlice("b", b)
	c := b[:2]
	printSlice("c", c)
	d := c[2:5]
	printSlice("d", d)

	// nil slice, slice 的零值是nil
	// 一个 nil 的 slice 的长度和容量是 0。
	var z []int
	fmt.Println(z, len(z), cap(z))
	if z == nil {
		fmt.Println("nil!")
	}

	// 像slice添加元素
	z = append(z, 0)
	printSlice("z", z)

	z = append(z, 1)
	printSlice("z", z)

	z = append(z, 2, 3, 4)
	printSlice("z", z)

	// range 范围
	for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
	// range 范围续
	pow1 := make([]int, 10)
	for i := range pow1 {
		pow1[i] = 1 << uint(i)
	}
	// 如果不适用_, 则value默认是rang的index值
	for _, vlaue := range pow1 {
		fmt.Printf("value=%d\n", vlaue)
	}

	//-->map
	m = make(map[string]Location)
	m["Bell Labs"] = Location{
		40.99922, -73.94391,
	}
	fmt.Println(m["Bell Labs"])

	//-->字面map
	fmt.Println(mi)
	//-->字面map(续)
	fmt.Println(mj)
	// 修改map
	mk := make(map[string]Location)
	mk["liaoxinjian"] = Location{120.00, -110.00}
	mk["loulihua"] = Location{120.00, -110.00}
	fmt.Println("mk=", mk)
	// 删除
	delete(mk, "loulihua")
	fmt.Println("loulihua.location", mk["loulihua"])
	// 通过双赋值检测某个键存在
	v1, ok := m["loulihua"]
	fmt.Println("value=", v1, " Present?", ok)

	// 函数值
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(3, 4))

	//-->函数的闭包
	pos, neg := adder(), adder()
	for i := 0; i < 10; i++ {
		fmt.Println(
			pos(i),
			neg(-2*i),
		)
	}
}

// 函数的闭包
func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}

func printSlice(s string, x []int) {
	fmt.Printf("%s len=%d cap=%d %v\n", s, len(x), cap(x), x)
}
{% endcodeblock %}