 # 学习GO遇到的问题

## 1. 变量初始化和声明
var 和 := (简短声明)的的区别


定义变量

````var num int````

定义变量并初始化

````var num int = 100````

简短声明

````num:=100````

:=只能在声明“局部变量”的时候使用


## 2. 常量

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
