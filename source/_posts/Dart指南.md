---
title: Dart指南
date: 2018-06-11 22:45:37
tags: Dart
# Go学习笔记

## 变量定义

### 特征
* 名字在前，类型在后
* 可以出现在函数里，也可以出现在函数外
* 可以多个变量一起定义
* 可以把变量定义用`()`包裹起来，形成块定义，以减少重复输入

### 有三种形式
* `var` 名称 类型
* `var` 名称=初始化值
* 简短初始化，省略`var`

### 示例
```go
    //a的默认值为0
    var a int
    //根据初始化值推断类型
    var b=1
    
    //函数内
    func vardef(){
        //定义并赋值
        c:=2
    }
    
    //块定义
    var(
        aa=3
        bb=4
        cc="abc"
    )
```

## 常量
### const
`const`定义常量，和`var`定义一致
### 枚举
`const`块
i

## if

### 特征
* if 后面定义的变量，只在if块内有效
* 不用小括号
```go
if a=0;a>100{
        fmt.Println(100)
    }
else if a<0{
    fmt.Println(0)
}else{
    fmt.Println(a)
}
}
```

## switch
### 特征
* 不需要显式break

## 循环
### 特征
* 可以省略初始条件，和递增条件，或者都不加

## 函数
### 特征
* 返回值在小括号后面
* 可以多值返回
* 返回形式，最后一个返回值一般是出错信息
* 返回值可以命名
* 参数，返回值，内部都可以是函数
* 可变参数`func sum(numbers ...int) int`
* 没有函数重载，没有默认值
### 形式
```go
func name(a,b int)(int){
    //内容
    return a+b
}

func apply(op func(int,int) int,a,b int) int{
    p:=reflact.Valueof(op).Pointer()
    name:=runtime.FuncForPC(p.Name)
    fmt.Printf('call function %s with args %d,%d',name,a,b)
    return op(a,b)
}
```

## 指针
### 特征
* 指针不能运算
* 只有引用传递

## 数组
### 特征
* [2]int和[3]不是相同类型
* 数组默认拷贝
* 可以直接对指针操作来改变值，不用解引用
### 形式
```go
//一般定义
var arr1=[3]int
//赋初值
arr2:=[3]{1,2,3}
//省略长度
arr3:=[...]{1,2,3}

```
### 遍历
```go
for i,v:=range arr3{
    fmt.Println(i,v)
}

for i:=range arr3{
    fmt.Println(i)
}

for _,v:=range arr3{
    fmt.Println(v)
}
```

## 切片
### 创建
```go
//零值
var s []int
//初始值
s1:=[]{2,4,6,8}
//预创
s2:=make(slice,32)

//添加
s=append(s,10)
//删除
s2=s2[1:]
//删除索引为3的元素，...表示取出里面的元素
s2=append(s2[:2],s2[4:]...)
```
### 结构
`slice`
ptr->len->cap

### 特征
* 切片是数组的视图
* 左闭右开区间
* 本身不保存数据，改变会改变底层数组
* 可以扩展，只能向后扩展
* 添加元素超越cap，会重新分配
```go
\\定义数组
arr:=[...]{0,1,2,3,4,5,6,7,8]

s1:=[:]     \\全部[0,1,2,3,4,5,6,7,8]
s2:=[2:4]   \\[2,3]
s3:=[2:]    \\[2,3,4,5,6,7,8]
s4:=[:4]    \\[0,1,2,3]
```

## Map
### 形式
```go
m1 := map[string]string{
    "one":"one",
    "two":"two",
    "three":"three"
}

m2 := make(map[string]int)

var m3=map[string]int
```

### 特征
* 无序
* 取不存在的值获得零值
* 判断key在不在
```go
value,ok:=m['four']
```
### 操作
```go
//遍历
for k,v:=range m{
    
}

//删除
delete(m,'one')

//元素个数
len(m)
```

### key规则
* 必须可以比较相等
* 除了slice,map,function内建类型都可以作为key
* Struct不含slice,map,function也可以作为key---
