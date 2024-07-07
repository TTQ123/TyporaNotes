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

// 04.any定义任何类型的数组 这样ts就没意义了
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
// 01 抛出异常时❤❤
function error(msg:string) : never {
    throw new Error(msg)
}

// 系统会自动推断为never类型
function fail() {
    return error('异常报错')
} 

// 02 函数存在永远无法返回的情况❤❤
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

![image-20231227161527807](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227161527807.png)

```ts
// 1.数字枚举
enum Gender {
    Male,
    Female
}

// 数字枚举的取值也可以是常量或者计算结果
const val = 100
let fn = () => 200

enum Gender1 {
    Male = val, //100
    Female, // 101 采用字面量对第一个成员赋值,下面会自动递增
    Female1 = fn() // 200
}
console.log(Gender1.Male); // 100
console.log(Gender1.Female); // 200


// 2.字符串枚举
/*
    1.如果采用字面量对第一个成员赋值,下面的成员必须赋值(❤重要)
    2.采用[index]不能获取值,需要传入[key]
    3.字符串枚举不能使用计算结果给枚举值赋值
    4.它可以使用内部其它枚举值来赋值
*/
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT"
}
console.log(Direction.Up); // UP
console.log(Direction["Up"]); // UP

const name1 = '杨幂'
let fn1 = () => '刘亦菲'
enum User {
    a = name1,
    // b = fn1() 不能用
    c = '李沁',  // 可以使用内部其它枚举值
    d = c
}

console.log(User); // {a: '杨幂', b: '李沁', c: '李沁'}

// 3.异构枚举 数字和字符串都有 还是遵循的字符串规则
enum User1 {
    a = 1,
    b = 'b'
}
console.log(User1.a, User1.b); // 1 b
console.log(User1[0], User1['b']); // undefined b


// 4.把枚举成员当做类型来使用
enum LeiXi {
    str,
    num
}

interface face {
    userName: LeiXi // userName: (LeiXi.str | LeiXi.num)
}
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



### 9.字典

字典其实也是对象 只是是一种约束型的对象

![image-20240707232101792](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240707232101792.png)

AI总结的有一些偏差  其实键也可以是很多类型的

```tsx
let dict:{[key:number]:string} = {1:"a",2:"b",3:"c"}

// 定义一个符号 符号也是可以做键的
let sy = Symbol('sy');

// 定义一个可以使用符号作为键的对象
let dict: { [key: symbol]: string } = {};

// 将字符串赋值给符号键
dict[sy] = "a";

// 使用符号键来访问值
console.log(dict[sy]); // 输出: "a"
```



### 10.js/ts操作符

1. **算术操作符**
   - `+` 加法
   - `-` 减法
   - `*` 乘法
   - `/` 除法
   - `%` 取模（求余数）
   - `++` 前置/后置递增
   - `--` 前置/后置递减
2. **比较操作符**
   - `==` 等于（类型转换后比较）
   - `===` 严格等于（类型和值都相等）
   - `!=` 不等于（类型转换后比较）
   - `!==` 严格不等于（类型或值不同）
   - `<`, `<=`, `>`, `>=` 小于、小于等于、大于、大于等于
3. **逻辑操作符**
   - `&&` 逻辑与
   - `||` 逻辑或
   - `!` 逻辑非
4. **位操作符**
   - `&` 按位与
   - `|` 按位或
   - `^` 按位异或
   - `~` 按位取反
   - `<<` 左移
   - `>>` 有符号右移
   - `>>>` 无符号右移
5. **赋值操作符**
   - `=` 赋值
   - `+=`, `-=` 算术赋值
   - `*=`, `/=`, `%=`, `**=` 快速算术赋值
   - `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=`, `&=`, `^=` 位操作符赋值
6. **成员操作符**
   - `in` 检查对象是否有指定的属性
   - `instanceof` 检查对象是否是某个构造函数的实例
7. **条件（三元）操作符**
   - `? :` 条件操作符，根据条件选择两个表达式之一的结果
8. **类型操作符**
   - `typeof` 返回变量的类型
   - `void` 运算结果为`undefined`
9. **特殊操作符**
   - `new` 创建对象实例
   - `this` 当前对象的引用
   - `super` 调用父类的方法或访问父类的属性
   - `await` 等待一个Promise完成（异步函数中使用）
   - `yield` 生成器函数中用于暂停和恢复执行
10. **TypeScript特有的操作符**
    - `as` 类型断言
    - `keyof` 获取类型的所有键的联合
    - `in` 用于迭代类型的所有属性
    - `typeof` 获取类型注释的类型
    - `import` 和 `export` 用于模块导入和导出
11. **删除操作符**
    - `delete` 用于删除对象的属性或数组中的元素。

- ```js
  delete
  ```

  操作符的语法如下：

  ```js
  1.delete object.property; // 删除对象的属性
  2.delete array[index];    // 删除数组中的元素
  ```

请记住，`delete`操作符只适用于删除对象的自有属性，对于原型链上的属性无效。同时，在数组中使用`delete`并不会改变数组的长度，只是将其设置为`undefined`。

这应该能帮助你更全面地理解JavaScript和TypeScript中的操作符。记得在使用`delete`时考虑其可能对数据结构产生的影响。



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

设置protected这种比较少用,还是抽象类用的多

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



### 5.抽象类

![image-20231221144002319](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221144002319.png)

```ts
abstract class MyClass {
    abstract name:string // 定义抽象属性
    abstract say():string // 定义抽象方法
    public age:number   // 定义具体属性
	
    constructor(age:number){
        this.age = age
    }
    // 抽象类也可以实现具体操作,这是和接口最不一样的地方
    sayName(){
        console.log(this.age);
        console.log(this.say());
    }
}

class MyClassImpl extends MyClass {
    name:string = "张三"
    say(){
        return this.name
    }
}

let myClass = new MyClassImpl()
myClass.sayName()
```



### 6.implements

**❤类继承类用extends,类实现接口用implements**

![image-20231221144834914](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221144834914.png)

**接口继承类这种使用场景是比较少的**

```ts
interface ITest {
    name: string;
    age: number;
}
class myClass {
    sex: string
    constructor(sex: string){
        this.sex = sex
    }

    public sayHello(name: string) {
        console.log(`hello `);
    }
}

// 类实现接口
class test implements ITest {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

// 接口继承类 必须重写类的属性和方法
interface ITest2 extends myClass {
    sex: string
    sayHello(name: string): void;
}

// 一个类可以同时继承类和实现接口
class Star extends myClass implements ITest {
    name:string
    age: number
    sex: string
    constructor(name:string,age:number,sex: string) {
        super(sex)
        this.sex = sex
        this.name = name
        this.age = age
    }
    sayHello(name: string): void {
        console.log(`hello `);
    }
}
```



### 7.类的实例化顺序

![image-20231221151147082](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221151147082.png)

```ts
/*
    类的实例化顺序
        1.基类的字段被初始化
        2.基类的构造函数执行
        3.子类的字段被初始化
        4.子类的构造函数执行
*/

class myClass {
    name: string
    constructor(name: string){
        this.name = name
    }
    public sayHello() {
        console.log('hello');
    }
}

class testClass extends myClass {
    age:number
    constructor(name: string, age:number) {
        super(name)
        this.age = age
    }
}
```



下面这段代码就可以看到运行顺序

```ts
class myClass {
    name: string = '林青霞'
    constructor(){
        console.log('旧名字', this.name);
    }

}

class testClass extends myClass {
    name: string = '张曼玉'
    constructor() {
        super()
        console.log('新名字', this.name);
    }
}

let test = new testClass()
// 打印的顺序
// 旧名字 林青霞
// 新名字 张曼玉  
```



## 7.泛型

![image-20231221152850775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231221152850775.png)

new Array()方法 和 fill方法

```ts
 let arr = new Array(1,2,3,4,5)
 console.log(arr); // [1,2,3,4,5]
 let arr1 = new Array(5)
 console.log(arr1); // [empty*5] 5个空数组
 let arr2 = new Array(4).fill(1)
 console.log(arr2); // [1,1,1,1]
```



```ts
// 使用泛型  定义的时候无需指定类型
let getArray = function <T>(value: T, items: number): T[] {
    // fill这个方法用来填充数组
    return new Array(items).fill(value);
}

let arr = getArray<string>('张三', 5); //  使用泛型  调用的时候指定类型
console.log(arr); // ['张三','张三','张三','张三','张三']
let res = arr.map(item => item.length) // 字符串有length
console.log(res);

let arr1 = getArray<number>(1, 5);
console.log(arr1); // [1,1,1,1,1]
let res1 = arr1.map(item => item.length) // 数字没有length,使用了泛型就可以检测到,在非编译阶段就报错
```



### 1.泛型约束

**由于泛型过于灵活,过于灵活也会造成很多报错，所以可以使用泛型接口来进行泛型的约束**

```ts
// 接口
interface ILength{
    length: number;
}
// 泛型继承接口
// 泛型为T 返回值为number
function getLength<T extends ILength>(arr: T): number{
    return arr.length;
}

let res1 = getLength('黄宇')
let res2 = getLength([1,2,3])
let res3 = getLength({length: 10})
```



### 2.泛型接口

```ts
// 定义接口时使用泛型约束
interface IPerson<T1, T2>{
    name: T1,
    age: T2
}

let p: IPerson<string, number> = {
    name: "张三",
    age: 18
}

// 泛型接口也可以拥有默认值
// 默认值只能是类型,而不是具体的值
interface IPerson1<T1=string, T2=number>{
    name: T1,
    age: T2
}

let p1: IPerson1 = {
    name: "张三",
    age: 18
}
```



### 3.泛型类

```ts
// 泛型类
class Person<T1, T2>{
    name: T1;
    age: T2;
    sex: T1

    constructor(name:T1, age:T2, sex:T1){
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
}

// 编译器自动推断T1 T2类型 要确保name和sex同类型
const p1 = new Person('张三', 18, '男');

// 明确指出类型 推荐
// 写法1
const p2 = new Person<string, number>('张三', 18, '男');
// 写法2
const p3:Person<string, number> = new Person('张三', 18, '男');
```



### 4.使用泛型参数进行约束

一个泛型必须包含在另一个泛型中

![image-20231225123940791](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225123940791.png)



没有约束前，代码不报错

![image-20231225124025912](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225124025912.png)

约束后

```ts
function getKeyProps<T, K extends keyof T>(obj: T, key: K){
    return obj[key]
}

let x = {a: '1', b: '2'}
let res = getKeyProps(x, 'a') // '1'
// let res1 = getKeyProps(x, 'c') // Error
```



## 8.补充

### 1.unknown类型

![image-20231225124255845](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225124255845.png)

```TS
// 1.任何类型都可以赋值给unknown类型
let str:unknown
str = 18
str = "18"
str = true

// 2.不能将unknown类型赋值给其它类型
let val:unknown
let num:number
// num = val 报错
// 解决方式
num = val as number // 类型断言跳过编译器
// 使用类型缩小
if(typeof val === 'number'){
    num = val
}

// 3.unknown与其它任何类型组成的交叉类型都是其它类型
// & 交叉类型
type MyType =  string & number // never类型 没这东西
type MyType1 =  string & unknown  // string类型

// 4.unknown除了与any以外,与其它类型组成的联合类型都是unknown类型 
type MyType2 = unknown | any // any类型
type MyType3 = unknown | string // unknown类型

// 5. never类型继承与unknown类型
type MyType4 = never extends unknown ? true : false // true
```



### 2.map类型

![image-20231225202158846](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225202158846.png)

```ts
const map = new Map()

map.set('1', 'one')
map.set('2', 'two')
map.set('3', 'three')

// 如果需要同时遍历键和值 有俩种方法
// 方法1
for (let [key, value] of map.entries()) {
    console.log(key, value)
}
for (let entries of map.entries()) {
    console.log(entries)
}

// 方法2
for (let [key, value] of map) {
    console.log(key, value);
}
```



### 3.索引类型

![image-20231225203447421](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225203447421.png)

```ts
// 需求: 获取指定对象部分属性的值,放在数组中返回
let obj = {
    name: 'zs',
    age: 20,
    sex: '男'
}

// T为泛型 K为继承自T的泛型
// 参数1: 对象 参数2:键值数组
function getObjValue<T, K extends keyof T>(obj:T, keys:K[]): T[K][]{
    let arr:T[K][] = [];
    // 对键值的数组进行遍历
    keys.forEach(key => {
        arr.push(obj[key])
    })
    return arr;
}

let res = getObjValue(obj, ['name', 'age'])
console.log(res);
```



### 4.条件类型

![image-20231225204211699](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225204211699.png)

```ts
// 1.条件类型的基本使用
type MyType<T> = T extends string ? string : any
type res = MyType<string> // string
type res1 = MyType<number> // any

// 2.解决函数重载
interface IName {
    name:string
}
interface IAge {
    age:number
}

// 如果T是继承自string就是IName 否则就是 IAge
type Condition<T> = T extends string ? IName : IAge
function reLoad<T extends string | number>(NameOrAge: T): Condition<T> {
    throw ''
}
reLoad('HuangYu')
reLoad(79)
```



### 5.分布式条件类型

![image-20231225210316648](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225210316648.png)

![image-20231225210149481](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225210149481.png)

![image-20231225210256642](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225210256642.png)



### 6.infer关键字

```ts

// 假如想获取数组里的元素类型。
// 如果是数组则返回数组中元素的类型，否则返回这个类型本身
type ID = number[]
type IName = string[]

type Unpacked<T> = T extends ID ? number : T extends IName ? string : T
type T1 = Unpacked<ID> // number
type T2 = Unpacked<IName> // string
type T3 = Unpacked<boolean> // boolean

// infer 关键字可以简化操作
type Unpacked2<T> = T extends Array<infer U> ? U : T;
type T4 = Unpacked2<ID> // number
type T5 = Unpacked2<IName> // string
type T6 = Unpacked2<boolean> // boolean

// infer 关键字可以推断出联合类型
type Foo<T> = T extends {a: infer U, b: infer U} ? U : never;
type T7 = Foo<{a: string, b: number}> // string | number
```



### 7.映射类型

#### 1.基本使用

通过已有的类型推断出新类型

```ts
// 旧类型
type Person = {
    name: string;
    age: number;
}

// 通过person类型映射一个只读的新类型
// 映射的类型不能添加新的
type ReadonlyPerson<T> = {
    readonly [P in keyof T]: T[P];
};
type res = ReadonlyPerson<Person>;

let obj: res = {
    name: '123',
    age: 123
}

// 通过person类型映射一个可选的新类型
type PartialTest<T> = {
    [P in keyof T]?: T[P];
}

// 简写上面代码
type Person1 = {
    name: string;
    age: number;
}
// 只读
type res1 = Readonly<Person1>;
// 可选
type res2 = Partial<Person1>;
```



#### 2.进阶

1.

```ts
// Record 映射类型 会将一个类型的所有属性值都映射到另一个类型上并创造一个新的类型
type Person = {
    name: string;
    age: number;
}
type Name = 'person' | 'animal'

// 想要谁为名称谁写前面, 底层属性写在后面
type NewType = Record<Name, Person>
let res:NewType = {
    person:{name: 'zs', age: 18},
    animal:{name: 'dog', age: 20}
}
```

2.

```ts
// Pick 映射类型 将原有类型中的部分内容映射到新类型中
interface Info {
    name: string
    age: number
}

type PartProp = Pick<Info, 'name'>
let res: PartProp = {name: 'zs'}
console.log(res);
```



### 8.其它公共类型

![image-20231225214629831](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225214629831.png)



## 9.Ts的兼容性

### 1.自动类型推论

![image-20231225214719596](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231225214719596.png)

```ts
// 根据初始值推论
let name = 'zs'
name = 'ls'
// name = 14 //报错
let arr = [0,1,null]
// arr = ['zs', null, undefined] //报错

// 不会进行推论
let age
age = 18
age = true

// 根据上下文推论
window.onmousedown = function (event) {
    event.clientX
}
```



### 2.对象类型兼容性

```ts
// 属性可多不可少
interface obj1 {
    name: string,
}

let o1 = {name: 'zs'}
let o2 = {name: 'zs', age: 18}
let o3 = {age: 18}

let obj1: obj1 = o1
obj1 = o2
// obj1 = o3  // error 至少需要一个name属性

// 不管嵌套多少层,类型必须一一对应,ts内部会进行递归检查
interface obj2 {
    name: string,
    children: {
        age: number,
    }
}

let o4 = {name: 'zs', children: {age: 18}}
let o5 = {name: 'zs', children: {age: true}}
let obj2:obj2 = o4
// obj2 = o5  // error 子属性age的类型必须和父属性children的类型一致
```



### 3.函数类型兼容性

```ts
// 参数个数可少不可多
let func1 = (x:number, y:string) => {}
let func2 = (x:number) => {}
// func1 = func2 // 正确 2赋值给1可以
// func2 = func1 // 错误 1赋值给2不可以

// 参数类型必须相同
let func3 = (x:string) => {}
let func4 = (x:string) => {}
let func5 = (x:number) => {}
// func3 = func4 // 正确
// func4 = func3 // 正确
// func5 = func4 // 错误

// 返回值类型必须相同
let func6 = (x:string) => 18
let func7 = (x:string) => 18
let func8 = (x:number) => '字符串'
// func6 = func7 // 正确
// func7 = func6 // 正确
// func8 = func7 // 错误
```

![image-20231227151731238](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227151731238.png)

函数重载的兼容性

可选参数及剩余参数的兼容性

视频地址：[50_对象类型的兼容性_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Wa411S7hr/?p=51&spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=0d0608d8a87b289f0f02f9f3332ce89b)

P51



### 4.枚举类型的兼容

都不兼容

```
1.数字枚举与数字不兼容
2.数字枚举与数字枚举不兼容
3.字符串枚举与字符串不兼容
4.字符串枚举与字符串枚举不兼容
```



### 5.类的兼容性

![image-20231227165510701](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227165510701.png)



### 6.泛型兼容性

![image-20231227165852048](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227165852048.png)



## 10.装饰器

![image-20231227170218915](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227170218915.png)



### 1.类的装饰器

![image-20231227170459805](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227170459805.png)

1.基本使用

```ts
// 装饰器的本质是一个函数
// 从外界接收装饰用来扩展自己

// 1.类装饰器的基本使用 缺点:不能传参
function fun1(constructor: any){
    // 往参数原型上添加一个name属性
    // 相当于往类的原型挂载了一个name属性
    constructor.prototype.name = '扩展名字:黄宇';
    // 挂载类的静态属性
    constructor.age = 18
}

// @fun1 ===> @fun1(Person)
@fun1
class Person{}

let p = new Person()
// @ts-ignore 取消下一行报错
console.log(p.name);
// @ts-ignore 取消下一行报错
console.log(Person.age);
```



2.装饰器工厂

```ts
function func(options:any){
    return function(target:any){
        target.prototype.username = options.name;
        target.prototype.age = options.age;
    }
}

// 这里相当于套了一层 调用了一次函数就可以传递参数 @func((User))
@func({
    name:'张三',
    age:20
})
class User{}

let user = new User();
// @ts-ignore
console.log(user.username,user.age); // 输出：张三 20
```



3.装饰器组合 nest.js用的非常多

代码

```ts
function demo1(target:any){
    console.log('demo1');
}
function demo2(){
    console.log('demo2');
    return function(target:any){
        console.log('demo2内部');
    }
}
function demo3(){
    console.log('demo3');
    return function(target:any){
        console.log('demo3内部');
    }
}
function demo4(target:any){
    console.log('demo4');
}

@demo1
@demo2()
@demo3()
@demo4
class User{}

let user = new User();
// 先从上下到下执行所有装饰器工厂，在从下至上执行所有类装饰器
```

![image-20231227174915274](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227174915274.png)

运行顺序

![image-20231227175218011](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227175218011.png)

### 2.类属性装饰器

4.类某个属性的装饰器

非传参写法

```ts
function demo(target:any, attr:any){
    // console.log(target, attr); // 类本身 属性
    target[attr] = '黄宇'
}

class User{
    @demo
    // @ts-ignore
    userName:string
}
let user = new User();
console.log(user.userName);
```

传参写法

```ts
function demo(options:any){
    return function(target:any, attr:any){
        target[attr] = options;
    }
}

class User{
    @demo('黄宇')
    // @ts-ignore
    userName:string
}
let user = new User();
console.log(user.userName);
```



### 3.类方法装饰器

![image-20231227181532240](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227181532240.png)

```ts
function demo(target:any, key:string, descriptor:PropertyDescriptor){
//    console.log(target); // 普通方法为类的原型 | 静态方法为类本身
//    console.log(key); // 方法名
      console.log(descriptor); // 方法修饰符 writable enumrable configurable
    descriptor.value = function(){
        return 'Hello,我是被修改后的宇宇'
    }
}

class User{
    @demo
    sayName(){
        console.log('hello,我是宇宇');
    }
}
let user = new User();
console.log(user.sayName()); // Hello,我是被修改后的宇宇
```



get和set访问器的装饰器也是和方法一样传入三个参数



### 4.参数的装饰器

![image-20231227220257314](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231227220257314.png)



### 5.例子

```ts
// 这东西一定不存在
const userInfo: any = undefined

function catchErrorDecorator(msg:string){
    return function(target: any, key: string, descriptor: PropertyDescriptor){
        const fn = descriptor.value // 记录旧函数
        descriptor.value = function(){
            try {
                fn()
            } catch (e) {
                console.log(msg);
            }
        }
    }
}

class User {
    @catchErrorDecorator('userInfo.name不存在')
    getName(){
        return userInfo.name
    }
    @catchErrorDecorator('userInfo.age不存在')
    getAge(){
        return userInfo.age
    }
}

let user = new User()
```



## 11.补充

### 1.混入

对象混入

```ts
let nameObj = {name:'王楚然'}
let ageObj = {age:23}
// 对象混入 让nameObj也拥有age属性
// Object.assign方法用于对象的合并，将源对象（ source ）的所有可枚举属性，复制到目标对象（ target ）
Object.assign(nameObj,ageObj)
```



![image-20240102220337133](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240102220337133.png)



类混入

```ts
// 类混入
class Name {
    name:string = '王楚然'
    getName(){
        console.log('我是王楚然');
    }
}

class Age {
    age:number = 23
    getAge(){
        console.log('我今年23岁');
    }
}

class Person implements Name,Age{
    // 实现接口
    name:string
    age:number
    getName: () => void
    getAge: () => void
}

// 定义混入函数 
// target 表示Person from 表示 Name和Age类
function mixins(target: any, from:any[]){
    from.forEach(item => {
        Object.getOwnPropertyNames(item.prototype).forEach(name => {
            target.prototype[name] = item.prototype[name]
        })
    })
}

// 调用混入函数
mixins(Person, [Name, Age])
let person = new Person()
person.getName()
person.getAge()
```



## 12.ts中的模块

![image-20231228221244099](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231228221244099.png)

js中的模块

![image-20231228221458664](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231228221458664.png)

node中的模块

![image-20231228221536418](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231228221536418.png)

ts中的模块

导入

```ts
export const obj = {
    name: '王楚然',
    age: 24
}

export const arr = [1, 2, 3]
```

使用

```ts
// 默认情况js中时不兼容上面俩种导入方式混合使用，而ts对它们进行了综合
// 这俩种方式都可以使用,NODE和js默认的都可以使用
import { obj } from './02'
console.log(obj);

import module = require('./02')
console.log(module.arr);
```



### 1.命名空间

![image-20231228222415222](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231228222415222.png)

单文件内使用

```ts
namespace A {
    export const a = 10
}
console.log(A.a);

// 嵌套的命名空间
namespace B {
    export const b = 20
    export namespace C {
        export const b = 30
    }
}
console.log(B.b);
console.log(B.C.b);

// 命名空间可以进行简化
import b = B.C.b
console.log(b);
```

导出给其它文件使用

定义

```ts
export namespace A {
    export const a = 10
    export const name = '王楚然'
}
```

使用

```ts
import { A } from './02'
console.log(A.a);
console.log(A.name);
```



### 2.三斜杠语法

在不同文件中(模块)使用命名空间更推荐使用这种语法导入导出

导出

```ts
// 三斜杆语法不能加上export
namespace User {
    export const name =  '王楚然'
    export const age = 25
}
```

导入

```ts
export default{}
/// <reference path="./02.ts" />
const name = User.name
console.log(name);
```



### 3.声明合并

![image-20231228224245175](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231228224245175.png)



## 13.ts配置文件

### 1.ts配置文件

```json
{
  "compilerOptions": {
    /////////////////////////////////////////////////////////////////////////////////////////////////////////

    /* 项目 */
    "incremental": true,              /* 启用增量编译 */

    /* 语言和环境 */
    "target": "es2016",               /* 设置 JavaScript 语言版本 */

    /* 模块 */
    "module": "es6",                  /* 指定生成什么模块代码 */
    "rootDir": "./src",               /* 指定源文件的根文件夹 */
    "resolveJsonModule": true,        /* 启用导入 .json 文件 */
    "moduleResolution": "node",       /* 指定 TypeScript 如何从给定的模块说明符中查找文件(为了向后兼容，不用管) */

    /* JavaScript 支持 */
    "allowJs": true,                  /* 允许 JavaScript 文件成为您程序的一部分。使用 `checkJS` 选项从这些文件中获取错误 */
    "checkJs": true,                  /* 在类型检查的 JavaScript 文件中启用错误报告 */

    /* 输出?(Emit) */
    // "declaration": true,           /* 从项目中的 TypeScript 和 JavaScript 文件生成 .d.ts 文件 */
    // "declarationMap": true,        /* 为 d.ts 文件创建源映射 */
    // "emitDeclarationOnly": true,   /* 只输出 d.ts 文件而不输出 JavaScript 文件 */
    "sourceMap": true,                /* 为创建的 JavaScript 文件创建源映射文件(生产环境不需要) */
    // "inlineSourceMap": true,       /* 在输出的 JavaScript 中写入映射文件位置(生产环境不需要) */
    "noEmitOnError": true,            /* 如果发现任何类型检查错误，则停止编译并不输出编译结果 */
    "outDir": "./build",              /* 为所有输出文件指定一个输出文件夹 */
    // "declarationDir": "./",        /* 指定生成的声明文件的输出目录. */
    // "importHelpers": true,         /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "noEmitHelpers": true,         /* 禁止在编译输出中生成自定义辅助函数，如`__extends`. */

    /* 类型检查 */
    "strict": true,                                      /* 启用所有严格的类型检查选项 */

    /* 互操作约束 */
    // "allowSyntheticDefaultImports": true,             /* 当模块没有默认导出时允许 `import x from y` */
    "esModuleInterop": true,                             /* 发出额外的 JavaScript 以简化对导入 CommonJS 模块的支持。这将启用 `allowSyntheticDefaultImports` 以实现类型兼容性 */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* 完整性 */
    // "skipDefaultLibCheck": true,                      /* 跳过 TypeScript 中包含 .d.ts 文件的类型检查 */
    "skipLibCheck": true                                 /* 跳过所有 .d.ts 文件类型检查. */

    /////////////////////////////////////////////////////////////////////////////////////////////////////////
    /* 项目 */
    // "incremental": true,                              /* 启用增量编译 */
    // "composite": true,                                /* 启用允许 TypeScript 项目与项目引用一起使用的约束 */
    // "tsBuildInfoFile": "./",                          /* 指定增量编译文件的文件夹(默认`.tsbuildinfo`) */
    // "disableSourceOfProjectReferenceRedirect": true,  /* 在引用复合项目时禁用首选源文件而不是声明文件 */
    // "disableSolutionSearching": true,                 /* 编辑时从多项目参考检查中选择一个项目 */
    // "disableReferencedProjectLoad": true,             /* 减少 TypeScript 自动加载的项目数量 */

    /* 语言和环境 */
    // "target": "es2016",                               /* 设置 JavaScript 语言版本 */
    // "lib": [],                                        /* 指定一组描述目标运行时环境的捆绑库声明文件. */
    // "jsx": "preserve",                                /* 指定生成什么 JSX 代码 */
    // "experimentalDecorators": true,                   /* 启用对 TC39 stage 2 草稿装饰器的实验性支持 */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files */
    // "jsxFactory": "",                                 /* 指定针对 React JSX 发出时使用的 JSX 工厂函数，例如'React.createElement' 或 'h' */
    // "jsxFragmentFactory": "",                         /* 指定在针对 React JSX 发出时用于片段的 JSX 片段引用，例如'React.Fragment' 或 'Fragment' */
    // "jsxImportSource": "",                            /* 指定用于在使用 `jsx: react-jsx` 时导入 JSX 工厂函数的模块说明符 */
    // "reactNamespace": "",                             /* 指定为 `createElement` 调用的对象。这仅适用于针对 `react` JSX 发出的 */
    // "noLib": true,                                    /* 禁用包括任何库文件，包括默认的 lib.d.ts */
    // "useDefineForClassFields": true,                  /* 发出符合 ECMAScript 标准的类字段 */

    /* 模块 */
    // "module": "commonjs",                             /* 指定生成什么模块代码 */
    // "rootDir": "./",                                  /* 指定源文件的根文件夹 */
    // "moduleResolution": "node",                       /* 指定 TypeScript 如何从给定的模块说明符中查找文件(为了向后兼容，不用管) */
    // "baseUrl": "./",                                  /* 指定解析非绝对路径模块名时的基准目录 */
    // "paths": {},                                      /* 一些将模块导入重新映射到相对于 baseUrl 路径的配置 */
    // "rootDirs": [],                                   /* 告诉编译器有许多“虚拟”的目录作为一个根目录。这将会允许编译器在这些“虚拟”目录中解析相对应的模块导入，就像它们被合并到同一目录中一样。 */
    // "typeRoots": [],                                  /* 指定"@types"包的路径，默认为 `./node_modules/@types`. */
    // "types": [],                                      /* 当 types 被指定，只有列出的包才会被包含在全局范围内 */
    // "allowUmdGlobalAccess": true,                     /* 允许从模块访问 UMD 全局变量 */
    // "resolveJsonModule": true,                        /* 启用导入 .json 文件 */
    // "noResolve": true,                                /* 禁止 `import`s、`require`s 或 `<reference>`s 扩展 TypeScript 应该添加到项目中的文件数量. */

    /* JavaScript 支持 */
    // "allowJs": true,                                  /* 允许 JavaScript 文件成为您程序的一部分。使用 `checkJS` 选项从这些文件中获取错误 */
    // "checkJs": true,                                  /* 在类型检查的 JavaScript 文件中启用错误报告 */
    // "maxNodeModuleJsDepth": 1,                        /* 指定用于从“node_modules”检查 JavaScript 文件的最大文件夹深度。仅适用于 `allowJs` */

    /* 发射? */
    // "declaration": true,                              /* 从项目中的 TypeScript 和 JavaScript 文件生成 .d.ts 文件 */
    // "declarationMap": true,                           /* 为 d.ts 文件创建源映射 */
    // "emitDeclarationOnly": true,                      /* 只输出 d.ts 文件而不输出 JavaScript 文件 */
    // "sourceMap": true,                                /* 为创建的 JavaScript 文件创建源映射文件 （source map) */
    // "outFile": "./",                                  /* 如果被指定，所有全局(非模块)文件将被合并到指定的单个输出文件中。如果 `declaration` 为 true，则还指定一个文件，该文件捆绑了所有 .d.ts 输出。如果 module 为 system 或 amd，所有模块文件也将在所有全局内容之后被合并到这个文件中 */
    // "outDir": "./",                                   /* 为所有输出文件指定一个输出文件夹 */
    // "removeComments": true,                           /* 移除注释. */
    // "noEmit": true,                                   /* 禁止编译器生成文件(只是运行检查) */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types */
    // "downlevelIteration": true,                       /* 为迭代发出更合规但冗长且性能较低的 JavaScript. */
    // "sourceRoot": "",                                 /* 为调试器指定根路径以参考源代码. */
    // "mapRoot": "",                                    /* 指定调试器应从指定路径获取映射文件而不是从生成位置 */
    // "inlineSourceMap": true,                          /* 在输出的 JavaScript 中写入映射文件位置 */
    // "inlineSources": true,                            /* 在输出的 JavaScript 中的源映射中包含源代码 */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* 设置输出文件的换行符 */
    // "stripInternal": true,                            /* 禁用在其 JSDoc 注释中包含 `@internal` 的发出声明 */
    // "noEmitHelpers": true,                            /* 禁止在编译输出中生成自定义辅助函数，如`__extends`. */
    // "noEmitOnError": true,                            /* 如果发现任何类型检查错误，则停止编译并不输出编译结果 */
    // "preserveConstEnums": true,                       /* 在生成的代码中禁用擦除 `const enum` 声明 */
    // "declarationDir": "./",                           /* 指定生成的声明文件的输出目录. */
    // "preserveValueImports": true,                     /* 保留 JavaScript 输出中未使用的导入 */

    /* 互操作约束 */
    // "isolatedModules": true,                          /* 确保每个文件都可以安全地转译，而不依赖于其他导入 */
    // "allowSyntheticDefaultImports": true,             /* 当模块没有默认导出时允许 `import x from y` */
    // "esModuleInterop": true,                          /* 发出额外的 JavaScript 以简化对导入 CommonJS 模块的支持。这将启用 `allowSyntheticDefaultImports` 以实现类型兼容性 */
    // "preserveSymlinks": true,                         /* 禁用解析符号链接到其真实路径。这与节点中的相同标志相关 */
    // "forceConsistentCasingInFileNames": true,         /* Ensure that casing is correct in imports. */

    /* 类型检查 */
    // "strict": true,                                   /* 启用所有严格的类型检查选项 */
    // "noImplicitAny": true,                            /* 为带有隐含“any”类型的表达式和声明启用错误报告。 */
    // "strictNullChecks": true,                         /* 类型检查时，考虑`null`和`undefined` */
    // "strictFunctionTypes": true,                      /* 分配函数时，检查以确保参数和返回值是子类型兼容的 */
    // "strictBindCallApply": true,                      /* 检查`bind`、`call` 和`apply` 方法的参数是否与原始函数匹配 */
    // "strictPropertyInitialization": true,             /* 检查在构造函数中声明但未设置的类属性 */
    // "noImplicitThis": true,                           /* 当 `this` 的类型为 `any` 时启用错误报告 */
    // "useUnknownInCatchVariables": true,               /* 将 catch 子句变量输入为“unknown”而不是“any” */
    // "alwaysStrict": true,                             /* 确保始终启用 'use strict' */
    // "noUnusedLocals": true,                           /* 未读取局部变量时启用错误报告 */
    // "noUnusedParameters": true,                       /* 未读取函数参数时引发错误 */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* 为未在函数中显式返回的代码路径启用错误报告. */
    // "noFallthroughCasesInSwitch": true,               /* 为 switch 语句中的失败案例启用错误报告 */
    // "noUncheckedIndexedAccess": true,                 /* Include 'undefined' in index signature results */
    // "noImplicitOverride": true,                       /* 确保派生类中的覆盖成员使用覆盖修饰符进行标记 */
    // "noPropertyAccessFromIndexSignature": true,       /* 强制对使用索引类型声明的键使用索引访问器 */
    // "allowUnusedLabels": true,                        /* 禁用未使用标签的错误报告 */
    // "allowUnreachableCode": true,                     /* 禁用无法访问代码的错误报告 */

    /* 完整性 */
    // "skipDefaultLibCheck": true,                      /* 跳过 TypeScript 中包含 .d.ts 文件的类型检查 */
    // "skipLibCheck": true                              /* 跳过所有 .d.ts 文件类型检查. */
  }
}
```



### 2.rollup打包ts文件

rollup、webpack、vite比较https://juejin.cn/post/7097493230572273700#heading-15

![image-20231230110017565](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230110017565.png)

package.json

```json
{
  "name": "rolluptest",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "cross-env NODE_ENV=production rollup -c", // 生产环境打包
    "dev": "cross-env NODE_ENV=development rollup -c -w" // 开发环境打包
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "cross-env": "^7.0.3",
    "rollup-plugin-livereload": "^2.0.5",
    "rollup-plugin-serve": "^2.0.0",
    "rollup-plugin-terser": "^7.0.2",
    "rollup-plugin-typescript2": "^0.36.0",
    "typescript": "^5.3.3"
  }
}
```



rollup.config.js

```ts
import path from 'path' // node核心模块
import ts2 from 'rollup-plugin-typescript2' // ts 转换器
import serve from 'rollup-plugin-serve' // rollup web服务
import livereload from 'rollup-plugin-livereload' // 热更新
import { terser } from 'rollup-plugin-terser' // 代码压缩

export default {
    input: './src/index.ts', // ts文件

    // 输出的文件
    output: {
        file: path.resolve(__dirname, './dist/index.js'),
        sourcemap: true, // 谷歌控制台显示源代码(ts配置文件中的这一项也要设置为true)
        format: 'umd' // 文件输出格式   UMD模块可以同时支持在浏览器环境和 Node.js 环境中使用。
    },

    plugins: [
        ts2(),// 开启ts转换
        livereload(),// 开启热更新
        terser(),// 开启代码压缩
        serve({
            open: true, // 自动打开浏览器
            port: 8080, // 设置服务启动端口号
            openPage: '/public/index.html' // 打开的页面
        })
    ]
}

// 打印环境变量 判别是生产环境还是开发环境
console.log(process.env.NODE_ENV);
```

tsconfig.json

```json
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for legacy experimental decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
    // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
    // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

    /* Modules */
    "module": "es6",  // 开启es6                              /* Specify what module code is generated. */
    // "rootDir": "./",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node10",                     /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
    // "allowImportingTsExtensions": true,               /* Allow imports to include TypeScript file extensions. Requires '--moduleResolution bundler' and either '--noEmit' or '--emitDeclarationOnly' to be set. */
    // "resolvePackageJsonExports": true,                /* Use the package.json 'exports' field when resolving package imports. */
    // "resolvePackageJsonImports": true,                /* Use the package.json 'imports' field when resolving imports. */
    // "customConditions": [],                           /* Conditions to set in addition to the resolver-specific defaults when resolving imports. */
    // "resolveJsonModule": true,                        /* Enable importing .json files. */
    // "allowArbitraryExtensions": true,                 /* Enable importing files with any extension, provided a declaration file is present. */
    // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    "sourceMap": true,   // 控制台显示源代码                                /* Create source map files for emitted JavaScript files. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
    // "outDir": "./",                                   /* Specify an output folder for all emitted files. */
    // "removeComments": true,                           /* Disable emitting comments. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types. */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */
    // "preserveValueImports": true,                     /* Preserve unused imported values in the JavaScript output that would otherwise be removed. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "verbatimModuleSyntax": true,                     /* Do not transform or elide any imports or exports not marked as type-only, ensuring they are written in the output file's format based on the 'module' setting. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                          /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}
```

项目文件夹截图

![image-20231230131438371](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230131438371.png)





### 3.webpack打包ts文件

![image-20231230142809106](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230142809106.png)

遇到了开发依赖不行，只能用全局安装webpack 和 webpack-cli的方式来解决

package.json

```json
{
  "name": "webpacktest",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "dev": "webpack serve --open"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "html-webpack-plugin": "^5.6.0",
    "ts-loader": "^9.5.1",
    "typescript": "^5.3.3",
    "webpack": "^5.89.0",
    "webpack-cli": "^5.1.4",
    "webpack-dev-server": "^4.15.1"
  }
}
```

webpack.config.js

```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    // 入口文件
    entry: './src/index.ts',
    
    // 输出文件
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'index.js'
    },

    // 模块配置
    module: {
        rules: [
            // TypeScript 文件的处理规则
            // 这个配置告诉 Webpack 当遇到 TypeScript 文件时，使用 ts-loader 进行加载和转译，
            // 但排除 node_modules 中的文件。这通常是在使用 TypeScript 进行项目开发时的常见配置。
            { test: /\.ts$/, use: 'ts-loader', exclude: /node_modules/ }
        ]
    },

    // 构建模式，这里是开发模式
    mode: 'development',

    // 解析模块请求的选项
    resolve: {
        // 指定扩展名，使导入文件时可以省略文件后缀
        extensions: ['.ts', '.js']
    },

    // 插件配置
    plugins: [
        // 自动生成 HTML 文件并引入打包后的 JavaScript 文件
        new HtmlWebpackPlugin({
            template: './public/index.html'
        })
    ]
};
```



### 4.描述声明文件 xx.d.ts

![image-20231230152241896](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230152241896.png)

**就是在ts中使用了js包，但是js包不能使用ts特性,所以需要我们引入描述声明文件,为js文件加上类型特性**

![image-20231230152824645](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230152824645.png)

执行完命令就不报错了



手写一个库导入项目

库 demo.js

![image-20231230153327979](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230153327979.png)

导入(在html引入相当就在项目中引入了)

![image-20231230153247401](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230153247401.png)

demo.js的声明文件 demo.d.ts

![image-20231230153402129](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231230153402129.png)



### 5.搭建vue+ts环境

![image-20231230154603022](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20231230154603022.png)

ts项目多了ts配置文件



### 6.搭建react+ts环境

![image-20231231133431936](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231231133431936.png)

```bash
$ cd 项目目录
$ npm start
```

