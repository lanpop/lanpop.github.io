---
layout: "post"
title: "Go的异常处理 defer\\panic\\recover"
date: "2019-02-13 14:49"
tag: [go,exception]
excerpt: 在GO语言中不支持try...catch...finally来处理异常，因为GO语言的设计者认为，将异常与控制结构混在一起容易使得代码变得混乱。
---

在GO语言中不支持try...catch...finally来处理异常，因为GO语言的设计者认为，将异常与控制结构混在一起容易使得代码变得混乱。在GO语言中，使用多值返回来返回错误。不要使用异常代替错误，更不要使用异常来控制流程。在极个别情况下，也就是说遇到真正的异常的情况下（比如除数为0）。才可以使用GO中引入的Exception处理：defer/panic/recover。

可以简单理解为抛出一个panic异常，然后在defer中通过recover捕获，然后正常处理。

```go
package main

import "fmt"

func main(){
	first()
	second()
	third()
}

func first()  {
	fmt.Println("我是第一个函数！")
}

func second(){
	fmt.Println("我是第二个函数，下面会发生异常！")
	panic("给我停！！！")
}

func third()  {
	fmt.Println("我是第三个函数，并没有停！")
}
```
>运行结果：  
我是第一个函数！  
我是第二个函数，下面会发生异常！  
panic: 给我停！！！

进行异常处理
```go
func main(){
	first()
	second()
	third()
}

func first()  {
	fmt.Println("我是第一个函数！")
}

func second(){
	fmt.Println("我是第二个函数，下面会发生异常！")
	defer func() {
		if err:=recover();err!=nil{
			fmt.Println("处理异常...","异常信息是：",err)
		}
	}()

	panic("给我停！！！")
}

func third()  {
	fmt.Println("我是第三个函数，并没有停！")
}
```
>运行结果：  
我是第一个函数！  
我是第二个函数，下面会发生异常！  
处理异常... 异常信息是： 给我停！！！  
我是第三个函数，并没有停！

## defer
defer 在函数返回前被调用，当存在多个defer时，后面的会先调用，类似栈。

```go
func a() (result int)  {
	defer func() {
		fmt.Println("defer 1")
	}()
	defer func() {
		fmt.Println("defer 2")
	}()
	defer func() {
		fmt.Println("defer 3")
	}()
	return 0;
}
```
>defer 3  
defer 2  
defer 1

## panic
panic 在Go语言中是一个内置函数，一般会导致程序挂掉。类似于throw异常。

## recover
recover 在Go语言中是一个内置函数，调用recover会捕获当前的panic，捕获后避免程序挂掉。

## 总结
defer,recover结合使用，类似于try...catch...
```go
defer func() {
  if err:=recover();err!=nil{
    fmt.Println("处理异常...","异常信息是：",err)
  }
}()
```
