# 数组基本方法

## 1. 数组判断

```javascript
Array.isArray([]); // true
Array.isArray(''); // false
Array.isArray({}); // false
Array.isArray(function(){}); // false

//判断某个对象是否是一个数组使用 Array.isArray() 方法，如果是，则返回true，否则返回false。
```

## 2.添加元素(push()、unshift()、apply()、concat()、arr[idx])

添加数组元素的方法比较多，主要有以下种：

- `push()`：在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度*（ 改变原数组）*。
- `unshift()`：在数组的开始位置添加一个或多个元素，并返回添加新元素后的数组长度*（ 改变原数组）*。
- `apply()`：合并数组（只能合并两个）*（ 改变原数组）*
- `concat()`：合并数组（允许合并多个数组） *（ 不改变原数组）*
- `arr[idx]`：下标法添加数组元素

```javascript
// 1、首尾添加数组元素
var arr = [];
arr.push(1); // [1]
arr.unshift(0); // [0, 1]

// 2、下标法添加数组元素(高效，建议使用)
var arr = [1];
arr[arr.length] = 2; // [1, 2]
arr[0] = 0;  // [0, 1, 2]

// 3、合并数组
var arr1 = [1, 2],
    arr2 = [3, 4];
var aLeng = Array.prototype.push.apply(arr1, arr2);
// aLeng = 4, arr1 = [1, 2, 3, 4]

// 4、合并数组
var arr1 = [1, 2],
    arr2 = [3, 4],
    newArr = [].concat(arr1, arr2);
console.log(newArr); // [1, 2, 3, 4]
```

## 3.删除元素(pop()、shift()、splice())

删除数组元素的方法如下：

- `pop()`：删除数组最后一个元素*（ 改变原数组）*。
- `shift()`：删除数组第一个元素*（ 改变原数组）*。
- `splice()`：范围删除*（ 改变原数组）*。

```javascript
var arr = [1, 2, 3, 4];
arr.pop();   // [1, 2, 3]
arr.shift(); // [2, 3]


var arr = [1, 2, 3, 4, 5];
arr.splice(1, 2); // 删除元素：2，3
console.log(arr); // [1, 4, 5]

//删除数组元素中 splice 方法最为灵活，不仅可以范围删除数组元素，还可以实现数组元素的插入和替换。该方法语法形式为：
arr.splice(1, 1, 'HTML', 'JavaScript'); // 删除元素：4，并追加'HTML', 'JavaScript'
console.log(arr); // [1, "HTML", "JavaScript", 5]

//该方法中的第一个参数是删除的起始位置，第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素。

//另外，该方法的第一个参数可以为负数（但是第二个不能，因为它表示长度），表示从数组末端开始计数，开始计数的值为“-1”。
var arr = [1, 2, 3, 4, 5];

arr.splice(-3, 2); // 删除元素：3，4
console.log(arr);  // [1, 2, 5] 
```

## 4.截取元素(slice())

```javascript
arr.slice(startIdx, endIdx);
//截取数组元素与字符串截取类似，使用 slice 方法，该方法语法形式如下：

var arr = [1, 2, 3, 4, 5, 6];
arr.slice(0, 3);  // [1, 2, 3]
arr.slice(3, -1); // [4, 5]
arr.slice(3); // [4, 5, 6]
arr.slice(3, 1); // []
```

>Array.prototype.slice.call(obj);

## 5.数组排序(sort())

```javascript
var nums = [1, 8, 13, 30]; 

// 1、升序
var ascending = nums.sort(function(a1, a2) {
	return a1 - a2;
});
console.log(ascending); // [1, 8, 13, 30]


// 2、降序
var descending = nums.sort(function(a1, a2) {
	return a2 - a1;
})
console.log(descending); // [30, 13, 8, 1]
//冒泡排序
var nums = [1, 8, 13, 30]; 
for(let j = 0;j < nums.length - 1;j++){
    for(let i = 0;i < nums.length - 1 - j;i++){
        if(nums[i] > nums[i+1]){
            let temp = nums[i];
            nums[i] = nums[i+1];
            nums[i+1] = temp;
        }
    }
}
```

## 6.数组倒序(reverse())

```javascript
//reverse()  方法的作用是将已有数组倒序排列，并返回改变后的数组。该方法同样会改变原数组。
var nums = [1, 2, 3, 4]
nums.reverse();
console.log(nums); // [4, 3, 2, 1]
```

## 7.操作元素(map())

```javascript
var nums = [1, 2, 3, 4];

/*
var newArr = nums.map(function(num){
	return num * 2;
});
*/

//map方法对数组的所有成员依次调用一个函数，根据函数结果返回一个新数组。该方法不会改变原来的数组。


var nums = [1, 2, 3];
nums.map((num, idx, arr) => {
	console.log(`idx = ${idx}, num = ${num}, arr = ${arr}`);
});

// idx = 0, num = 1, arr = 1,2,3
// idx = 1, num = 2, arr = 1,2,3
// idx = 2, num = 3, arr = 1,2,3


var arr = [1, , "", undefined, null, , 'China'];
console.log(arr.length);

let count = 0; // 7
arr.forEach((val) => {
	count++;
});
console.log(count); // 5
```

## 8.数组遍历(for、for-in、forEach())

```javascript
//- for 循环遍历数组元素
//- for-in 循环遍历数组元素
//- forEach() 方法遍历数组元素


var arr = ["HTML", "CSS", "JavaScript"]

// 1、for 循环遍历
for(let idx = 0; idx < arr.length; idx++) {
  console.log(arr[idx]);
}

// 2、for-in 遍历
for (let idx in arr) {
  console.log(arr[idx]);
}

// 3、forEach() 遍历
arr.forEach(function (item, curIdx, arr) {
    console.log(item);
});

// HTML
// CSS
// JavaScript
```

##9.过滤(filter())

```javascript
// 示例1：过滤偶数
var arr = [1, 2, 3, 4, 5, 6],
    filArr = arr.filter(function (num) {
        return num % 2 == 0;
    });
console.log(filArr); // [2, 4, 6]

// 和之前的map和forEach方法一样，该方法的函数仍旧支持3个参数，参数位和之前的这两个方法也是一样的，分别表示：数组元素、元素下标和原数组。
```

## 10.查询数组元素(indexOf()、lastIndexOf()、includes()、find()、findIndex())

- indexOf()`  方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回**-1**。
- `lastIndexOf()`  方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1。
- `includes()` 方法用来判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回false。
- `find()` 方法返回数组中满足提供的测试函数的第一个元素的值。否则返回 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)。
- `findIndex` 方法返回数组中满足提供的测试函数的第一个元素的**索引**。否则返回-1。

```javascript
var arr = [1, 2, 3, 2, 5];

arr.indexOf(2);     // 1
arr.lastIndexOf(2); // 3
arr.includes(3); // true

var res = arr.find(function(item) {
    return item > 2
});
console.log(res); // 3

var index = arr.findIndex(function(item) {
    return item == 3;
});
console.log(index);
```

## 11.数组元素累加

```javascript
array.reduce(callbackfn[, initialValue])
```
对数组中的所有元素调用指定的回调函数。该回调函数的返回值为累积结果，并且此返回值在下一次调用该回调函数时作为参数提供。

| 参数         | 定义                                                         |
| ------------ | ------------------------------------------------------------ |
| array        | 必需。一个数组对象。                                         |
| callbackfn   | 必需。一个接受最多四个参数的函数。对于数组中的每个元素，**reduce** 方法都会调用 *callbackfn* 函数一次。 |
| initialValue | 可选。如果指定 *initialValue*，则它将用作初始值来启动累积。第一次调用 *callbackfn* 函数会将此值作为参数而非数组值提供。 |

>1、如果提供了 *initialValue*，则 **reduce** 方法会对数组中的每个元素调用一次 *callbackfn* 函数（按升序索引顺序）。如果未提供 *initialValue*，则 **reduce** 方法会对从第二个元素开始的每个元素调用 *callbackfn* 函数。
>
>2、回调函数的返回值在下一次调用回调函数时作为 *previousValue* 参数提供。最后一次调用回调函数获得的返回值为 **reduce** 方法的返回值。
>
>3、不为数组中缺少的元素调用该回调函数。

## 12.数组去重

```javascript
//创建新数组接受旧数组
// 1. 
var nums   = [1, 2, 3, 1, 3, 4, 5, 4];
var tmpArr = [];
for(var i = 0; i < nums.length; i++) {
    var index = tmpArr.indexOf(nums[i]);
    if(index == -1) {
        tmpArr.push(nums[i]);
    }
}
console.log(tmpArr);

// 2.
var nums   = [1, 2, 3, 1, 3, 4, 5, 4];
var resArr = [...new Set(nums)];
console.log(resArr);

// 3. 
var nums   = [1, 2, 13, 1, 13, 4, 5, 4];
var tmpArr = [];
var resArr = [];
for(var i = 0; i < nums.length; i++) {
    if(tmpArr[nums[i]] != 1) {
        resArr.push(nums[i]);
    }
    tmpArr[nums[i]] = 1; 
}
console.log(tmpArr);
console.log(resArr);

// 4. 
Array.prototype.removeDuplicate = function () {
    var json = {};
    var arr  = [];
    for(var i = 0, len = this.length; i < len; i++) {
        if(!json[this[i]]) {
            json[this[i]] = true;
            arr.push(this[i]);
        }
    }
    return arr;
}
var result = [1, 2, 3, 3, 4, 5].removeDuplicate();
console.log(result); // [1, 2, 3, 4, 5]
```

## 13.reduce详解

### 为什么用

逼格高...

### 怎么用

```javascript
/**
 *  1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
    2、currentValue （数组中当前被处理的元素）
    3、index （当前元素在数组中的索引）
    4、array （调用 reduce 的数组）
    5、initialValue （作为第一次调用 callback 的第一个参数。）
 */
arr.reduce((previousValue,currentValue,index,array) =>{
    
},initialValue)
//例（不添加initialValue的情况）
var arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
})
console.log(arr, sum);
//打印结果
//1 2 1
//3 3 2
//6 4 3
//[1, 2, 3, 4] 10
//这里可以看出，上面的例子index是从1开始的，第一次的prev的值是数组的第一个值。数组长度是4，但是reduce函数循环3次。
//例（添加initialValue的情况）
var  arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
}，0) //注意这里设置了初始值
console.log(arr, sum);
//打印结果：
//0 1 0
//1 2 1
//3 3 2
//6 4 3
//[1, 2, 3, 4] 10
//这个例子index是从0开始的，第一次的prev的值是我们设置的初始值0，数组长度是4，reduce函数循环4次。
```

> 如果没有提供initialValue，reduce 会从索引1的地方开始执行 callback 方法，跳过第一个索引。如果提供initialValue，从索引0开始。
>
> 注意：如果如果数组为空，会抛出错误："TypeError: Reduce of empty array with no initial value"；
>
> 所以一般来说我们提供初始值通常更安全

### 高级用法

#### 计算元素出现的次数

```javascript
//计算字符串中某个字符串出现的次数
let str = 'dfafjghjdahgjadjfghdakghajkghfjkghkfhagkjagkaz';
function num(str){
    let returnData = str.split('').reduce((total,value,index,arr) =>{
        if(value in total){
            total[value]++;
        }else{
            total[value] = 1;
        };
        return total;
    },{});
    return returnData;
};
console.log(this.num(str));
//{d: 4, f: 5, a: 8, j: 7, g: 8, …}
```

#### 数组去重

```javascript
//数组去重
let arr1 = [1,2,3,4,5,5,6,6,7,7,8];
function reduce(arr){
    let returnData = [];
    arr.reduce((total, currentValue, currentIndex, arr) =>{
        if(!returnData.includes(currentValue)){
            returnData.push(currentValue);
        };
    },0);
    return returnData;
};
console.log(this.reduce(arr1));
//[1, 2, 3, 4, 5, 6, 7, 8]
```

#### 数组拉平

```javascript
//数组拉平(二维数组)
let arr = [[0, 1], [2, 3], [4, 5]];
function flat(arr){
    let newArr = arr.reduce((pre,cur)=>{
        return pre.concat(cur)
    },[]);
    return newArr;
};
console.log(this.flat(arr));
// [0, 1, 2, 3, 4, 5]
//数组拉平(多维数组)
let arr = [[0, 1], [2, 3], [4, 5,[1,2,3]]];
function flat(arr){
    let newArr = arr.reduce((pre,cur)=>{
        return pre.concat(Array.isArray(cur) ? flat(cur) : cur);
    },[]);
    return newArr;
}
console.log(this.flat(arr));
//[0, 1, 2, 3, 4, 5, 1, 2, 3]
```

#### 对象数组属性求和

```javascript
let arr = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];

function flat(arr){
    let sum = arr.reduce(function(prev, cur) {
        return cur.score + prev;
    }, 0);
    return sum;
}
console.log(this.flat(arr));
//60
```



