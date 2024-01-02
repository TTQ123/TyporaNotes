# Node.js

## 1.简介与安装

```css
Node.js
    - 运行在服务器端的js
    - 用来编写服务器
    - 特点：
        - 单线程、异步、非阻塞
        - 统一API
    - 缺点
	    - 大型项目运行速度不佳,毕竟只有一个线程
		- 只适合一些中小型项目

    nvm
        - 命令
            nvm list - 显示已安装的node版本
            nvm install 版本 - 安装指定版本的node
            配置nvm的镜像服务器
                nvm node_mirror https://npmmirror.com/mirrors/node/
            nvm use 版本 - 指定要使用的node版本
		   直接在官网下载的版本,不能灵活切换版本

    node.js和JavaScript有什么区别(宿主对象不一样,nodejs是服务器,js是浏览器)
        ECMAScript（node有） DOM（node没有） BOM（node没有）
	    但是nodejs中保留了一部分dom中好用的方法 例如输出语句以及定时器
```

**运行Node.js的方法**

![uTools_1676096873971](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676096873971.png)

![uTools_1676096916222](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676096916222.png)

**在Vscode中运行**

1. **ctrl+\打开vscode内置终端  在命令行运行,在终端输出**

2. **按f5选择Node执行  在调试控制台输出**



## 2.异步和同步

```javascript
/*
    进程和线程
        - 进程（厂房）
            - 程序的运行的环境
        - 线程（工人）
            - 线程是实际进行运算的东西
        - 线程进入进程中执行运算

    同步
        - 通常情况代码都是自上向下一行一行执行的
        - 前边的代码不执行后边的代码也不会执行
        - 同步的代码执行会出现阻塞的情况
        - 一行代码执行慢会影响到整个程序的执行

    解决同步问题：
        - java python
            - 通过多线程来解决(管理成本高,适合大型项目)
        - node.js
            - 通过异步方式来解决

    异步
        - 一段代码的执行不会影响到其他的程序
        - 异步的问题：
            异步的代码无法通过return来设置返回值(设置了return代表立即返回,同步的)
        - 特点：
            1.不会阻塞其他代码的执行
            2.需要通过回调函数(类似于手机)来返回结果
        - 基于回调函数的异步带来的问题
            1. 代码的可读性差
            2. 可调试性差
        - 解决问题：
            - 需要一个东西，可以代替回调函数来给我们返回结果
            - Promise横空出世
                - Promise是一个可以用来存储数据的对象(存储异步调用的代码)
                    Promise存储数据的方式比较特殊，
                    这种特殊方式使得Promise可以用来存储异步调用的数据
                    
    - 现实生活
        1.点菜
        2.厨师做菜(需要时间长,要等很久)
        3.吃
*/

/*
	下列代码输出顺序为111111,222222,579
		- 因为579采取了异步调用的方式,不会阻塞其它代码的执行
			- 原理是定时器把代码放到宏任务队列中了,这样会比调用栈的代码执行的更慢,从而不阻塞他人
*/
console.log("111111")

function sum2(a, b){
    const begin = Date.now()
    // 让程序停10秒
    while(Date.now() - begin < 10000){}
    return(a+b)//其它代码必须等它执行完才能执行
}


function sum(a,b,cb){
    setTimeout(()=>{
        //调用cb此时就是调用了传入的匿名函数,调cb就是再调函数
        //cb(a+b)=>>a+b的值计算后传给了result来接收(a+b就是传入的参数,也就是result的值)
        cb(a+b)
        //相当于cb(result=a+b){console.log(result)}
    },1000)
}

//result 此时会拿到回调函数cb的值传回来的值
//result只能在这个函数里得到值，在函数外面得不到
sum(123,456,(result)=>{console.log(result)})//执行结果为579



//如果要多次调用异步使用回调函数时就会产生问题
sum(123, 456, (result)=>{
    sum(result, 7, (result)=>{
        sum(result, 8, result => {
            sum(result, 9, result => {
                sum(result, 10, result => {
                    console.log(result)
                })
            })
        })
    })
})


console.log("222222") //如何解决这一行代码被阻塞(1.回调函数 然而回调函数太麻烦了 2.所以出现了Promise)
```



## 3.Promise

```javascript
//没有Promise时的
function sum(a, b, cb) {
    setTimeout(() => {
        cb(a + b)
    }, 1000)
}

const result = sum(123, 456, function(result) {
    console.log(result)
})

//上面的写法: sum(123,456,(result)=>{console.log(result)})

/* 
    异步调用必须要通过回调函数来返回数据，
        当我们进行一些复杂的调用的时，会出现“回调地狱”

    问题：
        异步必须通过回调函数来返回结果，回调函数一多就很痛苦

    Promise(Promise的中文意思是承诺)
        - Promise可以帮助我们解决异步中的回调函数的问题
        - Promise就是一个用来存储数据的容器
            它拥有着一套特殊的存取数据的方式
            这个方式使得它里边可以存储异步调用的结果
*/

// 创建Promise时，构造函数中需要一个函数作为参数
// Promise构造函数的回调函数，它会在创建Promise时调用，调用时会有两个参数传递进去
const promise = new Promise((resolve, reject) => {
    // resolve 和 reject 是两个函数，通过这两个函数可以向Promise中存储数据
    // resolve在执行正常时存储数据，reject在执行错误时存储数据
    // 通过函数来向Promise中添加数据，好处就是可以用来添加异步调用的数据
    setTimeout(() => {
        resolve("哈哈")//相当于前面的那个cb函数
    }, 2000)

    // throw new Error("哈哈，出错了")

    resolve("resolve返回的数据")
    reject("reject返回的数据")
})

/* 
    从Promise中读取数据
        - 可以通过Promise的实例方法then来读取Promise中存储的数据
        - then需要两个回调函数作为参数，回调函数用来获取Promise中的数据
            通过resolve存储的数据，会调用第一个函数返回，
                可以在第一个函数中编写处理数据的代码
        - then 方法获取容器的结果（成功的，失败的）
		 then 方法支持链式调用
		 以在 then 方法中返回一个 promise 对象，然后在后面的 then 方法中获取上一个 then 返回的 promise 对象的状态结果

            通过reject存储的数据或者出现异常时，会调用第二个函数返回
                可以在第二个函数中编写处理异常的代码

        - resolve 和 reject 是Promise自己创建的,result和resaon是我们自己创建来接收Promise中的数据的
*/

promise.then((result) => {
    console.log("1", result)
}, (reason) => {
    console.log("2", reason)
})//result接收成功的数据,reason接收错误的数据


/* 
    Promise中维护了两个隐藏属性：
        PromiseResult
            - 用来存储数据

        PromiseState
            - 记录Promise的状态（三种状态）
                pending   （进行中） 还没存入数据此时
                fulfilled（完成） 通过resolve存储数据时
                rejected（拒绝，出错了） 出错了或通过reject存储数据时
            - state只能修改一次，修改以后永远不会在变(要么变成fulfilled,要么变成rejected)
    
        流程：
            当Promise创建时，PromiseState初始值为pending，
                当通过resolve存储数据时 PromiseState 变为fulfilled（完成）
                    PromiseResult变为存储的数据
                当通过reject存储数据或出错时 PromiseState 变为rejected（拒绝，出错了）
                    PromiseResult变为存储的数据 或 异常对象(错误信息)

            当我们通过then读取数据时，相当于为Promise设置了回调函数，
                如果PromiseState变为fulfilled，则调用then的第一个回调函数来返回数据
                如果PromiseState变为rejected，则调用then的第二个回调函数来返回数据

            - then执行一定是比其它语句慢的
*/

const promise2 = new Promise((resolve, reject) => {
    resolve("哈哈")
    reject("哈哈")//这行代码不会执行了,因为State只能修改一次,Promise的数据不会被修改掉
})


promise2.then(result => {
    console.log(result)
}, reason => {
    console.log("出错了")
})

/* 
    catch() 用法和then类似，但是只需要一个回调函数作为参数
        catch()中的回调函数只会在Promise被拒绝时才调用(第二个)
        catch() 相当于 then(null, reason => {})
        catch() 就是一个专门处理Promise异常的方法

    finally() 
        - 无论是正常存储数据还是出现异常了，finally总会执行
        - 但是finally的回调函数中不会接收到数据
        - finally()通常用来编写一些无论成功与否都要执行代码(提示语句等)
*/

promise2.catch(reason => {
    console.log(222222)
})

promise2.finally(()=>{
    console.log("没有什么能够阻挡我执行的！")
})

// console.log(1111111)
//在使用then的时候都是只拿他的第一个回调函数的成功值的,错误交给后面的catch去拿结果和处理错误
```

```javascript
const promise1 = new Promise((resolve(执行),reject(拒绝)=>{
    throw(111)
    resolve("resolve返回的数据")
})

promise1.then((result 数据) => {
    console.log("1", result)
}, (reason 原因) => {
    console.log("2", reason)
})
```



## 4.Promise详解

```javascript
/* 
Promise就是一个用来存储数据对象
	但是由于Promise存取的方式的特殊，所以可以直接将异步调用的结果存储到Promise中
 	对Promise进行链式调用时
  	后边的方法（then和catch）读取的上一步的执行结果
    后边的方法读取的就是前边方法的值，如果上一步的执行结果不是当前想要的结果，则跳过当前的方法
      	- 例如第二步设置了catch(用来处理错误),然而接收到的数据是正常的,则会跳过当前这个catch语句
			- 我们使用Promise的时候通常只在最后处理错误
*/
/* 
    当Promise出现异常时，而整个调用链中没有出现catch，则异常会向外抛出
*/

const promise = new Promise((resolve, reject) => {
    reject("周一到周五19点，不见不散")
})

promise
    .then(r => console.log("第一个then", r))
    .catch(r => {
        throw new Error("报个错玩")//catch只处理它前面的错误,如果它自己出错以后会抛出去给后面的处理
        //所以开发的时候把catch一般放在最后一句可以处理所有错误
        console.log("出错了")
        return "嘻嘻"
    })
    .then(r => console.log("第二个then", r))
    .catch(r => {
        console.log("出错了")
    })

/* 
    promise中的方法
        then (return new Promise())
        catch
        - 这三个方法都会返回一个新的Promise,
            Promise中会存储回调函数的返回值
        finally
            - finally的返回值，不会存储到新的Promise中
            	- 返回一些不论成功与否都需要执行的代码，例如提示语句
*/

// 传统回调函数写法
// function sum(a, b, cb) {
//     setTimeout(() => {
//         cb(a + b)
//     }, 1000);
// }

// promise回调的固定写法
function sum(a, b) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(a + b)
        }, 1000)
    })
}
//resolve-result,reject-reason

// 但是这样调用利用了Promise的sum函数等于还是回调地狱
// sum(123, 456).then(result => {
//     sum(result, 7).then(result =>{
//         sum(result, 8).then(result => {
//             console.log(result)
//         })
//     })
// })

// Promise的链式调用
sum(123, 456)
     //箭头函数省略写法直接指向函数的返回值  相当于.then(result=>{return result+100})
    .then(result => result + 7)//只传一个参数,优先给第一个回调函数赋值(所以拿到的是result而不是reason)
    .then(result => result + 8)
    .then(result => console.log(result))
```

**Promise的静态方法**

```javascript
/* 
    静态方法(通过类直接调用,不用创建对象)
        Promise.resolve() 创建一个立即完成的Promise
        Promise.reject() 创建一个立即拒绝的Promise
        Promise.all([...]) 同时返回多个Promise的执行结果
            其中有一个报错，就返回错误
        Promise.allSettled([...]) 同时返回多个Promise的执行结果(无论成功或失败)
           {status: 'fulfilled', value: 579}
           {status: 'rejected', reason: '哈哈'}
        Promise.race([...]) 返回执行最快的Promise（不考虑对错）
        Promise.any([...]) 返回执行最快的完成的Promise(都报错才会跳出错误)
*/

Promise.resolve(10).then(r => console.log(r)) //10

Promise.reject("错误")

Promise.resolve(10)//和下面那个等价
new Promise((resolve, reject) => {
    resolve(10)
})

function sum(a, b) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(a + b)
        }, 1000)
    })
}

Promise.all([  //调用了3次sum其实就是创建了3个Promise,返回一个数组
    sum(123, 456),
    sum(5, 6),
    Promise.reject("此处出错了"),  //通过Promise.reject()使得程序报错,有一个报错就会返回错误
    sum(33, 44)
]).then(r => {
    console.log(r)
})

Promise.allSettled([ //返回一个对象数组
    sum(123, 456),
    sum(5, 6),
    Promise.reject("哈哈"), //无论失败成功都会返回
    sum(33, 44)
]).then(r => {
    console.log(r)
})

Promise.race([
    Promise.reject(1111), //立刻执行,返回的最快(不考虑对错)
    sum(123, 456),
    sum(5, 6),
    sum(33, 44)
]).then(r => {
    console.log(r)
}).catch(r => {
    console.log("错误")
})

Promise.any([//返回执行最快的完成的Promise(都报错才会跳出错误)
    Promise.reject(1111),
    Promise.reject(2222),
    Promise.reject(3333),
]).then(r => {
    console.log(r)
}).catch(r => {
    console.log("错误", r)
})

//vscode调试控制台不能直接点击查看 会报错
//需要在代码上打上断点才能查看
```



## 5.宏任务和微任务

```javascript
0.// 开启了一个定时器
// 定时器的作用是间隔一段时间后，将函数放入到任务队列中(宏任务)
 setTimeout(() => {
     console.log(1)//先排队后执行 最后执行
 }, 0)

/* 
     Promise的执行原理(then,catch都一样)
        - Promise在执行，then就相当于给了Promise回调函数
            当Promise的状态从pending 变为 fulfilled时，
                then的回调函数会被放入到任务队列中(微任务)
*/

Promise.resolve(1).then(() => {
     console.log(2)//第二执行
 })

console.log(3);//最先执行


/* 
    queueMicrotask()方法  用来向微任务队列中添加一个任务
*/


1.setTimeout(()=>{console.log(3);})//第3,加入宏任务队列的
  Promise.resolve().then(()=>{console.log(1);}) //第1,先加入微任务的
  queueMicrotask(() => {
     console.log(2) //第2,第2个加入微任务的
 })


2.// 套了一个定时器
Promise.resolve().then(() => {
     setTimeout(()=>{
         console.log(2) //后执行(微任务中的宏任务)
         //虽然Promise.resolve().then先执行了 但是里面的定时器还是要加入宏队列排队
     })
 })
 queueMicrotask(() => {
     console.log(1) 先执行
 })


3.Promise.resolve().then(() => {
     Promise.resolve().then(()=>{
         console.log(1) //后执行
         //一开始俩个人排队 此时执行完以后继续向队列里添加任务 所以第二个先执行了
     })
 })
 queueMicrotask(() => {
     console.log(2)//先执行
 })


 4.// 阅读下列代码，并说出执行结果：
    
    console.log(1);  1

    setTimeout(() => console.log(2));  5

    Promise.resolve().then(() => console.log(3)); 3

    Promise.resolve().then(() => setTimeout(() => console.log(4))); 7

    Promise.resolve().then(() => console.log(5)); 4

    setTimeout(() => console.log(6)); 6

    console.log(7); 2



/* 
    JS是单线程的，它的运行时基于事件循环机制（event loop）
        - 调用栈
            - 栈
                栈是一种数据结构，后进先出
            - 调用栈中，放的是要执行的代码
        - 任务队列
            - 队列
                - 队列是一种数据结构，先进先出
            - 任务队列的是将要执行的代码
            - 当调用栈中的代码执行完毕后，队列中的代码才会按照顺序依次进入到栈中执行
            - 在JS中任务队列有两种
                - 宏任务队列 （大部分代码都去宏任务队列中去排队）
                - 微任务队列 （Promise的回调函数（then、catch、finally））
            - 整个流程
                ① 执行调用栈中的代码
                ② 执行微任务队列中的所有任务
                ③ 执行宏任务队列中的所有任务
*/

//await和async是Promise还没出来时搞的,它的执行比微任务还快一点。

    /*
        所以完整的代码执行顺序就是
            1.同步代码
            2.await当函数执行完后
            3.微任务(promise)
            4.宏任务
    */
```

**Node的内存执行原理**

![uTools_1676293826582](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676293826582.png)



## 6.手写Promise

```javascript
/* 
    定义类的思路
        1. 先把功能都分析清楚了，在动手
        2. 写一点想一点，走一步看一步
*/

const PROMISE_STATE = {
    PENDING: 0,
    FULFILLED: 1,
    REJECTED: 2
}

class MyPromise {

    // 创建一个变量用来存储Promise的结果
    #result
    // 创建一个变量来记录Promise的状态
    #state = PROMISE_STATE.PENDING //pending 0 fulfilled 1 rejected 2

    // 创建一个变量来存储回调函数
    // 由于回调函数可能有多个，所以我们使用数组来存储回调函数
    #callbacks = []

    constructor(executor) {
        // 接收一个 执行器 作为参数
        executor(this.#resolve.bind(this), this.#reject.bind(this)) // 调用回调函数
    }

    // 私有的resolve() 用来存储成功的数据
    #resolve(value) {
        // 禁止值被重复修改
        // 如果state不等于0，说明值已经被修改 函数直接返回
        if (this.#state !== PROMISE_STATE.PENDING) return

        this.#result = value
        this.#state = PROMISE_STATE.FULFILLED // 数据填充成功

        // 当resolve执行时，说明数据已经进来了，需要调用then的回调函数
        queueMicrotask(() => {
            // 调用callbacks中的所有函数
            this.#callbacks.forEach(cb => {
                cb()
            })
        })
    }

    // #resolve = () => {
    //     console.log(this)
    // }

    // 私有的reject() 用来存储拒绝的数据
    #reject(reason) { }


    // 添加一个用来读取数据的then方法
    then(onFulfilled, onRejected) {

        /* 
            谁将成为then返回的新Promise中的数据？？？
                then中回调函数的返回值，会成为新的Promise中的数据
        */

        return new MyPromise((resolve, reject) => {
            if (this.#state === PROMISE_STATE.PENDING) {
                // 进入判断说明数据还没有进入Promise，将回调函数设置为callback的值
                // this.#callback = onFulfilled
                this.#callbacks.push(() => {
                    resolve(onFulfilled(this.#result))
                    
                })
            } else if (this.#state === PROMISE_STATE.FULFILLED) {
                /* 
                    目前来讲，then只能读取已经存储进Promise的数据，
                        而不能读取异步存储的数据
                */
                // onFulfilled(this.#result)

                /* 
                    then的回调函数，应该放入到微任务队列中执行，而不是直接调用
                */
                queueMicrotask(() => {
                    resolve(onFulfilled(this.#result))
                })
            }

        })
    }


}

const mp = new MyPromise((resolve, reject) => {
    setTimeout(() => {
        resolve("孙悟空")
    }, 1000)
})

mp.then((result) => {
    console.log("读取数据1", result)
    return "猪八戒"
}).then(r => {
    console.log("读取数据2", r)
    return "沙和尚"
}).then(r => {
    console.log("读取数据3", r)
})

// const p = Promise.resolve('孙悟空')

// p.then(r => console.log("第一次读", r))
// p.then(r => console.log("第二次读", r))
```



## 7.async和await(面试题)

```javascript
/* 
    nodejs文档：
        https://nodejs.dev/en/

    通过async可以快速的创建异步函数
*/
function fn() {
    return Promise.resolve(10)
}

/* 
    通过async可以来创建一个异步函数
        异步函数的返回值会自动封装到一个Promise中返回
    
    在async声明的异步函数中可以使用await关键字来调用异步函数
*/
async function fn2() {
    return 10
}

// fn和fn2函数是等价的
// fn().then(r => {
//     console.log(r)
// })

// fn2().then(r => {
//     console.log(r)
// })


/* 
    Promise解决了异步调用中回调函数问题，
        虽然通过链式调用解决了回调地狱，但是链式调用太多以后还是不好看，我多想以同步的方式去调用异步的代码
*/
function sum(a, b) {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve(a + b)
        }, 2000);
    })
}

❤❤//await的意思是等待,本行代码会立即执行(直接放栈中执行),因为要拿到结果才会向下继续执行
async function fn3() {
    // 传统写法
    // sum(123, 456)
    //     .then(r => sum(r, 8))
    //     .then(r => sum(r, 9))
    //     .then(r => console.log(r))

    // 当我们通过await去调用异步函数时，它会暂停代码的运行
    // 直到异步代码执行有结果时，才会将结果返回
    // 注意:await只能用于async声明的异步函数中，或es模块的顶级作用域中
    // await阻塞的知识异步函数内部的代码，不会影响外部代码
    // 通过await调用异步代码时，需要通过try-catch来处理异常

    //这就解决了链式调用多次不好看的情况
    try {
        let result = await sum(123, 456)
        result = await sum(result, 8)
        result = await sum(result, 9)
        console.log(result)
    } catch (e) {
        console.log("出错了~~")
    }

}

fn3()


//如果async声明的函数中没有写await，那么它里边就会依次执行
async function fn4(){
    console.log(1)
    console.log(2)
    console.log(3)
}

//fn4和fn5是等价的

function fn5(){
    return new Promise(resolve => {
        console.log(1)
        console.log(2)
        console.log(3)
        resolve()
    })
} 

async function fn4() {
    console.log(1)//第一
    
    //当我们使用await调用函数后，当前函数后边的所有代码, 会在当前函数执行完毕后，被放入到微任务队里中
    await console.log(2)//第二

    // await后边的所有代码，都会放入到微任务队列中执行
    console.log(3)//第四
}
 console.log(4)//第三

//fn4和fn5等价

function fn5() {
    return new Promise(resolve => {
        console.log(1)//第一
        //因为2加了await，s所以2后面的代码放到一个then中(微任务队列中)
        console.log(2)//第二
        resolve()
    }).then(r => {
        console.log(3)//第四
    })
}
fn5()

console.log(4)//第三


//await在非模块中调用要用异步的方式
async function fn6(){
     await console.log("哈哈")
 }
fn6()

//这俩个是等价的
//不想使用异步的方式可以使用匿名立即执行函数
;(async () => {
    await console.log("哈哈")
})()

```



## 总结:Node中代码的执行顺序(面试)

```css
        调用栈
        tick队列
        微任务队列
        宏任务队列
        特殊情况:await 后的代码会放入微任务队列中(await这一行会立即执行,有时候比调用栈还快)
```

**例子**

```javascript
;(async () => {
    await console.log(1)//第一,被放入调用栈中立即执行
    console.log(4);//第四,被放入微任务队列中,先排队
})()

process.nextTick(() => {
    console.log(3) // 第三,tick队列(在微任务之前执行)
})

queueMicrotask(() => {
    console.log(5)// 第5,微任务队列,后排队
}) 

setTimeout(() => {
    console.log(6) // 第6,宏任务队列，最后执行
})

console.log(2);//第二,调用栈中的代码
```

**执行顺序**

![uTools_1679289264250](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679289264250.png)



## 8.模块化

```bash
1.ES模块化是在浏览器中使用的，要在node中使用要进行配置，commjs是node默认支持的模块化

2.这俩种模块化规范都可以在浏览器和服务器(node)中使用，但是需要进行配置
```



### 1.commonJS

```javascript
/* 
    早期的网页中，是没有一个实质的模块规范的
        我们实现模块化的方式，就是最原始的通过script标签来引入多个js文件
        问题：
            1. 无法选择要引入模块的哪些内容
            2. 在复杂的模块场景下非常容易出错
            ......
        于是，我们就继续在js中引入一个模块化的解决方案

    在node中，默认支持的模块化规范叫做CommonJS，
        在CommonJS中，一个js文件默认就是一个模块

    CommonJS规范
        - 引入模块
            - 使用require("模块的路径")函数来引入模块
            - 引入自定义模块时
                - 模块名要以./ 或 ../开头
                - 扩展名可以省略
                    - 在CommonJS中，如果省略的js文件的扩展名
                        node，会自动为文件补全扩展名
                            ./m1.js 如果没有js 它会寻找 ./m1.json
                            js --> json --> node（特殊）
            - 引入核心模块时
                - 直接写核心模块的名字即可
                - 也可以在核心模块前添加 node:
*/
const m1 = require("./m1")//引入mi.js文件

const path1 = require("path") //引入核心模块path
const path2 = require("node:path") //引入核心模块path

const m2 = require("./m2.cjs")//ES Modules模块的引入要把文件设置为.cjs

const hello = require("./hello") // ./hello/index.js

// console.log(m1)
// m1.c()

console.log(hello)
```



### 2.如何暴露内容

```javascript
/* 
    在定义模块时，模块中的内容默认是不能被外部看到的
        可以通过exports来设置要向外部暴露的内容

    访问exports的方式有两种：
        exports
        module.exports
        - 当我们在其他模块中引入当前模块时，require函数返回的就是exports
        - 可以将希望暴露给外部模块的内容设置为exports的属性
*/
console.log(exports)
console.log(module.exports)
console.log(module.exports===exports)//true


// 可以通过exports 一个一个的导出值
// 可以导出属性和方法
exports.a = "孙悟空"
exports.b = {name:"白骨精"}
exports.c = function fn(){
     console.log("哈哈")
 }

// 也可以直接通过module.exports同时导出多个值
module.exports = {
    a: "哈哈",
    b: [1, 3, 5, 7],
    c: () =>{
        console.log(111)
    }
}
```

### 3.commonjs的原理

```javascript
/* 
    所有的CommonJS的模块都会被包装到一个函数中

    (function(exports, require, module, __filename, __dirname) {
    // 模块代码会被放到这里
    });
*/


let a = 10
let b = 20

// console.log(__filename) // __filename表示当前模块的绝对路径

console.log(__dirname) // 当前模块所在目录的路径
```



### 4.js自带的规范 es模块

es规范要是要在浏览器中生效   需要配置

![image-20231010195758679](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231010195758679.png)

```javascript
/* 
    默认情况下，node中的模块化标准是CommonJS
        要想使用ES的模块化，可以采用以下两种方案
            1. 使用mjs作为扩展名
            2. 修改package.json将模块化规范设置为ES模块
                当我们设置 "type": "module" 当前项目下所有的js文件都默认为es module
*/
console.log(module)


// 导入m4模块，es模块不能省略扩展名（官方标准）
import { a, b, c } from "./m4.mjs"

// 通过as来指定别名
import { a as hello, b, c } from "./m4.mjs" //a设置了别名

// 开发时要尽量避免import * 情况
import * as m4 from "./m4.mjs"

// 导入模块的默认导出
// 默认导出的内容，可以随意命名
import sum, { a } from "./m4.mjs"//导出m4的默认导出以及a
console.log(sum, a)

import { a, b, c } from "./m4.mjs"


// esmodule怎么向外部导出内容
export let a = 10
export const b = "孙悟空"
export const c = { name: "猪八戒" }

//设置默认导出， 一个模块中只有一个默认导出
export default function sum(a, b) {
     return a + b
 }

let d = 20
export default d 

// 通过ES模块化，导入的内容都是常量
// 此处a,b不能修改,c可以修改,c是改对象

// 补充
/*
 es模块都是运行在严格模式下的
 ES模块化，在浏览器中同样支持，但是通常我们不会直接使用
 通常都会结合打包工具使用(要考虑客户端的兼容性问题)
*/
```



### 4.1 es实现a文件在b文件中导出

```js
// a.js
export function someFunction() {
  // 函数的实现
}

export const someVariable = 123;
```

方式1

```js
//b.js
import { someFunction,someVariable  } from './a.js'
export { someFunction,someVariable }
```

方式2使用export from快捷方式

```js
// b.js 同时导入又导出
export { someFunction, someVariable } from './a.js';
```

其它文件引用

```js
// c.js
import { someFunction, someVariable } from './b.js';

// 现在你可以在 c.js 中使用 someFunction 和 someVariable 了
```



### 5.核心模块

```javascript
// 核心模块，是node中自带的模块，可以在node中直接使用
// window 是浏览器的宿主对象 node中是没有的
// global 是node中的全局对象，作用类似于window
// ES标准下，全局对象的标准名应该是 globalThis (commonjs和es模块不一样)
console.log(globalThis)

/* 
    核心模块
        process 
            - 表示当前的node进程
            - 通过该对象可以获取进程的信息，或者对进程做各种操作
            - 如何使用
                1. process是一个全局变量，可以直接使用
                2. 有哪些属性和方法：
                    process.exit()
                        - 结束当前进程，终止node
                    process.nextTick(callback[, …args])
                        - 将函数插入到 tick队列中
                        - tick队列中的代码，会在下一次事件循环之前执行
                            会在微任务队列和宏任务队列中任务之前执行
          ❤执行顺序：    
                调用栈
                tick队列
                微任务队列
                宏任务队列

*/
// console.log(11111)
// process.exit(0)
// console.log(22222)
// console.log(33333)

setTimeout(() => {
    console.log(1) // 宏任务队列
})

queueMicrotask(() => {
    console.log(2)
}) // 微任务队列

process.nextTick(() => {
    console.log(3) // tick队列
})

console.log(4) // 调用栈

//执行顺序 4 3 2 1
```



## 9.核心模块

### 1.path和fs简介

```javascript
/*
    path
        - 表示路径
        - 通过path可以用来获取各种路径
        - 要使用path，需要先对其进行引入
        - 方法：
            path.resolve([…paths]) 
                - 用来生成一个绝对路径
                    相对路径：./xxx  ../xxx  xxx
                    绝对路径：
                        - 在计算机本地
                            c:\xxx
                            /User/xxxx
                        - 在网络中
                            http://www.xxxxx/...
                            https://www.xxx/...

                    - 如果直接调用resolve，则返回当前的工作目录

                        C:\Program Files\nodejs\node.exe .\03_包管理器\01_path.js
                        c:\Users\lilichao\Desktop\Node-Course

                        node .\01_path.js
                        C:\Users\lilichao\Desktop\Node-Course\03_包管理器
                        - 注意，我们通过不同的方式执行代码时，它的工作目录是有可能发生变化的

                - 如果将一个相对路径作为参数，
                    则resolve会自动将其转换为绝对路径
                    此时根据工作目录的不同，它所产生的绝对路径也不同

                - 一般会将一个绝对路径作为第一个参数，
                    一个相对路径作为第二个参数
                    这样它会自动计算出最终的路径

*/
const path = require("node:path")

// const result = path.resolve()


// c:\Users\lilichao\Desktop\Node-Course\hello.js
// const result = path.resolve("./hello.js")
// const result = path.resolve(
//     "C:\\Users\\lilichao\\Desktop\\Node-Course\\03_包管理器",
//     "../../hello.js")


// 最终形态
// 以后在使用路径时，尽量通过path.resolve()来生成路径
const result = path.resolve(__dirname, "./hello.js")//生成当前模块所在目录的路径
console.log(result)


/* 
    fs （File System）
        - fs用来帮助node来操作磁盘中的文件
        - 文件操作也就是所谓的I/O，input output
        - 使用fs模块，同样需要引入
*/

const fs = require("node:fs/promises")
const { buffer } = require("stream/consumers")

// readFileSync() 同步的读取文件的方法，会阻塞后边代码的执行
// 当我们通过fs模块读取磁盘中的数据时，读取到的数据总会以Buffer对象的形式返回
// Buffer是一个临时用来存储数据的缓冲区
const buf = fs.readFileSync(path.resolve(__dirname, "./hello.txt"))
console.log(buf.toString())

//readFile() 异步的读取文件的方法
//回调函数的异步调用
fs.readFile(
     path.resolve(__dirname, "./hello.txt"),
     (err, buffer) => {
         if (err) {
             console.log("出错了~")
         } else {
             console.log(buffer.toString())
         }
     }
 )


// Promise版本的fs的方法(常用)
fs.readFile(path.resolve(__dirname, "./hello.txt"))
     .then(buffer => {
         console.log(buffer.toString())
      })
      .catch(e => {
        console.log("出错了~")
     })

//利用async和await语法糖调用(同步代码异步执行)
 ;(async () => {
     try {
          const buffer = await fs.readFile(path.resolve(__dirname, "./hello.txt"))
          console.log(buffer.toString())
      } catch (e) {
          console.log("出错了~~")
       }
  })()
```

#### 1.启动服务器有时无法启动

**这是因为通过f5启动时，根目录是大文件夹，通过node .\a.js启动时根目录是当前文件夹。  解决的方法就是const result = path.resolve(__dirname)**



### 2.fs方法1

```javascript
const fs = require("node:fs/promises")
const path = require("node:path")

/* 
    fs.readFile() 读取文件
    fs.appendFile() 创建新文件，或将数据添加到已有文件中
    fs.mkdir() 创建目录
    fs.rmdir() 删除目录
    fs.rm() 删除文件
    fs.rename() 重命名
    fs.copyFile() 复制文件
    fs.writeFile() 写入文件 //参数 1.文件名 2.写入的数据 3.回调函数 
*/

fs.appendFile(
     path.resolve(__dirname, "./hello123.txt"),
     "超哥讲的真不错"
 ).then(r => {
     console.log("添加成功")
 })

// 复制一个文件
// C:\Users\lilichao\Desktop\图片\jpg\an.jpg
fs.readFile("C:\\Users\\lilichao\\Desktop\\图片\\jpg\\an.jpg")
    .then(buffer => {

        return fs.appendFile(
            path.resolve(__dirname, "./haha.jpg"),
            buffer
        )
    })
    .then(() => {
        console.log("操作结束")
    })


fs.mkdir()
```



### 3.fsf方法2

```javascript
const fs = require("node:fs/promises")
const path = require("node:path")

/*
    fs.readFile() 读取文件
    fs.appendFile() 创建新文件，或将数据添加到已有文件中
    fs.mkdir() 创建目录
    fs.rmdir() 删除目录
    fs.rm() 删除文件
    fs.rename() 重命名 (剪切)
    fs.copyFile() 复制文件（复制）
*/

/*
    mkdir可以接收一个 配置对象作为第二个参数，
        通过该对象可以对方法的功能进行配置
            recursive 默认值为false
                - 设置true以后，会自动创建不存在的上一级目录
*/
fs.mkdir(path.resolve(__dirname, "./hello/abc"), { recursive: true })
     .then(r => {
         console.log("操作成功~")
     })
     .catch(err => {
         console.log("创建失败", err)
     })

 fs.rmdir(path.resolve(__dirname, "./hello"), { recursive: true })
     .then(r => {
         console.log("删除成功")
     })

fs.rename(
    path.resolve(__dirname, "../an.jpg"),
    path.resolve(__dirname, "./an.jpg")
).then(r => {
    console.log("重命名成功")
})
```



## 10.包管理器

### 1.npm

```javascript
/* 
    package.json
        - package.json是包的描述文件
        - node中通过该文件对项目进行描述
        - 每一个node项目必须有package.json

    命令
        npm init 初始化项目，创建package.json文件（需要回答问题）
        npm init -y 初始化项目，创建package.json文件（所有值都采用默认值）
        npm install 包名 将指定包下载到当前项目中
            install时发生了什么？
                ① 将包下载当前项目的node_modules目录下
                ② 会在package.json的dependencies属性中添加一个新属性
                    "lodash": "^4.17.21"
                ③ 会自动添加package-lock.json文件
                    这个文件的作用帮助加速npm下载的，不用动他

                
        npm install 自动安装所有依赖

        npm install 包名 -g 全局安装
            - 全局安装是将包安装到计算机中
            - 全局安装的通常都是一些工具

        npm uninstall 包名 卸载   
        
        https://docs.npmjs.com/cli/v8/commands 查询方法的网站
*/

/* 
    引入从npm下载的包时，不需要书写路径，直接写包名即可
*/
const _ = require("lodash")
console.log(_)
```

### 2.npm镜像及json的script命令

```javascript
/* 
    package.json
        scripts:
            - 可以自定义一些命令(当前项目必须执行的一些命令统一写在star里)
            - 定义以后可以直接通过npm来执行这些命令
            - start 和 test 可以直接通过 npm start npm test执行
            - 其他命令需要通过npm run xxx 执行

    npm镜像
        - npm的仓管的服务器位于国外，有时候并不是那么的好使
        - 为了解决这个问题，可以在npm中配置一个镜像服务器
        - 镜像的配置：
            ① 在系统中安装cnpm（我自己不太推荐大家使用）
                npm install -g cnpm --registry=https://registry.npmmirror.com
            ② 彻底修改npm仓库地址（我个人习惯的使用方式）
                npm set registry https://registry.npmmirror.com
                - 还原到原版仓库
                npm config delete registry
*/
```

### 3.其它包管理简介

```javascript
/* 
    早期的npm存在有很多的问题，
        所以有很多的厂商尝试着开发了一些代替npm的工具
        比如 yarn pnpm
        
        - 在之前，这些第三方的工具相较于npm具有的很多的优势
            但是随着时间的推进，npm也在进行不断的迭代，所以到今天npm和其他工具的差距并不是非常的大
        
        - 和npm相比，yarn下载包的速度会快一些

        yarn（个人习惯用yarn）
            安装
                corepack enable
                yarn init -y
            镜像配置
                yarn config set registry https://registry.npmmirror.com
            删除配置：
                yarn config delete registry
            安装依赖
            	yarn add xxx
            拷贝的项目安装依赖
	yarn

        pnpm
            - 安装
                npm install -g pnpm
            
            - 镜像
                pnpm config set registry https://registry.npmmirror.com

            - 取消
                pnpm config delete registry
             
*/
```



## 11.http协议

```css
HTTP协议
    - 网络基础
    - 网络的服务器基于请求和响应的
     
        https:// 协议名  http ftp ...

        lilichao.com 域名(domain)
            整个网络中存在着无数个服务器，每一个我服务器都有它自己的唯一标识
                这个标识被称为 ip地址 192.168.1.17，但是ip地址不方便记忆
                 - 域名就相当于是ip地址的别名

        /hello/index.html
            网站资源路径


    1.当在浏览器中输入地址以后发生了什么？(面试)
        https://lilichao.com/hello/index.html
        ① DNS解析，获取网站的ip地址
        ② 浏览器需要和服务器建立连接（tcp/ip）（三次握手）
        ③ 向服务器发送请求（http协议）
        ④ 服务器处理请求，并返回响应（http协议）
        ⑤ 浏览器将服务器响应的页面渲染
        ⑥ 断开和服务器的连接（四次挥手）


    2. 客户端如何和服务器建立（断开）连接
        - 通过三次握手和四次挥手
            - 三次握手（建立连接）
                - 三次握手是客户端和服务器建立连接的过程
                    1. 客户端向服务器发送连接请求(拨号)
                                    SYN(申请通话的标识)
                    2. 服务器收到连接请求，向客户端返回消息(电话接通了,同意通话)
                                    SYN ACK(同意的标识) 
                    3. 客户端向服务器发送同意连接的信息(开始通话)
                                    ACK
		- 理解:打电话,接通，开始说话

        - 四次挥手（断开连接）
                    1. 客户端向服务器发送请求，通知服务器数据发送完毕，请求断开来接(我说完了)
                                    FIN(申请断开的标识)
                    2. 服务器向客户端返回数据，知道了(我知道你说完了)
                                    ACK
                    3. 服务器向客户端返回数据，说完了，可以断开连接(可以断开)
                                    FIN ACK
                    4. 客户端向服务器发数据，可以断开了(同意断开)
                                    ACK
		- 理解:打电话,我说完了，好我知道你说完了，我也没什么要说的，挂了把，好的挂了。

        - 请求和响应实际上就是一段数据，只是这段数据需要遵循一个特殊的格式，这个特殊的格式由HTTP协议来规定

TCP/IP 协议族（了解）
    - TCP/IP协议族中包含了一组协议
        这组协议规定了互联网中所有的通信的细节
    - 网络通信的过程由四层组成
        应用层
            - 软件的层面，浏览器 服务器都属于应用层
        传输层
            - 负责对数据进行拆分，把大数据拆分为一个一个小包
        网络层
            - 负责给数据包，添加信息
        数据链路层
            - 传输信息

    - HTTP协议就是应用层的协议，
        用来规定客户端和服务器间通信的报文格式的
    - 报文（message）
        - 浏览器和服务器之间通信是基于请求和响应的
            - 浏览器向服务器发送请求（request）
            - 服务器向浏览器返回响应（response）
            - 浏览器向服务器发送请求相当于浏览器给服务器写信
                 服务器向浏览器返回响应，相当于服务器给浏览器回信这个信在HTTP协议中就被称为报文
            - 而HTTP协议就是对这个报文的格式进行规定

        - 服务器
            - 一个服务器的主要功能：
                1.可以接收到浏览器发送的请求报文
                2.可以向浏览器返回响应报文

        - 请求报文（request）
            - 客户端发送给服务器的报文称为请求报文
            - 请求报文的格式如下：
                请求首行
                请求头
                空行
                请求体

                请求首行
                    - 请求首行就是请求报文的第一行
                        GET /index.html?username=sunwukong HTTP/1.1
                        第一部分 get 表示请求的方式，get表示发送的是get请求
                            现在常用的方式就是get和post请求
                            get请求主要用来向服务器请求资源
                            post请求主要用来向服务器发送数据(安全性高)

                        第二部分 /index.html?username=sunwukong
                            表示请求资源的路径，
                                ? 后边的内容叫做查询字符串
                                查询字符串是一个名值对结构，一个名字对应一个值
                                    使用=连接，多个名值对之间使用&分割
                                    username=admin&password=123123
                                get请求通过查询字符串将数据发送给服务器
                                    由于查询字符串会在浏览器地址栏中直接显示
                                        所以，它安全性较差，同时，由于url地址长度有限制，所以get请求无法发送较大的数据

                                post请求通过请求体来发送数据
                                    - 在chrome中通过 载荷 可以查看
                                    post请求通过请求体发送数据，无法在地址栏直接查看
                                        所以安全性较好
                                    请求体的大小没有限制，可以发送任意大小的数据

                                如果你需要向服务器发送数据，能用post尽量使用post

                        第三部分
                            HTTP/1.1 协议的版本

                请求头
                    - 请求头也是名值对结构，用来告诉服务器我们浏览器的信息
                    - 每一个请求头都有它的作用：
                        Accept 浏览器可以接受的文件类型
                        Accept-Encoding 浏览器允许的压缩的编码
                        User-Agent 用户代理，它是一段用来描述浏览器信息的字符串

                空行
                    - 用来分隔请求头和请求体

                请求体
                    - post请求通过请求体来发送数据


            网页、css、 js、图片这些资源会作为响应报文中的哪一部分发送(响应体)

            响应报文：
                响应首行
                响应头
                空行
                响应体

                响应首行
                    HTTP/1.1 200 OK
                        200 响应状态码
                        ok 对响应状态码的描述
                        - 响应状态码的规则
                            1xx 请求处理中
                            2xx 表示成功
                            3xx 表示请求的重定向
                            4xx 表示客户端错误
                            5xx 表示服务器的错误

                响应头
                    - 响应头也是一个一个的名值对结构，用来告诉浏览器响应的信息
                    - Content-Type 用来描述响应体的类型
                    - Content-Length 用来描述响应体大小
                    Content-Type: text/html; charset=UTF-8
                    Content-Length: 2017
                空行
                    - 空行用来分隔响应头和响应体

                响应体
                    - 响应体就是服务器返回给客户端的内容
```

```css
GET 请求是可以有 body 的，只不过没有为其定义语义。
- 但是
	请求或响应需要传输实体时才会有 body。
	GET 请求用于请求实体，而不是传输实体
	GET 方法的语义是请求实体，POST 方法的语义是提交实体(需要传输)，两者有明确的分工。
	
	
get请求也是可以带请求体的，可以被servlet中的request.getInputStream()获取。
```



## 12.express服务器软件 web开发框架

**nest及egg框架比较新**

### 1.express简介

```javascript
/* 
    express 是node中的服务器软件
        通过express可以快速的在node中搭建一个web服务器
    - 使用步骤(确保安装了Node.js和npm)：
        1. 创建并初始化项目
            yarn init -y
        2. 安装express
            yarn add express
        3. 创建index.js 并编写代码
*/

// 引入express
const express = require("express")
// 获取服务器的实例（对象）
const app = express()

/* 
    如果希望服务器可以正常访问，则需要为服务器设置路由，
        路由可以根据不同的请求方式和请求地址来处理用户的请求
    
        app.METHOD(...)
            METHOD 可以是 get 或 post ...

    中间件
        - 在express我们使用app.use来定义一个中间件
            中间件作用和路由很像，用法很像，但是路由不区分请求的方式，只看路径

        - 和路由的区别
            1.会匹配所有请求
            2.路径设置父目录

    express是一个轻量级框架,很多功能都没有,我们要自己下载并引入扩展功能
*/

// next() 是回调函数的第三个参数，它是一个函数，调用函数后，可以触发后续的中间件
// next() 不能在响应处理完毕后调用
app.use((req, res, next) => {
    console.log("111", Date.now())
    // res.send("<h1>111</h1>")

    next() // 放行，我不管了~~
})

app.use((req, res, next) => {
    console.log("222", Date.now())
    // res.send("<h1>222</h1>")
    next()
})

app.use((req, res) => {
    console.log("333", Date.now())
    res.send("<h1>333</h1>")
})

// http://localhost:3000
// 路由的回调函数执行时，会接收到三个参数
// 第一个 request 第二个 response
	app.get("/hello", (req, res) => {
	console.log("有人访问我了~")
	// 在路由中，应该做两件事(读取请求,返回响应)
	//req 表示的是用户的请求信息，通过req可以获取用户传递数据
	console.log(req.url)
        
     // 根据用户的请求返回响应（response）
     // res 表示的服务器发送给客户端的响应信息
     //  可以通过res来向客户端返回数据
     // sendStatus() 向客户端发送响应状态吗
     // status() 用来设置响应状态吗，但是并不发送
     // send() 设置并发送响应体
	res.sendStatus(404)
	res.status(200)
	res.send("<h1>这是我的第一个服务器</h1>")
 })

// 启动服务器
// app.listen(端口号) 用来启动服务器
// 服务器启动后，我们便可以通过3000端口来访问了
// 协议名://ip地址:端口号/路径
// http://localhost:3000
// http://127.0.0.1:3000
app.listen(3000, () => {
    console.log("服务器已经启动~")
})
```

```css
如果2个路径相同的路由,express只会执行放在前面的那个
app.get("/",(req,res)=>{
    console.log(1);    
})
app.get("/",(req,res)=>{
    console.log(2);    
})

//只会打印1
```



### 2.*nodemon*自动监视代码修改

```css
  目前，服务器代码修改后必须要重启，
        我们希望有一种方式，可以自动监视代码的修改，代码修改以后可以自动重启服务器。

    要实现这个功能，我们需要安装一个模块 nodemon
        使用方式：
            1. 全局安装
                npm i nodemon -g
                yarn global add nodemon
                    - 同yarn进行全局安装时，默认yarn的目录并不在环境变量中
                    - 需要手动将路径添加到环境变量中
                - 启动：
                    nodemon  // 运行index.js
                    nodemon xxx // 运行指定的js

            2. 在项目中安装
                npm i nodemon -D
                yarn add nodemon -D

            3. 如何启动
                    npx nodemon
```



### 3.静态资源和get请求返回数据

```javascript
// use() 中间件
/* 
    服务器中的代码，对于外部来说都是不可见的，
        所以我们写的html页面，浏览器无法直接访问
        如果希望浏览器可以访问，则需要将页面所在的目录设置静态资源目录
*/

// 注意:❤谁写前面谁先访问
// 设置static中间件后，浏览器访问时，会自动去public目录寻找是否有匹配的静态资源
app.use(express.static(path.resolve(__dirname, "./public")))

// 配置路由
// 只有public里的东西会被看见 所以默认就会访问到index.html(public就是静态资源的存放地)
app.get("/", (req, res) => {
    /* 
        希望用户返回根目录时，可以给用户返回一个网页
    */
    res.send(`
    <!doctype html>
    <html>
         <head>
             <meta charset="utf-8">
             <title>这是一个网页</title>
         </head>
         <body>
             <h1>这是网页的标题</h1>
         </body>
     </html>
     `)
})

//使用get给用户返回数据时,第一种方式
app.get("/login", (req, res) => {
    // 获取到用户输入的用户名和密码
    // req.query 表示查询字符串中的请求参数
    console.log(req.query.username)
    console.log(req.query.password)

    // 验证用户输入的用户名和密码是否正确
    if(req.query.username === "sunwukong" && req.query.password === "123123"){
        res.send("<h1>登录成功！</h1>")
    }else{
        res.send("<h1>用户名或密码错误！</h1>")
    }

})

// 启动服务器
app.listen(3000, () => {
    console.log("服务器已起动~")
})
```



### 4.post请求和Param和和查询字符串

```javascript
const express = require("express")
const app = express()
const path = require("path")

// 配置静态资源的路径
// public http://localhost:3000/
app.use(express.static(path.resolve(__dirname, "public")))

// 引入解析请求体的中间件
// expressm没有的东西就用中间件来想办法
app.use(express.urlencoded())

// 添加一个路由，可以读取get请求的参数
// /login -->  http://localhost:3000/login
app.get("/login", (req, res) => {
    // 获取用户发送的数据
    // 通过req.query来获取查询字符串中的数据
    if (req.query.username === "admin" && req.query.password === "123123") {
        res.send("<h1>欢迎您回来！登录成功</h1>")
    } else {
        res.send("<h1>用户名或密码错误！</h1>")
    }
})

app.post("/login", (req, res) => {
    // 通过req.body来获取post请求的参数（请求体中的参数）
    // 默认情况下express不会自动解析请求体，需要通过中间件来为其增加功能
    const username = req.body.username
    const password = req.body.password

    if (username === "admin" && password === "123123") {
        res.send("<h1>登录成功</h1>")
    } else {
        res.send("<h1>登录失败</h1>")
    }
})

// get请求发送参数的第二种方式
// /hello/:id 表示当用户访问 /hello/xxx 时就会触发
// 在路径中以冒号命名的部分我们称为param(请求参数)，在get请求它可以被解析为请求参数
// param传参一般不会传递特别复杂的参数

// app.get("/hello/:name/:age/:gender", (req, res) => { 多个参数
app.get("/hello/:name", (req, res) => {
    // 约定优于配置(编程的一种思想)

    // 可以通过req.params属性来获取这些参数
    console.log(req.params)

    res.send("<h1>这是hello路由</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动~")
})
```

![uTools_1679407122871](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679407122871.png)

#### **1.get获取用户参数的方法**

```javascript
//使用get给用户返回数据时,第一种方式
app.get("/login", (req, res) => {
    // 获取到用户输入的用户名和密码
    // req.query 表示查询字符串中的请求参数
    console.log(req.query.username)
    console.log(req.query.password)

    // 验证用户输入的用户名和密码是否正确
    if(req.query.username === "sunwukong" && req.query.password === "123123"){
        res.send("<h1>登录成功！</h1>")
    }else{
        res.send("<h1>用户名或密码错误！</h1>")
    }

})


// get请求发送参数的第二种方式
// /hello/:id 表示当用户访问 /hello/xxx 时就会触发
// 在路径中以冒号命名的部分我们称为param(请求参数)，在get请求它可以被解析为请求参数
// param传参一般不会传递特别复杂的参数

// app.get("/hello/:name/:age/:gender", (req, res) => { 多个参数
app.get("/hello/:name", (req, res) => {
    // 约定优于配置(编程的一种思想)

    // 可以通过req.params属性来获取这些参数
    console.log(req.params)

    res.send("<h1>这是hello路由</h1>")
})
```

#### 2.post

```javascript
app.post("/login", (req, res) => {
    // 通过req.body来获取post请求的参数（请求体中的参数）
    // 默认情况下express不会自动解析请求体，需要通过中间件来为其增加功能
    const username = req.body.username
    const password = req.body.password

    if (username === "admin" && password === "123123") {
        res.send("<h1>登录成功</h1>")
    } else {
        res.send("<h1>登录失败</h1>")
    }
})
//post也是可以使用查询字符串的，只是不那样用，因为post是从请求体中拿到数据的
```



#### **3.小练习 登陆注册**

```javascript
const express = require("express")
const app = express()
const path = require("path")

// 创建一个数组来存储用户信息
const USERS = [
    {
        username: "admin",
        password: "123123",
        nickname: "超级管理员"
    },
    {
        username: "sunwukong",
        password: "123456",
        nickname: "齐天大圣"
    }
]

// 配置静态资源的路径
// public http://localhost:3000/
app.use(express.static(path.resolve(__dirname, "public")))
// 引入解析请求体的中间件
app.use(express.urlencoded())

app.post("/login", (req, res) => {
    const username = req.body.username
    const password = req.body.password

    // 不够优雅
    // 获取到用户的用户名和密码后，需要根据用户名去用户的数组中查找用户
    // for (const user of USERS) {
    //     if (user.username === username) {
    //         // 用户存在接着检查用户的密码
    //         if (user.password === password) {
    //             // 信息正确，登录成功
    //             res.send(`<h1>登录成功 ${user.nickname}</h1>`)
    //             return
    //         }
    //     }
    // }
    
    // res.send(`<h1>用户名或密码错误</h1>`)

    //新的解决方式
    const loginUser = USERS.find((item) => { //find：数组查找
        return item.username === username && item.password === password
    })

    //loginUser有值可以登陆 没值不可以登陆
    if (loginUser) {
        res.send(`<h1>登录成功 ${loginUser.nickname}</h1>`)
    } else {
        res.send(`<h1>用户名或密码错误</h1>`)
    }
})

app.post("/register", (req, res) => {
    // 获取用户输入的数据进行解构赋值
    const {username, password, repwd, nickname} = req.body

    // 验证这些数据是否正确，略... 
    // 只验证用户名是否存在
    const user = USERS.find(item => {
        return item.username === username || item.nickname === nickname
    })

    if(!user){
        // 进入判断说明用户不存在，可以注册
        USERS.push({
            username,
            password,
            nickname
        })

        res.send("<h1>恭喜您！注册成功！</h1>")
    }else{
        if(USERS.username === username){
            res.send(`<h1>用户名已存在！${username}</h1>`)
        }else{
            res.send(`<h1>昵称已存在！${nickname}</h1>`)
        }
    }

})

app.listen(3000, () => {
    console.log("服务器已经启动~")
})
```



### 5.模板引擎

**ejs就是一种模板引擎,可以在前端页面动态显示数据**

**代码**

```javascript
const express = require("express")
const path = require("path")
const app = express()

const STUDENT_ARR = [
    {
        name: "孙悟空",
        age: 18,
        gender: "男",
        address: "火锅山"
    },
    {
        name: "猪八戒",
        age: 28,
        gender: "男",
        address: "高老庄"
    },
    {
        name: "沙和尚",
        age: 38,
        gender: "男",
        address: "流沙河"
    }
]

//全局名称
let name = "猪八戒"

// 将ejs设置为默认的模板引擎
app.set("view engine", "ejs")
// 配置模板的路径
app.set("views", path.resolve(__dirname, "views"))

// 配置静态资源路径
app.use(express.static(path.resolve(__dirname, "public")))
// 配置请求体解析
app.use(express.urlencoded({ extended: true }))//无所谓true false 一个配置的东西
// app.use(express.json())


app.get("/hello", (req, res) => {
    res.send("hello")
})

    // 希望用户在访问students路由时，可以给用户返回一个显示有学生信息的页面
    /* 
        html页面属于静态页面，创建的时候什么样子，用户看到的就是什么样子
            不会自动跟随服务器中数据的变化而变化

        希望有这么一个东西，他呢长的像是个网页，但是他里边可以嵌入变量，这个东西在node中被称为 模板(格式定好了)
            ——在node中存在有很多个模板引擎，都各具特色，ejs是这之中比较好
            ——前后端分离时就不用考虑这个了

        ejs是node中的一款模板引擎，使用步骤：
            1.安装ejs
            2.配置express的模板引擎为ejs
                app.set("view engine", "ejs")
            3.配置模板路径
                app.set("views", path.resolve(__dirname, "views"))

            注意，模板引擎需要被express渲染后才能使用
    */

    //  res.render() 用来渲染一个模板引擎，并将其返回给浏览器
    // 可以将一个对象作为render的第二个参数传递，这样在模板中可以访问到对象中的数据
    // res.render("students", { name: "孙悟空", age: 18, gender: "男" })
    // <%= %>在ejs中输出内容时，它会自动对字符串中的特殊符号进行转义 &lt;
    //  这个设计主要是为了避免 xss 攻击
    // <%- %> 会直接将内容输出(容易造成XSS攻击)
    // <% %>  可以在其中直接编写js代码，js代码会在服务器中执行

//使用模板引擎渲染页面
app.get("/students", (req, res) => {
    res.render("students", { name })
})


app.get("/set_name", (req, res) => {
    //传入的值来替换全局的name
    name = req.query.name
    res.send("修改成功")
})

// 可以在所有路由的后边配置错误路由
app.use((req, res) => {
    // 只要这个中间件一执行，说明上边的地址都没有匹配到
    res.status(404)//设置响应状态码
    res.send("<h1>您访问的地址已被外星人劫持！</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**ejs模板  在服务器端中渲染的打印语句输出在服务器端(后端渲染)   react vue 是在浏览器端渲染的**

```ejs
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>这是ejs模板</title>
    </head>
    <body>
        <h1>Hello EJS 哈哈</h1>

        <!-- 
            通过它可以将render传递进来的数据直接在网页中显示出来
        -->
        
        <%=name %>

        <form action="/set_name">
            <input type="text" name="name" placeholder="请输入你的名字" />
            <button>提交</button>
        </form>

        <!-- 分开写和一起写是一样的 -->
        <!-- 分开写是为了嵌套模板字符串 -->
        <% if(name === "孙悟空"){ %>
        <h2>大师兄来了</h2>
        <%}else{%>
        <h2>二师兄来了</h2>
        <%}%>
    </body>
</html>
```

**练习 模板引擎动态显示页面**

**index.js**

```javascript
const express = require("express")
const path = require("path")
const app = express()
const fs = require("fs/promises")

//利用Json引入数据
let STUDENT_ARR = require("./data/students.json")

// 将ejs设置为默认的模板引擎
app.set("view engine", "ejs")

// 配置模板的路径
app.set("views", path.resolve(__dirname, "views"))

// 配置静态资源路径
app.use(express.static(path.resolve(__dirname, "public")))

// 配置请求体解析
app.use(express.urlencoded({ extended: true }))

//渲染ejs页面的路由
app.get("/students", (req, res) => {
    //整个数组用stus代名
    res.render("students", { stus: STUDENT_ARR })
})

// 创建一个添加学生信息的路由
app.post("/add-student",(req,res)=>{
    //生成一个id
    //“条件表达式?表达式1:表达式2”
    //最后一个元素存在就加1,如果最后一个元素不存在就返回1
    const id = STUDENT_ARR.at(-1) ? STUDENT_ARR.at(-1).id + 1 : 1

    //1.获取用户填写的信息
    const newUser = {
        id,
        name:req.body.name,//转换为number 防止后面要算数
        age:+req.body.age,
        gender:req.body.gender,
        address:req.body.address
    }
    //解构赋值 const newUser = {name,age,gender,address} = req.body

    //2.验证用户信息

    //3.将用户信息添加到数组中
    STUDENT_ARR.push(newUser)

    //4.返回响应
    // res.send("添加成功")
    // 直接在添加的路由中渲染ejs,会面临表单重复提交的问题
    // res.render("students",{stus:STUDENT_ARR})

    //将新的数据写入json文件中 写入成功才重定向
    fs.writeFile(
        //参数 1.文件名 2.写入的数据 3.回调函数 
        path.resolve(__dirname,"./data/students.json"),
        JSON.stringify(STUDENT_ARR)
    ).then(()=>{
        // res.redirect() 用来发起请求重定向
        // 重定向的作用是告诉浏览器你向另外一个地址再发起一次请求
        // 点击添加按钮的时候向add—student发送请求,路由最后在向
        // students发送请求,这样地址就不会跳转了
        // 浏览器在这个过程中发送了2个请求(执行到最后一个请求跳到students,这样就不会重复提交数据)
        res.redirect("/students")
    }).catch(()=>{
        //写入失败 处理异常
    })  
})

/* 
    删除
        - 点击删除链接后，删除当前数据
        - 点击 白骨精 删除 --> 删除id为5的学生
        - 流程：
            1. 点击白骨精的删除链接
            2. 向路由发送请求（写一个路由）
            3. 路由怎么写？
                - 获取学生的id n
                - 删除id为n的学生
                - 将新的数组写入文件
                - 重定向到学生列表页面
*/

//创建一个处理删除数据的路由(a标签点击跳转的位置)
app.get("/delete",(req,res)=>{
    // 1.获取要删除学生的id
    const id = +req.query.id//类型转换

    //2.根据id删除学生
    //利用过滤 返回满足stu.id !== id 的新数组
    //这样就会返回除了被点击的id以外的数据
    STUDENT_ARR = STUDENT_ARR.filter((stu) => stu.id !== id)
    
    //3.写入到文件中
    fs.writeFile(
        path.resolve(__dirname,"./data/students.json"),
        JSON.stringify(STUDENT_ARR)

    ).then(()=>{
        res.redirect("/students")
    }).catch(()=>{
        //写入失败 处理异常
    })  
})

/*
    修改
        - 点击修改链接后，显示一个表单，表单中应该有要修改的学生的信息(不一定会全修改)，
            用户对学生信息进行修改，修改以后点击按钮提交表单
        - 流程：
            1. 点击孙悟空的修改链接
            2. 跳转到一个路由
                - 这个路由会返回一个页面，页面中有一个表单，表单中应该显示孙悟空的各种信息
            3. 用户填写表单，点击按钮提交到一个新的路由
                - 获取学生信息，并对信息进行修改
*/

//跳转到修改数据的页面(a标签点击跳转的位置)
app.get("/to-update", (req, res) => {
    const id = +req.query.id
    // 获取要修改的学生的信息 find查找数组符合条件的第一个元素
    const student = STUDENT_ARR.find((item) => item.id === id)

    //点击修改跳转到update.ejs页面并且把页面回显
    res.render("update", { student })
})

//修改表单数据(进行表单修改,需要一个页面来显示页面数据才能进行修改)
app.post("/update-student",(req,res)=>{
    // 获取id的方法1 查询字符串(任何请求都可以用查询字符串获取)
    // const id = req.query.id

    // 方法2 接收了浏览器传过来的id(对用户来说隐藏了，req.body直接可以拿到 )
    const {id,name,age,gender,address} = req.body
    
    //根据学生id获取要修改的学生对象
    const student = STUDENT_ARR.find((item) => item.id == id)
    student.name = name
    student.age = +age
    student.gender = gender
    student.address = address

    //重新写入文件
    fs.writeFile(
        path.resolve(__dirname,"./data/students.json"),
        JSON.stringify(STUDENT_ARR)

    ).then(()=>{
        res.redirect("/students")
    }).catch(()=>{
        //写入失败 处理异常
    })  
})

// 可以在所有路由的后边配置错误路由
app.use((req, res) => {
    // 只要这个中间件一执行，说明上边的地址都没有匹配
    res.status(404)
    res.send("<h1>您访问的地址已被外星人劫持！</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**students.ejs**

```ejs
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>这是ejs模板</title>
    <style>
        table {
            /* 表格的俩条边框合一 */
            border-collapse: collapse;
        }

        th,
        td {
            border: 1px #000 solid;
            font-size: 20px;
            padding: 10px;
            text-align: center;
        }

        caption {
            font-size: 25px;
            font-weight: bold;
        }

        a {
            text-decoration: none;
        }
    </style>
</head>

<body>
    2种ejs的注释方法
       <%# address %>

        <%
            //console.log(1111)
        %>
    <!-- 没有数据的时候table不显示 -->
    <% if(stus && stus.length>0){ %>
        <table>
            <thead>
                <caption>学习列表</caption>
                <tr>
                    <th>学号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>地址</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody>
                <% for(const stu of stus){ %>
                    <tr>
                        <td>
                            <%=stu.id%>
                        </td>
                        <td>
                            <%=stu.name%>
                        </td>
                        <td>
                            <%=stu.age%>
                        </td>
                        <td>
                            <%=stu.gender%>
                        </td>
                        <td>
                            <%=stu.address%>
                        </td>
                        <td>
                            <!-- 查询字符串格式 -->
                            <!-- 用req.query接收 -->
                            <a onclick="return confirm('确认删除吗?') " href="/delete?id=<%=stu.id%>">
                                删除
                            </a>
                            <a onclick="return confirm('确认修改吗?') " href="/to-update?id=<%=stu.id%>">
                                修改
                            </a>
                        </td>
                    </tr>
                    <% } %>
            </tbody>
        </table>
        <% }else{ %>
            <p style="font-weight: bold;">学生列表为空!</p>
            <% } %>

                <hr>

       <!-- 
        1.点完按钮表单提交给后台路由 
        2.路由接收数据并存到数据库
        3.将新添加的数据返回给前端页面进行渲染
     -->
                <form action="/add-student" method="post">
                    <div>姓名：<input type="text" name="name" /></div>
                    <div>
                        年龄：<input type="number" max="150" min="0" name="age" />
                    </div>
                    <div>
                        性别：<input type="radio" name="gender" value="男" /> 男
                        <input type="radio" name="gender" value="女" /> 女
                    </div>
                    <div>地址：<input type="text" name="address" /></div>
                    <div>
                        <button>添加</button>
                    </div>
                </form>
</body>

</html>
```

**update.ejs**

```ejs
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>修改学生信息</title>
</head>

<body>
    <h1>修改学生信息</h1>
    <form action="/update-student?id<%= student.id %>" method="post">
        <!-- 向服务器偷偷传了一个隐藏的id 用户不可见不可读 服务器可以获取id -->
        <input type="hidden" name="id" value="<%= student.id %>">
        <div>姓名：<input type="text" name="name" value="<%= student.name %>" /></div>
        <div>
            年龄：<input type="number" max="150" min="0" name="age" value="<%= student.age %>" />
        </div>
        <div>
            性别：<input type="radio" name="gender" value="男" <%=student.gender==="男" && "checked" %> /> 男
            <input type="radio" name="gender" value="女" <%=student.gender==="女" && "checked" %>/> 女
        </div>
        <div>地址：<input type="text" name="address" value="<%= student.address %>" /></div>
        <div>
            <button>修改</button>
        </div>
    </form>
</body>

</html>
```

**students.json**

```json
[{"id":2,"name":"黄宇","age":11,"gender":"男","address":"仙游"},{"id":3,"name":"1","age":1,"gender":"男","address":"1"},{"id":4,"name":"1","age":1,"gender":"男","address":"1"}]
```

### 6.补充 bodyParser.json() 

```css
是一个中间件函数，用于解析 HTTP 请求体中的 JSON 数据。它会将请求体中的 JSON 数据解析成 JavaScript 对象，并将其作为 req.body 属性的值存储，以便后续的处理程序可以使用它。这个方法通常用于处理 POST、PUT 和 DELETE 请求中的 JSON 数据。
```



## 13.Route

**路由的作用就是在index外编写增删改查的功能,方便index解耦合,方便项目维护**

### 1.route页面

```javascript
1.students
const express = require("express")
const router = express.Router()
let STUDENT_ARR = require("../data/students.json")
const fs = require("fs/promises")
const path = require("path")

// 学生列表的路由
router.get("/list", (req, res) => {
    if(req.cookies.username){
        res.render("students", { stus: STUDENT_ARR })
    }else{
        res.redirect("/")
    }

    // res.render("students", { stus: STUDENT_ARR })
})

// 添加学生的路由
router.post("/add", (req, res, next) => {
    const id = STUDENT_ARR.at(-1) ? STUDENT_ARR.at(-1).id + 1 : 1

    const newUser = {
        id,
        name: req.body.name,
        age: +req.body.age,
        gender: req.body.gender,
        address: req.body.address
    }

    STUDENT_ARR.push(newUser)

    //调用next交由后续路由继续处理
    next()
})

// 删除学生的路由
router.get("/delete", (req, res, next) => {
    const id = +req.query.id

    STUDENT_ARR = STUDENT_ARR.filter((stu) => stu.id !== id)

    next()
})

router.post("/update-student", (req, res, next) => {
    const { id, name, age, gender, address } = req.body
    const student = STUDENT_ARR.find((item) => item.id == id)

    student.name = name
    student.age = +age
    student.gender = gender
    student.address = address
    next()
})

router.get("/to-update", (req, res) => {
    const id = +req.query.id
    const student = STUDENT_ARR.find((item) => item.id === id)

    res.render("update", { student })
})

// 处理存储文件的中间件
router.use((req, res) => {
    fs.writeFile(
        path.resolve(__dirname, "../data/students.json"),
        JSON.stringify(STUDENT_ARR)
    )
        .then(() => {
            res.redirect("/students/list")
        })
        .catch(() => {
            res.send("操作失败！")
        })
})

module.exports = router

```

### 2.index.js

```javascript
const express = require("express")
const path = require("path")
const app = express()
const cookieParser = require("cookie-parser")

const userRouter = require("./routes/user")//引入路由
const goodsRouter = require("./routes/goods")//引入路由

app.set("view engine", "ejs")
app.set("views", path.resolve(__dirname, "views"))

app.use(express.static(path.resolve(__dirname, "public")))
app.use(express.urlencoded({ extended: true }))
app.use(cookieParser())

// 使路由生效
// app.use("/user", userRouter)
// app.use("/goods", goodsRouter)

app.use("/students", require("./routes/student"))//引入路由

app.get("/", (req, res) => {

    res.render("login")
})

app.get("/get-cookie", (req, res) => {

    // 给客户端发送一个cookie
    res.cookie("username", "admin")

    res.send("cookie已经发送")
})

app.get("/hello", (req, res) => {

    /* 
        需要安装中间件来使得express可以解析cookie
            1.安装cookie-parser
                yarn add cookie-parser
            2.引入
                const cookieParser = require("cookie-parser")
            3.设置为中间件
                app.use(cookieParser())
    */

    // req.cookies 用来读取客户端发回的cookie
    console.log(req.cookies)

    res.send("hello路由")
})

app.post("/login", (req, res) => {
    /* 
        现在咱们这个登录，简直形同虚设，
            HTTP协议是一个无状态的协议，
                服务器无法区分请求是否发送自同一个客户端

            cookie
                - cookie是HTTP协议中用来解决无状态问题的技术
                - cookie的本质就是一个头
                    - 服务器以响应头的形式将cookie发送给客户端
                        客户端收到以后会将其存储，并在下次向服务器发送请求时将其传回
                        这样服务器就可以根据cookie来识别出客户端了
    */
    // 获取用户的用户名和密码
    const {username, password} = req.body
    if(username === "admin" && password === "123123"){
        // 登录成功
        // res.send("登录成功")
        // 将用户名放入cookie
        res.cookie("username", username)
        res.redirect("/students/list")
    }else{
        res.send("用户名或密码错误")
    }

})


app.use((req, res) => {
    res.status(404).send("<h1>您访问的页面已经被外星人劫持</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})

```

### 3.ejs页面

```javascript
1.students
<!DOCTYPE html>
<html lang="zh">
    <!-- 
        C:\Users\lilichao\Desktop\Node-Course\12_express\views\students.ejs

        localhost:3000/students/list（虚拟路径）

        localhost:3000/css/index.css

        res.render("student")
    
    -->
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>学生列表</title>
        <link rel="stylesheet" href="/css/index.css">
        <!-- <link rel="stylesheet" href="../css/index.css"> -->
        <style>
            table {
                border-collapse: collapse;
            }

            th,
            td {
                border: 1px #000 solid;
                font-size: 20px;
                padding: 10px;
                text-align: center;
            }

            caption {
                font-size: 25px;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <hr />
        <% if(stus && stus.length > 0) { %>
        <table>
            <caption>
                学生列表
            </caption>
            <thead>
                <tr>
                    <th>学号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>地址</th>
                    <th>操作</th>
                </tr>
            </thead>

            <tbody>
                <% for(const stu of stus){ %>
                <tr>
                    <td><%=stu.id%></td>
                    <td><%=stu.name %></td>
                    <td><%=stu.age %></td>
                    <td><%=stu.gender %></td>
                    <td><%=stu.address %></td>
                    <td>
                        <a
                            onclick="return confirm('确认删除吗？')"
                            href="/students/delete?id=<%=stu.id%>"
                            >删除</a
                        >
                        <a href="/students/to-update?id=<%=stu.id%>">修改</a>
                    </td>
                </tr>
                <% }%>
            </tbody>
        </table>
        <%}else{%>
        <p>学生列表为空！</p>

        <%}%>

        <hr />

        <form action="/students/add" method="post">
            <div>姓名：<input type="text" name="name" /></div>
            <div>
                年龄：<input type="number" max="150" min="0" name="age" />
            </div>
            <div>
                性别：<input type="radio" name="gender" value="男" /> 男
                <input type="radio" name="gender" value="女" /> 女
            </div>
            <div>地址：<input type="text" name="address" /></div>
            <div>
                <button>添加</button>
            </div>
        </form>
    </body>
</html>
2.update
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <h1>修改学生信息</h1>
        <form action="/students/update-student" method="post">
            <!-- hidden是一个隐藏的表单项，可以通过它传递一些不希望被用户看见的数据 -->
            <input type="hidden" name="id" value="<%=student.id%>" />
            <div>
                姓名：<input
                    type="text"
                    name="name"
                    value="<%=student.name%>"
                />
            </div>
            <div>
                年龄：<input
                    type="number"
                    max="150"
                    min="0"
                    name="age"
                    value="<%=student.age%>"
                />
            </div>

            <div>
                性别：
                <input type="radio" name="gender" value="男"
                <%=student.gender === "男" && "checked" %> /> 男 
                <input type="radio" name="gender" value="女" 
                <%=student.gender === "女"
                && "checked" %> /> 女
            </div>
            <div>
                地址：<input
                    type="text"
                    name="address"
                    value="<%=student.address%>"
                />
            </div>
            <div>
                <button>修改</button>
            </div>
        </form>
    </body>
</html>

```



## 14.cookie简介

**cookie服务器发送，客户端存储，所以第一次访问的时候会慢**

**index.js页面**

```javascript
const express = require("express")
const path = require("path")
const app = express()
const cookieParser = require("cookie-parser")

const fs = require("fs/promises")
const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")

// 将ejs设置为默认的模板引擎
app.set("view engine", "ejs")

// 配置模板的路径
app.set("views", path.resolve(__dirname, "views"))

// 配置静态资源路径
app.use(express.static(path.resolve(__dirname, "public")))

// 配置请求体解析
app.use(express.urlencoded({ extended: true }))

// 使路由生效(路由其实就是接口)
// 为了避免多个路由之间路径冲突,可以为其指定前缀
// 此时原js文件记得向 /goods/list发送请求
// app.use("/user",userRouter)
// app.use("/goods",goodsRouter)
//引入cookie
app.use(cookieParser())

// 也可以直接用require引入
app.use("/students",require("./routes/student"))

//cookie的安装
/* 
    需要安装中间件来使得express可以解析cookie
        1.安装cookie-parser
             yarn add cookie-parser
        2.引入
            const cookieParser = require("cookie-parser")
        3.设置为中间件
            app.use(cookieParser())
*/


//页面登录 登录成功返回到login页面
app.get("/", (req, res) => {
    res.render("login")
})

app.post("/login",(req,res)=>{
    /* 
        现在咱们这个登录，简直形同虚设，
            HTTP协议是一个无状态的协议，
                服务器无法区分请求是否发送自同一个客户端

        cookie
            - cookie是HTTP协议中用来解决无状态问题的技术
            - cookie的本质就是一个头
                - 服务器以响应头的形式将cookie发送给客户端
                    客户端收到以后会将其存储，并在下次向服务器发送请求时将其传回
                    这样服务器就可以根据cookie来识别出客户端了
    */
   //获取用户名密码
    const {username, password} = req.body
    
    if(username === "admin" && password=== "123123"){
        // 给客户端发送一个cookie
        // cookie是发送数据的一种技术,token只是一个数据
        //拿到cookie以后可以重定向
        res.cookie("username", username)
        res.redirect("/students/list")
        // console.log(req.cookies); req.cookies用来获取cookie
    }else{
        res.send("登录失败!")
    }

})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})

```

**login页面**

```ejs
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>首页</title>
</head>

<body>
    <h1>hello!</h1>
    <hr>
    <form action="/login" method="post">
        <div>
            <input type="text" name="username" placeholder="用户名">
        </div>
        <div>
            <input type="password" name="password" placeholder="密码">
        </div>
        <div>
            <button type="submit">登录</button>
        </div>
    </form>
</body>

</html>
```

**students.js**

```javascript
const express = require("express")
const router = express.Router()
const path = require("path")
const fs = require("fs/promises")

//利用Json引入数据
let STUDENT_ARR = require("../data/students.json")

// 学生列表的路由
router.get("/list",(req,res)=>{
    //如果返回了cookie才显示列表
    //登录成功了才会有cookie
    if(req.cookies.username){
        res.render("students", { stus: STUDENT_ARR })
    }else{
        res.redirect("/")
    }
})
```

### 1.cookie的问题

1.cookie只能发到自己的网站   a.com不能发到b.com(跨域问题)

2.fetch发送请求不会带cookie

3.在跨域的请求中，请求不会自动带上cookie，需要前后端配合设置才可以。

4.cookie用不了的地方session也用不了,session基于cookie

5.cookie是由服务器创建，浏览器保存
 每次浏览器访问服务器时都需要将cookie发回
 这就导致我们不能在cookie存放较多的数据
 并且cookie是直接存储在客户端，容易被篡改盗用



## 15.完善cookie 使用

```javascript
const express = require("express")
const path = require("path")
const app = express()
const cookieParser = require("cookie-parser")

const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")

app.set("view engine", "ejs")
app.set("views", path.resolve(__dirname, "views"))

app.use(express.static(path.resolve(__dirname, "public")))
app.use(express.urlencoded({ extended: true }))
app.use(cookieParser())

app.get("/set", (req, res) => {
    /*
        cookie是有有效期
            - 默认情况下cookie的有效期就是一次会话（session）
                会话就是一次从打开到关闭浏览器的过程 
            - maxAge 用来设置cookie有效时间，单位是毫秒
    */
    res.cookie("name", "sunwukong", {
        // expires:new Date(2022, 11, 7)
        // expires 也可以设置过期时间 maxage常用
        maxAge: 1000 * 60 * 60 * 24 * 30
    })
    res.send("设置cookie")
})
 // 第一次发请求看不见请求cookie，只能看见响应cookie
 // 第二次发请求才能看见
    

app.get("/get", (req, res) => {
    const name = req.cookies.name

    console.log(name)

    res.send("读取cookie")
})

app.get("/delete-cookie", (req, res) => {
    // cookie一旦发送给浏览器我们就不能在修改了
    // 但是我们可以通过发送新的同名cookie来替换旧cookie，从而达到修改的目的

    res.cookie("name", "", {
        maxAge: 0
    })

    res.send("删除Cookie")
})

app.use((req, res) => {
    res.status(404).send("<h1>您访问的页面已经被外星人劫持</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```



## 16.session简介

**session简介**

```javascript
const express = require("express")
const path = require("path")
const app = express()
// 引入session
const session = require("express-session")

const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")

app.set("view engine", "ejs")
app.set("views", path.resolve(__dirname, "views"))

app.use(express.static(path.resolve(__dirname, "public")))
app.use(express.urlencoded({ extended: true }))

// 设置session中间件
app.use(
    /*
        设置了session后 每次客户端发送的请求会先到中间件中
            -如果该请求有cookie 证明该用户是"会员"，服务器会把用户信息(存数据的对象)设置到request中
            -我们可以通过req.session去获取他

            -如果该请求没有cookie 证明该用户不是"会员"，服务器给该用户设置一个cookie和用户信息(存数据的对象)设置到request中
            -然后返回cookie给该用户

            简单理解:有卡直接能到数据,没卡办卡然后把卡发给用户，下一次就能拿到数据

            - 经过这样处理以后 cookie中只需要存一个id就行
    */ 

    session({
        //secret是必填的  它是一种加密手段 随便指定一个值即可
        secret: "hello"
    })
)

app.get("/set", (req, res) => {
    /*
        cookie的不足
            - cookie是由服务器创建，浏览器保存
                每次浏览器访问服务器时都需要将cookie发回
                这就导致我们不能在cookie存放较多的数据
                并且cookie是直接存储在客户端，容易被篡改盗用
            - 注意：
                我们在使用cookie一定不会在cookie存储敏感数据

            - 所以为了解决Cookie的不足，我们希望可以这样
                将用户的数据统一存储在服务器中，
                    每一个用户的数据都有一个对应的id
                    我们只需通过cookie将id发送给浏览器
                    浏览器只需每次访问时将id发回，即可读取到服务器中存储的数据
                    这个技术我们称之为session（会话）

            session
                - session是服务器中的一个对象，这个对象用来存储用户的数据
                - 每一个session对象都有一个唯一的id，id会通过cookie的形式发送给客户端
                - 客户端每次访问时只需将存储有id的cookie发回即可获取它在服务器中存储的数据
                - 在express 可以通过 express-session 组件来实现session功能
                - 使用步骤：
                    ① 安装
                        yarn add express-session
                    ② 引入
                        const session = require("....")
                    ③ 设置为中间件
                        app.use(session({...}))
                         
    */

    // session是存客户端的信息在服务器中  访问还是要用req
    // console.log(req.session)
    req.session.username = "sunwukong"

    res.send("查看session")
})

app.get("/get",(req, res) => {

    const username = req.session.username

    console.log(username)

    res.send("读取session")
})

app.use((req, res) => {
    res.status(404).send("<h1>您访问的页面已经被外星人劫持</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**修改cookie为session**

**index**

```javascript
const express = require("express")
const path = require("path")
const app = express()
const session = require("express-session")

const fs = require("fs/promises")
const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")

// 将ejs设置为默认的模板引擎
app.set("view engine", "ejs")

// 配置模板的路径
app.set("views", path.resolve(__dirname, "views"))

// 配置静态资源路径
app.use(express.static(path.resolve(__dirname, "public")))

// 配置请求体解析
app.use(express.urlencoded({ extended: true }))

app.use(session({
    secret:"sssss"
}))

app.use("/students",require("./routes/student"))


//页面登录 登录成功跳到到login页面(因为会执行下一个路由) 再由login进行逻辑判断
//进入根目录 把login返回给页面
//res.render()函数用于呈现视图，并将呈现的HTML字符串发送给客户端。
app.get("/", (req, res) => {
    res.render("login")
})


app.post("/login",(req,res)=>{

   //获取用户名密码
    const {username, password} = req.body
    
    if(username === "admin" && password=== "123123"){
        //❤❤登录成功后,将用户信息放入到session中
        req.session.loginUser = username

        res.redirect("/students/list")
       
    }else{
        res.send("登录失败!")
    }

})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**students.js**

```javascript
const express = require("express")
const router = express.Router()
const path = require("path")
const fs = require("fs/promises")

//利用Json引入数据
let STUDENT_ARR = require("../data/students.json")

// 为登录及CRUD统一是指验证 没登陆成功获取session就不能进行下面的操作
// 不能直接访问列表 也不能直接CRUD
router.use((req,res,next)=>{
    if(req.session.loginUser){
        next()
    }else{
        res.redirect("/")
    }
})

// 学生列表的路由
router.get("/list",(req,res)=>{
    // session的默认有效期是一次会话
    // if (req.session.loginUser) {
    //     res.render("students", { stus: STUDENT_ARR })
    // } else {
    //     res.redirect("/")
    // }
    res.render("students", { stus: STUDENT_ARR })
})

// 添加学生
// 记得修改students.ejs表单的的路径,因为在index中指定了students前缀
router.post("/add",(req,res,next)=>{

    const id = STUDENT_ARR.at(-1) ? STUDENT_ARR.at(-1).id + 1 : 1
    
    const newUser = {
        id,
        name:req.body.name,
        age:+req.body.age,
        gender:req.body.gender,
        address:req.body.address
    }

    //调用写入文件的基础
    STUDENT_ARR.push(newUser)  

    // 调用next交由后续路由继续处理
    next()

})

// 删除路由
router.get("/delete",(req,res,next)=>{
    const id = +req.query.id

    STUDENT_ARR = STUDENT_ARR.filter((stu) => stu.id !== id)

    next()
})

//修改表单数据
router.post("/update-student",(req,res,next)=>{
    const {id,name,age,gender,address} = req.body
    
    const student = STUDENT_ARR.find((item) => item.id == id)
    student.name = name
    student.age = +age
    student.gender = gender
    student.address = address

    next()
})

// 修改路由
router.get("/to-update", (req, res) => {
    const id = +req.query.id
    const student = STUDENT_ARR.find((item) => item.id === id)

    res.render("update", { student })
})

// 处理存储文件的中间件
router.use((req, res) => {
    fs.writeFile(
        path.resolve(__dirname, "../data/students.json"),
        JSON.stringify(STUDENT_ARR)
    )
        .then(() => {
            res.redirect("/students/list")
        })
        .catch(() => {
            res.send("操作失败！")
        })
})

module.exports = router
```



## 17.session完善

```javascript
const express = require("express")
const path = require("path")
const app = express()
const cookieParser = require("cookie-parser")
//这个session是被存储的那个
const session = require("express-session")
// 引入file-store
const FileStore = require("session-file-store")(session)

const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")
const { Cookie } = require("express-session")

app.set("view engine", "ejs")
app.set("views", path.resolve(__dirname, "views"))

app.use(express.static(path.resolve(__dirname, "public")))
app.use(express.urlencoded({ extended: true }))
app.use(cookieParser())
app.use(
    session({
        store: new FileStore({
            // path用来指定session本地文件的路径
            path: path.resolve(__dirname, "./sessions"),

            // 设置了secret会自动加密文件(secret不能被知道 会被解密)
            secret: "哈哈"

            // session的有效时间 秒 默认1个小时  
            // ttl: 10, //十秒以后session失效

            // 默认情况下，fileStore会每间隔一小时，清除一次session对象
            // reapInterval 用来指定清除session的间隔，单位秒，默认 1小时
            // reapInterval: 10
        }),
        secret: "dazhaxie"
        // 如果要设置一个长时间的cookie页要和ttl一起设置
        // Cookie:{maxAge:1000}
    })
)

/* 
    session是服务器中的一个对象，这个对象用来存储用户的信息
        每一个session都会有一个唯一的id，session创建后，
            id会以cookie的形式发送给浏览器
        浏览器收到以后，每次访问都会将id发回，服务器中就可以根据id找到对应的session

    id（cookie） ----> session对象
    
    session什么时候会失效？(默认情况是一次会话就失效)
        - 有session的时候在浏览器看到的是请求cookie 没有会看到响应cookie(服务器发给你的新的)
        第一种 浏览器的cookie没了(关闭浏览器,会话结束)
        第二种 服务器中的session对象没了(服务器关机了丢失了)
    
    express-session默认是将session存储到浏览器内存中的，所以服务器一旦重启session会自动重置，
        所以我们使用session通常会对session进行一个持久化的操作（写到文件或数据库）

    如果将session存储到本文件(还没讲数据库)中：
        - 需要引入一个中间件session-file-store
        - 使用步骤：
            ① 安装
                yarn add session-file-store
            ② 引入
                const FileStore = require("session-file-store")(session) 
            ③ 设置为中间件       
            app.use(
                session({
                    store: new FileStore({}),
                    secret: "dazhaxie"
                })
            )

*/

app.use("/students", require("./routes/student"))

app.get("/", (req, res) => {
    res.render("login")
})

//session中也有一些方法
app.get("/logout", (req, res) => {
    // 使当前session立刻失效(退出的功能)
    req.session.destroy(() => {
        //不止要退回首页 session还要销毁
        res.redirect("/")
    })
})

app.post("/login", (req, res) => {
    // 获取用户的用户名和密码
    const { username, password } = req.body
    if (username === "admin" && password === "123123") {
        // 登录成功后，将用户信息放入到session中
        req.session.loginUser = username

        res.redirect("/students/list")
    } else {
        res.send("用户名或密码错误")
    }
})
app.use((req, res) => {
    res.status(404).send("<h1>您访问的页面已经被外星人劫持</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**给students加上退出功能 用到session失效的方法**

```ejs
<!DOCTYPE html>
<html lang="zh">
    <!-- 
        C:\Users\lilichao\Desktop\Node-Course\12_express\views\students.ejs

        localhost:3000/students/list（虚拟路径）

        localhost:3000/css/index.css

        res.render("student")
    
    -->
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>学生列表</title>
        <link rel="stylesheet" href="/css/index.css">
        <!-- <link rel="stylesheet" href="../css/index.css"> -->
        <style>
            table {
                border-collapse: collapse;
            }

            th,
            td {
                border: 1px #000 solid;
                font-size: 20px;
                padding: 10px;
                text-align: center;
            }

            caption {
                font-size: 25px;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <h2>当前用户：<%=username %></h2>
        <a href="/logout">登出</a>
        <hr />
        <% if(stus && stus.length > 0) { %>
        <table>
            <caption>
                学生列表
            </caption>
            <thead>
                <tr>
                    <th>学号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>地址</th>
                    <th>操作</th>
                </tr>
            </thead>

            <tbody>
                <% for(const stu of stus){ %>
                <tr>
                    <td><%=stu.id%></td>
                    <td><%=stu.name %></td>
                    <td><%=stu.age %></td>
                    <td><%=stu.gender %></td>
                    <td><%=stu.address %></td>
                    <td>
                        <a
                            onclick="return confirm('确认删除吗？')"
                            href="/students/delete?id=<%=stu.id%>"
                            >删除</a
                        >
                        <a href="/students/to-update?id=<%=stu.id%>">修改</a>
                    </td>
                </tr>
                <% }%>
            </tbody>
        </table>
        <%}else{%>
        <p>学生列表为空！</p>

        <%}%>

        <hr />

        <form action="/students/add" method="post">
            <div>姓名：<input type="text" name="name" /></div>
            <div>
                年龄：<input type="number" max="150" min="0" name="age" />
            </div>
            <div>
                性别：<input type="radio" name="gender" value="男" /> 男
                <input type="radio" name="gender" value="女" /> 女
            </div>
            <div>地址：<input type="text" name="address" /></div>
            <div>
                <button>添加</button>
            </div>
        </form>
    </body>
</html>
```



## 18.Bug处理和csrf攻击

**找bug要先理清程序执行的流程  找到出错的一环**

**index.js**

```javascript
const express = require("express")
const path = require("path")
const app = express()
const cookieParser = require("cookie-parser")
const session = require("express-session")
// 引入uuid
const uuid = require("uuid").v4
// 引入file-store
const FileStore = require("session-file-store")(session)

const userRouter = require("./routes/user")
const goodsRouter = require("./routes/goods")

app.set("view engine", "ejs")
app.set("views", path.resolve(__dirname, "views"))

app.use(express.static(path.resolve(__dirname, "public")))
app.use(express.urlencoded({ extended: true }))
app.use(cookieParser())
app.use(
    session({
        store: new FileStore({
            path: path.resolve(__dirname, "./sessions")
        }),
        secret: "dazhaxie"
    })
)

/* 
    csrf攻击
        - 跨站请求伪造
            - 删除id为3的用户连接 http://localhost:3000/students/delete?id=3
        如何攻击:
            - 写一个网页 用img下的src"http://localhost:3000/students/delete?id=3"
            - 当id为3的用户登录此时刚好登录  黑客网页刷新网站 此时src"http://localhost:3000/students/delete?id=3"会自行向浏览器发送请求
            - 老版本的浏览器(IE)会自动把cookie带回来，浏览器会认为有效  这样用户就被删除了
            - 利用表单为可以向网页中添加用户等功能
        - 现在大部分的浏览器的都不会在跨域的情况下自动发送cookie
            这个设计就是为了避免csrf的攻击
        - 如何解决？
            1. 使用referer头来检查请求的来源
            2. 使用验证码(验证是不是你本人,最安全的方式)
            3. 尽量使用post请求（结合token）

        - token（令牌）
            - 可以在创建表单时随机生成一个令牌
                然后将令牌存储到session中，并通过模板发送给用户
                用户提交表单时，必须将token(先对暗号在处理业务)发回，才可以进行后续操作
                （可以使用uuid(帮助我们生成一个不可计算的唯一id)来生成token）
                    -1.  yarn add uuid
                    -2. 引入 const uuid = require("uuid").v4
                    -3. 为重要功能设置token验证
*/

app.use("/students", require("./routes/student"))

app.get("/", (req, res) => {
    res.render("login")
})

//退出功能
app.get("/logout", (req, res) => {
    // 使session失效
    req.session.destroy(() => {
        res.redirect("/")
    })
})

app.post("/login", (req, res) => {
    // 获取用户的用户名和密码
    const { username, password } = req.body
    if (username === "admin" && password === "123123") {
        // bug问题:登录成功后，没有将用户信息立刻放入到session中
        // 这行代码执行后 req.session.loginUser = username
        // 仅仅是将loginUser添加到了内存中的session中
        // 而没有将值写入到文件中(请求执行后才会写进去)
        // 此时"/students/list"发送第2次请求 会重新拿到session的值(这个值不是最新的,所以登录不上去)
        req.session.loginUser = username

        // 为了使得session可以立刻存储，需要手动调用save
        req.session.save(()=>{
            res.redirect("/students/list")
        })
    } else {
        res.send("用户名或密码错误")
    }
})
app.use((req, res) => {
    res.status(404).send("<h1>您访问的页面已经被外星人劫持</h1>")
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**huairen.html**

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>坏人的网站</title>
</head>

<body>
    <h1>这个网站中有很多你想要的东西！</h1>

    <img src="http://localhost:3000/students/delete?id=7">

    <!-- 强行添加用户 -->
    <!-- <iframe src="display:none;" name="hello"></iframe> -->
    <!-- IE中这样有用 Google没用 -->
    <!-- 但是如果删除了iframe Google也识别不出来 -->
    <!-- <form action="http://localhost:3000/students/add" method="post" target="hello">
        <input type="text" name="name" value="大闸蟹3">
        <input type="text" name="age" value="77">
        <input type="text" name="gender" value="女">
        <input type="text" name="address" value="宁波">
    </form>

    <script>
        //一打开网页自动提交用户的表单
        document.forms[0].submit()
    </script> -->

</body>

</html>
```

**student.js**

```javascript
const express = require("express")
const router = express.Router()
let STUDENT_ARR = require("../data/students.json")
const fs = require("fs/promises")
const path = require("path")

// 引入uuid
const uuid = require("uuid").v4

router.use((req, res, next) => {
    // 获取一个请求报头referer
    const referer = req.get("referer")
    // referer.startsWith() 判断请求来自的方法
    if(!referer || !referer.startsWith("http://localhost:3000/")){
        res.status(403).send("你没有这个权限！")
        return
    }

    // 登录以后，req.session.loginUser是undefined
    if (req.session.loginUser) {
        next()
    } else {
        res.redirect("/")
    }
})

// 学生列表的路由
router.get("/list", (req, res) => {
    // session的默认有效期是一次会话
    // if (req.session.loginUser) {
    //     res.render("students", { stus: STUDENT_ARR })
    // } else {
    //     res.redirect("/")
    // }

    // 生成一个token
    const csrfToken = uuid()

    // 将token添加到session中
    req.session.csrfToken = csrfToken

    req.session.save(() => {
        res.render("students", {
            stus: STUDENT_ARR,
            username: req.session.loginUser,
            csrfToken //一起传入文件
        })
    })
})

// 添加学生的路由
router.post("/add", (req, res, next) => {
    // 取到客户端和表单一起发送的token
    const csrfToken = req.body._csrf //客户端的token
    const sessionToken = req.session.csrfToken //session中的token
    req.session.csrfToken = null //token是一次性的 取完值去比对就置为空

    // 将客户端的token和 session中的token进行比较
    if (sessionToken=== csrfToken) {
        const id = STUDENT_ARR.at(-1) ? STUDENT_ARR.at(-1).id + 1 : 1

        const newUser = {
            id,
            name: req.body.name,
            age: +req.body.age,
            gender: req.body.gender,
            address: req.body.address
        }

        STUDENT_ARR.push(newUser)


        req.session.save(() => {
            //调用next交由后续路由继续处理
            next()
        })
        
    }else{
        res.status(403).send("token错误")
    }
})

// 删除学生的路由
router.get("/delete", (req, res, next) => {
    const id = +req.query.id

    STUDENT_ARR = STUDENT_ARR.filter((stu) => stu.id !== id)

    next()
})

router.post("/update-student", (req, res, next) => {
    const { id, name, age, gender, address } = req.body
    const student = STUDENT_ARR.find((item) => item.id == id)

    student.name = name
    student.age = +age
    student.gender = gender
    student.address = address
    next()
})

router.get("/to-update", (req, res) => {
    const id = +req.query.id
    const student = STUDENT_ARR.find((item) => item.id === id)

    res.render("update", { student })
})

// 处理存储文件的中间件
router.use((req, res) => {
    fs.writeFile(
        path.resolve(__dirname, "../data/students.json"),
        JSON.stringify(STUDENT_ARR)
    )
        .then(() => {
            res.redirect("/students/list")
        })
        .catch(() => {
            res.send("操作失败！")
        })
})

module.exports = router
```

**student.ejs**

```ejs
<!DOCTYPE html>
<html lang="zh">
    <!-- 
        C:\Users\lilichao\Desktop\Node-Course\12_express\views\students.ejs

        localhost:3000/students/list（虚拟路径）

        localhost:3000/css/index.css

        res.render("student")
    
    -->
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>学生列表</title>
        <link rel="stylesheet" href="/css/index.css">
        <!-- <link rel="stylesheet" href="../css/index.css"> -->
        <style>
            table {
                border-collapse: collapse;
            }

            th,
            td {
                border: 1px #000 solid;
                font-size: 20px;
                padding: 10px;
                text-align: center;
            }

            caption {
                font-size: 25px;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <h2>当前用户：<%=username %></h2>
        <a href="/logout">登出</a>
        <hr />
        <% if(stus && stus.length > 0) { %>
        <table>
            <caption>
                学生列表
            </caption>
            <thead>
                <tr>
                    <th>学号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>地址</th>
                    <th>操作</th>
                </tr>
            </thead>

            <tbody>
                <% for(const stu of stus){ %>
                <tr>
                    <td><%=stu.id%></td>
                    <td><%=stu.name %></td>
                    <td><%=stu.age %></td>
                    <td><%=stu.gender %></td>
                    <td><%=stu.address %></td>
                    <td>
                        <a
                            onclick="return confirm('确认删除吗？')"
                            href="/students/delete?id=<%=stu.id%>"
                            >删除</a
                        >
                        <a href="/students/to-update?id=<%=stu.id%>">修改</a>
                    </td>
                </tr>
                <% }%>
            </tbody>
        </table>
        <%}else{%>
        <p>学生列表为空！</p>

        <%}%>

        <hr />

        <form action="/students/add" method="post">
            <!-- 存储一个token -->
            <input type="hidden" name="_csrf" value="<%=csrfToken %>">
            <div>姓名：<input type="text" name="name" /></div>
            <div>
                年龄：<input type="number" max="150" min="0" name="age" />
            </div>
            <div>
                性别：<input type="radio" name="gender" value="男" /> 男
                <input type="radio" name="gender" value="女" /> 女
            </div>
            <div>地址：<input type="text" name="address" /></div>
            <div>
                <button>添加</button>
            </div>
        </form>
    </body>
</html>
```







![uTools_1676104912967](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676104912967.png)
