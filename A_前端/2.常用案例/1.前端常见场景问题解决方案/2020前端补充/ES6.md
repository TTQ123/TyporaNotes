## 什么是ES6

- ES6， 全称 ECMAScript 6.0 ，是 JavaScript 的下一个版本标准，2015.06 发版

- ES6 的出现主要是为了**解决 ES5 的先天不足**，比如 JavaScript 里并没有类的概念

- 目前存在**少数低版本浏览器**的 JavaScript 是 ES5 版本，大多数的浏览器已经支持 ES6

- ES6提供了大量的语法糖。

-  定义：在计算机科学中，语法糖(syntactic sugar)是指编程语言中可以更容易的表达一个操作的语法，它可以使程序员更加容易去使用这门语言：操作可以变得更加清晰、方便，或者更加符合程序员的编程习惯。

-   具体来说，语法糖是指语言中的一个构件，当去掉该构件后并不影响语言的功能和表达能力。例如，C语言中的标记a[i]就是*(a+i)的语法糖。语言的处理器，包括编译器，静态分析器等，经常会在处理之前把语法糖构件转换成更加基础的构件，这个过程通常被称为"desugaring"。

- **简而言之，语法糖就是一种便捷写法。**

  ```javascript
  例如：input.map(a => a-8);
     去掉语法糖就是：
  
     input.map(function (a) {
         
        return a-8;
         
    });
  ```

  

## 1.let与const

### 1.1let与var

- let：ES6新增，用于声明变量，有**块级作用域**

- var：ES5中用于声明变量的关键字，存在各种问题

  

  **var存在的问题**：

```javascript
 // 1.声明提升
 // 此处会正常打印，但这是错误的（属于先上车后买票了！）
 console.log(name); 
 var name = "大帅比";
 
 // 2. 变量覆盖
 var demo = "小明";
 var demo = "小红";
 // 此处会打印小红，这也是错误的（属于套牌车，违法的啊，兄弟）
 // 同一个项目中，发生变量覆盖可能会导致数据丢失以及各种不可预知的bug，原则上来说：变量不能重名
 console.log(demo)

// 3. 没有块级作用域
  function fn2(){
      for(var i = 0; i < 5; i++){
          // do something
      }
      // 此处会正常打印出 i 的值，这是错误的
      // i是定义在循环体之内的，只能在循环体内打印，当前现象叫做红杏出墙！！！
      console.log(i);
  }
  fn2();

```

**let不会存在上述问题：**

```javascript
 // 1. 不会存在声明提前
 // 此处会报错（这里必须报错，原则上来说不能先上车后买票）
 console.log(name); 
 let name = "大帅比";
 
 // 2. 不会有变量覆盖
 let demo = "小明";
 let demo = "小红";
 // 此处会报错（不能使用套牌车！）告诉你已经定义了此变量。避免了项目中存在变量覆盖的问题
 console.log(demo)

// 3. 有块级作用域
  function fn2(){
      for(let i = 0; i < 5; i++){
          // do something
      }
      // 此处会报错，无法打印，防止红杏出墙！！！
      // i是定义在循环体之内的，循环体外当然无法打印 
      console.log(i);
  }
  fn2();

```

**const**

- const 声明一个只读的常量，一旦声明，常量的值就不能改变
- 一般用于全局变量
- 通常变量名全部大写（请按照规则来，不要乱搞，容易出事情）

```javascript
const PI = "3.1415926";
```

## 2.解构赋值

- 解构赋值是对赋值运算符的扩展
- 针对数组或者对象进行模式匹配，然后对其中的变量进行赋值
- 代码简洁且易读，语义更加清晰明了，方便了复杂对象中数据字段获取（**简而言之：用起来很爽！**）

### 2.1用在数组上

```javascript
let [a, b, c] = [1, 2, 3];
// a = 1，b = 2，c = 3 相当于重新定义了变量a,b,c，取值也更加方便

// , = 占位符
let arr = ["小明", "小花", "小鱼", "小猪"];
let [,,one] = arr; // 这里会取到小鱼

// 解构整个数组
let strArr = [...arr];
// 得到整个数组
console.log(strArr);
```

### 2.2用在对象上

```javascript
let obj = {
   className : "卡西诺",
   age: 18
}
let {className} = obj; // 得到卡西诺
let {age} = obj;	// 得到18

// 剩余运算符
let {a, b, ...demo} = {a: 1, b: 2, c: 3, d: 4};
// a = 1
// b = 2
// demo = {c: 3, d: 4}
```

## 3.模板字符串

- 模板字符串相当于**加强版的字符串**，用反引号 ``
- 除了作为普通字符串，还可以用来定义多行字符串，可以在字符串中加入变量和表达式

### 3.1普通字符串

```javascript
// 普通字符串
let string = "hello"+"小兄弟"; // hello小兄弟
// 如果想要换行
let string = "hello'\n'小兄弟"
// hello
// 小兄弟
```

### 3.2模板字符串

```javascript
let str1  = "穿堂而过的";
let str2 = "风";
// 模板字符串
let newStr = `我是${str1}${str2}`;
// 我是穿堂而过的风
console.log(newStr)

// 字符串中调用方法
function fn3(){
  return "帅的不行！";
}
let string2= `我真是${fn3 ()}`;
console.log(string2);  // 我真是帅的不行！
```

## 4.ES6函数

### 4.1箭头函数

- 箭头函数是一种更加简洁的函数书写方式
- **箭头函数本身没有作用域（无this）**
- 箭头函数的this指向上一层，**上下文决定其this**
- 基本语法：**参数 => 函数体**

**a. 基本用法**

```javascript
let fn = v => v;
//等价于
let fn = function(num){
 return num;
}
fn(100);  // 输出100
```

**b. 带参数的写法**

```javascript
let fn2 = (num1,num2)=>{
    let result = num1 + num2;
 	return result;
}
fn2(3,2);  // 输出5
```

**c. 箭头函数中的this指向问题**

- 箭头函数体中的 this 对象，是定义函数时的对象，而不是使用函数时的对象。**在函数定义的时候就已经决定了**

```javascript
function fn3(){
  setTimeout(()=>{
    // 定义时，this 绑定的是 fn3 中的 this 对象
    console.log(this.a);
  },0)
}
var a = 10;
// fn3 的 this 对象为 {a: 10}，因为它指向全局: window.a
fn3.call({a: 18});  // 改变this指向，此时 a = 18
```

**d. 箭头函数适用的场景**

- 当我们代码里存在这样的代码：let self = this;
- 需要新建变量去保存this的时候
- 案例如下：

```javascript
let Person1 = {
    'age': 18,
    'sayHello': function () {
      setTimeout(()=>{
        console.log(this.age);
      });
    }
};
var age = 20;
Person1.sayHello();  // 18
```

### 4.2函数参数的扩展

**1. 默认参数**

```javascript
// num为默认参数，如果不传，则默认为10
function fn(type, num=10){
 console.log(type, num);
}
fn(1);	// 打印 1，10
fn(1,2); // 打印 1，2 （此值会覆盖默认参数10）
```

- 需要注意的是：**只有在未传递参数，或者参数为 undefined 时，才会使用默认参数，null 值被认为是有效的值传递**。

**2. 不定参数**

```javascript
// 此处的values是不定的，且无论你传多少个
function f(...values){
    console.log(values.length);
}
f(1,2);      // 2
f(1,2,3,4);  // 4
```

## 5.Class类

- class (类)作为对象的模板被引入，可以通过 class 关键字定义类
- class 的本质是 function，同样可以看成**一个块**
- 可以看作一个语法糖，让**对象原型的写法更加清晰**
- 更加标准的**面向对象编程**语法

### 5.1类的定义

```javascript
// 匿名类
let Demo = class {
    constructor(a) {
        this.a = a;
    }
}
// 命名类
let Demo = class Demo {
    constructor(a) {
        this.a = a;
    }
}
```

### 5.2类的声明

```javascript
class Demo {
    constructor(a) {
        this.a = a;
    }
}
```

- 请注意，类不能重复声明
- 类定义不会被提升，必须在访问前对类进行定义，否则就会报错。
- 类中方法不需要 function 关键字。
- 方法间不能加分号

### 5.3类的主体

- 公共属性（依然可以定义在原型上）

```javascript
class Demo{}
Demo.prototype.a = 2;
```

- 实例属性

```javascript
class Demo {
    a = 2;
    constructor () {
        console.log(this.a);
    }
}
```

- 方法：constructor

```javascript
class Demo{
    constructor(){
      console.log('我是构造器');
    }
}
new Demo(); // 我是构造器
```

如果不写constructor，也会默认添加

### 5.4实例化对象

```javascript
class Demo {
    constructor(a, b) {
        this.a = a;
        this.b = b;
        console.log('Demo');
    }
    sum() {
        return this.a + this.b;
    }
}
let demo1 = new Demo(2, 1);
let demo2 = new Demo(3, 1);
// 两者原型链是相等的
console.log(demo1._proto_ == demo2._proto_); // true
 
demo1._proto_.sub = function() {
    return this.a - this.b;
}
console.log(demo1.sub()); // 1
console.log(demo2.sub()); // 2
```

## 6.Map()

### 6.1Maps和Objects的区别

1.一个 Object 的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值。
2.Map 中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
3.Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
4.Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。
![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20210601005359180.png)



### 6.2Map中的Key

```javascript
// 1. key是字符串
let myMap = new Map();
let keyString = "string"; 
 
myMap.set(keyString, "和键'string'关联的值");

// keyString === 'string'
myMap.get(keyString);    // "和键'string'关联的值"
myMap.get("string");   // "和键'string'关联的值"

// 2.key是对象
let myMap = new Map();
let keyObj = {}, 
 
myMap.set(keyObj, "和键 keyObj 关联的值");
myMap.get(keyObj); // "和键 keyObj 关联的值"
myMap.get({}); // undefined, 因为 keyObj !== {}

// 3. key也可以是函数或者NaN                         
```

### 6.3Map中的迭代

```javascript
// 1.使用 forEach
let myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 0 = zero , 1 = one
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
}, myMap)

// 2. 也可以使用 for...of
```

### 6.4Map和Array的转换

```javascript
letkvArray = [["key1", "value1"], ["key2", "value2"]];
 
// Map 构造函数可以将一个 二维 键值对数组转换成一个 Map 对象
let myMap = new Map(kvArray);
 
// 使用 Array.from 函数可以将一个 Map 对象转换成一个二维键值对数组
let outArray = Array.from(myMap);
```

### 6.5关于map的重点面试题

请谈一下 Map和ForEach 的区别（问到map，必定问到此题）

**详细解析：**

forEach()方法不会返回执行结果，而是undefined
map()方法会得到一个新的数组并返回
同样的一组数组，map()的执行速度优于 forEach()**（map() 底层做了深度优化）**
性质决定了两者应用场景的不同

- forEach() 适合于你并不打算改变数据的时候，而只是想用数据做一些事情（比如存入数据库）

```javascript
let arr = ['a', 'b', 'c', 'd'];
arr.forEach((val) => {
 console.log(val); // 依次打印出 a,b,c,d
});
```

- map() 适用于你要改变数据值的时候，它更快，而且返回一个新的数组

```javascript
let arr = [1, 2, 3, 4, 5];
let arr2 = arr.map(num => num * 2).filter(num => num > 5);
// arr2 = [6, 8, 10]
```
