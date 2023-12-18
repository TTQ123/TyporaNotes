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

接口比抽象类好的就是 接口可以有多个 抽象类只能有一个

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

