title: Golang 快速入门 方法 接口
date: 2015-07-07 15:10:05
categories:
- Golang
tags:
- Golang

---

##Golang 快速入门 方法 接口

内容来自[https://tour.golang.org/]()

格式说明:
>// 正常注释  
//-----依赖关系  
//-->关联关系  

{% codeblock lang:golang %}
package main

import "os"
import "time"
import (
	"fmt"
	"image"
	"io"
	"log"
	"math"
	"net/http"
	"strings"
)

//--- 方法
type Vertex struct {
	X, Y float64
}

//Go 没有类。然而，仍然可以在结构体类型上定义方法。
//方法接收者 出现在 func 关键字和方法名之间的参数中。
func (v *Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

//---

//-- 方法(续)
//你可以对包中的 任意 类型定义任意方法，而不仅仅是针对结构体。
//但是，不能对来自其他包的类型或基础类型定义方法。
type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

//---

// 接收者为指针的方法
func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

// 接口
//接口类型是由一组方法定义的集合。
//接口类型的值可以存放实现这些方法的任何值。
type Abser interface {
	Abs() float64
}

// 隐式接口
//类型通过实现那些方法来实现接口。 没有显式声明的必要；所以也就没有关键字“implements“。
//隐式接口解藕了实现接口的包和定义接口的包：互不依赖。
//因此，也就无需在每一个实现上增加新的接口名称，这样同时也鼓励了明确的接口定义。
type Reader interface {
	Read(b []byte) (n int, err error)
}

type Writer interface {
	Write(b []byte) (n int, err error)
}

type ReadWriter interface {
	Reader
	Writer
}

//---

// Stringers 与java的toString()方法类似
// 在打印或format时生效
type Person struct {
	Name string
	Age  int
}

func (p Person) String() string {
	return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
}

//---

// 错误
// Go 程序使用 error 值来表示错误状态
type MyError struct {
	When time.Time
	What string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %v", e.When, e.What)
}

func run() error {
	return &MyError{
		time.Now(),
		"it didn't work",
	}
}

//---

// Web服务器
type Hello struct{}

func (h Hello) ServeHTTP(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello")
}

func main() {
	//--> 方法
	v := &Vertex{3, 4}
	fmt.Println(v.Abs())

	//--> 方法续
	f := MyFloat(-math.Sqrt2)
	fmt.Println(f.Abs())
	//--> 接收者为指针的方法
	v.Scale(5)
	fmt.Println(v, v.Abs())

	//--> 接口
	var a Abser
	f1 := MyFloat(-math.Sqrt2)
	v1 := Vertex{3, 4}
	// a MyFloat 实现了Abser
	a = f1
	// a *Vertext 实现了Abser
	a = &v1
	// 下面一行，v1是一个 Vertex（而不是 *Vertex）
	// 所以没有实现 Abser。
	//a = v1
	fmt.Println(a.Abs())

	//-->隐式接口
	var w Writer
	w = os.Stdout
	fmt.Fprintf(w, "Hello, writer\n")

	//-->Stringers
	p1 := Person{"xjliao", 25}
	p2 := Person{"lllou", 25}
	fmt.Println(p1, p2)

	// 错误
	if err := run(); err != nil {
		fmt.Println(err)
	}

	// Readers
	r := strings.NewReader("Hello, Reader!")
	br := make([]byte, 8)
	for {
		n, err := r.Read(br)
		fmt.Printf("n = %v err = %v br=%v\n", n, err, br)
		fmt.Printf("br[:n] = %q\n", br[:n])
		if err == io.EOF {
			break
		}
	}

	//--> 图片
	m := image.NewRGBA(image.Rect(0, 0, 100, 100))
	fmt.Println("m.Bounds=", m.Bounds())
	fmt.Println(m.At(0, 0).RGBA)

	//--> Web服务器
	var h Hello
	err := http.ListenAndServe("localhost:4000", h)
	if err != nil {
		log.Fatal(err)
	}

}
{% endcodeblock %}