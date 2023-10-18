## 1.ES6特性

```js
// 1.展开运算符的使用
// 1.1
const arr1 = [1,2,3]
const arr2 = [4,...arr1,5]

// 1.2
const obj1 = {
    name:'Hy',
    age:'18'
}
const obj2 = {
    gender:'男',
    ...obj1 // 将obj1 放入obj2中
}

// 1.3
const {name, age, ...other} = { //将对象的剩余属性展开到other中
    name:'Hy',
    age:18,
    gender:'男',
    address:'不知道'
}

// console.log(other);

// 2.Array.from 将一个伪数组转换为数组
function fn(){
    console.log(Array.from(arguments))
}
// fn(1,2,3,4)

// 3.Object.assign()
const objA = {
    name:'Hy'
}

const objB = {
    age:18
}

const objC = Object.assign({},objA) //浅拷贝
const objD = Object.assign({},objA,objB) //可以多个

// 4.Class
class A {
    constructor(name,age){
        this.name = name
        this.age = age
    }

    sayHello1(){
        console.log('你好'+this.name)
    }
}

const a1 = new A('Hy',28) //创建实例对象

class B extends A { //继承
    constructor(name,age,gender){
        super(name,age) //调用父类的构造方法 将父类的属性在子类也生成
        this.gender = gender
    }

    sayHello2(){
        console.log(11121);
    }
}

const B1 = new B('Hy',28,'男')

// 5.箭头函数 const fn = (参数1,参数2) => 返回值

const getSum1 = n => n+3
const getSum2 = (n1,n2) => n1+n2
const getSum3 = (n1,n2,...other) => console.log(n1,n2,other)
const getSum = arr => {
    let sum = 0
    arr.forEach(item => sum += item)
    return sum  // 需要指定返回值
}

```



## 2.ES6Promise

```js
const p1 = new Promise((resolve, reject) => {
    resolve('任务1成功返回')
    // reject('任务失败')
})

// then用来接收promise成功的数据
p1.then(data => {
    console.log(data);
    return new Promise((resolve, reject) => {
        resolve('任务2成功返回')
    })
}, err => {
    console.log('任务1失败了')
    // 可以抛出异常让后续都不执行
    throw new Error('任务1失败,后续都不执行')
})
// 用来接收第二个异步的promise结果
.then(data => {
    console.log(data)
}, err => {
    console.log('任务2失败了')
})
// 找不到当前的catch最终会找到最后的catch
.catch(err => {
    console.log('统一的失败失败'+ err);
})
.finally(()=>{
    console.log('成功或失败我都会执行')
})

// p1.then().then().catch().finally()  结构是同级的

// async 和 await  调用异步函数等待结果 达到类似同步的功能
function asyncTask () {
    return new Promise((resolve, reject) => {
        let flag = true // 标记成功
        if (flag) {
            resolve('成功执行')
        }else{
            reject('失败了')
        }
    })
}

console.log('任务1');
async function main () {
    const data = await asyncTask() //data接收异步调用的结果
    console.log('任务2');
    console.log(data);
}

main()

console.log('任务3');
```



## 3.Proxy

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="container">123</div>
    <script src="./b.js"></script>
</body>
</html>
```



js

```js
const obj = { name: '无忧', ahe: 18 }
const container = document.getElementById('container')
container.textContent = obj.name
console.log(container);

// 参数1:代理对象 参数2:配置项
const user1 = new Proxy(obj, {
    // 获取  参数1:数据对象(哪个数据被修改) 参数2:属性
    get(target, prop){
        return obj[prop]
    },
    // 设置  参数1:数据对象(哪个数据被修改) 参数2:属性 参数3:设置的值
    set(target, prop, value){
        console.log(target)
        obj[prop] = value //修改值
        container.textContent = obj.name // 呈现修改的值
    }
})

user1.name = 'jack'
```

