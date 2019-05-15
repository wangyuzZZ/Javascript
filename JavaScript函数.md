# 函数定义(funcition)

```javascript
function function_name(arguments) {
	// body...
}
```

# 函数调用

函数定义以后，并不会立即执行（自调函数除外，自调函数一旦创建，程序执行之后自调函数也会自动执行）

```javascript
funciton sayHi(){
    console.log('1')
}
sayHi();
```

# 函数参数

##1.参数声明

函数参数无需指定类型，它的类型是在调用函数时，根据传递的参数值的类型所确定的，并且，函数参数无需使用`var`或 `let` 关键字声明，函数允许有多个参数。

```javascript
// 1、定义函数
function sayHelloWith(name) {
	console.log(`Hello, ${name}!`);
}

function sumWith(a, b) {
	console.log(a + b);
}

// 2、调用函数
sayHelloWith('Petter'); // "Hello, Petter!"
sumWith(10, 10);     // 20
sumWith("ab", "cd"); // "abcd"
```

## 2.参数作用域

在之前讲变量时我们已经提到变量的作用域，所谓“**作用域** “，就是变量起作用的范围，全局变量的作用域为全局，而局部变量的作用域限定在某个范围。函数参数为局部变量，其起作用的范围只限于函数内部，外界不能访问。

```javascript
function test() {
	var x = 10;
}
console.log(x);
// Uncaught ReferenceError: x is not defined(…)
```

##3、形参与实参

函数参数分为”**形参** “与”**实参** “，所谓形参，就是指形式参数，它并无确定的值；所谓实参，就是指实际参数，它有确定的值。定义函数时，圆括号内的参数为形参，调用函数时，圆括号内的参数为实参，具有确定的值。

```javascript
var x = 0;
function test(n) {
	n++;
}
test(x)
console.log(x); // 0
```

## 4.为参数设置默认值

为参数设置默认值可通过 三元运算符（`?:`）或者 或运算符（`||`）。

```javascript
function print(str, num) {
    num = num == undefined ? 18 : num;
    str = str || "Hello, world!";
    console.log(str);
}

print(); // "Hello, world!"
print('What are you doing?'); // "What are you doing?"
```

>值得注意的是，或运算符只对非数字对象有效，如果参数为数值类型，则使用三元运算符，因为如果传递的数字为0，根据自动类型转换，0被转换为false，因此也会认为该参数没有值。

## 5.对为参数(与Java类似)

函数参数的配置和参数的设置需要一一对位，即配置参数的顺序和函数定义参数时的顺序一致。根据这个要求参数的配置又可以分为另外几种特殊（异常）情况。

- 为函数预设了多余的参数
- 配置的参数少于预置的参数
- 配置的参数多于预置的参数
- 配置的参数与预置的参数没有对位

```javascript
// 1、为函数预设了多余的参数
function fnc_1(a, b, c) {
	return a;
} 
fnc_1(10); // 10

// 2、配置的参数少于预置的参数
function func_2(a, b, c) {
	return a + b + c;
} 
func_2(10, 5) // NaN

// 3、配置的参数多于预置的参数
function func_3(a, b, c) {
	return a + b + c;
} 
func_3(1, 2, 3, 4, 5) // 6

// 4、配置的参数与预置的参数没有对位
function func_4(a, b, c) {
	return b;
} 
func_4(1) // undefined



function fnc_4(a, b) {
	return b;
} 
func_4(1, 2);            // 2
func_4(undefined, 2);    // 2
func_4("可以是任意值", 2); // 2
func_4( , 2);            // 程序报错
```

## 6.对象传参

```javascript
function userInfo(obj) {
	console.log(`
		姓名：${obj.name}
		性别：${obj.sex}
		年龄：${obj.age}
		地址：${obj.address}
		`)
}

userInfo({
	name: '小明',
	sex: '男',
	age: 25,
	address: '四川省成都市'
});

// 姓名：小明
// 性别：男
// 年龄：25
// 地址：四川省成都市


function userInfo(obj) {
	obj.name    = obj.name    == undefined ? `名字只是一个代号`         : obj.name;
	obj.sex     = obj.sex     == undefined ? `你猜`                   : obj.sex;
	obj.age     = obj.age     == undefined ? `身高不是问题，年龄不是距离` : obj.age;
	obj.address = obj.address == undefined ? `地球`                   : obj.address; 

	console.log(`
		姓名：${obj.name}
		性别：${obj.sex}
		年龄：${obj.age}
		地址：${obj.address}
		`);
}是问题，年龄不是距离
// 地址：地球


function sum(a, b, c) {    return a + b + c;}sum.length; // 3function sum(a, b, c) {    return a + b + c;}sum(1, 2, 3)sum.length; // 3function sum(a, b, c) {    return a + b + c;}sum(1, 2, 3, 4, 5)sum.length; // 3function sum(a, b, c) {    return a + b + c;}sum(1, 2)sum.length; // 3
```

## 7.arguments对象

在某些特定的情况下，我们根本不知道函数在调用的时候到底需要配置几个参数，比如你要设置一个求和的函数，可能你需要求两个数的和，那就需要两个参数，如果需要求五个数的和，就需要五个参数。为了应对这种情况，JavaScript对函数提供了一个“**arguments** ”对象来应对以上情况。

我们首先要对“arguments”这个对象进行一个基本概念的了解。“arguments”对象只能出现在函数内部，在“全局空间”里该对象是无效的。该对象包含了函数运行时的所有参数，arguments[0]就是第一个参数，arguments[1]就是第二个参数，以此类推。

```javascript
function test(param) {
	console.log(arguments);
}

test(1, 2); // [1, 2]
test('a', 'b', 'c'); // ["a", "b", "c"]


//arguments 会忽视函数定义时参数定义的个数，以实际调用时配置的参数为准，也就是说函数的括号内哪怕没有预置参数也是可以的。我们通过arguments对象的“length”属性（之前的length属性是对函数名使用的）来再次证明这一点。


function test() {
	retutn arguments.length;
}
test({name:"Petter"}); // 1
test(1, 2);            // 2
test("a", "b", "c");   // 3


function sum(val) {
	var sum = 0;
	for(let idx = 0; idx < arguments.length; idx++) {
		sum += arguments[idx];
	}
	return sum;
}
console.log(sum(1, 2));    // 3
console.log(sum(1, 2, 3)); // 6
```

arguments 是一个类似数组 在调用数组方法的时候需要将其转换成数组 	Array.prototype.slice.call(arguments);

```javascript
function average(val) {
	console.log(arguments)
	let sum = 0;
	arguments = Array.prototype.slice.call(arguments);
	arguments.forEach(function(num) {
		sum += num;
	});
	return sum / arguments.length;
}

console.log(average(1, 2, 3)); // 2
console.log(average(6, 6));    // 6
```

## 8.值传递与地址传递

参数传递分为“**值传递**” 与 “**地址传递**”，所谓值传递，就是调用函数时，形参是对实参的拷贝，即将实参值拷贝一份赋给了形参，因此我们不能在函数内部通过形参修改原始值。而地址传递，传递的是地址，在计算机内存中，地址是唯一的，在函数内部我们可以通过该地址修改原始值。

在JavaScript中，如果参数为“**包装对象**”，即为值传递，如果参数为“**内置对象**”，即为地址传。判断是否为内置对象或包装对象的方法是，使用 `Object()` 方法之后是否还全等于自身。接下来我们看一组示例：

```javascript
var a = 10;
var b = {name: "Henrry Lee"};

console.log(Object(a) === a); // false 包装对象
console.log(Object(b) === b); // true  内置对象

function test1(argument) {
	argument = 20;
}
function test2(argument) {
	argument.name = `Petter`;
}

// 值传递
test1(a); 
console.log(a); // 10

// 参数传递
test2(b);
console.log(b.name);  // "Petter"
```

>注意：尽管 **地址传递** 传递的是变量的地址，我们可以通过该地址修改原始值，但是我们不能改变原始变量的指向，即我们不能企图重新为变量赋值。如下所示：
>
>```javascript
>var b = {name: `Henrry Lee`};
>function test(argument) {
>	argument = 10;
>}
>console.log(b); // {name: `Henrry Lee`}
>```

# 函数返回值

```javascript
function getSkill() {
	return '佛山无影脚';
}
getSkill(); // "佛山无影脚"
```

return**关键字，除了能够返回值以外，另外一个作用便是终止函数，**return关键字后的代码不会执行。

```javascript
function getSkill() {
	return '佛山无影脚';
    console.log("Hello, world!"); // 该语句不会被执行
}
getSkill(); // "佛山无影脚"
```

  **return**关键字后可以是变量也可以是表达式，甚至可以是数组或对象，只要符合JavaScript六种基本数据类型，都可以返回。

```javascript
// 1、返回值为变量
function func_1() {
	var a = 10;
	return a;
}
// 2、返回值为表达式
function func_2() {
	var a = 10, b = 10;
	return a + b;
}
// 3、返回值为数组
function func_3() {
	return [1, 2, 3];
}
// 4、返回值为对象
function func_4() {
	return {name:"Petter", age:23}
}
// 5、返回值为布尔类型的值
function func_5() {
	return true;
}
```

  函数返回值只能是一个，不能有多个返回值，否则程序报错，如果要返回多个值，可以用数组或对象。

```javascript
// 以数组形式返回
function minAndMaxNumInArr(arr) {
	var min = arr[0];
	var max = arr[0];
	for(var i = 0; i < arr.length; i++) {
		max = arr[i] > max ? arr[i] : max;
		min = arr[i] < min ? arr[i] : min;
	}
	return [min, max];
}

// 以对象形式返回
function minAndMaxNumInArr(arr) {
	var min = arr[0];
	var max = arr[0];
	for(var i = 0; i < arr.length; i++) {
		max = arr[i] > max ? arr[i] : max;
		min = arr[i] < min ? arr[i] : min;
	}
	return {minNum:min, maxNum:max};
}
```

## 函数名提升

JavaScript引擎将函数名视同变量名，所以采用**function**命令声明函数时，整个函数会像变量声明一样，被提升到代码头部。所以，下面的代码不会报错。

```javascript
sayHello();
// "Hello, world!"
function sayHello() {
	console.log("Hello, world!");
}
```

上述代码中，函数的调用在函数定义之前，但是由于变量提升，函数**sayHello**被提升到了代码头部，也就是在调用之前已经声明了。但是，如果采用赋值语句定义函数，JavaScript就会报错。

```javascript
f();
var f = function (){};
// TypeError: undefined is not a function

var f;
f();
f = function () {};
```

上面代码第二行，调用*f*的时候，*f*只是被声明了，还没有被赋值，等于*undefined*，所以会报错。因此，如果同时采用`function`命令和赋值语句声明同一个函数，最后总是采用赋值语句的定义。

```javascript
var f = function() {
  console.log('1');
}

function f() {
  console.log('2');
}

f() // 1
```

如果函数名重复，则后定义的函数会覆盖之前定义的函数。

```javascript
function sayHello() {
	console.log("Hello, world!");
}
function sayHello() {
	console.log("Hello, China!");
}

sayHello();
// "Hello, China!"
```

# 函数类型

## 1.变量函数

```javascript
var function_name = function(argument) {
	// body...
}
```

- **1、**这样声明的函数，需要先声明后调用;
- **2、**表达式内部的 **function** 无需再设置函数名，如果这样写，function后方的函数名只能被函数内部调用，在外部是无法使用的;

  除了上述需要注意的两点外，这种方式声明的函数和利用funciton关键字定义的函数并没有什么区别。

## 2.自调用函数

```javascript
(function() {
	console.log("Hello, world!");
})();
// "Hello, world!"

(function(a, b) {
	return a + b;
})(1, 2);
// 3



//这种函数的声明方式和其它函数的声明方式一样，它仍然有自己的独立作用域。自调用函数还有一个特点就是，它的运行虽然还是在程序的独立线程完成的，但是却可以达到程序在主线程完成的效果。
```

## 3.闭包函数(难点)

```JavaScript
var str = "Hello, world!";
function test() {
	console.log(str);
}
test()//str

//函数sayHi 方法可以读取全局变量str。但是，在函数外部无法读取函数内部声明的变量。

function test() {
	var str = "Hello, world!";
}
test()
console.log(str);
// Uncaught ReferenceError: str is not defined


function func_1() {
	var str = "Hello, world!";
	function func_2() {
		console.log(str);
		// "Hello, world!"
	}
    func_2();
}
func_1();

//，函数 func_2 定义在函数 func_1 内部，这时 func_1 内部的所有局部变量，对 func_2 都是可见的。但是反过来就不行，func_2 内部的局部变量，对 func_1 是不可见的。这就是JavaScript语言特有的”链式作用域”结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。既然 func_2 可以读取 func_1 的局部变量，那么只要把 func_2 作为返回值，我们就可以在 func_1 外部读取它的内部变量了。

function func_1() {
	var str = "Hello, world!";
	function func_2() {
		console.log(str);
	}
	return func_2;
}
func_1()(); // "Hello, world!"

//函数 func_1 的返回值就是函数 func_2，由于 func_2 可以读取 func_1 的内部变量，所以就可以在外部获得 func_1 的内部变量了。
```

func\_2 函数就是闭包 ，即能够读取其他函数内部变量的函数。由于在JavaScript语言中，只有函数内部的子函数才能读取内部变量，因此可以把闭包简单理解成 “**定义在一个函数内部的函数即为闭包**”。闭包最大的特点，就是它可以“记住”诞生的环境，比如 func\_2 记住了它诞生的环境 func\_1，所以从 func\_2 可以得到 func\_1 的内部变量。在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的最大用处有两个，一个是**可以读取函数内部的变量**，另一个就是**让这些变量始终保持在内存中**，即闭包可以使得它诞生环境一直存在。请看下面的例子，闭包使得内部变量记住上一次调用时的运算结果。

```javascript
function createIncrementor(val) {
	return function () {
		return val++;
	};
}
var inc = createIncrementor(5);
inc() // 5
inc() // 6
inc() // 7
inc() // 8
```

val`是函数**createIncrementor**的内部变量。通过闭包，`val` 的状态被保留了，每一次调用都是在上一次调用的基础上进行计算。从中可以看到，闭包 **inc** 使得函数 **createIncrementor** 的内部环境一直存在。所以，闭包可以看作是函数内部作用域的一个接口。

 **inc** 始终在内存中，而 **inc** 的存在依赖于 **createIncrementor**，因此也始终在内存中，不会在调用结束后，被垃圾回收机制回收。

闭包的另一个用处，是封装对象的私有属性和私有方法。

```javascript
function Person(name, sex, age) {
	var _id = 0;
	this.setId = function(val) {
		_id = val;
	}
	this.getId = function() {
		return _id;
	}
}


//由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。如将当前变量的值设置为“null”，将变量的引用解除，当垃圾回收启动时，会自动对这些值为“null”的变量回收。将上面的闭包示例稍微修改一下来减少对内存的消耗：
function createIncrementor(start) {
	return function () {
		return start++;
	};
}
var inc = createIncrementor(5);
createIncrementor = null;
```

## 4.构造函数

```javascript
// 创建函数模板
function Person(name, sex, age) {
	this.name = name;
	this.sex  = sex;
	this.age  = age;

	this.skill = function() {
		return `动感光波`;
	}
}

// 实例化函数对象
let per = new Person('小明', '男', 25);
console.log(`
	姓名：${per.name}
	性别：${per.sex}
	年龄：${per.age}
	技能：${per.skill()}
	`);

//用构造函数实例化对象
// 创建对象模型
function Person(name, age, profession, address) {
	this.name       = name;
	this.age        = age;
	this.profession = profession;
	this.address    = address;
}
// 实例化对象
var person1 = new Person("张三", 24, "Web前端工程师", "四川省成都市");
var person2 = new Person("李四", 30, "iOS工程师", "重庆市");
var person3 = new Person("王五", 28, "Java工程师", "广东省深圳市");

//用字面量创建对象
var person1 = {
	name:"张三",
	age:24,
	profession:"Web前端工程师",
	address:"四川省成都市"
}
var person2 = {
	name:"李四",
	age:30,
	profession:"iOS工程师",
	address:"重庆市"
}
var person3 = {
	name:"王五",
	age:28,
	profession:"Java工程师",
	address:"广东省深圳市"
}
```

## 5.递归函数

JavaScript和其它编程技术一样，拥有一种函数在执行的时候调用自身的实现，这种实现在编程技术中叫做**“递归”**，通过递归可以同更少的代码完成很多需要大量代码，甚至是不确定代码所能完成的事。我们先在看一个简单的“递归”实现的例子：

```javascript
function count(n) {
	console.log(n--);

	if (n > 0) {
		count(n);
	}
}

count(5); 

// 5
// 4
// 3
// 2
// 1


// 5! -> 5 * 4 * 3 * 2 * 1
function factorial(n) {
	if (n == 0 || n == 1) {
		return 1;
	}else {
		return n * factorial(n - 1);
	}
}
factorial(5);  // 120
```

#  尾调用

## 1、尾调用概念

  尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，一句话就能说清楚，就是指某个函数的最后一步是调用另一个函数，注意是最后一步。

```javascript
function f(x){
	return g(x);
}
```

  上面代码中，函数 **f** 的最后一步是调用函数 **g**，这就叫尾调用。以下三种情况，都不属于尾调用。

```javascript
// 情况一
function f(x) {
	var y = g(x);
	return y;
}

// 情况二
function f(x){
	return g(x) + 1;
}

// 情况三
function f(x){
	g(x);
}
```

  上面代码中，情况一是调用函数g之后，还有赋值操作，所以不属于尾调用，即使语义完全一样。情况二也属于调用后还有操作，即使写在一行内。情况三等同于下面的代码。

```javascript
function f(x){
	g(x);
	return undefined;
}
```

  尾调用不一定出现在函数尾部，只要是最后一步操作即可。

```javascript
function f(x) {
	if (x > 0) {
		return m(x);
	}
	return n(x);
}
```

  上面代码中，函数m和n都属于尾调用，因为它们都是函数f的最后一步操作。

## 2、尾调用优化

  尾调用之所以与其他调用不同，就在于它特殊的调用位置。我们知道，函数调用会在内存形成一个“调用记录”，又称“调用帧”（call frame），保存调用位置和内部变量等信息。如果在函数A的内部调用函数B，那么在A的调用帧上方，还会形成一个B的调用帧。等到B运行结束，将结果返回到A，B的调用帧才会消失。如果函数B内部还调用函数C，那就还有一个C的调用帧，以此类推。所有的调用帧，就形成一个“调用栈”（call stack）。

  尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用帧，因为调用位置、内部变量等信息都不会再用到了，只要直接用内层函数的调用帧，取代外层函数的调用帧就可以了。

```javascript
function f() {
	var m = 1;
	var n = 2;
	return g(m + n);
}
f();

// 等同于
function f() {
	return g(3);
}
f();

// 等同于
g(3);
```

  上面代码中，如果函数g不是尾调用，函数f就需要保存内部变量m和n的值、g的调用位置等信息。但由于调用g之后，函数f就结束了，所以执行到最后一步，完全可以删除 f(x) 的调用帧，只保留 g(3) 的调用帧。

  这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。

  注意，只有不再用到外层函数的内部变量，内层函数的调用帧才会取代外层函数的调用帧，否则就无法进行“尾调用优化”。

```javascript
function addOne(a){
	var one = 1;
	function inner(b){
		return b + one;
	}
	return inner(a);
}
```

  上面的函数不会进行尾调用优化，因为内层函数`inner`用到了外层函数`addOne`的内部变量`one`。