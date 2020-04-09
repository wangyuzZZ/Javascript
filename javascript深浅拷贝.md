# JS数据拷贝——深浅拷贝

## 为什么会有深拷贝浅拷贝之分

JS主要有其中数据类型其中包括**五种基本数据类型**（Undefined、Null、Boolean、Number 和 String）、一种**复杂数据类型**（Object）和一种新的**原始数据类型**（Symbol），在此基础上又分为**引用类型**跟**非引用类型**之分，其中**引用类型**主要包括 Object类型、Array类型、Function类型

首先来看一下如下代码:

```javascript
let a = b = 2
a = 3
console.log(a)
console.log(b)
let c = d = [1,2,3]
let e = f = {a:1,b:2,c:3}
c[0] = 2
e.a = 2
console.log(d[0])
console.log(f.a)
```

你会发现，同一个Array或者Object赋值给两个不同变量时，变量指向的是同一个内存地址，所以就会造成其中一个变量改变属性值，同时改变了另外一个变量的对应属性值。

>而大多数实际项目中，我们想要的结果是两个变量（初始值相同）互不影响。所以就要使用到**拷贝（分为深浅两种）**

## 深浅拷贝的区别

浅拷贝只复制一层对象的属性，而深拷贝则递归复制了所有层级。浅拷贝有效性针对的是单一层级对象 **[1,2,3]或者{a:1,b:2}**，深拷贝有效性针对的是单层或者多层级对象 **[1,2,3]或者{a:1,b:2}或者[1,[1],{a:1}]或者{a:[1],b:{c:2}}**

## 如何实现深拷贝

### 1、简单实现

```javascript
//定义测试数据
let data = {
        name:'悟空',
        age:'18'
    };
function copy1(data) {
    var newData = {};
    for (const key in data) {
        //Object.prototype.hasOwnProperty.call 判断属性是定义在对象本身而不是继承自原型链。
        if(Object.prototype.hasOwnProperty.call(data, key)){
            if(typeof data[key] === 'object'){
                newData[key] = copy1(data[key]);
            }else{
                newData[key] = data[key];
            }
        }
    }
    return newData;
}
```

>一个简单的深拷贝就完成了，但是这个实现还存在很多问题。
>
>- 1、没有对传入参数进行校验，传入 `null` 时应该返回 `null` 而不是 `{}`
>- 2、对于对象的判断逻辑不严谨，因为 `typeof null === 'object'`
>- 3、没有考虑数组的兼容

### 2、拷贝数组

```javascript
//定义测试数据
let arrObj = [{
        name:'悟空',
        age:'18'
    },{
        name:'猴子',
        age:'19'
    }];
function copy2(arrObj){
    //对传递的参数做判断
    if (typeof data !== 'object' || data == null) return data;
    //定义参数接收数据
    let newData = Array.isArray(data) ? [] : {};
    for (const key in data) {
        if(Object.prototype.hasOwnProperty.call(data, key)){
            if(typeof data === 'object' || data != null){
                newData[key] = copy2(data[key]);
            }else{
                newData[key] = data[key];
            };
        };
    };
    return newData;
}
```

## 解决递归爆栈[](https://segmentfault.com/a/1190000016672263)

上面两个方法使用的都是递归方法，但是有一个问题在于会爆栈，错误提示如下。

```javascript
// RangeError: Maximum call stack size exceeded
```

解决方法：

```javascript
function copy3(x) {
    const root = {};
    // 栈
    const loopList = [
        {
            parent: root,
            key: undefined,
            data: x,
        }
    ];
    while(loopList.length) {
        // 广度优先
        const node = loopList.pop();
        const parent = node.parent;
        const key = node.key;
        const data = node.data;

        // 初始化赋值目标，key为undefined则拷贝到父元素，否则拷贝到子元素
        let res = parent;
        if (typeof key !== 'undefined') {
            res = parent[key] = {};
        }

        for(let k in data) {
            if (data.hasOwnProperty(k)) {
                if (typeof data[k] === 'object') {
                    // 下一次循环
                    loopList.push({
                        parent: res,
                        key: k,
                        data: data[k],
                    });
                } else {
                    res[k] = data[k];
                }
            }
        }
    }

    return root;
}
```

