# 字符串基本方法

## 1.字符串长度

```javascript
var str = "China!";
str.length; // 6
```

##2.字符串查询(charAt()、index Of()、lastIndexOf()、match()、search())

### 2.1charAt()

```javascript
var s = new String("abc");
s.charAt(0); // a
s.charAt(s.length - 1); // c

// 使用数组的下标语法
s.charAt(0); // a
s[0]; // a

// 如果参数为负数，或大于等于字符串的长度，charAt返回空字符串。
s.charAt(-1); // ""
s.charAt(10); // ""
```

### 2.2 indexof()、lastIndexOf()

```javascript
var str = 'Hello, world!';

str.indexOf('l');      // 2
str.indexOf('world!'); // 7
str.lastIndexOf('l')   // 10

var str = 'Hello, world!';

str.indexOf('l', 5); // 10
str.lastIndexOf('l', 5) // 3

//未找到返回-1
```

### 2.3 match()

```javascript
var str = "abc";

str.match("ab"); // ["ab"]
str.match("ac"); // null
//match 方法用于字符串查询，如果没有找到，则返回null，如果找到，返回一个数组。
```

### 2.4 search()

```javascript
var str = 'Hello, china!';

str.search('china'); // 7
str.search('world'); // -1
//search 方法的用法等同于 indexOf/lastIndexOf，但是其返回值为匹配到的第一个位置。如果没有找到匹配，则返回 -1。
```

### 2.5 正则表达式

```javascript
var website = "http://www.baidu.com";
// 查询头部
//  reg -> /^条件/
console.log(/^http/.test(website));

// 查询尾部
// reg -> /条件$/
console.log(/com$/.test(website));

// 查询是否包含
// reg -> /条件/
console.log(/baidu/.test(website));
```

## 3.字符串拼接(concat())

### 3.1concat

```javascript
var s1 = 'a', s2 = 'b';
s1.concat(s2); // "ab"

var s3 = 'c';
s1.concat(s2, s3); // "abc"

//常用 + 拼接
```

>如果参数不是字符串，**concat** 方法会将其先转为字符串，然后再连接。

## 4.字符串截取(slice()、subString()、substr())

### 4.1 slice()(常用)

```javascript
//slice 方法用于字符串截取，其语法形式为：slice(start, end)
'JavaScript'.slice(0, 4) // "Java"

'JavaScript'.slice(4) // "Script"

'JavaScript'.slice(-6) // "Script"
'JavaScript'.slice(0, -6) // "Java"
'JavaScript'.slice(-2, -1) // "p"

'JavaScript'.slice(2, 1) // ""
//如果第一个参数大于第二个参数，slice 方法返回一个空字符串。
```

### 4.2 subString()

```javascript
//substring 方法用于字符串截取，不改变原字符串。它与slice作用相同，使用方法类似，但有一些奇怪的规则，因此不建议使用这个方法，优先使用slice。其语法形式为：subString(start, end)

//它的第一个参数是开始位置，第二个参数是结束位置（不含该位置）。
'JavaScript'.substring(0, 4) // "Java"

'JavaScript'.substring(4) // "Script"

'JavaScript'.substring(10, 4) // "Script"
// 等同于
'JavaScript'.substring(4, 10) // "Script"
//如果第二个参数大于第一个参数，substring 方法会自动更换两个参数的位置。

'Javascript'.substring(-3) // "JavaScript"
'JavaScript'.substring(4, -3) // "Java"
//如果参数是负数，substring 方法会自动将负数转为0。
```

### 4.3 subStr()

```javascript
//substr 方法用于字符串截取，不改变原字符串。其语法形式为：subStr(start, end)

'JavaScript'.substr(4, 6) // "Script"
//它的第一个参数是开始位置，第二个参数是结束位置（不含该位置）。

'JavaScript'.substr(4) // "Script"
//如果省略第二个参数，则表示从指定位置开始截取到末尾。

'JavaScript'.substr(-6) // "Script"
'JavaScript'.substr(4, -1) // ""
//如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0，因此会返回空字符串。
```

## 5.字符串去空格(trim())

```javascript
'  Hello world!'.trim() // "Hello world!"
//trim 方法用于去除字符串两端的空格，返回一个新字符串，不改变原字符串。
```

## 6.字符串大小写转换(toLowerCase、toUpperCase)

toLowerCase** 方法用于将一个字符串全部转为小写，**toUpperCase** 则是全部转为大写。它们都返回一个新字符串，不改变原字符串。

```javascript
'Hello World'.toLowerCase();
// "hello world"

'Hello World'.toUpperCase();
// "HELLO WORLD"

String.prototype.toUpperCase.call(true)
// 'TRUE'
String.prototype.toUpperCase.call(['a', 'b', 'c'])
// 'A,B,C'
```

>String.prototype.toUpperCase.call(true)
>// 'TRUE'
>String.prototype.toUpperCase.call(['a', 'b', 'c'])
>// 'A,B,C'

## 7. 字符串比较(> 、<、==)

JavaScript允许使用 `>` 、`<` 或 `==` 运算比较字符串，返回一个布尔。

```javascript
var compare = (s1, s2) => {
	if (s1 > s2) {
		console.log(`${s1} > ${s2}`);
	}else if(s1 == s2) {
		console.log(`${s1} = ${s2}`);
	}else {
		console.log(`${s1} < ${s2}`);
	}
}

compare('a', 'b');   // "a < b"
compare('a', 'A');   // "a > A"
compare('ab', 'ac'); // "ab < ac"
compare('ab', 'ab'); // "ab = ab"
```

## 8.字符串替换(replace())

```javascript
var str = "Hello, world!";
str.replace("world", "china"); // "Hello, china!"
//replace 方法用于字符串替换，其语法形式为：replace(search, replacement)
```

## 9.将字符串切割为数组(split())

```javascript
var str = "HTML,CSS,JavaScript";
str.split(","); // ["HTML","CSS","JavaScript"]

//split 方法将一个字符串根据某个字符串切割为数组，其语法形式为：split(str)
```

