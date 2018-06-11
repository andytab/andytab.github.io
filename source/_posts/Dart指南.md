---
title: Dart指南
date: 2018-06-11 23:30:05
tags: Dart
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
//添加
gifts['fourth']='calling birds';
//获取
assert(gifts['first'==partridge)
//如果获取的元素不存在，返回null
assert(gifts['fifth']==null)
//获取长度
gifts.length
```
### Runes
Runes在Dart里面表示string的UTF-32的码点(Code Point)
Dart的字符串是UTF-16为编码单位的，因此表示32位的Unicode值需要特殊语法

通常。表示一个Unicode值会写成`\uxxxx`，`x`表示一个16进制值，表示超过4个的16进制数，需要用大括号包裹住值，如emoji中大笑的表示形式为`\u{1f600}`

`String`里面提供了一些属性操作`runes`，如`runes`属性可以获取到一个字符串的`runes`

### 标识符（symbols）
`Symbols`对象表示`Dart`程序里面一个操作符或者声明的标识符

### 函数
所有的函数都是`Function`类型的对象，所以函数可以作为赋值给一个变量，或者作为参数传递给其他函数，也可以像调用函数一样调用一个类的实例，以下是个简单例子
```dart
bool isNoble(int atomicNumber){
    return _nobleGases[atomicNumber]!=null
}

//当然省略类型注解也是可以的，只是不推荐这样做
bool isNoble(atomicNumber){
    return _nobleGases[atomicNumber]!=null
}
//函数只有一个简单表达式，则可以简写为这样，称为短箭头语法
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```
#### 可选参数
函数可以有两种类型的形参列表，必须的和可选的，必须的写在前面，后面可以加上任意可选的参数
可选参数可以是位置参数或者命名参数，但不能同时用
##### 可选命名参数
调用函数的时候可以通过`paramName: value`的形式来指定可选命名参数
```dart
enableFlags(bold: true, hidden: false);
```
定义的时候，可以通过`{param1, param2, …}`的形式指定命名参数
```dart
void enableFlags({bool bold, bool hidden}) {
  // ...
}
```
##### 可选的位置参数
用一个`[]`包裹的集合来标记一个可选的位置参数列表
```dart
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```
调用形式有两种，一种是不提供可选实参，一种是提供，如
```dart
assert(say('Bob', 'Howdy') == 'Bob says Howdy');

assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```
##### 参数默认值
可以使用`=`的形式为两种形式的参数提供默认值，但是值必须是编译期常量，没有默认值，则为null

#### main函数
返回值为`void`有一个可选的`List<String>`参数，是所有应用的入口

#### ..级联操作语法
`..`可以对同一个对象进行一系列的操作
```dart
querySelector('#sample_text_id')
    ..text = 'Click me!'
    ..onClick.listen(reverseText);
```
#### 匿名函数
可普通函数的定义一样，只是不需要名字
```dart
([[Type] param1[, …]]) {
  codeBlock;
};
```
#### 作用域
作用域是静态的，你可以根据大括号来确定一个变量是否在作用域内
#### 闭包
闭包是一个函数对象，即使它被用在原始作用域之外的地方，它也可以访问它作用域内的变量
```dart

Function makeAdder(num addBy){
    return (num i)=> addBy+i
}

void main(){
    //通过2来创建函数
    var add=makeAdder(2)
    
    //现在addBy是2，传递形参3调用函数，得到5
    assert(add(3)==5
}
```
#### 返回值
没有指定返回值，返回null

## 操作符
可以重载操作符，和其他语言类似
### 类型操作
操作符 | 涵义
-------|-----
`as`   |类型转换
`is`   |如果是特定类型则为True
`is!`  |如果是特定类型则为False
### 条件表达式
形式1，条件成立则表达式的值为表达式1，肉则值为表达式2
```条件 ? 表达式1 : 表达式2```

形式2，表达式1不为null，则表达式的值为表达式1，否则为表达式2
```表达式1 ?? 表达式2```

## 异常
所有异常都是非受检的，函数不会声明它会抛出什么异常，也不需要使用者捕获什么异常。Dart可以将任意非空对象作为异常和错误抛出
```dart
//抛异常
void op(Op op)=>throw 'something happan';
//捕获异常
try{
    op(new Op('+');
}on Exception catch(e){
    print('$e')
}
```
## 类
* 单继承，都是`Object`的子类
* 构造对象可以省略`new`
* `?.`可以避免发生null异常
* `const`创建常量值
* 使用`runtimeType`获取运行时类型，返回`Type`对象
* 未初始化的成员变量值都为`null`
* 所有实例变量都隐式实现了`getter`，非`final`实例变量实现了`setter`
* 构造器不能继承

### 构造
构造器名字可以是`ClassName`或者`ClassName.identifier`的形式

同理，`this`指代当前对象，建议出现命名冲突时才使用
```dart
class Point{
    num x,y;
    
    Point(num x,num y){
        this.x=x;
        this.y=y;
    }
    //语法糖，推荐使用这种赋值方式，在构造器体运行前运行
    //Point(this.x,this.y)
}
```
#### 命名构造器
使用命名构造器来实现多构造器，或者提供一个更明确的实例构造形式
```dart
class Point{
    num x,y;
    
    //命名构造器
    Point.origin(){
        x=0;
        y=0;
    }
}
```
#### 调用非默认父类构造器
默认情况下，子类的构造器会在构造器的开始调用父类中未命名，无参的构造器。如果提供了初始化列表，初始化列表先于父类构造器执行。所以执行顺序为
1. 初始化列表
2. 父类无参构造器
3. 主类无参构造器

如果主类没有未命名，无参的构造器，则需要手动调用。调用形式为子类构造器小括号之后加入冒号
#### 初始化列表
构造器冒号之后，不仅可以调用父类构造器，还可以初始化实例变量，当然，不能访问到`this`,初始化列表用来设置`final`字段
#### 重定向构造器
一个构造器可以在冒号之后调用同一类的其他构造器，函数体为空
#### 常量构造器
如果类生成的对象 不会改变，可以使用`const`来定义构造器，同时保证所有的实例变量是`final`
#### 工厂构造器
当不需要经常创建类的实例时，可以使用`factory`创建构造器。返回的类型可以是从缓存中获取的，也可以是子类对象

### 方法
方法是为对象提供行为的函数
#### 实例方法
可以访问`this`和实例变量
#### Getter和Setter
可以使用`get`和`set`关键字来覆盖默认的getter和setter
#### 抽象方法
抽象方法只存在于抽象类中，用分号(`;`)代替函数体
#### 重载操作符
可以重载下面这些操作符
<  |+  |\| |[]
---|---|---|--
<  |/  |^  |[]==
<= |~/ |&  |~
>= |*  |<< |==
-  |%  |>> |

```dart
class Vector {
  final int x, y;

  const Vector(this.x, this.y);

  /// Overrides + (a + b).
  Vector operator +(Vector v) {
    return new Vector(x + v.x, y + v.y);
  }

  /// Overrides - (a - b).
  Vector operator -(Vector v) {
    return new Vector(x - v.x, y - v.y);
  }
}

```
如果重载`==`需要同时重载`hashcode`getter

## 抽象类
使用`abstract`修饰符定义抽象类，抽象类不能实例化，提供接口定义。
### 实现接口
一个类只需要通过`implements`关键字声明和实现接口定义的API就能实现接口
### 扩展类
`extends`可以创建子类
### 重载
子类可以重载实例方法，setter和getter，返回类型和参数类型可以收窄
可以重载`noSuchMethod()`方法来相应访问不到属性或方法的情况
## 枚举
### 特征
* 不能显示实例化
* 不能继承，组合和实现
```dart
enum Color{ red,green,blue}

//每个枚举值都有一个index的getter,从0开始
assert(Coloe.red.index==0)
//获取所有枚举值的列表，使用枚举的values常量
List<Color> colors=Color.values;
```
## 混合
混合是一种实现代码重用的方法
使用关键字`with`实现混合
实现混合,没有构造器
## 类变量和方法
使用`static`可以实现类变量和方法
static变量会在他们被使用时才初始化
## 泛型
使用泛型的原因
* 类型安全
* 更通用的代码
* 可以减少代码重复

Dart的泛型是具体化的，也就是会在运行时携带类型信息
```dart
var names=List<String>();
names.add('Andy')
print(names is List<String)
```

可以使用`extends`关键字来限定泛型类型的类型。这种情况下，只能传递该类型和该类型的子类型作为类型参数

### 泛型函数
泛型函数中，类型参数可以用在返回值，参数列表，函数局部变量中
```dart
T swap<T>(List<T> ts){
    T temp=ts[0]
    ts[0]=ts[ts.length-1]
    ts[ts.length-1]=temp
}
```
### 集合直接量
集合直接量像普通直接量一样，只需要在尖括号中写入相应的类型即可，如列表写为`<type>`，映射表写为`<keyType,valueType>`
```dart
var names=<String>['Andy','Bob','Jack']
var counts=<String,int>{
    'a':3,
    'b'=1,
    'c'=2
}
```
## 库和可见性
`import`h和`library`可以创建模块和共享代码。库也是私有成员的单位，以下划线开始的标识符只在所在库可见。每一个App都是一个`library`
### 使用库
`import`可以将另一个库中的某一个命名空间引入到当前的作用域里，然后使用
```dart
//web通常需要使用html
import 'dart:html'
```
`import`唯一需要的一个参数就是库的URI,内建库有特定的`dart:`协议。其他的库可以使用文件系统目录或者`package`协议
### 指定库前缀
当两个库有命名冲突的时候，可以指定前缀来避免冲突
```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = new Element();

// Uses Element from lib2.
lib2.Element element2 = new lib2.Element();
```
### 部分导入
```dart
// 只导入foo
import 'package:lib1/lib1.dart' show foo;

// 导入除了foo以外的所有
import 'package:lib2/lib2.dart' hide foo;
```
### 懒加载
使用懒加载的情况
* 缩短应用的启动时间
* A/B测试
* 载入很少使用的功能

懒加载一个库，需要通过deferred as 的方式导入库,使用的时候需要调用库的`loadLibrary()`来加载库
```dart
//导入
import 'package:greetings/hello.dart' deferred as hello;

//使用
hello.loadLibrary()
```
虽然可以导入多次，但是实际上只需要一次导入就行

### 实现库
* 组织库源代码
* 使用`export`指令
* 使用`part`指令

## 异步支持
Dart库全部都是返回`Future`和`Stream`对象的函数，这些函数都是异步的。
### 处理Futures
当你需要一个完成的Future的结果的时候，通常有两种选择
* 使用`async`和`await`
* 使用Future API

`await`和`async`可以像写同步代码一样进行异步编程
使用`await`的地必须是在`async`函数里
```dart
Future checkVersion() async{
    var version =await lookUpVersion();
}
```
使用`try`，`cathc`，`finally`来处理`await`的错误和清理
```dart
try{
    version=await lookupVersion();
}catch(e){
    //错误情况
}
```
在`async`函数中，`await`可以使用多次
`await expression`中表达式的值通常是Future，如果不是，则会自动包装成Future，表示会返回一个对象。`await`表达式会在返回对象可用前中断执行

### 异步函数
用`async`修饰的函数，标记该函数返回Future，如果函数没有返回值，则返回`Future<Void>`
```dart
//普通函数
String lookUpVersion() => '1.0.0';
//异步函数
Future<String> lookUpVersion() async => '1.0.0';
```
## 处理流
从流中获取值，有两种选择
* `async`和异步循环`await for`
* 使用Stream API

异步循环的形式如下
```dart
await for (varOrType identifier in expression){
    //对值进行处理
}
```
该代码的执行顺序为
1. 等待流发送一个值
2. 执行循环体，循环体中可以使用发送的值
3. 重复1，2，直到流被关闭

可以使用`break`和`return`停止接收数据

## 生成器
惰性加载一序列的值，可以使用生成器。Dart内建支持两种类型的生成器
* 同步生成器，返回`Iterable`对象
* 异步生成器，返回`Stream`对象

实现同步生成器，需要把函数体标记为`sync*`，用`yield`传递数据
```dart
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
```
实现异步生成器，需要把函数体标记为`async*`，用`yield`传递数据
```dart
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while (k < n) yield k++;
}
```
如果函数是递归的，可以使用`yield*`来提高性能
```dart
Iterable<int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
```

### 可调用的类
一个类实现了`call()`方法就可以像普通函数一样调用

## 隔离(Isolates)
所有的Dart代码都运行在隔离器里面，有自己的堆内存，不会被其他任何隔离器访问到状态信息

## Typedefs
类型定义也称函数类型别名，可以给函数类型一个名字，方便在声明字段和返回值时使用。
```dart
typedef int Compare(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

// Initial, broken implementation.
int sort(Object a, Object b) => 0;

void main() {
  SortedCollection coll = new SortedCollection(sort);
  assert(coll.compare is Function);
  assert(coll.compare is Compare);
}
```
## 元数据
元数据可以为代码提供额外的信息，都是以`@`字符开始，后面接着一些编译期常量

创建
```dart
library todo;

class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
```
使用
```dart
import 'todo.dart';

@Todo('seth', 'make this do something')
void doSomething() {
  print('do something');
}
```
元数据可以出现在库，类，typedef，构造器，工厂构造器，函数，字段，参数列表，变量声明，`iport`和`export`指令之前，可以在运行时通过反射获取到元数据的信息

## 注释
* `//`单行注释
* `/* */`多行注释
* `///`,`/**`文档注释，里面可以使用中括号来引用类，方法，字段，顶层变量，函数
