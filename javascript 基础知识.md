# 1.定义变量

-var、let、const 

# 2.作用域

```javascript
var a = "全局变量";
function print() {
  // a 为全局变量，在任意位置都可以访问
  console.log(a);    
}

function test(y) {
  // 参数 y 也为局部变量
  // x 在函数内部创建，为一个局部变量
  var x = "局部变量"; 
}
console.log(x); // x 为局部变量，此处不能访问x变量，程序会报错
console.log(y); // y 为局部变量，此处不能访问y变量，程序会报错
```

# 3.运算符

 ## 1.基本运算符

 基本运算符主要用于一些数值操作

- `+`：加法运算符，如 `a + b`
- `-`：减法运算符，如 `a - b`
- `*`：乘法运算符，如 `a * b`
- `/`：除法运算符，如 `a / b`
- `%`：模运算（取余数），如 `a % b`
- `++`：自增运算符（自身+1）
- `--`：自减运算符（自身-1）

## 2.逻辑运算符

赋值运算符是为JavaScript中的变量赋值，即将该运算符右方计算出的值赋予左侧的变量。

- `=`：赋值运算符，如 `x = 10;` ，将 `10` 赋值给变量 `x`
- `+=`：变量与值相加，如 `x += y;` 相当于 `x = x + y`
- `-=`：变量与值相加，如 `x -= y;` 相当于 `x = x - y`
- `*=`：变量与值相加，如 `x *= y;` 相当于 `x = x * y`
- `/=`：变量与值相加，如 `x /= y;` 相当于 `x = x / y`
- `%=`：变量与值相加，如 `x %= y;` 相当于 `x = x % y`

## 3.关系运算符

关系运算符描述两个变量的关系，其返回值类型为布尔类型（boolean），即 `true` 和 `false`。

- `==`：判断两个变量是否相等，如 `'hello' == 'hello'`，返回 `true`
- `>`：判断等号左边的变量是否大于等号右边的变量，如 `20 > 10`，返回 `true`
- `<`：判断等号左边的变量是否小于等号右边的变量，如 `20 < 10` ，返回 `false`
- `>=`：判断等号左边的变量是否大于等于等号右边的变量，如 `20 >= 10`，返回 `true`
- `<=`：判断等号左边的变量是否小于等于等号右边的变量，如 `20 <= 10`，返回 `false`
- `===`：恒等于，要求不仅数据类型要一致，值也要一致，如 `1 === '1'`，返回 `false`
- `!==`：不恒等于，只要类型或值不一样，结果为true，如 `1 !== '1'`，返回 `true`

## 4.逻辑运算符

逻辑运算符是JavaScript用于判断几条语句成立情况的一种运算，该运算符的返回值类型为布尔类型。

- 逻辑与：`&&` ，同时为真才为真，如 `(1 > 2) && (2 > 3)`，返回 `false`
- 逻辑或：`||` ，同时为假才为假，如 `(1 > 2) || (2 > 1)`，返回 `true`
- 逻辑非：` !` ，取反，如 `!(1 > 2)`，返回 `true`

## 5.三元运算符

三元运算用于条件判断，根据判断的结果执行不同的语句，其语法形式为：`a ? b : c`。如果a表达式的条件为真，则执行b语句，否则执行c语句。示例：

```javascript
var isLogin = true; // 定义变量’isLogin‘用于记录登录状态
isLogin ? console.log('已登录！') : console.log('未登录！');
```

## 6.优先级

| 运算符                             | 说明                                                   |
| ---------------------------------- | ------------------------------------------------------ |
| .[ ] ( )                           | 字段访问、数组索引、函数调用和表达式分组               |
| ++ -- - ~ ! delete new typeof void | 一元运算符、返回数据类型、对象创建、未定义的值         |
| * / %                              | 相乘、相除、求余数                                     |
| + - +                              | 相加、相减、字符串串联                                 |
| << >> >>>                          | 移位                                                   |
| < <= > >= instanceof               | 小于、小于或等于、大于、大于或等于、是否为特定类的实例 |
| == != === !==                      | 相等、不相等、全等，不全等                             |
| &                                  | 按位“与”                                               |
| ^                                  | 按位“异或”                                             |
| \|                                 | 按位“或”                                               |
| &&                                 | 逻辑“与”                                               |
| \|\|                               | 逻辑“或”                                               |
| ?:                                 | 条件运算                                               |
| = *OP*=                            | 赋值、赋值运算（如 += 和 &=）                          |
| ,                                  | 多个计算                                               |

圆括号用于改变由运算符优先级确定的计算顺序。  这就是说，先计算完圆括号内的表达式，然后再将它的值用于表达式的其余部分。

# 4.基本数据类型(与JAVA类似)

## 1.数值型(number)

阿拉伯数字

##2.字符串类型(string)

该类型用于表示如“英文”，“中文”，“其它国家语言”，“键盘上的符号”，“特殊编码”等字符，甚至可以是数字。该类型的值都需要用一对英文引号（可以是单引号，也可以是双引号）阔起来，否则在使用该变量的时候会报出未定义的错误，成为一个“未定义”类型，而本想作为字符串的数字也会成为一个“数值型”。

## 3.布尔类型(boolean)

true or false

## 4.对象类型(object)

该类型用于表示一个对象，在JavaScript中并没有“数组”这个类型，所以数组在JavaScript里也作为一个对象，空值`null`也是一个对象。

```javascript
var a = new Object();    // 对象
var b = [1, 2, 3, 4, 5]; // 数组对象
var d = {
	name: "小明",
	gender: "male",
	e_mail: "Wangyu_9805@163.com",
	age: "24",
  github:"https://github.com/wangyuzZZ/Blogs"
}
var e = {
	stu1: {name:"Q", age:"23", grade="A"},
	stu2: {name:"K", age:"22", grade="B"},
	stu3: {name:"J", age:"23", grade="A+"},
}
```

## 5.函数类型(function)

```javascript
// 定义函数
function sum(a, b) {
    return a + b;
}
// 调用函数
var result = sum(10, 20);
console.log(result); // 30
```

函数类型是JavaScript中最复杂的一个数据类型，但它在JavaScript中扮演中相当重要的作用，它也同是**面向对象编程**中一个非常核心的内容。

## 6.未定义(undefined)

变量不存在或未定义值时产生的类型。

# 类型转换

JavaScript 与 Java相比在变量定义方面比较宽松 变量类型没有很严格的限制，可以随时赋予任意值

```javascript
var x = y ? 3.14 : "china"
```

## 1.强制转换(number、string()、boolean())

###1.1 Number()

转换成数值

![1557912486393](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912486393.png)

![1557912510912](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912510912.png)

![1557912523068](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912523068.png)

### 1.2String()

![1557912629968](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912629968.png)

![1557912661631](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912661631.png)

### 1.3Boolean()

![1557912698282](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912698282.png)

![1557912715773](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1557912715773.png)

