---
title: Dart指南
date: 2018-06-05 22:19:14
tags:
---
# Dart语言重点

## 重要概念
1. Dart是纯面向对象的语言，所有的一切都是对象，包括内置类型。所以，Dart的变量未显式初始化前都为null(null也是对象);
2. 所有对象都是从Object类继承的；
3. Dart是强类型语言，但是具备类型推导，可以省略类型注解；
4. Dart支持泛型；
5. Dart支持顶层函数，main是一个特殊的顶层函数，提供应用的入口；
6. Dart支持顶层变量；
7. 以下划线开始的标识符表示库私有；

## 变量
变量持有对象的引用，默认值为null

```dart
    String name='Bob'
```

使用`var`可以省略类型,使用`Object`或者`dynamic`可以改变类型。

### final
如果不想改变变量的值，可以使用 `final`修饰,该变量只会初始化一次

### 更进一步const
const修饰的值在编译期就确定了，是个常量。任何变量都能保存常量值

## 内建类型
* 数值
* 字符串
* 布尔
* 列表
* 映射表
* 字符(runes)
* 标记(symbols)

### 数值
有两种变体`int`和`double`。
都是`num`的子类型，`num`提供基本的运算符和一些数学工具函数，没有`math`库

```dart
    //整形使用
    int x=1;
    int hex=0xDEADBEEF;
    //浮点型使用
    double y=1.0;
    double e=3.14e5;
    //数值和字符串转换
    var one=int.parse('1');
    String two=2.toString();
```

### 字符串
1. Dart字符串是UTF-16编码的，可以使用单引号或者双引号创建字符串；
2. 可以在字符串中插入表达式`${表达式}`，把表达式和字符串的值组合成新的字符串；
3. 使用`+`连接字符串；
4. 使用```创建多行字符串；
5. 使用前缀r创建原始字符串

### 布尔
只有两个对象`ture`和`false`

### 列表
```dart
    var list=[1,2,3];
```
`list`的类型是`List<int>`,不能放入非整形的对象。
可以使用`const`创建编译期常量列表。
```dart
    var cons=const [1,2,3];
```

### 映射表
Dart里面通过Map实现映射表，存储键值对，键不能重复，值可以重复
```dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

