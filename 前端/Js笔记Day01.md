# JavaScript

## 一、引入JavaScript

1.内部标签

```html
<script>
    alert("hello world");
</script>
```

2.外部引入

```html
<script src="js/index.js"></script>
```

## 二、基础语法

1.定义变量

```html
<script>
    var num = 1;
    alert(num);
</script>
```

2.条件控制

```javascript
if (2>1)
{
    alert("true");
}
```

```javascript
<script>
    var score = 65;
    // alert(num);
    if (score>60&&score<70)
    {
        alert("60-70")
    }
    else if (score>70&&score<80)
    {
        alert(70-80)
    }
    else
    {
        alert("other")
    }
</script>
```

## 三、数据类型

### 1.number

js不区分整数和小数

``` javascript
123  //整数123
123.1   //浮点数123.1
1.122e3   //科学计数法
NaN  //not a number
Infinity  //无限大
```

### 2.字符串

```javascript
'a' 'abc'
```

转义符号\

```javascript
\'
\n   //换行
\t   //空格
\u4e2d   //unicode编码
\x41    //ascii
```

多行字符串的编写，使用反引号

```javascript
var str = `haha
        nihao
        666`
```

模版字符串

```javascript
let name='xay';
let words=`你好，${name}`;
```

字符串的特性，不可变

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/6a0eca10573b4f5f802c363bf8749862.png)

大小写转换

```javascript
var word = 'aBcD';
word.toUpperCase()//转化为大写
word.toLowerCase()//转化为小写
```

substring()是字符串截取函数

```javascript
substring(1)  //从第一个字符串截取到最后一个
substring(1,3)  //[1,3)
```

### 3.布尔值

true false

### 4.逻辑运算

```javascript
&& //与
|  //或
!  //非
```

### 5.比较运算符

```javascript
=
==  //类型不一样，值一样也是真
===  //绝对等于，类型和值都必须一样
```

NaN===NaN返回的是false，只能通过`isNaN(NaN)`来判断

NaN有一个专门的方法是isNaN，这个方法会判断该常量是否为数字，如果是数字，返回false，如果不是，则返回true；



### 6.数组

```html
<script>
    var arr = [1,2,3,4,5,'hello']
</script>
```

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/99a36665b0eb4f458d31b0133a343028.png)

取数组下标时，如果越界了，会输出undefined
在给arr.length赋值后，数组长度也会发生变化，如果赋值过小，数组中的元素会丢失

**indexOf**可以通过元素获得其下标索引

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/963deda8824b4fb6b9fd991460fb9832.png)

**slice()** 可以截取数组的一部分，相当于字符串中的substring

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/fe13aa5974e64112a535c5aac1efa868.png)

**push() pop()**分别是向尾部压入和弹出元素

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/8b2137ff744c4b0bab72ced97e8756db.png)

**unshift() shift()**分别是向头部压入和弹出元素

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/892e0cc9f3a443ee8ab1844348eccc85.png)

**sort()** 按照ascii排序
**reverse()** 反转
**concat()** 拼接数组
**join()** 用指定符号将数组拼接起来

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/e7c6bc6d4ee6442f8e2a5cbf8c192566.png)



### 7.对象

js中{…}表示一个对象，键值对描述属性xxxxx:xxxxx，多个属性之间使用逗号隔开，最后一个属性不加逗号

```javascript
var person = {
    name: 'xay',
    age: 18,
    tags: ['js','java','python']
}
```

对象赋值

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/736be2a9bd1c41b49f13eae79cf54978.png)

动态的删减属性**delete person.name**

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/0213bcdd92064b0bbab447a890c3abb6.png)

对象属性的添加，直接赋值即可

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/8144a485b10746829d877407f58f751a.png)

判断属性是否在对象中

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/a4704099876347c4a3b8090fe1ee90d2.png)



### 8.流程控制

1.if判断

2.while

3.for循环

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

4.for循环遍历数组

```javascript
var arr=[1,2,3,4,5,6,7,8,9,10];
for (var num in arr)
{
    console.log(num)
}
```

### 9.Map和Set

#### Map

```javascript
var map=new Map([['tom',100],['jack',90],['haha',80]]);//key/value
var name=map.get('tom');  //通过key获得value
console.log(name)
```

**set()**向Map中添加数据

```javascript
map.set('admin',10);
map.delete('tom')  //map中的删除
```

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/a94d9981cca842ab9a4a111ffdc83b9a.png)

#### Set

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

```javascript
const s = new Set();
[2,3,5,4,5,2,2].forEach(x => s.add(x));
// Set结构不会添加重复的值
for(let i of s) {
  console.log(i);
}


//初始化
//1.可以接受一个数组作为参数
const set = new Set([1,2,3,4,4,]);
//将一个数组转化为用逗号分隔的参数序列
console.log([...set]);

//2.
const items = new Set([1,2,3,4,5,5,5,5,]);
console.log(items.size);

//3.可以接受具有iterable接口的其他数据结构作为参数
const set2 = new Set(document.querySelectorAll('div'));
console.log(set.size);

// 类似于
const set2 = new Set();
document
    .querySelectorAll('div')
    .forEach(div => set.add(div));
console.log(set.size);

//4.set中NaN等于自身，其余比较相当于 ===
let set3 = new Set();
let a = NaN;
let b = NaN;
set3.add(a);
set3.add(b);
console.log(set3)

//5.两个对象总是不相等的
let set4 = new Set();
set4.add({});  // 1
console.log(set4.size);

set4.add({});  // 2
console.log(set4.size);
```



```javascript
const s = new Set();

s.add(1).add(2).add(2);

console.log(s.size);

console.log(s.has(1));
console.log(s.has(2));
console.log(s.has(3));

s.delete(2);
console.log(s.has(2));

// set转数组
const items = new Set([1,2,3,4,5]);
const array = Array.from(items);
console.log(array);

// 去除数组重复成员
function dedupe(array) {
  return console.log(Array.from(new Set(array)));
}

dedupe([1,1,2,3]);
```



```javascript
let set = new Set(['red', 'green', 'blue']);

// 返回键名
for(let item of set.keys()) {
  console.log(item);
}

// 返回键值
for(let item of set.values()) {
  console.log(item);
}
// set 键名=键值

// 返回键值对
for(let item of set.entries()){
  console.log(item);
}

// 可以直接用 for of遍历Set
// for in 和 for of的区别是：in 是遍历对象，of是遍历值
for (let x of set) {
  console.log(x);
}

// set也有forEach()方法
set.forEach((value, key) => console.log(key + ' : ' + value));
// 此处forEach方法的参数是一个处理函数。

// 数组的 map 和 filter 方法也可以间接用于Set
let s = new Set([1,2,3]);

// map 将原数组映射成新数组
s = new Set([...s].map(x => x * 2));
console.log(s);

// filter返回过滤后的新数组
s = new Set([...s].filter(x => (x % 3) ==0));
console.log(s);

// 实现并集、交集、差集
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);

let union = new Set([...a, ...b]);
console.log(union);

let intersect = new Set([...a].filter(x => b.has(x)));
console.log(intersect);

let difference = new Set([...a].filter(x => !b.has(x)));
console.log(difference);

// 在遍历操作中，同步改变原来的Set结构的两种变通方法

// 1.利用原Set结构映射出一个新的结构，然后赋值给原来的Set结构
let set1 = new Set([1,2,3]);
set1 = new Set([...set1].map(val => val *2));
console.log(set1);

// 2.利用Array.from
let set2 = new Set([1,2,3]);
set2 = new Set(Array.from(set2, val => val * 2));
console.log(set2);
```



Set可以去重

```javascript
var set = new set([3,1,1,1,1]);
```

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/839500d7989f4b199ec142eaea3522c1.png)

```javascript
set.add(2)  //添加
set.delete(1)  //删除
console.log(set.has(3));  //是否存在3
```

### 10.iterator

遍历Map

```javascript
var map=new Map([['tom',100],['jack',90],['haha',80]]);
for (let x of map)
{
    console.log(x);
}
```

遍历Set

```javascript
var set=new Set([3,1,1,1,1]);
for (let x of set)
{
    console.log(x);
}
```

### 11.函数及参数获取

函数的定义

```javascript
function abs(x)
{
    if (x>=0)
        return x;
    else
        return -x;
}
```

一旦执行到return代表函数结束，返回结果。还有另一种函数定义方式：

```javascript
var abs = function (x) {
    if (x >= 0)
        return x;
    else
        return -x;
}
```

手动抛出异常    //throw "not a number";

```javascript
function abs(x)
{
    if (typeof x!=='number') {
        throw "not a number";
    }
    if (x>=0)
        return x;
    else
        return -x;
}
```

当函数有多个参数时，可以使用`arguments`，它代表传进来的参数是一个数组

```javascript
function abs(x)
{
    console.log("x->"+x);
    for (var i=0;i<arguments.length;i++){
        console.log(arguments[i]);
    }
    if (typeof x!=='number') {
        throw "not a number";
    }
    if (x>=0)
        return x;
    else
        return -x;
}
```

![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/2168b3e784a44a1197e51ca6039484ca.png)

当需要使用多余的参数来进行附加操作时，需要排除已有的参数，可以用`rest`

```javascript
function aaa(a,b,...rest){
	console.log("a->"+a);
	console.log("b->"+b);
	console.log(rest);
}
```

![请添加图片描述](https://img-blog.csdnimg.cn/4afd1f15ec5f4684acb00fb906d1f052.png)

### 12.变量的作用域

1. 假设在函数体内声明，则在函数外无法引用（非要使用，闭包可以实现）

   ```javascript
    function a() {
               var x=1;
               x=x+1;
          }
          x=x+2; // Uncaught ReferenceError: x is not defined
   ```

   如果两个函数使用相同的变量名

   ```javascript
   	function f() {
               var x = 1;
               x = x + 1;
           }
    
           function f1() {
               var x = 'A';
               x = x + 1;
   
   ```

   

2. 内部函数可以访问外部函数的成员，外部无法访问内部

   ```javascript
   function f() {
               var x = 1;
    
               //内部函数可以访问到外部函数的成员，反之不行
               function f1() {
                   var y = x + 1; //2
               }
    
               var z = y + 1; //Uncaught ReferenceError: y is not defined
           }
   ```

### 13.方法

方法就是把函数放在对象的里面，对象只有两个东西：属性和方法。

```javascript
var kuangshen={
	name:"kuangshen",
	birth:2000,
	age:function (){
	    var now=new Date().getFullYear();
	    return now=this.birth;
	}
}
```



![请添加图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/2c56e88142c64d2aa82171e2f3d0b7a7.png)

### 14.内部对象

#### Date

```javascript
var now=new Date() //Tue Sep 28 2021 13:56:03 GMT+0800 (中国标准时间)
now.getFullYear(); //年
now.getMonth(); //月 0-11代表月
now.getDate(); //日
now.getDay(); //星期几
now.getHours(); //时
now.getMinutes(); //分
now.getSeconds(); //秒
now.getTime(); //时间戳
console.log(new Date(1632808811159)); //时间戳转时间
```



### 15.JSON对象

JavaScript中一切皆对象，任何js支持的类型都可以用json来表示。

格式：

- 对象用{}
- 数组用[]
- 所有的键值对用key:value

```javascript
var user = {
    name:"qinjian",
    age:30,
    sex:"男"
}
//{name: 'qinjian', age: 30, sex: '男'}

//对象转json 此处对象为jsonUser
var jsonUser= JSON.stringify(user);
//{"name":"qinjian","age":30,"sex":"男"}

//json转对象
var obj=JSON.parse('{"name":"qinjian","age":30,"sex":"男"}');
```

