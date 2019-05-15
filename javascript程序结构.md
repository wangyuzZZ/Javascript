# 分支结构

## 1.条件语句(与Java类似)

### 1.1 if语句

```javascript
var year = 2019;
if((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
    console.log(year + '是闰年');
}
```

### 1.2 if-else

```javascript
if(condition) {
  // 代码块1
}else {
  // 代码块2
}
```

### 1.3 if-else if-else

```javascript
var score = 92;

if(score >= 90 && score <= 100) {
    console.log('优秀！');
}else if(score >= 70 && score < 90) {
    console.log('良好！');
}else if(score >= 60 && score < 70) {
    console.log('及格！');
}else if(score >= 0  && score < 60) {
    console.log('不及格！');
}else {
    console.log('成绩有误！');
}
// 注意：else 如果后面没有跟上if，则表示排除以上所有情况之外的情况，在这里当成绩小于0或成绩大于100时执行；
```

>- 在三种形式的if语句中，`if` 关键字之后均为表达式，该表达式通常是逻辑表达式或关系表达式，但也可以是其他表达式，如赋值表达式等，甚至也可以是一个变量。
>- 在 `if` 语句中，条件判断表达式必须用括号括起来，在语句之后必须加分号。
>- 嵌套使用 `if` 语句应该注意，`else` 总是与它前面最近的  `if` 配对。

## 2.switch语句

```javascript
switch (表达式) {
		case 常量表达式1: 语句1;break;
		case 常量表达式2: 语句2;break;
		case 常量表达式3: 语句3;break;
		...
		case 常量表达式n: 语句n;break;
		default: 语句n+1;
	}
```

>计算表达式的值，并逐个与其后的常量表达式值比较。当表达式的值与某个常量表达式的值相等时，即执行其后的语句，然后不再进行判断，继续执行后面所有case后的语句。如表达式的值与所有case的常量表达式均不相同时，则执行 `default` 后的语句。语句后的 `break` 用于跳出switch，执行switch后面的内容。

| if-else语句                                                  | switch语句                                                   |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| else不是必需的，可以只使用if语句；在多个if语句连续使用的时候，每一if都会被执行检测，即使已经找到了匹配（所以它的效率比switch语句要慢很多）； | 可以使用default语句来处理所有case之外的情况；如果找到了一个匹配，相应的代码会被执行，然后break语句会停止执行switch语句中的其他分支（比同样功能的连续多个if语句性能要好）； |

# 循环结构(与Java类似)

## 1.for

```javascript
for (初始化; 循环条件; 迭代增量) {
	循环体
}
```

## 2.while

```javascript
初始化语句
while(循环条件) {
  循环体
  迭代增量
}
```

## 3.do-while

```javascript
do {
	循环体
}while(循环条件)
```

# 流程控制

break or continue