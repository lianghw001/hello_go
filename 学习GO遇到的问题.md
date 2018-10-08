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
var a [5]int             //[0 0 0 0 0]
var s []int = a[1:4]     //[0 0 0],半开区间，包括第一个元素，但排除最后一个元素。

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
