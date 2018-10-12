 # 学习GO遇到的问题

## 变量初始化和声明
- rune，相当于char

var 和 := (简短声明)的的区别


定义变量

````var num int````

定义变量并初始化

````var num int = 100````

简短声明

````num:=100````

:=只能在声明“局部变量”的时候使用


##  常量

常量的声明与变量类似，只不过是使用 const 关键字

常量可以是字符、字符串、布尔值或数值

常量不能用 := 语法声明

````
const Pi = 3.14
const Truth = true
````

## 3. 没有while，用for
for 初始化语句和后置语句是可选的。

````
 for ; sum < 1000; {
  sum += sum
 }
````
 省略分号，当while用
 
````
  for sum < 1000 {
   sum += sum
  }
````

无限循环

````
for {
	}
````

range 形式

````
for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
````

## 4. 输出

````
num := 10
fmt.Println(num)　　//right
fmt.Println("abc")　　//right
fmt.Printf("%d",num)　　//right
fmt.Printf(num)　　//error
````

## 5. switch

只执行只执行选定的case，除非fallthrough

## 6. defer

外层函数return时调用

````defer fmt.Println(i)````

## 7. 整型转字符串

````
// 通过Itoa方法转换
str1 := strconv.Itoa(i)

// 通过Sprintf方法转换
str2 := fmt.Sprintf("%d", i)
 
````

## 数组与切片

	````
	var a [5]int {1,2,3,4,5}            //[1 2 3 4 5] 数组
	var s []int = a[1:4]     //[2 3 4],切片：半开区间，包括第一个元素，但排除最后一个元素。
	var b := s		//切片是引用
	k := make([]int, 5)     //make 函数会分配一个元素为零值的数组并返回一个引用了它的切片	
	s = append(s, 6，7)  	//[2 3 4 6 7]，自动扩展
	for i, v := range s { 	//range遍历，返回下标，和值
		fmt.Printf("2**%d = %d\n", i, v)
	}
	````
## 映射 map
	````
	m := make(map[string]int)
	m["Bell Labs"] = 8
	fmt.Println(m["Bell Labs"])
	delete(m,"Bell Labs")		//删除元素
	elem, ok := m["Bell Labs"]	//元素检查
	package main
	````
## 函数的闭包
	````
	import "fmt"

	func adder() func(int) int {
		sum := 0
		return func(x int) int {
			sum += x
			return sum
		}
	}

	func main() {
		pos, neg := adder(), adder()
		for i := 0; i < 10; i++ {
			fmt.Println(
				pos(i),
				neg(-2*i),
			)
		}
	}
	````	

## 方法
- 一般使用指针作为接收者
	````
	func (v Vertex) Abs() float64 {//Vertxx结构体的方法
		return math.Sqrt(v.X*v.X + v.Y*v.Y)
	}
	func (v *Vertex) Scale(f float64) {//指针接收者，可以修改原来对象的值（若不是指针，只会修改传进来的副本）
		v.X = v.X * f
		v.Y = v.Y * f
	}
	````
	
## 接口
	````
	type I interface {
		M()
	}
	interface {}//空接口
	var i I
	i = "hello"
	
	//类型断言
	t := i.(string)  //t=="hello"
	w := i.(int)	//i没有int，引发pannic
	q, ok := i.(int)//不引发panic
	
	
	switch v := t.(type) {
	case int:
		//
	case string:
		//执行
	default:
		//
	}
	````
## 信道

- 创建信道

````
ch := make(chan int)

````

- 带缓冲的信道
````
ch := make(chan int, 100)

````

- 传值,自动阻塞


````
ch <- v    // 将 v 发送至信道 ch。
v := <-ch  // 从 ch 接收值并赋予 v。

````

- 当接收者需要知道想知道是否关闭时，发送者需要close信道
````
func fibonacci(n int, c chan int) {
	x, y := 0, 1
	for i := 0; i < n; i++ {
		c <- x
		x, y = y, x+y
	}
	close(c)
}

func main() {
	c := make(chan int, 10)
	go fibonacci(cap(c), c)
	for i := range c {
		fmt.Println(i)
	}
}

````

- select，随机执行非阻塞的分支
````
select {
		case c <- x:
			x, y = y, x+y
		case <-quit:
			fmt.Println("quit")
			return
		}

````
