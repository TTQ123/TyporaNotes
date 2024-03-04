# Node.js

## Node底层架构

![537cdf6aae7094648300271f61c86c8](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/537cdf6aae7094648300271f61c86c8.jpg)

解释

![image-20240128214345299](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240128214345299.png)

引出了其它的概念

```bash
1.跨平台就是不用一套电脑设备(或换一个操作系统)编一套程序，可以在Linux或者Windows都可以执行 这个功能的实现就是是通过libnv
2.node是单线程，node的单线程体现在程序员只能操作一个线程；但是node底层使用c++实现，c++有线程池，js可以通知c++让线程池帮忙工作(一般有四个线程池)
3.同步的代码在js主线程跑 其它代码他就是在另外三个c++线程上跑
4.浏览器和node一样给js提供了多线程的能力
```



## 1.简介与安装

node十个知识点

![image-20240114152820626](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114152820626.png)

![image-20240114173215724](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114173215724.png)



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



**node涉及的领域**

![image-20240114233939744](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114233939744.png)

**nodejs开发的典型软件**

![image-20240114225502919](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114225502919.png)



**在开发时要安装低版本的node时可以去node中文网的全部安装包下寻找**



## 补充 -命令行常用命令

1.chrome url  就可以使用谷歌打开url的网站

![image-20240114234845321](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114234845321.png)

dir /s  可以查看文件夹下的所有内容



## 补充 -nodejs不能使用Dom和Bom这些Api

![image-20240114235246341](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114235246341.png)



## 补充

### 1.nodejs的顶级对象

顶级对象已经不在是window了

![image-20240114235459945](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114235459945.png)

### 2.Buffer

![image-20240114235605162](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114235605162.png)

创建buffer

![image-20240114235957009](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240114235957009.png)

操作buffer

![image-20240115000407482](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115000407482.png)

![image-20240115000516518](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115000516518.png)

### 3.计网基础

![image-20240115000853951](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115000853951.png)

![image-20240115001008208](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115001008208.png)

![image-20240115001023654](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115001023654.png)

进程就是执行中的程序

![image-20240115001112337](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115001112337.png)

![image-20240115001159769](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115001159769.png)

查看火狐的线程(一个进程至少一个线程可以有多个)

**pslist需要配置命令后才能查看**

![image-20240115001310006](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115001310006.png)





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

![image-20240227000935204](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240227000935204.png)



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

![image-20240226123536275](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240226123536275.png)





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

调用栈和消息队列(事件队列)

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



### 2.如何暴露内容和访问内容

![image-20240131201632998](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131201632998.png)

![image-20240131201715524](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131201715524.png)

注意点说明

```js
// 不能使用exports = value 的形式暴露数据
console.log(moudle.exports === exports); // true
console.log(moudle.exports, exports); // {} {}

// require函数最后导入的是moudle.exports的值
// 所以当你使用exports = '123' 它并没有修改moudle.exports 所以打印出来是一个 {}

// 当你使用exports.str = '123' 相当于是往对象身上挂载了一个属性 这样moudle.exports也会被改变
// 因为exports和moudle.exports引用是同一个对象  你exports = '123'这样就是改了引用地址 但是require引入的是moudle.exports的值
```



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



访问

![image-20240131203127498](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131203127498.png)

**导入包管理工具时导入的就是文件夹**

可以导入的方式1

![image-20240131203934485](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131203934485.png)

导入的方式2

![image-20240131204131697](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131204131697.png)

导入的方式3

![image-20240131204242365](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131204242365.png)



### 补充:导入模块的基本流程

![image-20240131204329507](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240131204329507.png)

```js
/**
 * 伪代码
 */

function require(file){
    //1. 将相对路径转为绝对路径，定位目标文件
    let absolutePath = path.resolve(__dirname, file);

    //2. 缓存检测（有导入过的直接从缓存中拿了返回）
    if(caches[absolutePath]){
      return caches[absolutePath];
    }

    //3. 读取文件的代码转为字符串
    let code = fs.readFileSync(absolutePath).toString();

    //4. 包裹为一个函数 然后执行
    let module = {};
    let exports = module.exports = {};
    // 这是一个立即执行函数 小括号包裹的
    (function (exports, require, module, __filename, __dirname) {
      const test = {
        name: '尚硅谷'
      }
      module.exports = test;
    
      //输出
      console.log(arguments.callee.toString());
    })(exports, require, module, __filename, __dirname)

    //5. 缓存结果
    caches[absolutePath] = module.exports;

    //6. 返回 module.exports 的值
    return module.exports;
  }
  
// 当你导入了一个文件 就会发生上面函数的事情
  const m = require('./me.js')
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

![image-20240202020353424](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240202020353424.png)



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



启动服务器有时无法启动

**这是因为通过f5启动时，根目录是大文件夹，通过node .\a.js启动时根目录是当前文件夹。  解决的方法就是const result = path.resolve(__dirname)**

#### 1.相对路径和绝对路径

```js
const fs = require('fs');

// 相对路径
fs.writeFileSync('./index.html', 'love') // 同级目录
fs.writeFileSync('index1.html', 'love') // 同级目录
fs.writeFileSync('../index2.html', 'love') // 上一级目录

// 绝对路径
fs.writeFileSync('/index3.html', 'love') // / 表示访问根目录
// 补充一个 在d盘要把文件写入c盘权限不够
fs.writeFileSync('D:/index4.html', 'love') // D: 表示访问D盘根目录
```

![image-20240115141643367](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115141643367.png)

![image-20240115141801231](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115141801231.png)

#### 2.补充 __dirname和path.resolve

__dirname提供了当前执行脚本所在目录的路径信息(绝对路径)

![image-20240206034234138](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206034234138.png)



path.resolve用于将路径解析为绝对路径

![image-20240206034359769](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206034359769.png)





### 2.fs基本使用(写入文件)

1.wirteFile

![image-20240115110906946](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115110906946.png)

```js
/*
* 利用fs模块创建一个txt文件
* 并写入内容
*/
// 导入
const fs = require('fs');
// 写入  如果该文件不存在，系统会自动创建
fs.writeFile('./备忘录.txt', '明天是林晶晶生日', err => {
    if (err) {
        console.log('写入失败');
        return
    }
    console.log('写入成功');
})
```

2.writerFileSync

同步的性能差一点(js主线程会等待写入完毕)，但是更容易理解API代码，用在一些对性能要求不是特别高的时候

![image-20240115111333712](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115111333712.png)

3.appendFile异步写入和appendFileSync

![image-20240115112537385](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115112537385.png)

```ts
const fs = require('fs');
// 1.writeFile实现追加写入 开启配置对象
fs.writeFile('./备忘录.txt', ',记得提醒我', {flag: 'a'}, err => {
    if (err) {
        console.log('写入失败');
        return
    }
    console.log('写入成功');
})

// 2.appendFile追加写入
fs.appendFile('./备忘录.txt', ',一定要记得', err => {
    if (err) {
        console.log('写入失败');
        return
    }
    console.log('追加写入成功');
})

// 3.同步追加
fs.appendFileSync('./备忘录.txt', '\r\n这个很重要')
```

#### 1.流式写入文件

![image-20240115112913902](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115112913902.png)

![image-20240115112931884](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115112931884.png)

![image-20240115113142148](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115113142148.png)



#### 2.读取文件

![image-20240115113244984](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115113244984.png)

![image-20240115113456473](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115113456473.png)

![image-20240115113518745](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115113518745.png)



#### 3.流式读取文件

一块一块的读取文件,用来读取大文件性能好

```ts
const fs = require('fs');

// 1.创建读取流对象
const rs = fs.createReadStream('./备忘录.txt')

// 2.绑定data事件 参数chunk为块(每一个块读取的是64kb)
rs.on('data', (chunk) => {
    console.log(chunk.length); // 65536b-> 64kb
    console.log(chunk.toString());
})

// 3.end 可选事件
rs.on('end', () => {
    console.log('读取完成');
})
```



#### 4.直接读取写入和流式读取写入的对比

```js
const fs = require('fs');
// 这个模块可以查看内存占用空间
const process = require('process');

// 直接读取的方式
// 读取文件内容
const data = fs.readFileSync('./备忘录.txt')
// 写入
fs.writeFileSync('./备忘录-1.txt', data)
console.log(process.memoryUsage()); // rss 1107107784字节 -> 105M

// 流式操作
// 创建读取流对象
const rs = fs.createReadStream('./备忘录.txt')
// 创建写入流对象
const ws = fs.createWriteStream('./备忘录-2.txt')

// 监听流的打开
rs.on('data', chunk => {
  // 开始读取文件
  ws.write(chunk)
})

// 结束时统计
rs.on('end', () => {
  ws.end()
  console.log(process.memoryUsage()); // rss 41M
})
```



#### 5.移动和重命名文件

```ts
const fs = require('fs');

// 重命名和移动本质都是更改文件路径
// 文件重命名
fs.rename('./备忘录.txt', './改名.txt', (err) => {
    if(err){
        logger.error('重命名失败');
        return
    }
    console.log('重命名成功');
})

// 文件移动
fs.rename('./改名.txt', './test/改名.txt', (err) => {
    if(err){
        logger.error('移动失败');
        return
    }
    console.log('移动成功');
})
```



#### 6.删除文件

![image-20240115120337409](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120337409.png)

#### 7.文件夹操作

创建文件夹

![image-20240115120635096](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120635096.png)

![image-20240115120652537](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120652537.png)

读取文件夹

![image-20240115120949410](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120949410.png)

删除文件夹

![image-20240115120913149](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120913149.png)

![image-20240115120931075](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115120931075.png)

#### 8.查看资源状态

读取只能获取文件信息 这个方法可以获取文件的所有信息 例如创建时间 大小等等

![image-20240115121247154](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115121247154.png)



#### 9.案例 批量重命名

```js
const fs = require('fs');

// 给每个文件前面加上个0
const files = fs.readdirSync('./test')

// 遍历数组
files.forEach(item => {
    let data = item.split('-')
    let [num, name] = data
    
    // 判断 小于10的加0
    if(Number(num) < 10){
        num = '0' + num
    }

    // 创建新的文件名
    let newName = num + '-' + name

    // 重命名
    fs.renameSync(`./test/${item}`, `./test/${newName}`)
})
```



#### fs方法

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



### 3.path模块

![image-20240115144512208](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115144512208.png)

```js
const fs = require('fs');
const path = require('path');

// resolve 拼接规范的绝对路径
// console.log(path.resolve(__dirname, './index.html'));
// console.log(path.resolve(__dirname, 'index.html'));

// sep 路径分隔符  window是 \  linux是 /
console.log(path.sep);

// __filename 返回文件的绝对路径
console.log(__filename);

// parse 可以解析路径并返回对象
let str = 'D:\\Vs Project\\Node\\2024-1-test\\test.js'
console.log(path.parse(str));

// path.basename 获取文件名
console.log(path.basename(str)); // test.js
```





## 10.包管理器

![image-20240202020759844](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240202020759844.png)

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

#### 1.补充:初始化注意事项

![image-20240202021235499](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240202021235499.png)



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

#### 1.补充npm官网(如何搜索包)

![image-20240202021451841](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240202021451841.png)

`https://www.npmjs.com`

支持中文搜索 比如你要轮播图就直接搜索轮播图



#### 2.补充

![image-20240205002424666](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205002424666.png)

![image-20240205002604839](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205002604839.png)

这个文件是确保依赖包的版本一致的(依赖声明文件)



#### 3.补充：require导入npm包的流程

![image-20240205002944253](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205002944253.png)

![image-20240205003006819](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205003006819.png)

这三行代码都是可以执行的，第三行的逻辑是，首先找到node_modules下的uniq文件夹，然后查看该文件的package.json找到项目入口文件，发现是uniq.js，于是就执行uniq.js



#### 4.开发依赖和生产依赖

![image-20240205003227847](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205003227847.png)

当你安装一个包的时候，这个包大概率也依赖了其它包(没有这些包运行不了)，所以node_modules文件夹会有很多包。

#### 

#### 5.npm全局安装

全局安装的包都会暴露命令让我们去操作包，而不是通过require直接导入在项目中

![image-20240205003903137](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205003903137.png)

#### 6.cjs和mjs

![image-20240205004149949](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205004149949.png)



#### 7.修改windows执行策略

![image-20240205004544034](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205004544034.png)



#### 8.环境变量补充

![image-20240205004949256](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205004949256.png)

windows的可执行文件后缀一般是exe和cmd

#### 9.删除包和安装特定版本的包

![image-20240205005345058](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205005345058.png)



#### 10.npm配置命令别名

![image-20240205005542619](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205005542619.png)



#### 11.配置淘宝镜像

镜像是加速npm的  cnpm是直接到淘宝镜像下载的

![image-20240205005950009](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205005950009.png)

**使用nrm的时候，当你要切换回官方地址的时候直接**

```bash
nrm ls  #查看npm支持的镜像地址
nrm use npm #切换回官网地址
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



#### 1.cnpm

![image-20240205005819432](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205005819432.png)



#### 2.yarn

![image-20240205010748749](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205010748749.png)

全局安装没法使用是因为yarn是基于npm安装的

我们配置node的环境变量时，系统只能找到node.exe和npm.cmd 找不到yarn全局安装的路径

**解决**

![image-20240205011305357](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205011305357.png)



### 4.发布一个npm包

![image-20240205011434008](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205011434008.png)

![image-20240205011911654](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205011911654.png)

npm unpublish --force  删除



### 5.扩展 软件包管理工具

![image-20240205012124751](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205012124751.png)



### 6.nvm

介绍

![image-20240205012208586](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205012208586.png)

安装nvm的时候最后默认安装地址，不要改到d盘里

![image-20240205012517454](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240205012517454.png)

地址 [Releases · coreybutler/nvm-windows (github.com)](https://github.com/coreybutler/nvm-windows/releases)



## 11.http协议

协议就是双方共同遵守的一套规则 

### 1.基础知识

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



### 2.报文

**Get请求的请求体一般为空**

请求报文

![image-20240115180902286](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115180902286.png)

请求行

![image-20240115180959663](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115180959663.png)

![image-20240115181107225](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115181107225.png)

**请求头**

https://developer.mozilla.org/zh-CN/docs/Web/HTTP

请求体

**一般现代的项目都是把数据用json的格式存在请求体中,服务器收到数据后从请求体中拿到数据**



**响应报文**

![image-20240115181832473](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115181832473.png)

![image-20240115181910308](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115181910308.png)

![image-20240115182108124](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182108124.png)



### 3.网络基础概念

ip地址：用来标识网络中的设备，实现设备间通信

![image-20240115182315240](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182315240.png)

![image-20240115182326869](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182326869.png)

![image-20240115182348202](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182348202.png)

ip的分类 解决ip不够用的方法之一

局域网的ip地址是可以共用的，这就是私网ip，只有局域网内的设备可以互相通信，要访问外网就需要一个公共的外网ip

![image-20240115182820065](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182820065.png)

![image-20240115182723956](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115182723956.png)

本地回环ip地址 访问这个地址就是在访问本机

![image-20240115183027237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115183027237.png)

![image-20240115183042804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115183042804.png)

标准ip的完整分类

https://zhuanlan.zhihu.com/p/193729352



**端口 就像大集上的摊位**

![image-20240115183307122](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115183307122.png)

![ ](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115183322353.png)

![image-20240115183436608](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115183436608.png)



### 4.创建一个node原生的http服务

```js
// 1.导入 http 模块
const http = require('http');

// 2.创建服务对象
// req 是请求报文的封装  res 是响应报文的封装
const server = http.createServer((req, res) => {
    // 设置响应头,告诉浏览器返回的是html并且是用utf-8编码格式的
    res.setHeader('content-Type', 'text/html; charset=utf-8'); 
    res.end('你好!'); // 设置响应体,并结束响应
})

// 3.监听端口,启动服务
server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



![image-20240115184328978](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115184328978.png)

![image-20240115184753505](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115184753505.png)

**❤默认端口号在浏览器回车以后会消失不见，其它端口号是不会的。**

![image-20240115185039906](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240115185039906.png)

### 5.通过浏览器查看报文信息

![image-20240123165628406](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240123165628406.png)

在载荷中可以查看我们发给浏览器的参数或者是查询字符串参数

![image-20240123170256587](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240123170256587.png)

![image-20240123170342948](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240123170342948.png)



### 6.获取http请求报文

![image-20240123170531576](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240123170531576.png)

#### 1.获取请求行和请求头

```js
// 1.导入 http 模块
const http = require('http');


// 2.创建服务对象
const server = http.createServer((req, res) => {
    // 获取请求的方法
    console.log(req.method);
    // 获取请求的url url只包括路径和查询参数
    console.log(req.url);
    // 获取请求头 会得到一个对象
    console.log(req.headers);
    res.end('你好!');
})

// 3.监听端口,启动服务
server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

#### 2.获取请求体

```js
const http = require('http');

const server = http.createServer((req, res) => {
    // 1.声明一个变量
    let body = '' // 存储请求体
    // 2.绑定 data 事件
    req.on('data', chunk => {
        // chunk就是一个Buffer对象
        body += chunk
    })
    // 3.绑定 end 事件
    req.on('end', () => {
        // 事件结束后输出请求体
        console.log(body);

        // 系统响应
        res.end('请求体打印ok')
    })
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

#### 3.获取请求路径和查询字符串

老版本 新版本用不了

```js
const http = require('http');

// 1.引入node内置的url模块
const url = require('url');

const server = http.createServer((req, res) => {
    // 2.解析 req.url
    // parse方法是url模块的内置方法 参数1解析路径,参数2解析查询字符串
    let reqUrl = url.parse(req.url, true);
    let pathname = reqUrl.pathname;
    let keyword = reqUrl.query.keyword;
    console.log(pathname,keyword);

    res.end('ok');
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

新版本

![image-20240129014538764](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129014538764.png)

![image-20240129014549998](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129014549998.png)

![image-20240129014459727](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129014459727.png)

```js
const http = require('http');

const server = http.createServer((req, res) => {
   let url = new URL(req.url, 'http://127.0.0.1:3000');
    // 输出路径
    console.log(url);
    // 输出查询字符串（拿出指定的方法）
    console.log(url.searchParams.get('name'));
    res.end('ok');
})


server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

new URL在前端中也是可以使用的

![image-20240124013007303](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240124013007303.png)



#### 4.http请求练习

```js
const http = require('http');

const server = http.createServer((req, res) => {
    // 获取请求方法
    let { method } = req
    // 获取请求路径
    let { pathname } = new URL(req.url, 'http://127.0.0.1:3000');
    res.setHeader('Content-Type', 'text/html;charset=utf-8');

    if (method === 'GET' && pathname === '/login') {
        res.end('登录成功')
    } else if (method === 'GET' && pathname === '/register') {
        res.end('注册成功')
    } else {
        res.end('Not Found')
    }
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



### 7.设置响应报文

![image-20240124013950190](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240124013950190.png)

```js
const http = require('http');

const server = http.createServer((req, res) => {
    // 1.设置响应状态码
    res.statusCode = 203
    // 2.设置响应状态描述(一般是不需要的，会根据状态码自动匹配)
    res.statusMessage = 'Forbidden'
    // 3.设置响应头(响应头可以设置多次,可以自定义响应头,可以设置同名的响应头)
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
    res.setHeader('Server', 'Node.js')
    // 自定义的响应头
    res.setHeader('name', 'zs')
    // 设置同名响应体用一个数组
    res.setHeader('Set-Cookie', ['name=zs', 'age=18'])
    // 4.设置响应体(可以通过write方法或end方法设置,但end有且只能有一个,且每次请求必须有一个)
    res.write('你好')
    res.end(', 我是黄宇哥哥')
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

#### 1.http响应练习

最原始的方法

```js
const http = require('http');

const server = http.createServer((req, res) => {
    res.end(`
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>表格页面</title>
            <style>
                td {
                    width: 100px;
                    height: 100px;
                }
                table,td{
                    border-collapse: collapse;
                }
                table tr:nth-child(odd){
                    background-color: red;
                }
                table tr:nth-child(even){
                    background-color: yellow;
                }
            </style>
        </head>
        <body>
            <table border="1">
                <tr><td></td><td></td><td></td></tr>
                <tr><td></td><td></td><td></td></tr>
                <tr><td></td><td></td><td></td></tr>
                <tr><td></td><td></td><td></td></tr>
            </table>
        
            <script>
                let tds = document.querySelectorAll('td');
                tds.forEach(item => {
                    item.onclick = function(){
                        item.style.backgroundColor = 'blue';
                        console.log(this);
                    }
                })
            </script>
        </body>
        </html>
    `)
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

**进行优化**

```js
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    // 读取html文件
    let html = fs.readFileSync(__dirname + '/index.html')
    // 设置响应体  end可以接收字符串或者是Buffer
    res.end(html)
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



#### 2.网页如何请求资料

首先请求html页面，然后同时并发多个请求加载css、img、js等资源。



#### 3.实现网页引入外部资源

**每一次请求(请求网页、请求资源这些都在向服务器发请求)的时候，我们设置的回调函数都会执行，所以请求css等资源的时候，我们依旧返回html就会造成样式不生效的情况。**

服务器情况

![image-20240129014843282](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129014843282.png)

```js
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    // 参数1必填 完整 URL 或唯一路径
    // 参数2选填 可选的基本 URL：如果设置和url参数只有路径，则相对于 生成 URL base。
    let { pathname } = new URL(req.url, 'http://127.0.0.1:3000')
    if (pathname === '/') {
        let html = fs.readFileSync(__dirname + '/index.html')
        res.end(html)
    }else if (pathname === '/index1.js') {
        let js = fs.readFileSync(__dirname + '/index1.js')
        res.end(js)
    }else if(pathname === '/index.css'){
        let css = fs.readFileSync(__dirname + '/index.css')
        res.end(css)
    }else{
        res.statusCode = 404
        res.end('404 not found')
    }

})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



这样做还是很麻烦，才三个路径要写一堆

引入概念

![image-20240129015031352](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129015031352.png)



#### 4.静态资源服务

对第三小节的代码进行优化

项目结构

![image-20240129021316618](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129021316618.png)

代码

```js
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    // 获取请求url的路径
    let { pathname } = new URL(req.url, 'http://127.0.0.1')
    // 拼接文件路径
    let filePath = __dirname + '/page' + pathname;
    // 读取文件
    fs.readFile(filePath, (err, data) => {
        if(err){
            res.statusCode = 500;
            res.end('文件读取失败');
            return
        }
         // 响应文件内容
         res.end(data);
    })
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

访问127.0.0.1:3000/index.html  就可以访问了



#### 5.网站根目录或静态资源目录

![image-20240129021801284](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129021801284.png)

思考题的答案就是打开的当前文件夹



#### 6.绝对路径补充

![image-20240129022236827](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129022236827.png)

```html
    <!-- 完整外链 -->
    <a href="https://www.baidu.com">百度</a>

    <!-- /与页面的协议进行拼接在发送请求 -->
    <a href="//jd.com">京东</a>
    
    <!-- 与页面协议、主机名、端口拼接在发送请求(有点是前面的主机名等变了也不影响) -->
    <!-- 跳转到http://127.0.0.1:5500/serach -->
    <a href="/serach">搜索</a>
```



#### 7.相对路径补充

![image-20240129022902023](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129022902023.png)

根据url得到根目录为/course



#### 8.网页中url的使用小结

![image-20240129023140081](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129023140081.png)

相对路径不可靠，我们还是要用绝对路径，这点就像前端工程中的@

![image-20240129023412444](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129023412444.png)

这三种方式都可以跳转，但是我们还是选择第二种绝对路径。



#### 9.设置MIME类型(资源类型)

![image-20240129023540987](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129023540987.png)

```js
const http = require('http');
const fs = require('fs');
const path = require('path');
let mimes = {
    html: 'text/html',
    css: 'text/css',
    js: 'text/javascript',
    jpg: 'image/jpeg',
    png: 'image/png',
    json: 'application/json',
    gif: 'image/gif'
}


const server = http.createServer((req, res) => {
    // 获取请求url的路径
    let { pathname } = new URL(req.url, 'http://127.0.0.1')
    // 拼接文件路径
    let filePath = __dirname + '/page' + pathname;

    // 读取文件
    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.statusCode = 500;
            res.end('文件读取失败');
            return
        }

        // 获取文件类型的后缀名
        let ext = path.extname(filePath).slice(1)
        let type = mimes[ext]
        if(type){
            res.setHeader('content-type', type)
        }else{
            // 未知的资源类型(会进行下载)
            res.setHeader('content-type', 'application/octet-stream')
        }
        
        res.end(data);

    })
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



#### 10.乱码解决和错误处理

乱码

```js
const http = require('http');
const fs = require('fs');
const path = require('path');
let mimes = {
    html: 'text/html',
    css: 'text/css',
    js: 'text/javascript',
    jpg: 'image/jpeg',
    png: 'image/png',
    json: 'application/json',
    gif: 'image/gif'
}


const server = http.createServer((req, res) => {
    // 获取请求url的路径
    let { pathname } = new URL(req.url, 'http://127.0.0.1')
    // 拼接文件路径
    let filePath = __dirname + '/page' + pathname;

    // 读取文件
    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.statusCode = 500;
            res.end('文件读取失败');
            return
        }

        // 获取文件类型的后缀名
        let ext = path.extname(filePath).slice(1)
        let type = mimes[ext]
        if (type) {
            if (ext === 'html') {
                // 这里设置的字符集优先级比html的meta标签优先级高
                res.setHeader('content-type', type + ';charset=utf-8') // 解决乱码
            } else {
                res.setHeader('content-type', type)  // 除了html页面 其它资源没必要设置字符集，让他根据网页的字符集解析(这样还不会暴露js等资源)
            }
        } else {
            // 未知的资源类型(会进行下载)
            res.setHeader('content-type', 'application/octet-stream')
        }

        res.end(data);

    })
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```

错误处理

```js
const http = require('http');
const fs = require('fs');
const path = require('path');
let mimes = {
    html: 'text/html',
    css: 'text/css',
    js: 'text/javascript',
    jpg: 'image/jpeg',
    png: 'image/png',
    json: 'application/json',
    gif: 'image/gif'
}


const server = http.createServer((req, res) => {
    // 请求方法判断
    if (req.method !== 'GET') {
        res.statusCode = 405;
        res.end('405 Method Not Allowed');
        return
    }
    // 获取请求url的路径
    let { pathname } = new URL(req.url, 'http://127.0.0.1')
    // 拼接文件路径
    let filePath = __dirname + '/page' + pathname;

    // 读取文件
    fs.readFile(filePath, (err, data) => {
        if (err) {
            // 设置字符集
            res.setHeader('content-type', type + ';charset=utf-8')
            //  错误的类型
            switch(err.code){
                case 'ENOENT':
                    res.statusCode = 404;
                    res.end('404 Not Found');
                case 'EPERM':
                    res.statusCode = 403
                    res.end('403 Forbidden')
                default:
                    res.setHeader = 500
                    res.end('500 Internal Server Error')        
            }
            return
        }

        // 获取文件类型的后缀名
        let ext = path.extname(filePath).slice(1)
        let type = mimes[ext]
        if (type) {
            if (ext === 'html') {
                // 这里设置的字符集优先级比html的meta标签优先级高
                res.setHeader('content-type', type + ';charset=utf-8') // 解决乱码
            } else {
                res.setHeader('content-type', type)  // 除了html页面 其它资源没必要设置字符集，让他根据网页的字符集解析(这样还不会暴露js等资源)
            }
        } else {
            // 未知的资源类型(会进行下载)
            res.setHeader('content-type', 'application/octet-stream')
        }
        res.end(data);

    })
})

server.listen(3000, () => {
    console.log('服务已经启动了');
})
```



#### 11.GET和POST请求

![image-20240129030822503](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129030822503.png)

![image-20240129030847828](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129030847828.png)





##### 1.区别

![image-20240226235929408](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240226235929408.png)























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



### 补充: 路由

![image-20240206024549992](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206024549992.png)

#### 1.第一个服务

```js
const express = require('express')

const app = express()

app.get('/home',(req,res)=>{
    res.end('我是home路由')
})

app.post('/test', (req, res) => {
    res.end('我是test路由,我是post方法')
})

// all方法可以匹配所有方法  *可以匹配所有路径
app.all('*', (req, res) => {
    res.send('404 NOT FOUND')
})

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```

#### 2.获取请求参数

![image-20240206025620733](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206025620733.png)



#### 3.获取路由参数

获取路由参数(params) 根据参数返回不同的页面

![image-20240206030848019](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206030848019.png)

？前面的是路由参数，？后边的是查询字符串参数

练习:根据路由参数响应歌手的信息

```js
const express = require('express')
const { singer } = require('./singer.json')
const app = express()

app.get('/singer/:id.html', (req, res) => {
    // 获取路由参数
    let id = req.params.id

    // 在json中寻找对应的数据
    let data = singer.find(item => {
        if (item.id === Number(id)) {
            // id正确放行
            return true
        }
    })

    // 确保数据存在
    if (!data) {
        res.end('404')
    }

    res.end(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <h2>id:${data.id}</h2>
        <h2>name:${data.name}</h2>
    </body>
    </html>
    `)
})

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```



#### 4.express响应设置

![image-20240206032806050](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206032806050.png)

**express的send方法会自动在响应头上设置字符集方法，解决中文乱码**

设置响应文件内容

```js
app.get('/test', (req, res) => {
    // let result = path.resolve(__dirname, './singer.json')
    // res.sendFile(result)

    // 可以简便设置
    res.sendFile(path.resolve(__dirname, 'singer.json'))
    // 或者使用拼接 拼接时不能用./
    // res.sendFile(__dirname + '/singer.json')
})
```

#### 5.中间件

![image-20240206150115481](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240206150115481.png)



##### 1.全局中间件案例

记录每一次访问服务器的ip和路径

```js
const express = require('express')
const path = require('path')
const fs = require('fs')
const app = express()


// 声明中间件函数
function recordMiddleware(req, res, next) {
    let {url, ip} = req
    fs.appendFileSync(path.resolve(__dirname, 'log.txt'), `${url}, ${ip}\r\n`)
    // 调用下一个路由回调函数
    next()
}

// 使用中间件
app.use(recordMiddleware)
 
app.get('/test', (req, res) => {
    res.send('前台页面')
})

app.get('/admin', (req, res) => {
    res.send('后台页面')
})

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```



##### 2.中间件实践(局部中间件)

**这个功能常常用于需要授权的访问的路径时**

![image-20240208015112923](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208015112923.png)

```js
const express = require('express')
const app = express()

// 声明中间件函数
function checkMiddleware(req, res, next) {
    if(req.query.code === '521'){
        // 调用下一个回调函数(访问什么路径调什么)
        next()
    }else{
        res.send('无权限访问,安号错误')
    }
}
 
//  需要授权的路径都调用这个中间件(抽取公共代码)
app.get('/setting', checkMiddleware, (req, res) => {
    res.send('设置页面')
})

app.get('/admin', checkMiddleware, (req, res) => {
    res.send('后台页面')
})

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```



##### 3.静态资源中间件

在express框架中只需要一行代码就可以解决请求静态资源的处理(没有框架时很麻烦)

框架会帮我们寻找到文件并自动设置MIME类型

![image-20240208020716152](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208020716152.png)

**注意点**

当设置了静态路由中间件时，/ 路径是谁写前面先访问谁。

![image-20240208021101077](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208021101077.png)



#### 6.解析请求体数据body-parser

```js
const express = require('express')
// 引入express请求体解析的包
const bodyParser = require('body-parser')
const app = express()

// 解析querystring格式请求体的中间件函数
const urlencodedParser = bodyParser.urlencoded({ extended: false })
// 解析json格式请求体的中间件函数
const json = bodyParser.json()

// 登录页
app.get('/login', (req, res) => {
    res.sendFile(__dirname + '/login.html')
})

// 提交后跳转进行处理
app.post('/login', urlencodedParser, (req, res) => {
    let {username, password} = req.body
    console.log(username, password);
    res.send('登录成功')
})

app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```

登录页

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
</head>
<body>
    <h2>Login页面</h2>
    <hr>
    <form action="/login" method="post">
        用户名: <input type="text" name="username"> <br>
        密码: <input type="text" name="password">
        <button>提交</button>
    </form>
</body>
</html>
```



#### 7.防盗链实现

**防盗链就是为了防止外部网站盗用本网站资源，依靠refer请求头来实现**

**referer请求头会自动携带当前网页的协议、域名、端口号向服务器发送请求，我们可以拿到域名来做限制，非本服务器发送的静态资源请求返回404**

![image-20240208023222007](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208023222007.png)

例子(简单实现)

```js
const express = require('express')
const app = express()

// 声明中间件判断有无referer
app.use((req, res, next) => {
    // 检测请求头中的 referer是否为127.0.0.1
    let referer = req.get('referer')

    // 如果referer存在
    if (referer) {
        let url = new URL(referer)
        // 获取域名
        let hostname = url.hostname
        // 进行限制 非127.0.0.1访问时返回404
        if (hostname !== '127.0.0.1') {
            res.status(404).send('404 not found')
            return
        }
    }
    next()
})

// 静态资源中间件设置
app.use(express.static(__dirname + '/public'))

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```

html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>资源页面</title>
</head>
<body>
    <p>资源页面</p>
    <!-- 向本网站服务器发送请求获取图片 -->
    <img src="http://127.0.0.1:3000/images/w.png">
</body>
</html>
```

严谨一点的 https://juejin.cn/post/7321964344397152256



#### 8.路由模块化

拆分路由，每个子路由管理部分路由规则

入口文件

```js
const express = require('express')
const app = express()

// 导入路由
const homeRouter = require('./routes/useHomeRoute')

// 使用路由规则
app.use(homeRouter)

// 启动服务
app.listen(3000, () => {
    console.log('服务已经启动,端口3000');
})
```

路由文件

```js
// 1.导入express
const express = require('express')

// 2.创建路由对象
const router = express.Router()

// 创建全局中间件函数
const fn = (req, res, next) => {
    console.log('我是/home路由规则的全局中间件函数');
    next()
}
// 使用中间件
router.use(fn)

// 创建局部中间件函数
const fn1 = (req, res, next) => {
    console.log('我是/home路由规则的局部中间件函数');
    next()
}


// 3.创建路由规则
router.get('/home', (req, res) => {
    res.send('首页')
})

router.get('/test', fn1, (req, res) => {
    res.send('测试')
})

// 4.暴露路由
module.exports = router
```

**路由可以设置前缀**

![image-20240208225305125](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208225305125.png)

indexRouter下的每个路由都会在前面补/

usersRouter下的每个路由都会在前面补/users

![image-20240208225646889](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208225646889.png)



#### 9.express-generator

可以快速创建一个express应用的骨架

```bash
npm i -g express-generator

# 创建 -e命令 generator表示文件夹名称
express -e generator
```



#### 10.文件上传

##### 1.文件上传的报文

也是一段http报文，但是分成了多段的报文。

##### 2.express处理文件上传

准备工作

![image-20240218233524194](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240218233524194.png)

![image-20240218233539774](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240218233539774.png)

![image-20240218233602852](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240218233602852.png)

安装formidable库  这个库可以处理文件上传

```js
var express = require('express');
var router = express.Router();
var { formidable } = require('formidable');

// 文件上传表单网页
router.get('/', function (req, res, next) {
  res.render('portrait');
})

// 文件处理
router.post('/', function (req, res, next) {
  // 创建form对象
  const form = formidable({
    multiples: true, // 支持多文件上传
    keepExtensions: true, // 保持文件的后缀
    uploadDir: __dirname + '/../public/images' // 文件上传目录
  });

  // 解析请求报文
  // fields存放的是radio select这些简单的
  // files存放的就是图片这些file类型的
  form.parse(req, (err, fields, files) => {
    if (err) {
      next(err);
      return;
    }
    
    // 在服务器中保存文件的访问URL 便于之后用户请求
    // 例如/images/1.png
    let url = '/images/' + files.portrait[0].newFilename; // 将来保存在数据库中
    res.send(url)
  });
})

module.exports = router;
```



##### 3.项目案例

###### 1.lowdb数据管理

通过一个JSON文件来实现数据的管理

npm i lowdb@1.0.0

![image-20240219032402093](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219032402093.png)



### 2.*nodemon*自动监视代码修改

```css
  目前，服务器代码修改后必须要重启,我们希望有一种方式，可以自动监视代码的修改，代码修改以后可以自动重启服务器。

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

![image-20240208031007984](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208031007984.png)

**ejs就是一种模板引擎,可以在前端页面动态显示数据，比如java的(jsp、Thymeleaf)**

**ejs的优势是内容通过服务器返回，网站的SEO排名更高，毕竟是前后端混合的。**

#### 1.初体验

语法

```ejs
<%= %> 在ejs中输出内容时，它会自动对字符串中的特殊符号进行转义 &lt;这个设计主要是为了避免 xss 攻击
<%- %> 会直接将内容输出(容易造成XSS攻击)
<% %>  可以在其中直接编写js代码，js代码会在服务器中执行
```

服务端

```js
// 导入ejs
const ejs = require('ejs')

// 定义西游记数组
const xiyou = ['唐三藏', '孙悟空', '猪八戒', '沙僧', '白龙马']

// 导入fs
const fs = require('fs')

// 导入html
const html = fs.readFileSync('./03.html').toString() // 读取html并转化为字符串格式

// ejs模板渲染
// 第一个参数是html字符串,第二个参数是数据
const result = ejs.render(html, {xiyou})

console.log(result);
```

模板引擎

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>西游记</title>
</head>

<body>
    <ul>
        <% xiyou.forEach(item=> { %>
            <li>
                <%= item %>
            </li>
        <% }) %>
    </ul>
</body>

</html>
```

#### 2.ejs条件渲染

```js
// 导入ejs
const ejs = require('ejs')

let isLogin = true

// 导入fs
const fs = require('fs')

// 导入html
const html = fs.readFileSync('./03.html').toString() // 读取html并转化为字符串格式

// ejs模板渲染
// 第一个参数是html字符串,第二个参数是数据
const result = ejs.render(html, {isLogin})
console.log(result);
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>西游记</title>
</head>

<body>
    <% if(isLogin){ %>
        <span>欢迎回来</span>
    <% }else{ %>
        <p>未登录状态</p>
    <% } %>
</body>

</html>
```

#### 3.express中使用ejs模板引擎

```js
const express = require('express')
const app = express()
const path = require('path')

// 1.设置nodejs的模板引擎为ejs(安装后才能设置,会自动导入)
app.set('view engine', 'ejs')
// 2.设置模板引擎文件存放的位置 (模板文件:具有模板语法内容的文件)
// 参数1固定的 参数2表示路径地址
app.set('views', path.resolve(__dirname, './views'))

// 创建路由
app.get('/home', (req, res) => {
    // 3. render响应并创建模板文件
    let msg = '我是一条消息'
    // res.render('模板文件名', '传入的数据')
    res.render('home', {msg})
})

app.listen(3000, () => {
  console.log('服务启动');  
})
```

ejs文件

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板文件后缀名ejs</title>
</head>
<body>
    <h2>输出:<%= msg %></h2>
</body>
</html>
```

![image-20240208224412217](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240208224412217.png)



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



## 19.MongoDB

![image-20240219032913053](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219032913053.png)

![image-20240219033123701](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219033123701.png)



### 1.安装

![image-20240219034435554](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219034435554.png)

![image-20240219034454128](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219034454128.png)

mongo启动交互  mongod启动服务



### 2.语法

![image-20240219034637124](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219034637124.png)

![image-20240219034847305](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219034847305.png)

#### 1.增删改查

![image-20240219034918218](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219034918218.png)

**1.find不加条件时默认查询整个集合**

**2.更新时默认是将整个对象重新赋值更新，所以我们不想覆盖时需要加上$set**

#### 2.字段类型(属性值类型)

![image-20240219042802020](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219042802020.png)

ObjectId必须是文档ID，就是一个数组去查另一个数组(相当于表的外键)

#### 3.字段校验和验证

![image-20240219131105866](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219131105866.png)



### 3.mongoose

**我们这里没有用promise的写法**

![image-20240219040313880](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219040313880.png)

![image-20240219040426245](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219040426245.png)

具体操作

```js
// 1.导入mongoose
const mongoose = require('mongoose');

// 设置strictQuery为true(规避一些提醒)
mongoose.set('strictQuery', true);

// 2.连接服务器
mongoose.connect('mongodb://127.0.0.1:27017/bilibili');

// 3.设置回调处理业务  once一次,事件回调函数执行一次(on如果服务断了连回来还会执行)
// 所以官方建议open事件用once 其它用on
// 连接成功
mongoose.connection.once('open', () => {
    // 开始执行业务
    // 4.创建文档的结构对象(设置集合中文档的属性及属性值的类型)
    let userSchema = new mongoose.Schema({
      name: String,
      age: 18  
    })
    // 5.创建模型对象(对文档操作的封装对象,可以增删改查文档)
    let userModel = mongoose.model('users', userSchema);
})
// 连接失败
mongoose.connection.on('error', () => {
    console.log('连接失败了');
})
// 连接关闭
mongoose.connection.on('close', () => {
    console.log('连接已关闭');
})

// 延时关闭mongodb的连接
// setTimeout(() => {
//     mongoose.disconnect();
// })
```

#### 1.增删改查

增

![image-20240219131747571](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219131747571.png)

删

![image-20240219131727688](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219131727688.png)

![image-20240219134741775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219134741775.png)

改

![image-20240219134606457](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219134606457.png)

![image-20240219134834138](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219134834138.png)

查

![image-20240219135043546](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219135043546.png)

![image-20240219135023909](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219135023909.png)

**获取所有  BookModel.find()**



#### 2.条件控制

分为三种

![image-20240219141803612](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219141803612.png)

![image-20240219141844096](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219141844096.png)

普通条件

![image-20240219141559642](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219141559642.png)

正则

![image-20240219141702543](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219141702543.png)

![image-20240219141728060](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219141728060.png)



#### 3.个性化读取(带条件)

![image-20240219142040848](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219142040848.png)

![image-20240219142313341](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219142313341.png)

**skip是跳过,比如你要取4-6条   就可以写成.find().skip(3).limit(3)**

**实例**

![image-20240219142423149](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219142423149.png)

![image-20240219142443012](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219142443012.png)

![image-20240219142504211](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219142504211.png)

#### 4.mongoose模块化

![image-20240219153605017](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240219153605017.png)



入口文件index.js

```js
// 导入mongoose
const mongoose = require('mongoose');

// 导入db(数据库连接文件)
const db = require('./db/db');

// 导入user模型
const userModel = require('./models/UserModel');

// 调用db的函数 执行success步骤
db(() => {
    // 新增
    userModel.create({
        name: '李四',
        age: 19
    }, (err, data) => {
        if (err) {
            console.log(err);
            return
        }
        console.log(data);
        mongoose.disconnect();
    })
})
```

数据库地址配置文件config.js

```json
module.exports = {
    DBHOST: '127.0.0.1',
    DBPORT: '27017',
    DBNAME: 'bilibili'
}
```

数据库基础操作文件 db.js

```js
// mongoose入口文件
/**
 * @param {*} success 数据库连接成功回调
 * @param {*} error 数据连接失败的回调  
 **/
// 导入数据库地址配置文件
const {DBHOST, DBPORT, DBNAME} = require('../config/config');

module.exports = (success, error) => {
    // 连接错误时进行默认值赋值
    if (typeof error !== 'function') {
        error = () => {
            console.log('连接失败');
         }
    }

    // 导入mongoose
    const mongoose = require('mongoose');
    mongoose.set('strictQuery', true);
    mongoose.connect(`mongodb://${DBHOST}:${DBPORT}/${DBNAME}`);
    
    // open时调用success()
    mongoose.connection.once('open', () => {
        success()
    })

    // 失败时调用error()
    mongoose.connection.on('error', () => {
        error()
    })

    mongoose.connection.on('close', () => {
        console.log('连接已关闭');
    })
}
```

数据库模型对象 UserModel.js

```js
const mongoose = require('mongoose');

// 创建文档结构规范
let userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
        default: '匿名'
    },
    age: Number
})
// 创建集合
let userModel = mongoose.model('users', userSchema);

// 暴露模型对象
module.exports = userModel;
```









![uTools_1676104912967](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676104912967.png)





