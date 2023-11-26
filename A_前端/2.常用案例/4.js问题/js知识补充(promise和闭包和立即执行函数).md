## 1.Promsie和async

```js
        // async function m() {
        //     console.log(1)
        //     const n = await 3
        //     console.log(n)
        // }
        // // 在这里补充node的代码执行顺序
        // // 1.await xx  这行代码最先执行(前提是全局log在它后面)
        // // 2.tick队列
        // // 3.微任务队列(await后的代码会进入)  创建方式 ueueMicrotask
        // // 4.宏任务队列 定时器

        // // 其实async和await就是语法糖 本质是Promise 为了解决回调地狱创造出来的
        // function m1 () {
        //     return Promise.resolve(1).then((n) => {
        //         console.log(n);
        //     })
        // }

        // m()
        // console.log(2);

        // 以前解决异步
        // function sum(a,b,cb) {
        //     setTimeout(()=>{
        //         // res = a + b
        //         cb(a+b)
        //     },1000)
        // }

        // sum(1,2,(res)=>{console.log(res)})

        // // 假设我们需要多次调用就会出现 太不优雅了 于是promise出现
        // sum(1,2,(res)=>{
        //     sum(res,3,(res)=>{
        //         console.log(res)
        //     })
        // })


        // 这就是promise的基本使用 
        // const proMise = new Promise((resolve, reject) => {
        //     setTimeout(() => {
        //         resolve("哈哈")//相当于前面的那个cb函数
        //     }, 2000)

        //     resolve("resolve返回的数据")
        //     reject("reject返回的数据")
        // })

        // proMise.then(res => console.log(res))

        // // 以后固定的写法
        function sum(a, b) {
            return new Promise((resolve, reject) => {
                setTimeout(()=>{
                    resolve(a+b)
                    // 一秒后返回
                    console.log("一秒过去了~~~");
                },1000)
            })
        }

        // // sum(1,2).then(result => console.log(result))
        // sum(1,2)
        // .then(res => res + 3)
        // .then(res => console.log(res))

        // // async 和 await 语法糖(用来同步书写代码，以及解决回调地狱)
        // async function a() {
        //     let sum1 = await sum(1,2)
        //     sum1 = await sum(sum1,3)
        //     console.log(sum1)
        // }
        // a()
```



## 2.function 函数的提升

```js
        // function命名 --> 函数声明 --> 会在其它代码执行前辈创建 所以我们可以在函数声明前调用函数
        function fn() {}

  	    // function可以做语句也可以做表达式
        // 语句
        function f(){}
        // 表达式
        var fn1 = function(){}
        
        // 所以Js规定  function出现在行首  一律解析为语句
        // 所以当js看到(function () {console.log(1)})() 会立即执行
```

![image-20230919191807514](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919191807514.png)

```js
function(){} 会报错 必须要命名才不会报错 套上()  --> (function(){})
这样就不会报错了    因为是以()开头了,也变成表达式了,可以立即执行
```



## 3.关于 { }  ()

```
由于var没有块作用域,let有块作用域{}  所以要兼容老版本浏览器才会产生了立即执行函数
()会提升代码的优先级,()也是用来方法调用的
```

俩个立即执行函数会干扰浏览器 所以要记得加分号

![image-20230919192928043](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919192928043.png)

解析成  `()()` 了



## 4.立即执行函数表达式

**立即执行函数就是为了只执行一次的函数创建的,还有以前为var隔离作用域**

```js
	   // 有以下三种写法
        ;(function () {console.log(1)})() //相当于写完了函数然后调用这个函数
      
        ;(function () {console.log(2)}()) //直接在括号中执行这个函数
       
        ;var test = function () {console.log(3)}()

        // 为什会有立即执行函数?  因为表达式在js中会被解析立即执行
        ❤❤通过括号() 及 运算符! + - ~等等运算符可以将它转换为表达式 
```

![image-20230919191543180](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919191543180.png)

**立即执行函数执行完会直接被销毁**

![image-20230919191627454](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919191627454.png)



## 5.闭包

1.基本使用

```js
        <script>
            /* 
                要求: 创建一个函数，第一次调用时打印1，第二次调用打印2，以此类推
                所以可以利用函数，来隐藏不希望被外部访问到的变量

                闭包：
                    闭包就是能访问到外部函数作用域中变量的函数❤(桥梁)
                    在javascript中，只有函数内部的子函数才能读取局部变量，
                    所以闭包可以理解成“定义在一个函数内部的函数“。在本质上，
                    闭包是将函数内部和函数外部连接起来的桥梁。
                什么时候使用：
                    当我们需要隐藏一些不希望被别人访问的内容时就可以使用闭包(不想被全局看到)
                构成闭包的要件：
                    1. 函数的嵌套
                    2. 内部函数要引用外部函数中的变量
                    3. 内部函数要作为返回值返回
            */

            function outer(){
                let num = 0 // 位于函数作用域中
                return () => {
                    num++ //内部函数作用域可以访问到外部函数作用域
                    console.log(num)
                }
            }

            const newFn = outer()

            newFn() //1
            newFn() //2
            newFn() //3
```



2.原理

**词法作用域：函数定义的就确定了作用域  和在哪里调用没关系**

内部作用域(函数作用域)可以看到全局作用域,全局作用域无法访问到内部作用域(函数作用域)



3.闭包生命周期

```js
        /* 
               闭包的生命周期：
                   1. 闭包在外部函数调用时产生，外部函数每次调用都会产生一个全新的闭包
                   2. 在内部函数丢失时销毁（内部函数被垃圾回收了[没人使用]，闭包才会消失）

               注意事项：
                   闭包主要用来隐藏一些不希望被外部访问的内容，这就意味着闭包需要占用一定的内存空间

                   相较于类来说，闭包比较浪费内存空间（类可以使用原型(原型就不会重复创建)而闭包不能），
                       需要执行次数较少时，使用闭包(js一般使用习惯是用闭包)
                       需要大量创建实例时，使用类(类也可以藏东西)  
           */

        function outer2() {
            let num = 0
            return () => {
                num++
                console.log(num)
            }
        }

	    //fn1 和 fn2 是俩个互相独立的  fn1和fn2都指向outer2进行引用
        let fn1 = outer2() // 独立闭包
        let fn2 = outer2() // 独立闭包
        
        fn1 = null  fn2 = null  //此时闭包消失了
```

