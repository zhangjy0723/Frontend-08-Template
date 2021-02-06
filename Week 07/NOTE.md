学习笔记
# Expression
## Member
 - a.b  成员访问
 - a[b]   成员访问，支持运行时的字符串
 - foo`string` 会把反引号部分拆开，然后传入foo函数里
 - super.b   构造函数中使用
 - super['b']   构造函数中使用
 - new.target  前后一个字都不能替换，固定写法
 - new Foo()  

### new
- new Foo  优先级比 new Foo()低

Example:
new a()()
new new a()  和第二个new先结合

## Reference
- Object
- Key
- delete
- assign
> a.b访问的是一个属性的引用，而不是值

## Call 
- foo()
- super()
- foo()['b']
- foo().b
- foo()`abc`
最基础的用法是函数后面跟了一对圆括号 优先级比new低，同时低于前面所有的member运算，在后面加上成员访问，运算优先级也降低了

Example:
new a()['b']  a()先和new相结合  即 new出来一个a对象 然后访问它的b属性


Expressions
a.b = c √
a+b = c ×
只有left handside才能放到左边

## Update(left hand 几乎一定是right hand)
- a ++
- a--
- --a
- ++ a

Example:
++ a ++ （a优先和后面的++结合）
++ （a ++）

##  Unary (单目运算符)
- delete a.b 必须是引用类型才能生效
- void foo()
- typeof a
- +a  正号
- -a  负号
- ~ a  按位取反
- ! a  非运算
- await a 

## Exponental
- **  乘方
Example:
3 ** 2 ** 3  -> 3**(2**3)  
先算2 的3次方 

## Equality
- ==  (类型不同时优先把布尔类型转成number类型)
- !=
- ===
- !==

## Bitwise
- & ^ |

## Logical
- &&  前面如果是false 则不执行后面的部分
- ||  前面如果是true 则后面的就不被执行

## Conditional
- ? :


## Type Convertion
- a+b   
>   同类型 字符串+字符串 或者 数字加数字  
>   不同类型 数字+字符串->把数字转成字符串
- "false" == false  -> false 
> 类型相等直接比较，类型不等  全部转成数字再比较  
> “ ” == false -> true  
> 0 == false -> true  
  尽量使用三等号
- a[O] = 1 ??

## 几种特殊转换规则
- undefiend 
> 转number NaN  
> 转boolean false  
> 转string 'undefiend'

- null 
> 转number 0  
> 转boolean false 
> 转string 'null'


- Object
> 转number 调用valueOf  
> 转String 调用valueOf toString  
> 转boolean 均为true

- string
> 转Boolean 空字符串转成false  其他为true

- Boolean
> true -> 1  
> false -> 0  
> true -> 'true'  
> false -> 'false'

- Symbol
>无法转成其他任何变量


## unboxing(拆箱转换)

> 把Object转成普通的基本类型
- toPremitive
> 加法，如果遇到object+object或者object参与的情况，都会调用
- valueOf toString
> 加法优先调用valueOf，即使是字符串的相加  转Number也是先调用valueOf  
> 作为属性名，则优先调用toString()
- Symbol.toPremitive
>如果定义了该方法，就会忽略valueOf toString

- Example :
```
var o = {
  toString(){ return "2"},
  valueOf(){ return "1"},
  [Symbol.toPremitive]() {return 3}

}
var x = {}
x[o] = 1
console.log('x'+ o) //x1 如果注释掉valueOf 则为x2 如果都注释了 则为x[object object]??

```

## boxing 装箱转换
| 类型       | 对象                      | 值          |
|:----------|:----------               |:----------  |
| Number    | new Number(1)            | 1           |
| String    | new String("a")          | "a"         |
| Boolean   | new Boolean(1)           | true        |
| Symbol    | new Object(Symbol("a"))  | Symbol("a") |

> number类型和number类并不一样

# Statement

## Grammar
- 简单语句
- 复合语句
- 声明
> const class let 在声明之前访问就报错


## Runtime
- Compleion Record (执行结果记录)
> 基本类型、return break throw...
- Lexical Environment (作用域)


```
try{
}catch(){
}finally{
}
```
> 即使在try里面return，finally里的语句也会继续执行


## 预处理机制  
> 所有的声明都有预处理机制，都能把变量变成局部变量，const在声明前使用会报错，可以用try catch处理

```
var a=2;
void function(){
    a=1;
    return;
    var a;// 不管写哪里，都会被先挑出来声明到这个函数的作用级别
}()
console.log(a) //2
```
```
var a=2;
void function(){
    a=1;
    return;
    const a;
}()
console.log(a) //2
```

## 作用域
```
var a=2;
void function(){
    a=1;
    {
	 var a
	}
}()
console.log(a) //2

var a=2;
void function(){
    a=1;
    {
	 const a
	}
}()
console.log(a) //报错

```

>var的作用域是它所在的函数体  
>const的作用域是它所在的{}

## 宏任务和微任务
- 宏任务  
传给javascript引擎的任务，最大粒度的范围
- 微任务  
在javascript引擎内部的任务 由Promise来产生的，只有Promise会产生微任务

```
var x = 1;
var p = new Promise(resolev => resolve());
p.then(() => x=3);
x = 2;

//结果 两个异步任务
x = 1
p = ...
x = 2
x = 3


```

## 函数调用
- 执行上下文 EC
> 执行所需要的语句都保存在这里


## 闭包
> 每个函数都会生成闭包？？？？（是不是有问题）
```
var y = 2;
function foo2(){
  var z= 3;
  return () =>{ //可以同时访问到 y, z,this
   console.log(y,z);
  }
}
var foo3 = foo2();
export foo3



```

 

