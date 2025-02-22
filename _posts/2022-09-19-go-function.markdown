---
layout: post
title:  "Go：函数"
author: Gjq
date:   2022-09-19 23:46:16 +0800
categories: learn golang
tags: [Go语言, 编程]
---
## 引言

本文基于Go 1.19版本。

## 声明
Go语言中，函数的声明由名字、形参列表、返回列表（可选）和函数体构成，注意Go对代码格式要求比较严格：

```go
func name(parameter-list) (result-list) {
    body
}
```

### 声明的组成成分

函数的名字和其他名字有着同样的规则，由字母或下划线开头，后面可以跟任意数量的字符、数字和下划线，并且区分大小写。

函数的形参列表由一组变量的参数名和参数类型构成。

函数的形参变量由函数的实参的值进行初始化，为函数最外层作用域的局部变量。

函数的返回列表制定了返回值的类型和名字（可选）。如果函数的没有返回值或只有一个未命名的返回值是，返回列表的圆括号可以省略。

命名的返回值会根据变量类型初始化为相应的0值，和形参变量一样，同为函数最外层作用域的局部变量。

存在返回列表时，无论返回值有没有得到命名，函数必须显式地以return结束。如下，return不能省略：

```go
func sub(x int, y int) (z int) {
    z = x - y
    return
}
```

### 相同类型简写

当多个形参或返回值的类型相同时，可以采用简写的方式，只写一次类型。如下的两个声明完全等价：

```go
func f(i, j, k, int, s, t string ) {
    /* ... */
}

func f(i int, j int, k int, s string, t string) {
    /* ... */
}
```

### 函数签名及其等价性

函数的类型被称为函数签名，如果两个函数的形参列表和返回列表相同（形参和返回值的名称不影响），则认为两个函数的类型是相同的。如下的两个函数签名即是相同的：

```go
func add(a int, b int) int {
    return a + b
}

func sub(x int, y int) (z int) {
    z = x - y
    return
}
```

### 无默认参数

Go语言中没有默认参数值，也不能指定实参名，因此GO语言中需要提供实参来对应函数中的每个形参，并保持调用顺序的一致。以下在Python中的语法，Go中不存在：

```Python
def func(a=2, b=3, c=5):
    return a + 2*b + 3*c


# 2+2*3+3*5 = 23
print(func())
# 1+2*3+3*5 = 22
print(func(1))
# 2+2*4+3*1 = 13
print(func(c=1, b=4, a=2))
```

### 按值传递

和C语言类似的，Go语言的实参也是按值传递的，修改函数的形参变量并不会影响被调用者提供的实参。当然，可以通过指针、slice等特定形参变量间接修改实参的变量。

### 无函数体的声明

Go语言中存在没有函数体的函数声明，这样的函数是由其他语言实现的：

```go
package math

func Sin(x float64) float64 // 使用汇编语言实现
```
