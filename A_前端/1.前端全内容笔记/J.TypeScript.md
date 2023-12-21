**ts简介**

![image-20231219152700710](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219152700710.png)

![image-20231219152808929](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219152808929.png)



# 1.ts基础内容速成

**使用typescipt的三种方式**

1. 官网打开演练场
2. 本地项目下载 npm i typescipt -g
3. 前端工程项目直接安装ts

官网演练场:https://www.typescriptlang.org/zh/play



## 1.类型推断、断言、注解、别名

类型推断和类型注解

```ts
// 1.ts会自动进行类型推断 不推荐
let str = 'hello'

// 2.类型注解
let str1:string = 'word'
```



类型断言

![image-20231217202830738](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217202830738.png)

此时需要使用到断言 as

![image-20231217202907252](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217202907252.png)



类型别名

![image-20231217210206801](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217210206801.png)



## 2.数据类型

![image-20231217203927555](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217203927555.png)



枚举类型

![image-20231217204231471](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217204231471.png)



void类型 无返回值的意思

![image-20231217204553321](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217204553321.png)



## 3.函数和接口、泛型

使用函数

![image-20231217204828112](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217204828112.png)

接口

![image-20231217205824994](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217205824994.png)

泛型

```ts
// 泛型的概念
function myFn<T>(a:T, b: T): T[]{
    return [a, b]
}

// 使用的时候就可以有各种类型
myFn<number>(1, 2)
myFn<string>('hello', 'world')

function identity<T>(arg: T): T {
	return arg;
}
identity<numer>(2)
```



## 4.判断变量类型

![image-20231217212255740](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217212255740.png)



## 5.函数重载

重写是继承后重写父类方法，重载是通过参数的个数不同或类型不同以及返回值类型的不同来实现一个函数完成多种功能

1

```ts
// 函数重载
function sayHello(name:string):string
function sayHello(age:number):string
function sayHello(val: string | number): string {
    if(typeof val === "string"){
        return `我的名字是,${val}`
    } else if(typeof val === "number"){
        return `我的年龄是,${val}`
    }else{
        return '非法格式'
    }
}
//调用的时候就可以传number或者string
```



2

```ts
// 函数重载
function myFn1(a: number, b: number): number;
function myFn1(a: string, b: string): string;
function myFn1(a: any, b: any): any {
if (typeof a === "number" && typeof b === "number") {
        // 处理数字类型的情况
        return a - b;
    } else if (typeof a === "string" && typeof b === "string") {
        // 处理字符串类型的情况
        return a + b;
    } else {
        throw new Error("Unsupported type");
  }
}
```



## 6.接口继承

![image-20231217214045278](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217214045278.png)



## 7.类

### 1.类修饰符

```ts
// 类
class Article{
    // ts中声明类需要给属性设置类型
    // 默认修饰为public 公共
    public title: string
    public content: string
    public a? :string
    public b = 100
    private tempData?: string // 私有属性 只能在类内部使用
    protected innerData?: string // 受保护的属性 只能在类内部使用或子类中使用
    static author?: string // 静态属性 只能给类的实例使用
    // static修饰符可以联合使用 需要注意的是 static 只能在最后面
    private static me?: string
    public readonly test?:string  // 只读属性不能设置值


    constructor(title: string, content: string, a?: string) {
        this.title = title;
        this.content = content;
        this.a = a; // 在构造函数中进行赋值
        console.log(this.tempData)// 访问私有属性
        console.log(this.innerData)// 访问受保护的属性
        Article.me = 'world' // 访问受保护的静态属性
    }

    
}

const art1 = new Article('标题', '内容', '可选参数')  // 创建类的实例

Article.author = 'hello' // 访问静态属性

class B extends Article {
    constructor(title:string, content:string){
        super(title, content)

        // 子类可以访问受保护的属性
        console.log(this.innerData)
    }
}
```



开闭原则

![image-20231217221748988](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217221748988.png)



### 2.存取器

```ts
// 类的存取器
class User {
    private _password: string = ''

    get password(): string {
        return '********'
    }

    set password(newPw: string) {
        this._password = newPw
    }
}

const user1 = new User()
// 访问的时候只能访问到****
console.log(user1.password)
// 但是可以设置值  这就是类的开闭原则的一种 调用API但是不知道具体的实现细节
user1.password = '李华'
```



### 3.抽象类

```ts
abstract class Animal {
    public title: string
    abstract name: string // 抽象名称
    abstract sayName(): void // 抽象方法
    // 抽象类中也可以有非抽象类和方法
    move() : void {
        console.log('移动了~~~')
    }
    // 构造方法
    constructor(title: string) {
        // 在抽象类的构造方法中初始化属性
        this.title = title
    }
}

class Cat extends Animal {
    name: string = '小猫' 
    sayName(): void {
        console.log(this.name)
    }
}

const cat1 = new Cat('标题')
```

![image-20231217223719889](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217223719889.png)



### 4.接口定义类行为

**接口比抽象类好的就是 接口可以有多个 抽象类只能有一个**

![image-20231217223845829](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217223845829.png)



### 5.泛型类

```ts
class MyClass<T> {
    public value: T
    constructor(value: T){
        this.value = value
    }

    do(input: T): T {
        // this.value = input
        console.log('处理数据', this.input)
        return input
    }
}

const myClass = new MyClass<string>('hello')
myClass.do('world') 

const myClass1 = new MyClass<number>(123)
myClass1.do(456) 
```



# 2.TS完整补充

## 1.安装和基本使用ts

![image-20231219152950802](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219152950802.png)

**配置ts配置文件**

```bash
tsc --init
```

配置书写代码的文件夹

![image-20231219153607226](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219153607226.png)

编译以后的文件夹

![image-20231219153630597](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219153630597.png)

编译ts

```bash
tsc --watch
```

### 1.export default {}

![image-20231219204550804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219204550804.png)





## 2.数据类型补充

**number、string、object、boolean这是最常用的四个类型**

### 1.定义数组

```ts
// 定义数组的四种方式
// 01.通过类型注解 说明这是一个number类型的数组
let numArr : number[] = [1,2,3,4];
let numArr1 : Array<number> = [1,2,3,4];

// 02.通过泛型 声明这是一个对象数组
let objArr : Array<object> = [{name:'zs'}]
let strArr : Array<string> = ['1','2','3','4'];

// 03.定义联合类型数组
let unionArr : (string | number)[] = ['1','2','3','4',1,2,3,4];
let unionArr2 : Array<string | number> = ['1','2','3','4',1,2,3,4];

// 04.any定义任何类型 这样ts就没意义了
let anyArr: any[] = ['1','2','3','4',1,2,3,4];
```



### 2.元组

**在js中没有元组的概念**

![image-20231219155241097](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219155241097.png)

```ts
// 定义元组
// 元组的意义是用来保存定长长度且数据类型不变的数组
let tupleArr: [string, number] = ['1',2];
```



### 3.any和void

#### 1.any

在 TypeScript 中，any 是一种特殊的类型，它表示任意类型。使用 any 类型的变量可以接受任何类型的值，而不会进行类型检查和推断。虽然 any 类型在某些情况下可以提供灵活性，但过度使用它可能导致代码失去类型安全性，因为 TypeScript 将不再对该变量进行类型检查。

**重点 1.any可以接收任何类型的值  2.设置了any不会进行类型检查和推断,报错不会直接显示，要运行了才会显示**

```ts
// any
// 使用场景一: 项目从js迁移ts,我们可以用any避免一次性处理所有的数据类型

// 使用场景二: 用户输入,用户的输入可能是任意类型
let userInput: any;
userInput = 42;
userInput = '我是黄宇'

// 使用场景三: 一些场景下我们希望让系统暂时不要进行类型检查和推断 不安全不要随便用
let x:any = 4
// 此时这俩个函数我们根本未定义,但是系统不会报错
x.toFixed()
x.ifItExist()

// 使用场景四: 我们需要一个数组,可以存任意类型的数据 
let list: any[] = [1, '我是黄宇', true, {name: 'zs'}]
```



#### 2.void

![image-20231219160625024](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219160625024.png)

![image-20231219162020406](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219162020406.png)

![image-20231219162005245](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219162005245.png)



**例子**

```ts
let value: void

// 未开启严格模式下 void类型只能被赋值给undefined和null
// 但是一个定义了undefined或null的变量是不能重新赋值给void
value = undefined
value = null
```



### 4.undefined和null

![image-20231219162758421](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219162758421.png)

```ts
let x: undefined = undefined
let y: null = null

let num: number = 1
let str: string = "1"
// 在非严格模式下 undefined和null是可以赋值给number和string的
num = x
num = y

str = x
str = y
```



### 5.never类型

![image-20231219163039236](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219163039236.png)

```js
// never类型的使用场景 
// 01 抛出异常时
function error(msg:string) : never {
    throw new Error(msg)
}

// 系统会自动推断为never类型
function fail() {
    return error('异常报错')
} 

// 02 函数存在永远无法返回的情况
function infiniteLoop(): never {
    while (true) {

    }
}
```



### 6.enum枚举类型

![image-20231219172613295](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219172613295.png)

```ts
// 在js中,枚举类型的本质就是数值类型,可以给他赋值数值类型不会报错
// 默认从0开始,依次递增,我们可以在创建的时候为它指定数值也可以

// 常用场景 性别只分男女
enum Gender{
    Male = 1, // 男
    Female = 2 // 女
}

console.log(Gender.Male);
console.log(Gender.Female);
```



### 7.bigint和symbol

bigint只能在es2020可用

![image-20231219172812154](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219172812154.png)

```ts
let bigNum:bigint = 100n;
console.log(bigNum);

const firstName:symbol = Symbol("name");
const secondName:symbol = Symbol("name");
console.log(firstName === secondName);

// 这个比较永远都是false
if (firstName === secondName) {
    console.log('ok');
}else{
    console.log('no');   
}
```



### 8.解构

```ts
// 写上这行代码相当于开启了模块作用域
// 模块在其自身的作用域里执行，而不是在全局作用域里
// 这种情况下，TypeScript 编译器会将该文件视为一个模块，
// 并将文件内的变量、函数等作为该模块的私有成员。这样做的好处是，模块内部的变量不会与全局作用域中的变量发生冲突，因此不会报错。
export default{
}

// 数组解构1 在ts中不允许解构空值
let [a, b, c, d] = ['1', '2', '3', '4']

// 数组解构2
let [e, ...rest] = ['1', '2', '3', '4']
console.log(e);
console.log(rest); // ['2', '3', '4']
console.log(...rest); // 2 3 4

// 数组解构3 axios请求以后返回的数据有些我们不需要 可以用这种逗号的形式
let [, data, , code] = ['msg', 'data', 'msg1', 'code']


// 简单的对象解构
let obj1 = {
    name: '张三',
    age: 18,
    address: '北京'
};

let {name, age, address} = obj1
```



## 3.类型

### 1.类型断言

```bash
1.<我们想要的类型>变量名
2.变量名 as 我们想要的类型
```

```ts
function Fn(x: number | string): void{
    let len = (x as string).length;
    let len1 = (<string>x).length
}
```



### 2.类型别名

```ts
export default{
}

// ns只能是这三种类型
type ns = string | number | Array<number>
let ns:ns = '黄宇'

// ns1只能是这三个选择
type ns1 = '黄宇' | '死狗宇' | '老宇'
let ns1:ns1 = '黄宇'

// 定义一个函数类型别名
type fn = (a:number, b:number) => number
let myFn:fn = (a:number, b:number) => a+b
console.log(myFn(1,2));

// 定义对象别名
type obj = {
    name:string,
    age:number
}

let obj:obj = {
    name:'黄宇',
    age:18
}
```



## 4.接口

![image-20231219211540940](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219211540940.png)

**接口可以同名,同名的相当于结合起来**

![image-20231219211736056](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219211736056.png)



### 1.可选属性和只读属性

可选属性 ?

**只读属性和可选属性的区别**

![image-20231219211826483](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219211826483.png)



### 2.索引签名

**实际开发中,参数的不确定性如何解决**

![image-20231219212830945](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219212830945.png)

```ts
export default{
}

// 如果参数可能是少一个或多个属性的情况 利用可选属性解决
interface IFullName1 {
    firstName: string
    lastName: string
    age?: number // 可选属性
    singName?:string // 可选属性
}

let test1:IFullName1 = {
    firstName: '黄',
    lastName: '宇'
}

// 如果参数多一个或多个
// 方案一: 使用变量 不推荐
// 原理是 ts编译器校验的时候是浅层次校验,套一层对象它就发现不了
interface IFullName2 {
    firstName: string
    lastName: string
}

let info = {firstName: '黄',lastName: '宇', age: 18}
let test2:IFullName2 = info

// 方案二: 使用类型断言
// 原理是 类型断言加上以后ts编译器就不去校验了,因为是我们人为确定的
let test3:IFullName2 = {firstName: '黄',lastName: '宇', age: 18} as IFullName2


// 方案三: 使用索引签名
interface IFullName4 {
    firstName: string
    lastName: string
    // 键名为string类型 值为any类型,这里指的是可以有很多个参数
    [propName: string]: any
}

// 注意: 对象中的键 最终都会被转化为字符串
let test4:IFullName4 = {
    firstName: '黄',
    lastName: '宇',
    age: 18,
    singName: '黄宇'
}
```



### 3.函数与接口

```ts
/* 
    为了使用接口表示函数类型,我们需要给接口定义一个调用签名
    它就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型
*/
interface MyFunc {
    // 调用签名
    (a: number, b: number): number
}

let fn: MyFunc = function (x: number, y: number): number {
    return x + y
}
let res = fn(1, 2) 
console.log(res)// 3
```



### 4.数组与接口（索引签名）

JS中数组就是一个特殊的对象

```ts
interface IsStringArray {
    // 数组索引签名 必须为number类型 不然下标就取不到值
    // 数组的索引就是 number 类型的 0,1,2,3...
    // 数组可以存储的值为 number 和 string
    [index: number] : number | string
}
let myArr: IsStringArray = [1, 2, 3, '1', '2' , '3']
let myStr:any = myArr[2]
console.log(myStr);
```



### 5.对象与接口(索引签名补充)

```ts
interface IsStringArray1 {
    // 这种就是对象的索引签名
    // 对象的索引就是 string 类型的属性名
    // 可以存储的值就为 string | number | boolean
    [props: string] : string | number | boolean
}
let myArr1: IsStringArray1 = {
    name: '1',
    age: 1,
    isFlag: true
}
console.log(myArr1.name);
console.log(myArr1['age']);
```



### 6.接口继承

![image-20231219222847643](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219222847643.png)

![image-20231219222905480](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219222905480.png)

**类在引用接口的时候可以引用多个,这是它比抽象类更好的地方**



### 7.混合类型的接口

没懂

![image-20231219223853761](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231219223853761.png)



### 8.接口与类型别名的异同点

```bash
相同点
1.都可以描述属性和方法
2.都允许扩展

不同点
1.type可以声明基本数据类型,联合类型,数组,对象等等...而interface只能声明对象
2.type不会进行合并(报错,不允许多次定义),interface会进行合并(后面定义的会添加到前面的)
```

1. ```ts
   // 都可以描述属性和方法
   interface IUser {
       name: string;
       fn(): string;
   }
   
   type Iuser1 = {
       name:string
       fn():string
   }
   
   let user: IUser = {
       name: 'zhangsan',
       fn() {
           return 'hello'
       }
   }
   
   
   let user1: Iuser1 = {
       name: 'zhangsan',
       fn() {
           return 'hello'
       }
   }
   ```

2. ```ts
   // 都可以支持扩展
   type ty1 = {
       y1:number
   }
   // ty2扩展了ty1
   type ty2 = ty1 & {
       y2:number
   }
   
   interface inter1 {
       i1:number
   }
   
   // inter2扩展了inter1
   interface inter2 extends inter1 {
       i2:number
   }
   ```

3. ```ts
   // type可以定义的类型更为丰富
   type name = 'zs' | 'ls' | 'ww'
   type props = string | number
   type arr = string[] | number[]
   type arr1  = Array<string | number>
   type obj = {
       name:string,
       age:number,
       fn() : string
   }
   
   interface obj1 {
       name:string,
       age:number,
       fn() : string
   }
   ```

4. ```ts
   // type不允许多次定义
   type ty1 = {
       name:string
   }
   
   // 这是接口对自己的扩展 会合并
   interface in3 {
       name:string
   }
   interface in3 {
       age:number
   }
   ```

## 

## 5.ts中的函数额外功能

### 1.基本使用

```ts
// 基本使用
// 匿名函数 function(){}
const fn = function(a:number, b:number):number {
    return a + b
}
// 具名函数 function(){}
function fn1(a:number, b:number):number {
    return a + b
}
// 箭头函数 () => {}
const fn2 = (a:number, b:number):number => {
    return a + b
}
```



### 2.函数参数处理

![image-20231220210153711](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220210153711.png)

**演示**

![image-20231220212335292](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220212335292.png)

![image-20231220211023740](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220211023740.png)

![image-20231220212631162](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220212631162.png)



### 3.构造函数和递归函数

![image-20231220212734298](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220212734298.png)

```ts
// 构造函数
var myFn = new Function('a', 'b' ,'return a * b')
let fn = myFn(3, 4)
console.log(fn); // 12

// 递归函数在ts的使用
function sum(arr: number[], n: number): number {
    if(n<=0){
        return 0
    }else{
        return sum(arr, n-1) + arr[n-1]
    }
}

let res = sum([2,3,4,5], 3)
console.log(res); // 9
// 第一次 sum[(2,3,4,5), 2] + arr[2] => sum[(2,3,4,5), 2] + 4
// 第二次 sum[(2,3,4,5), 1] + arr[1] => sum[(2,3,4,5), 1] + 3 + 4
// 第三次 sum[(2,3,4,5), 0] + arr[0] => sum[(2,3,4,5), 0] + 2 + 3 + 4
// 第四次 0 + 2 + 3 + 4 = 9
```



### 4.函数重载

**很少用,一般都用泛型。**

![image-20231220213745273](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220213745273.png)

![image-20231220214240074](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220214240074.png)

![image-20231220214401129](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220214401129.png)



### 5.ts中的this

![image-20231220214630093](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220214630093.png)

```ts
// js中的this指定
// this指向是在执行时确定的，不是定义时确定的
class Rectangle1 {
    w:number
    h:number

    constructor(w:number, h:number){
        this.w = w
        this.h = h
    }

    getArea(){
        return () => {
            // 由于箭头函数中没有this 所以this会向上层寻找
            // 箭头函数被定义在 getArea 方法中，而 getArea 方法是在 Rectangle1 类的实例对象上调用的。
            // 因此，箭头函数中的 this 指向的是 Rectangle1 类的实例对象。
            // 找到getArea -> 找到Rectangle1 -> 指向 Rectangle1 类的实例对象。
            return this.w * this.h
        }
    }
}

// 上面那段代码可读性差的一
// 在ts中 我们可以声明this的类型 增强代码可读性
class Rectangle2 {
    w:number
    h:number

    constructor(w:number, h:number){
        this.w = w
        this.h = h
    }

    // 显示指定this类型就是指向Rectangle2的实例对象
    // getArea(this:Rectangle2){
    //     return () => {
    //         return this.w * this.h
    //     }
    // }

    // 如果将this类型指定为void 那就等于this为空 不能用this 
    getArea(this:void){
        return () => {
            return this.w * this.h
        }
    }
}
```



### 6.特殊的函数返回值

![image-20231220215938450](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231220215938450.png)

**只是让我们知道有这种写法,这样写是不规范的**

```ts
// 定义了一个别名或者在接口里定义一个函数,指定返回值为void
// 我们可以强行给它返回值,这个返回值是有效的 但是不要这样做
type VoidFunc = () => void;

let fn1: VoidFunc = () => {
    return 'hello world'
}

interface func{
    fn():void
}

let fn2:func = {
    // 接口中的方法返回值定义为void的时候也可以强行返回别的
    fn:()=>{
        return 'hello world'
    }
}

// 在函数定义时指定返回值为void 强行返回除了null和undefined的值时会报错
function func2(): void {
    // return 'hello world'
}
```



## 6.类

### 1.类基本使用

![image-20231221084325088](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221084325088.png)



### 2.类的继承

![image-20231221084610095](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221084610095.png)

```ts
class Father {
    public name: string;
    public age: number;
    constructor(name:string, age:number){
        this.name = name;
        this.age = age;
    }
    sayFather():void{
        console.log('我是父类')
    }
}

// 子类中可以继承父类非私有的方法和属性 构造函数和私有的不能继承
// 继承属性和方法调用super() 相当于引用了父类
class Son extends Father {
    public score: string
    constructor(name:string, age:number, score:string){
        // 继承父类的属性
        super(name, age)
        this.score = score;
    }

    sayChild():void{
        // 在子类的方法中调用父类方法,如果是在子类实例调用是默认继承的
        super.sayFather()
        console.log('我是子类')
    }
}

let son = new Son('黄宇', 99, '0')
son.sayChild()
// son.sayFather()  子类实例可以直接调用
```



### 3.类修饰符

#### 1.static 和 instanceof

![image-20231221090608154](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221090608154.png)

直接实例化和继承的类实例使用instanceof都是为true

![image-20231221090731724](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221090731724.png)



#### 2.四个常用的

![image-20231221090947281](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221090947281.png)

**给类的构造函数加上protected修饰符**

```ts
class Father {
    public name: string;

    // 如果给constructor加上protected, 则该类不能被实例化，只能被继承 
    // 在开发中这种方式常用来确定一个基类
    protected constructor(name:string){
        this.name = name;
    }
}

class Son extends Father {
    public age: number;

    constructor(name:string, age:number){
        super(name);
        this.age = age;
    }
}

// 子类可以正常继承
let son = new Son('Son', 10);
```



**抽象类和给类构造函数设置protected的区别**

![image-20231221092823147](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221092823147.png)



**抽象类和接口继承时的区别**

```ts
export default{
}

// 接口和抽象类的对比 就是接口可以被继承多个
interface classA {
    name:string
}
interface classB {
    age:number
}
class className implements classA,classB {
    name:string
    age:number
    constructor(name:string,age:number){
        this.name = name
        this.age = age
    }
}

abstract class abstractClass {
    public name:string  // 非抽象属性 可以在构造函数中访问
    abstract age:number // 抽象属性 不能在构造函数中访问,继承的子类需要实现该属性
    constructor(name:string){
        this.name = name
    }
    abstract say():void // 抽象方法 子类必须实现
}

// 一个类只能直接继承一个抽象类
class abstractClassName extends abstractClass {
    public age:number
    constructor(name:string,age:number){
        super(name)
        this.age = age
    }
    say(): void {
        console.log('我是抽象方法');
    }
}
let class1 = new abstractClassName('张三',18)
console.log(class1.name,class1.age);
class1.say()

```



### 4.getter和setter

![image-20231221103425380](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221103425380.png)

```ts

class MyClass {
    private _fullName: string = '张三'; 
    // 目前有一个需求是想将这个私有的属性开放给外部访问 此时可以使用存取器
    get fullName(): string {
        console.log('get被调用了,展示名字');
        return this._fullName;
    }
    set fullName(newName: string) {
        console.log('set被调用了,修改名字');
        this._fullName = newName;
    }
}

// 外部访问
let myClass = new MyClass();
myClass.fullName = '李四'; // 设置值
console.log(myClass.fullName);
```

