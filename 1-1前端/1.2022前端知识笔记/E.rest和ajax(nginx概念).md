# Rest和Ajax(包含Fetch和Axios)

## 1.传统服务器总结

**MVC M数据模型 V视图  C控制器**

**传统前端  M 表示json等数据模型,Ejs等模板引擎代表视图，路由可以理解为控制器**

**现在的发展方向就是对服务器解耦合,服务器只负责向客户端返回数据，前端就有了用武之地(视图层 VUE React)**

```css
我们之前编写的服务器都是传统的服务器，服务器的结构是基于MVC模式
    Model -- 数据模型
    View -- 视图，用来呈现
    Controller -- 控制器，复杂加载数据并选择视图来呈现数据
    - 传统的服务器是直接为客户端返回一个页面(ejs)
    - 但是传统的服务器并不能适用于现在的应用场景

现在的应用场景，一个应用通常都会有多个客户端（client）存在
    web端    移动端（app）    pc端  
    - 如果服务器直接返回html页面，那么服务器就只能为web端提供服务
        其他类型的客户端还需要单独开发服务器，这样就提高了开发和维护的成本

如何解决这个问题？
    - 传统的服务器需要做两件事情，第一个加载数据，第二个要将模型渲染进视图
    - 解决方案就是将渲染视图的功能从服务器中剥离出来，
        服务器只负责向客户端返回数据，渲染视图的工作由客户端自行完成
    - 分离以后，服务器只提供数据，一个服务器可以同时为多种客户端提供服务器
        同时将视图渲染的工作交给客户端以后，简化了服务器代码的编写

Rest
    - REpresentational State Transfer(全称) 
    - 表示层状态的传输(把数据传给前端)
    - Rest实际上就是一种服务器的设计风格
    - 它的主要特点就是，服务器只返回数据
    - 服务器和客户端互相传输数据时通常会使用JSON作为数据格式
		- 使用了Rest风格的服务器都用JSON传递
		- JSON的好处是体积小,还可以转化为各种语言的对象,方便跨语言开发
    - 请求的方法：
        GET    加载数据(获取学生信息)
        POST   新建或添加数据(新建学生信息)
        PUT    添加或修改数据(修改学生信息)
        PATCH  修改数据 ..
        DELETE 删除数据  ..
        OPTION 由浏览器自动发送，检查请求的一些权限(预请求)
    - API（接口） Endpoint（端点）[访问Rest服务的路径:其实就是路由,也就是接口和断点]
        GET /user  加载user
        POST /user  添加user
        DELETE /user/:id  删除id为xx的用户
        ...

postman
    - 这是一个软件，通过它可以帮助向服务器发送各种请求
        它帮助我们测试API

AJAX
跨域的问题
```



## 2.编写一个Rest风格的API接口

**index.js**

```javascript
const express = require("express")

const app = express()

const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]

app.use(express.urlencoded({extended:true}))
// 解析json格式请求体的中间件
app.use(express.json())

// 定义学生信息的路由
app.get("/students", (req, res) => {
    console.log("收到students的get请求")
    // 返回学生信息
    res.send({
        status: "ok",
        data: STU_ARR
    })
})

// 查询某个学生的路由


// 定义一个添加学生的路由
app.post("/students", (req, res) => {
    console.log("收到students的post请求", req.body)
    // 获取学生的信息
    const {name, age, gender, address} = req.body
    // 将学生信息添加到数组
    STU_ARR.push({
        id: +STU_ARR.at(-1).id + 1 + "",
        name,
        age:+age,
        gender,
        address
    })

    // 添加成功
    res.send({
        status: "ok",
        //获取数据 data表示数据
        data: STU_ARR
    })
})

// 定义一个删除学生的路由 根据id删除学生
// app.delete()

// 定义一个修改学生的路由
// app.put()


app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```



## 3.Postman

**由于路径都是同名的，我们无法测试所有路由，所以需要Postman这个测试工具**

**Post请求提交数据,用请求体**

![uTools_1679473108316](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679473108316.png)

**开发中常用的:传JSON格式**

![uTools_1679473250920](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679473250920.png)

**此时express需要引入解析JSON格式的中间件**

```javascript
// 解析json格式请求体的中间件
app.use(express.json())
```

**尝试发送JSON**

![uTools_1679473725043](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679473725043.png)

![uTools_1679473702813](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679473702813.png)



## 4.完整Rest风格的API

```javascript
const express = require("express")

const app = express()

const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]

app.use(express.urlencoded({extended:true}))
// 解析json格式请求体的中间件
app.use(express.json())

// 定义学生信息的路由
app.get("/students", (req, res) => {
    console.log("收到students的get请求",req.body)
    // 返回学生信息
    res.send({
        status: "ok",
        data: STU_ARR
    })
})

// 查询某个学生的路由
app.get("/students/:id",(req,res)=>{
    //获取传入的id
    const id = req.params.id
    //根据id查找数据
    const stu = STU_ARR.find( item => item.id === id)
    // const stu = STU_ARR.find((item)=>{
    //  item其实相当于指代数组  item.id=>>数组.id
    //     return item.id === id
    // })

    res.send({
        status:"OK",
        data:stu
    })
})


// 定义一个添加学生的路由
app.post("/students", (req, res) => {
    console.log("收到students的post请求", req.body)
    // 获取学生的信息
    const {name, age, gender, address} = req.body
    //创建学生信息
    const stu = {
        id: +STU_ARR.at(-1).id + 1 + "",
        name,
        age:+age,
        gender,
        address
    }
    // 将学生信息添加到数组
    STU_ARR.push(stu)

    // 添加成功
    res.send({
        status: "ok",
        //只显示当前新添加的
        data: stu
    })
})

// 定义一个删除学生的路由 根据id删除学生
app.delete("/students/:id",(req,res) => {
    //获取传入的id
    const id = req.params.id
    //遍历数组删除元素
    for(let i =0;i<STU_ARR.length;i++){
        if (id===STU_ARR[i].id) {
            //返回被删除的数据
            const delStu = STU_ARR[i]
            STU_ARR.splice(i, 1)
            res.send({
                status:"ok",
                data:delStu
            })
            //返回 不返回下面的错误一定会执行
            return
        }      
    }

    //id错误或不存在
    //返回错误状态码
    res.status(403).send({
        status:"error",
        data:"学生id不存在或错误"
    })
})

// 定义一个修改学生的路由
app.put("/students",(req,res) => {
    //获取要修改的学生的数据
    const {id,name,age,gender,address}=req.body
    const updateStu = STU_ARR.find(item => item.id===id)

    //updateStu存在就是找到了可以进行修改
    if (updateStu) {
        updateStu.name = name
        updateStu.age = age
        updateStu.gender = gender
        updateStu.address = address

        res.send({
            status: "ok",
            data: updateStu
        })
    } else {
        res.status(403).send({
            status: "error",
            data: "学生id不存在"
        })
    }
})


app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```



## 5.AJAX简介

**项目上线时,服务器和客户端要放在俩个不同的服务器中,就算是相同的服务器也要放在不同的端口号下。这样是为了解耦合**

**此时我们需要用到AJAX在客户端拿到服务器的数据**

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>这是一个网页</title>
    </head>
    <body>
        <h1>这是客户端</h1>
        <!-- 
        把服务器中的数据在网页中显示出来！
    -->
        <button id="btn">点我加载数据</button>

        <script>
            // 点击按钮以后，就去自动去加载服务器的数据
            const btn = document.getElementById("btn")
            btn.onclick = () => {
                // 向服务器发送请求了
                // https://restfulapi.net/http-status-codes/
                /* 
                    在js中向服务器发送请求来加载数据的技术叫AJAX

                    AJAX
                        - A 异步  J JavaScript A 和 X xml
                        - 异步的js和xml
                        - 它的作用就是通过js向服务器发送请求来加载数据
                        - xml是早期AJAX使用的数据格式
                            <student>
                                <name>孙悟空</name>    
                            </student>
                        - 目前数据格式都使用json
                            {"name" :"孙悟空"}
                        
                        - 可以选择的方案：
                            ① XMLHTTPRequest（xhr）
                            ② Fetch
                            ③ Axios

                    - CORS (跨域资源共享)
                        - 跨域请求
                            - 如果两个网站的完整的域名不相同
                                a网站：http://haha.com 
                                b网站：http://heihei.com
                                a网站向b网站发送请求，此时会发生跨域
                            - 跨域需要检查三个东西：
                                协议 域名 端口号
                                http://localhost:5000
                                http://127.0.0.1:5000
                                - 三个只要有一个不同，就算跨域
                            - 当我们通过AJAX去发送跨域请求时，
                                浏览器为了服务器的安全，会阻止JS读取到服务器的数据

                        - 解决方案
                            - 在服务器中设置一个允许跨域的头
                                Access-Control-Allow-Origin
                                    - 允许那些客户端访问我们的服务器
                                https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
                        
                */           
            }
        </script>
    </body>
</html>
```



## 6.跨域问题

```css
 		- CORS (跨域资源共享)
                        - 跨域请求
                            - 如果两个网站的完整的域名不相同
                                a网站：http://haha.com 
                                b网站：http://heihei.com
                                a网站向b网站发送请求，此时会发生跨域
                            - 跨域需要检查三个东西：
                                协议 域名 端口号
                                http://localhost:5000
                                http://127.0.0.1:5000
                                - 三个只要有一个不同，就算跨域
                            - 当我们通过AJAX去发送跨域请求时，
                                浏览器为了服务器的安全，会阻止JS读取到服务器的数据

                        - 解决方案
                            - 在服务器中设置一个允许跨域的头
                                Access-Control-Allow-Origin
                                    - 允许那些客户端访问我们的服务器
                                https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
                                
```

**index.js**

```javascript
const express = require("express")

const app = express()

const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]

//解析请求体
app.use(express.urlencoded({ extended: true }))
// 解析json格式请求体的中间件
app.use(express.json())

app.use((req, res) => {
    // 设置响应头
    res.setHeader("Access-Control-Allow-Origin", "*")
    //❤设置跨域以后 发送请求的时候会发送俩个请求 一个预请求检查跨域问题 然后才发真正的请求 
    res.setHeader("Access-Control-Allow-Methods", "GET,POST")
    res.setHeader("Access-Control-Allow-Headers", "Content-type")
    // Access-Control-Allow-Origin 设置指定值时只能设置一个
    // res.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500")
    // ❤要设置多个客户端可以访问，我们要用数组来解决(指定客户端)
    // res.setHeader("Access-Control-Allow-Origin", ARR)
    // Access-Control-Allow-Methods 允许的请求的方式
    // Access-Control-Allow-Headers 允许传递的请求头
})

// 统一的api
// 定义学生信息的路由
app.get("/students", (req, res) => {
    console.log("收到students的get请求")
    // 返回学生信息
    res.send({
        status: "ok",
        data: STU_ARR
    })
})


app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

**设置跨域处理以后,每次会发送俩个请求，options预请求检查跨域问题 然后才发真正的请求 **

![uTools_1679495696397](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679495696397.png)

**能解决跨域的情况必须1.是服务器是自己人(常见情况:前端页面一个服务器，处理请求的后台服务器自己占一个服务器 可以通过cors解决) 2.通过src或者href请求不会发生跨域(所以可以用jsonp解决)**

![image-20230818004707421](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818004707421.png)



## 7.通过XHR使用AJAX

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>

<body>
    <h1>AJAX测试</h1>
    <hr />
    <button id="btn">点我加载数据</button>

    <div id="root"></div>

    <script>
        /*
          AJAX步骤
            1.向服务器发送请求
            2.读取服务器响应的数据
            3.将数据渲染到页面
        */
        /*
           XHR步骤
             1.创建xhr对象并设置类型转换
             2.设置onload事件并获取获取数据
             3.将数据渲染到前端页面
             4.配置请求信息
             5.发送请求
 
        */

        const btn = document.getElementById("btn")
        const root = document.getElementById("root")

        btn.onclick = () => {
            // 创建一个xhr对象
            const xhr = new XMLHttpRequest()

            // 设置响应体的类型，设置后会自动对数据进行类型转换(不用进行手动转换)
            xhr.responseType = "json"

            // 可以为xhr对象绑定一个load事件,onload表示加载完毕在执行,这样xhr就可以等加载完毕在读取数据
            xhr.onload = function () {
                // xhr.status 表示响应状态码   路由中设置的status是读取数据成功与否

                if (xhr.status === 200) {
                    // xhr.response 表示响应信息
                    // const result = JSON.parse(xhr.response) 先把json字符串转为js对象,才能读取到信息
                    // 读取响应信息
                    // console.log(xhr.response)

                    const result = xhr.response//返回的响应信息保存到result
                    // 判断数据是否正确 ok就是成功取到数据了
                    if (result.status === "ok") {
                        // 创建一个ul
                        const ul = document.createElement("ul")
                        // 将ul插入到root中
                        root.appendChild(ul)
                        // 遍历数据
                        // 要根据服务器返回的数据名来取数据
                        for (let stu of result.data) {
                            ul.insertAdjacentHTML(
                                "beforeend",
                                `<li>${stu.id} - ${stu.name} - ${stu.age} - ${stu.gender} - ${stu.address}</li>`
                            )
                        }
                    }
                }
            }

            // 设置请求的信息
            xhr.open("get", "http://localhost:3000/students")
            // send() 设置并发送响应体 
            // 这里用来发送请求,路由中用来给客户端返回响应数据
            xhr.send()
        }
    </script>
</body>

</html>
```

![uTools_1679492672752](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679492672752.png)



## 8.通过Fetch使用AJAX

### 1.如何使用

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <style>
            table{
                border-collapse: collapse;
                width: 50%;
            }

            td, th{
                font-size: 20px;
                text-align: center;
                border: 1px solid #000;
            }

            caption{
                font-size: 30px;
                font-weight: bold;
            }

        </style>
    </head>
    <body>
        <h1>AJAX测试</h1>
        <hr />
        <button id="btn">点我加载数据</button>
<hr>
        <div id="root"></div>

        <script>
            const btn = document.getElementById("btn")
            const root = document.getElementById("root")
            btn.onclick = () => {
                /* 
                    fetch
                        - fetch是xhr的升级版，采用的是Promise API
                        - 作用和AJAX是一样的，但是使用起来更加友好
                        - fetch原生js就支持的一种ajax请求的方式
                */
                // 1.发送请求
                fetch("http://localhost:3000/students")
                    .then((res) => {
                        if(res.status === 200){
                            // res.json() 可以用来读取json格式的数据
                            // 将响应信息作为当前Promise的值返回
                            return res.json()
                        }else{
                            throw new Error("加载失败！")
                        }
                    })
                    .then(res => {
                        // 2.获取到数据后，将数据渲染到页面中
                        if(res.status === "ok"){
                            // 创建一个table
                            const table = document.createElement("table")
                            root.appendChild(table)
                            table.insertAdjacentHTML("beforeend", "<caption>学生列表</caption>")
                            table.insertAdjacentHTML("beforeend", `
                                <thead>
                                    <tr>
                                        <th>学号</th>    
                                        <th>姓名</th>    
                                        <th>年龄</th>    
                                        <th>性别</th>    
                                        <th>地址</th>    
                                    </tr> 
                                </thead>
                            `)

                            const tbody = document.createElement("tbody")
                            table.appendChild(tbody)
                        
                            // 遍历数据
                            for(let stu of res.data){
                                tbody.insertAdjacentHTML("beforeend", `
                                    <tr>
                                        <td>${stu.id}</td>    
                                        <td>${stu.name}</td>    
                                        <td>${stu.age}</td>    
                                        <td>${stu.gender}</td>    
                                        <td>${stu.address}</td>    
                                    </tr>
                                `)
                                
                            }   
                        }
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                    })
            }
        </script>
    </body>
</html>
```

### 2.如何获取指定数据

```css
1.get直接获取数据:直接在fetch中获取

2.根据id获取相应数据:直接在fetch中获取,路径记得跟上id

3.POST等其它方式获取数据:需要进行配置
```

**实例**

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <style>
            table {
                border-collapse: collapse;
                width: 50%;
            }

            td,
            th {
                font-size: 20px;
                text-align: center;
                border: 1px solid #000;
            }

            caption {
                font-size: 30px;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <h1>AJAX测试</h1>
        <hr />
        <button id="btn">点我加载数据</button>
        <button id="btn02">点我加载数据2</button>
        <hr />
        <div id="root"></div>

        <script>
            const btn = document.getElementById("btn")
            const btn2 = document.getElementById("btn02")
            const root = document.getElementById("root")
            btn2.onclick = () => {
                //post请求需要进行配置参数的设置
                fetch("http://localhost:3000/students", {
                    method: "post",
                    
                    //指定数据类型
                    headers:{
                        // application/x-www-form-urlencoded 通过表单项传数据的时候
                        "Content-type":"application/json"
                    },

                    // ❤通过body去发送数据时，必须通过请求头来指定数据的类型(数据用body发送请求)
                    // 将js对象转为JSON字符串，这样服务器才能获取到数据
                    body: JSON.stringify({
                        //如果通过表单项传数据
                        //"id=1&&name=swk......"
                        name: "白骨精",
                        age: 16,
                        gender: "女",
                        address: "白骨洞"
                    })
                })
            }

            btn.onclick = () => {
                //get请求可以直接获取数据"http://localhost:3000/students/2"
                //获取学生信息的路由
                fetch("http://localhost:3000/students")
                    .then((res) => {
                        if(res.status === 200){
                            // res.json() 可以用来读取json格式的数据
                            // res.json() 拿到的数据是作为一个Promise返回的
                            // 将数据作为Promise的返回值返回
                            return res.json()
                        }else{
                            throw new Error("加载失败！")
                        }
                    })
                    .then(res => {
                    	// then接收上一个Promise的数据
                        // 获取到数据后，将数据渲染到页面中
                        if(res.status === "ok"){
                            // 创建一个table
                            const table = document.createElement("table")
                            root.appendChild(table)
                            table.insertAdjacentHTML("beforeend", "<caption>学生列表</caption>")
                            table.insertAdjacentHTML("beforeend", `
                                <thead>
                                    <tr>
                                        <th>学号</th>    
                                        <th>姓名</th>    
                                        <th>年龄</th>    
                                        <th>性别</th>    
                                        <th>地址</th>    
                                    </tr> 
                                </thead>
                            `)

                            const tbody = document.createElement("tbody")
                            table.appendChild(tbody)
                        
                            // 遍历数据
                            for(let stu of res.data){
                                tbody.insertAdjacentHTML("beforeend", `
                                    <tr>
                                        <td>${stu.id}</td>    
                                        <td>${stu.name}</td>    
                                        <td>${stu.age}</td>    
                                        <td>${stu.gender}</td>    
                                        <td>${stu.address}</td>    
                                    </tr>
                                `)
                            }  
                        }
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                    })
            }
        </script>
    </body>
</html>
```

### 3.登录功能

**页面**

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>

<body>
    <div id="root">
        <h1>请登录以后再做操作</h1>
        <h2 id="info"></h2>
        <form>
            <div>
                <input id="username" type="text" />
            </div>
            <div>
                <input id="password" type="password" />
            </div>
            <div>
                <!-- 设置为button 这样提交以后表单内容就不会消失了 -->
                <button id="login-btn" type="button">登录</button>
            </div>
        </form>
    </div>

    <script>
        // 点击login-btn后实现登录功能
        const loginBtn = document.getElementById("login-btn")
        const root = document.getElementById("root")
        loginBtn.onclick = () => {
            // 获取用户输入的用户名和密码
            const username = document.getElementById("username").value.trim()
            const password = document.getElementById("password").value.trim()


            //调用fetch发送请求来登录
            fetch("http://localhost:3000/login", {
                method: "POST",
                headers: {
                    "Content-type": "application/json"
                },
                // ❤把username和password的值拿来发送请求
                body: JSON.stringify({ username, password })
            })
                .then((res) => res.json())//将数据作为返回值返回)
                .then((res) => {
                    console.log(username, password);
                    //错误时抛出
                    if (res.status !== "ok") {
                        throw new Error("用户名或密码错误")
                    }
                    //登录成功 页面重新渲染
                    root.innerHTML = `
                            <h1>欢迎 ${res.data.nickname} 回来！</h1>
                            <hr>
                            <button id="load-btn">加载数据</button>
                        `
                })
                .catch((err) => {
                    console.log("出错了！", err)
                    // 这里是登录失败在h2显示错误提示
                    document.getElementById("info").innerText = "用户名或密码错误"
                })
        }
    </script>
</body>

</html>
```

**路由**

```javascript
const express = require("express")

const app = express()

const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]

app.use(express.urlencoded({ extended: true }))
// 解析json格式请求体的中间件
app.use(express.json())

app.use((req, res, next) => {
    // 设置响应头
    res.setHeader("Access-Control-Allow-Origin", "*")
    res.setHeader("Access-Control-Allow-Methods", "GET,POST,PUT,DELETE,PATCH")
    res.setHeader("Access-Control-Allow-Headers", "Content-type")
    // Access-Control-Allow-Origin 设置指定值时只能设置一个
    // res.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500")
    // Access-Control-Allow-Methods 允许的请求的方式
    // Access-Control-Allow-Headers 允许传递的请求头
    next()
})

//登陆路由
app.post("/login",(req,res) => {
    const {username,password} = req.body
    if (username==="admin"&&password==="123123") {
        res.send({
            status:"ok",
            data:{ id: "12345", username: "admin", nickname: "超级管理员" }
        })
    }else{
        res.status(403).send({
            status:"error",
            data:"用户名或密码错误!"
        })
    }
})

// 统一的api
// 定义学生信息的路由
app.post("/students", (req, res) => {
    console.log("收到students的get请求")
    // 返回学生信息
    res.send({
        status: "ok",
        data: STU_ARR
    })
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

### 4.本地存储及登录功能

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>

<body>
    <div id="root">
        <h1>请登录以后再做操作</h1>
        <h2 id="info"></h2>
        <form>
            <div>
                <input id="username" type="text" />
            </div>
            <div>
                <input id="password" type="password" />
            </div>
            <div>
                <!-- 设置为button 这样提交以后表单内容就不会消失了 -->
                <button id="login-btn" type="button">登录</button>
            </div>
        </form>
    </div>

    <script>



        // 点击login-btn后实现登录功能
        const loginBtn = document.getElementById("login-btn")
        const root = document.getElementById("root")

        //加载数据的函数
        //这里换成get方式的fetch 路由记得改成get方式
        function loadData() {
            fetch("http://localhost:3000/students")
                .then((res) => {
                    if (res.status === 200) {
                        // res.json() 可以用来读取json格式的数据
                        return res.json()
                    } else {
                        throw new Error("加载失败！")
                    }
                })
                .then(res => {
                    // 获取到数据后，将数据渲染到页面中
                    if (res.status === "ok") {
                        //登录成功点击按钮以后data就被创建了
                        const dataDiv = document.getElementById("data")
                        // 创建一个table
                        const table = document.createElement("table")
                        dataDiv.appendChild(table)
                        table.insertAdjacentHTML("beforeend", "<caption>学生列表</caption>")
                        table.insertAdjacentHTML("beforeend", `
                                <thead>
                                    <tr>
                                        <th>学号</th>    
                                        <th>姓名</th>    
                                        <th>年龄</th>    
                                        <th>性别</th>    
                                        <th>地址</th>    
                                    </tr> 
                                </thead>
                            `)

                        const tbody = document.createElement("tbody")
                        table.appendChild(tbody)

                        // 遍历数据
                        for (let stu of res.data) {
                            tbody.insertAdjacentHTML("beforeend", `
                                    <tr>
                                        <td>${stu.id}</td>    
                                        <td>${stu.name}</td>    
                                        <td>${stu.age}</td>    
                                        <td>${stu.gender}</td>    
                                        <td>${stu.address}</td>    
                                    </tr>
                                `)
                        }
                    }
                })
                .catch((err) => {
                    console.log("出错了！", err)
                })
        }


        // 判断用户是否登录过(localStorage存储过)
        if (localStorage.getItem("nickname")) {
            //已经登陆过
            root.innerHTML = `
            <h1>欢迎 ${localStorage.getItem(
                "nickname"
            )} 回来！</h1>
               <hr>
               <button id="load-btn" onclick="loadData()">加载数据</button>
               <hr>
               <div id="data"></div>
                        `
        } else {
            loginBtn.onclick = () => {
                // 获取用户输入的用户名和密码
                const username = document.getElementById("username").value.trim()
                const password = document.getElementById("password").value.trim()

                //调用fetch发送请求来登录
                fetch("http://localhost:3000/login", {
                    method: "POST",
                    headers: {
                        "Content-type": "application/json"
                    },
                    // ❤把username和password的值拿来发送请求
                    body: JSON.stringify({ username, password })
                })
                    .then((res) => res.json())//将数据作为返回值返回)
                    .then((res) => {
                        console.log(username, password);
                        //错误时抛出
                        if (res.status !== "ok") {
                            throw new Error("用户名或密码错误")
                        }

                        //登录成功以后，需要保持用户的登录状态
                        //Rest风格服务器会产生跨域问题，cookie用不了
                        //所以我们需要将用户信息存储到本地存储
                        /* 
                        所谓的本地存储就是指浏览器自身的存储空间，
                        可以将用户的数据存储到浏览器内部(主动存储，cookie是服务器将数据发过来在存储)
                        sessionStorage 中存储的数据 页面一关闭就会丢失(会话存储)
                        localStorage 存储的时间比较长(本地存储)
                          - 可以在开发者工具的应用中看到
                        */
                        // setItem() 用来存储数据
                        // getItem() 用来获取数据
                        // removeItem() 删除数据
                        // clear() 清空数据

                        localStorage.setItem("username", res.data.username)
                        localStorage.setItem("userId", res.data.id)
                        localStorage.setItem("nickname", res.data.nickname)
                        root.innerHTML = `
                        <h1>欢迎 ${localStorage.getItem(
                            "nickname"
                        )} 回来！</h1>
                        <hr>
                        <button id="load-btn" onclick="loadData()">加载数据</button>
                        <hr>
                        <div id="data"></div>
                        `
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                        // 这里是登录失败在h2显示错误提示
                        document.getElementById("info").innerText = "用户名或密码错误"
                    })
            }
        }
    </script>
</body>

</html>
```

**路由**

```javascript
const express = require("express")

const app = express()

const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]

app.use(express.urlencoded({ extended: true }))
// 解析json格式请求体的中间件
app.use(express.json())

app.use((req, res, next) => {
    // 设置响应头
    res.setHeader("Access-Control-Allow-Origin", "*")
    res.setHeader("Access-Control-Allow-Methods", "GET,POST,PUT,DELETE,PATCH")
    res.setHeader("Access-Control-Allow-Headers", "Content-type")
    // Access-Control-Allow-Origin 设置指定值时只能设置一个
    // res.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500")
    // Access-Control-Allow-Methods 允许的请求的方式
    // Access-Control-Allow-Headers 允许传递的请求头
    next()
})

//登陆路由
app.post("/login",(req,res) => {
    const {username,password} = req.body
    if (username==="admin"&&password==="123123") {
        res.send({
            status:"ok",
            data:{ id: "12345", username: "admin", nickname: "超级管理员" }
        })
    }else{
        res.status(403).send({
            status:"error",
            data:"用户名或密码错误!"
        })
    }
})

// 统一的api
// 定义学生信息的路由
app.get("/students", (req, res) => {
    console.log("收到students的get请求")
    // 返回学生信息
    res.send({
        status: "ok",
        data: STU_ARR
    })
})

// 查询某个学生的路由
app.get("/students/:id", (req, res) => {
    const id = req.params.id
    const stu = STU_ARR.find((item) => item.id === id)

    // 将数据返回
    res.send({
        status: "ok",
        data: stu
    })
})

// 定义一个添加学生的路由
app.post("/students", (req, res) => {
    console.log("收到students的post请求", req.body)
    // 获取学生的信息
    const { name, age, gender, address } = req.body
    // 创建学生信息
    const stu = {
        id: +STU_ARR.at(-1).id + 1 + "",
        name,
        age: +age,
        gender,
        address
    }

    // 将学生信息添加到数组
    STU_ARR.push(stu)

    // 添加成功
    res.send({
        status: "ok",
        data: stu
    })
})

// 定义一个删除学生的路由 根据id删除学生
// app.delete()
app.delete("/students/:id", (req, res) => {
    // 获取学生的id
    const id = req.params.id

    // 遍历数组
    for (let i = 0; i < STU_ARR.length; i++) {
        if (STU_ARR[i].id === id) {
            const delStu = STU_ARR[i]
            STU_ARR.splice(i, 1)
            // 数据删除成功
            res.send({
                status: "ok",
                data: delStu
            })
            return
        }
    }

    // 如果执行到这里，说明学生不存在
    res.status(403).send({
        status: "error",
        data: "学生id不存在"
    })
})

// 定义一个修改学生的路由
// app.put()
app.put("/students", (req, res) => {
    // 获取数据
    const { id, name, age, gender, address } = req.body

    // 根据id查询学生
    const updateStu = STU_ARR.find((item) => item.id === id)

    if (updateStu) {
        updateStu.name = name
        updateStu.age = age
        updateStu.gender = gender
        updateStu.address = address

        res.send({
            status: "ok",
            data: updateStu
        })
    } else {
        res.status(403).send({
            status: "error",
            data: "学生id不存在"
        })
    }
})

app.listen(3000, () => {
    console.log("服务器已经启动！")
})
```

### 5.退出

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>

<body>
    <div id="root">
        <h1>请登录以后再做操作</h1>
        <h2 id="info"></h2>
        <form>
            <div>
                <input id="username" type="text" />
            </div>
            <div>
                <input id="password" type="password" />
            </div>
            <div>
                <!-- 设置为button 这样提交以后表单内容就不会消失了 -->
                <button id="login-btn" type="button">登录</button>
            </div>
        </form>
    </div>

    <script>



        // 点击login-btn后实现登录功能
        const loginBtn = document.getElementById("login-btn")
        const root = document.getElementById("root")

        //加载数据的函数
        //这里换成get方式的fetch 路由记得改成get方式
        function loadData() {
            fetch("http://localhost:3000/students")
                .then((res) => {
                    if (res.status === 200) {
                        // res.json() 可以用来读取json格式的数据
                        return res.json()
                    } else {
                        throw new Error("加载失败！")
                    }
                })
                .then(res => {
                    // 获取到数据后，将数据渲染到页面中
                    if (res.status === "ok") {
                        //登录成功点击按钮以后data就被创建了
                        const dataDiv = document.getElementById("data")
                        // 创建一个table
                        const table = document.createElement("table")
                        dataDiv.appendChild(table)
                        table.insertAdjacentHTML("beforeend", "<caption>学生列表</caption>")
                        table.insertAdjacentHTML("beforeend", `
                                <thead>
                                    <tr>
                                        <th>学号</th>    
                                        <th>姓名</th>    
                                        <th>年龄</th>    
                                        <th>性别</th>    
                                        <th>地址</th>    
                                    </tr> 
                                </thead>
                            `)

                        const tbody = document.createElement("tbody")
                        table.appendChild(tbody)

                        // 遍历数据
                        for (let stu of res.data) {
                            tbody.insertAdjacentHTML("beforeend", `
                                    <tr>
                                        <td>${stu.id}</td>    
                                        <td>${stu.name}</td>    
                                        <td>${stu.age}</td>    
                                        <td>${stu.gender}</td>    
                                        <td>${stu.address}</td>    
                                    </tr>
                                `)
                        }
                    }
                })
                .catch((err) => {
                    console.log("出错了！", err)
                })
        }

        //❤清除本地存储
        function replay() {
            localStorage.clear();
            //页面刷新
            location.reload();
        }


        // 判断用户是否登录过(localStorage存储过)
        if (localStorage.getItem("nickname")) {
            //已经登陆过
            root.innerHTML = `
            <h1>欢迎 ${localStorage.getItem(
                "nickname"
            )} 回来！</h1>
               <hr>
               <button id="load-btn" onclick="loadData()">加载数据</button>
               <button onclick="localStorage.clear()">注销</button>
               <hr>
               <div id="data"></div>
                        `
        } else {
            loginBtn.onclick = () => {
                // 获取用户输入的用户名和密码
                const username = document.getElementById("username").value.trim()
                const password = document.getElementById("password").value.trim()

                //调用fetch发送请求来登录
                fetch("http://localhost:3000/login", {
                    method: "POST",
                    headers: {
                        "Content-type": "application/json"
                    },
                    // ❤把username和password的值拿来发送请求
                    body: JSON.stringify({ username, password })
                })
                    .then((res) => res.json())//将数据作为返回值返回)
                    .then((res) => {
                        console.log(username, password);
                        //错误时抛出
                        if (res.status !== "ok") {
                            throw new Error("用户名或密码错误")
                        }

                        //登录成功以后，需要保持用户的登录状态
                        //Rest风格服务器会产生跨域问题，cookie用不了
                        //所以我们需要将用户信息存储到本地存储
                        /* 
                        所谓的本地存储就是指浏览器自身的存储空间，
                        可以将用户的数据存储到浏览器内部(主动存储，cookie是服务器将数据发过来在存储)
                        sessionStorage 中存储的数据 页面一关闭就会丢失(会话存储)
                        localStorage 存储的时间比较长(本地存储)
                          - 可以在开发者工具的应用中看到
                        */
                        // setItem() 用来存储数据
                        // getItem() 用来获取数据
                        // removeItem() 删除数据
                        // clear() 清空数据

                        localStorage.setItem("username", res.data.username)
                        localStorage.setItem("userId", res.data.id)
                        localStorage.setItem("nickname", res.data.nickname)
                        root.innerHTML = `
                        <h1>欢迎 ${localStorage.getItem(
                            "nickname"
                        )} 回来！</h1>
                        <hr>
                        <button id="load-btn" onclick="loadData()">加载数据</button>
                        <button onclick="replay()">注销</button>
                        <hr>
                        <div id="data"></div>
                        `
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                        // 这里是登录失败在h2显示错误提示
                        document.getElementById("info").innerText = "用户名或密码错误"
                    })
            }
        }

    </script>
</body>

</html>
```



### 6.token简介

**开发的验证分为前后端验证,前端用本地存储验证，后端在服务器验证**

```css
        问题：
                   - 现在是登录以后直接将用户信息存储到了localStorage
                   - 主要存在两个问题：
                        1.数据安全问题
                        2.服务器不知道你有没有登录
                   - 解决问题：
                        如何告诉服务器客户端的登录状态
                            - Rest风格的服务器是无状态的服务器，所以注意不要在服务器中存储用户的数据
                            - 服务器中不能存储用户信息，可以将用户信息发送给客户端保存
                                比如：{id:"xxx", username:"xxx", email:"xxx"}
                                客户端每次访问服务器时，直接将用户信息发回，服务器就可以根据用户信息来识别用户的身份
                            - 但是如果将数据直接发送给客户端同样会有数据安全的问题，
                                所以我们必须对数据进行加密(加密算法，一种规则)，
								加密以后在发送给客户端保存，这样即可避免数据的泄露
                            - 在node中可以直接使用jsonwebtoken这个包来对数据进行加密
                                jsonwebtoken（jwt） --> 通过对json加密后，生成一个web中使用的令牌
            					- 使用步骤：
        						 1.安装
                                     yarn add jsonwebtoken
        						2.引入
        						3.配置                
```

#### 1.token简介

```js
// 引入jwt
const jwt = require("jsonwebtoken")

// 创建一个对象
const obj = {
    name: "swk",
    age: 18,
    gender: "男"
}

// 使用jwt来对json数据进行加密
// 第二个参数表示加密的依据  我们自己定义 解密时要用这个依据来解密
// 开发中我们都是随机生成一个别人不好猜到的值来设置
const token = jwt.sign(obj, "hellohellohowyou", {
    expiresIn: "1"
})
try {
    //服务器收到客户端的token后
    const decodeData = jwt.verify(token, "hellohellohowyou")

    console.log(decodeData)
} catch (e) {
    // 说明token解码失败，说明token
    console.log("无效的token")
}
```

#### 2.token使用

```css
        token的使用过程
            1.服务器生成token发给客户端(服务器要生成token并发送 服务器中写代码)
            2.客户端接收token并解密保存(客户端要接收token 服务器中写代码)
            3.客户端将token发给服务器(客户端中将token发送 客户端中写代码)
            4.服务器根据客户端发来的token进行解密,来识别不同的用户(服务器中写代码)
```

**页面**

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        table {
            border-collapse: collapse;
            width: 50%;
        }

        td,
        th {
            font-size: 20px;
            text-align: center;
            border: 1px solid #000;
        }

        caption {
            font-size: 30px;
            font-weight: bold;
        }
    </style>
</head>

<body>
    <div id="root">
        <h1>请登录以后再做操作</h1>
        <h2 id="info"></h2>
        <form>
            <div>
                <input id="username" type="text" />
            </div>
            <div>
                <input id="password" type="password" />
            </div>
            <div>
                <button id="login-btn" type="button">登录</button>
            </div>
        </form>
    </div>

    <script>



        // 点击login-btn后实现登录功能
        const loginBtn = document.getElementById("login-btn")
        const root = document.getElementById("root")

        /*
            token的使用过程
                1.服务器生成token发给客户端
                2.客户端接收token并保存
                3.客户端将token发给服务器
                4.服务器根据客户端发来的token进行解密,来识别不同的用户
        */

        function loadData() {

            // 当我们访问的是需要权限的api时，必须在请求中附加权限的信息
            // token一般都是通过请求头来发送
            const token = localStorage.getItem("token")
            fetch("http://localhost:3000/students", {
                headers: {
                    // 格式:"Bearer xxxxxx" //Bearer是一种权限认证规定
                    "Authorization": `Bearer ${token}`
                }
            })
                .then((res) => {
                    if (res.status === 200) {
                        // res.json() 可以用来读取json格式的数据
                        return res.json()
                    } else {
                        throw new Error("加载失败！")
                    }
                })
                .then((res) => {
                    // 获取到数据后，将数据渲染到页面中
                    if (res.status === "ok") {
                        // 创建一个table
                        const dataDiv = document.getElementById("data")
                        const table = document.createElement("table")
                        dataDiv.appendChild(table)
                        table.insertAdjacentHTML(
                            "beforeend",
                            "<caption>学生列表</caption>"
                        )
                        table.insertAdjacentHTML(
                            "beforeend",
                            `
                                <thead>
                                    <tr>
                                        <th>学号</th>    
                                        <th>姓名</th>    
                                        <th>年龄</th>    
                                        <th>性别</th>    
                                        <th>地址</th>    
                                    </tr> 
                                </thead>
                            `
                        )

                        const tbody = document.createElement("tbody")
                        table.appendChild(tbody)

                        // 遍历数据
                        for (let stu of res.data) {
                            tbody.insertAdjacentHTML(
                                "beforeend",
                                `
                                    <tr>
                                        <td>${stu.id}</td>    
                                        <td>${stu.name}</td>    
                                        <td>${stu.age}</td>    
                                        <td>${stu.gender}</td>    
                                        <td>${stu.address}</td>    
                                    </tr>
                                `
                            )
                        }
                    }
                })
                .catch((err) => {
                    console.log("出错了！", err)
                })
        }



        // 判断用户是否登录
        if (localStorage.getItem("token")) {
            // 用户已经登录
            // 登录成功
            root.innerHTML = `
                            <h1>欢迎 ${localStorage.getItem(
                "nickname"
            )} 回来！</h1>
                            <hr>
                            <button id="load-btn" onclick="loadData()">加载数据</button>
                            <button onclick="localStorage.clear()">注销</button>
                            <hr>
                            <div id="data"></div>
                        `
        } else {
            loginBtn.onclick = () => {
                // 获取用户输入的用户名和密码
                const username = document
                    .getElementById("username")
                    .value.trim()
                const password = document
                    .getElementById("password")
                    .value.trim()

                // 调用fetch发送请求来完成登录
                fetch("http://localhost:3000/login", {
                    method: "POST",
                    headers: {
                        "Content-type": "application/json"
                    },
                    body: JSON.stringify({ username, password })
                })
                    .then((res) => res.json())
                    .then((res) => {
                        if (res.status !== "ok") {
                            throw new Error("用户名或密码错误")
                        }

                        // 登录成功以后，需要保持用户的登录的状态，需要将用户的信息存储到某个地方
                        // 需要将用户信息存储到本地存储
                        /* 
                        所谓的本地存储就是指浏览器自身的存储空间，
                            可以将用户的数据存储到浏览器内部
                            sessionStorage 中存储的数据 页面一关闭就会丢失
                            localStorage 存储的时间比较长
                    */

                        // sessionStorage
                        // localStorage
                        // console.log(res)
                        // 登录成功，向本地存储中插入用户的信息
                        localStorage.setItem("token", res.data.token)
                        localStorage.setItem("nickname", res.data.nickname)

                        // 登录成功
                        root.innerHTML = `
                            <h1>欢迎 ${res.data.nickname} 回来！</h1>
                            <hr>
                            <button id="load-btn" onclick="loadData()">加载数据</button>
                            <button onclick="localStorage.clear()">注销</button>
                            <hr>
                            <div id="data"></div>
                        `
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                        // 这里是登录失败
                        document.getElementById("info").innerText =
                            "用户名或密码错误"
                    })
            }
        }
    </script>
</body>

</html>
```

**此时只有输入正确才能拿到token,postman中要访问要进行header配置**

![uTools_1679581831305](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679581831305.png)

### 7.fetch补充

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        table {
            border-collapse: collapse;
            width: 50%;
        }

        td,
        th {
            font-size: 20px;
            text-align: center;
            border: 1px solid #000;
        }

        caption {
            font-size: 30px;
            font-weight: bold;
        }
    </style>
</head>

<body>
    <button id="btn01">点我一下</button>

    <button id="btn02">取消</button>
    <button id="btn03">按钮3号</button>
    <script>
        // 获取按钮
        const btn01 = document.getElementById("btn01")//发送请求
        const btn02 = document.getElementById("btn02")//结束请求
        const btn03 = document.getElementById("btn03")

        let controller//全局变量 都可以访问

        btn01.onclick = () => {
            // 如何终止请求
            // 创建一个AbortController
            controller = new AbortController()
            // setTimeout(()=>{
            //     controller.abort() 这个方法可以控制终止
            // }, 3000)

            // 点击按钮向test发送请求
            fetch("http://localhost:3000/test", {
                signal: controller.signal//controller的配置对象
            })
                .then((res) => console.log(res))
                .catch((err) => console.log("出错了", err))
        }

        btn02.onclick = () => {
            //controller存在才会执行终止 因为一开始是没有请求发送的controller不存在
            controller && controller.abort()
        }

        btn03.onclick = async () => {
            // fetch("http://localhost:3000/test").then()...
            // 注意：将promise改写为await时，一定要写try-catch
            // 普通的方式我们还要用then去获取Promise的值 所以也可以用async await直接获取promise的值
            try {
                const res = await fetch("http://localhost:3000/students")
                const data = await res.json()
                console.log(data)
            } catch (e) {
                console.log("出错了", e)
            }
        }
    </script>
</body>

</html>
```

**路由**

test路由中没有东西，students返回学生数据

## 9.Axios

**基于Promise，是对xhr的封装**

### 0.Axios和Fetch的区别

```css
1.不用配置请求头参数类型
2.返回的结果不用我们手动转换类型
3.Fetch只要有响应就会走then，Axios只有2xx会走then
```



### 1.安装

![image-20230324165022124](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230324165022124.png)



### 2.引入

**node中可以通过npm yarn等引入，浏览器可以通过打包工具和script引入**

![uTools_1679647856591](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679647856591.png)



### 3.基本用例

#### 1.get

![uTools_1679648125721](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679648125721.png)

#### 2.post

![uTools_1679648148797](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679648148797.png)

### 4.发送请求

![uTools_1679648731696](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679648731696.png)

**简便方法**

![uTools_1679648776932](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679648776932.png)



### 5.配置参数

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Axios</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>

<body>
    <button id="btn1">按钮1</button>
    <button id="btn2">按钮2</button>

    <script>
        document.getElementById("btn1").onclick = () => {
            // 直接调用axios发送请求
            // axios(config)
            axios({
                // baseURL 指定服务器的根目录（路径的前缀）
                baseURL: "http://localhost:3000",
                // 请求地址(必须写！所有都可以不写)
                url: "test",
                //这样写就是默认向这个地址发送get请求
                // url: "http://localhost:3000/students",

                // 请求方法，默认是get
                method: "get",

                // 指定请求头("Content-type":"application/json"这个默认带 其它的要自己配置)
                // headers:{"Content-type":"application/json"}

                // 请求体
                //1.data:"name=唐僧&age=16"（www那个表单提交的方式）
                // 2.{}
                data: {
                    name: "唐僧",
                    age: 18,
                    gender: "男",
                    address: "女儿国"
                },

                // params 用来指定路径中的查询字符串
                params: {
                    id: 1,
                    name: "swk"
                },
                //此时url相当于"http://localhost:3000/test?id=1&name=swk"


                //timeout 过期时间
                timeout: 1000, //1秒钟没返回响应自动取消
                //fetch没这个功能


                // 用来终止请求
                // signal
                // 用法
                //  let controller = new AbortController()
                //  setTimeout(()=>{
                //      controller.abort() 这个方法可以控制终止
                //  }, 3000)

                // transformRequest 可以用来处理请求数据（data）
                // 它需要一个数组作为参数，数组可以接收多个函数，请求发送时多个函数会按照顺序执行
                // 函数在执行时，会接收到两个参数data和headers
                // transformRequest:[function(data, headers){
                //     // 可以在函数中对data和headers进行修改
                //     data.name = "猪八戒"
                //     这里要用Content-Type大写才可以
                //     headers["Content-Type"] = "application/json"
                //     return data
                // }, function(data, headers){
                //     // 最后一个函数必须返回一个字符串，才能使得数据有效
                //     return JSON.stringify(data)
                // }]

                //transformResponse 可以用来处理响应数据（data）

            })
                .then((result) => {
                    // result是axios封装过的，所以会带很多东西
                    console.log(result.data)
                })
                .catch((err) => {
                    console.log("出错了！", err)
                })
        }
    </script>
</body>

</html>
```



### 6.响应结构

![uTools_1679650203050](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679650203050.png)

**request就是对xhr封装的那个对象,可以通过他调用原生的xhr方法**



### 7.默认配置

![uTools_1679650441218](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679650441218.png)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Axios</title>
        <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    </head>
    <body>
        <button id="btn1">按钮1</button>
        <button id="btn2">按钮2</button>

        <script>
            //一次性配置根目录
            axios.defaults.baseURL = "http://localhost:3000"
            //一次性配置请求头的token(带上令牌，检测是否有权限)
            axios.defaults.headers.common[
                "Authorization"
            ] = `Bearer ${localStorage.getItem("token")}`

            document.getElementById("btn1").onclick = () => {
                axios({
                    url: "students",
                    method: "post",
                    data: {
                        name: "唐僧",
                        age: 18,
                        gender: "男",
                        address: "女儿国"
                    },

                    timeout: 1000
                })
                    .then((result) => {
                        // result是axios封装过
                        console.log(result.data)
                    })
                    .catch((err) => {
                        console.log("出错了！", err)
                    })
            }
        </script>
    </body>
</html>
```



### 8.axios实例

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Axios</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>

<body>
    <button id="btn1">按钮1</button>
    <button id="btn2">按钮2</button>

    <script>
        axios.defaults.baseURL = "http://localhost:3000"
        axios.defaults.headers.common[
            "Authorization"
        ] = `Bearer ${localStorage.getItem("token")}`
        // 默认配置有一个问题就是会对所有请求生效，有时候我们要在一个页面中
        //同时向多个服务器发请求，这时候就需要用到axios实列对其单独配置
        // 这样就可以做到每个实例有自己的不同功能(向不同地方发请求获取不同功能)

        // axios实例相当于是axios的一个副本，它的功能和axios一样
        // axios的默认配置在实例也同样会生效
        //  但是我可以单独修改axios实例的默认配置
        // 1.修改的方式1
        // const instance = axios.create({
        //     baseURL:"http://localhost:4000"
        // })
          
        // 2.修改的方式2
        // const instance = axios.create()
        // instance.defaults.baseURL = "xxx"


        document.getElementById("btn1").onclick = () => {
            instance
                .get("students")
                .then((res) => console.log(res.data))
                .catch((err) => {
                    console.log("出错了", err)
                })
        }
    </script>
</body>

</html>
```



### 9.axios拦截器(类似中间件)

**在服务器和请求之间设置拦截器，可以对请求再发送前做处理，类似中间件在请求到达路由之前对路由进行处理**

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Axios</title>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>

<body>
    <button id="btn1">按钮1</button>
    <button id="btn2">按钮2</button>

    <script>
        /* 
        // 添加响应拦截器
        axios.interceptors.response.use(function (response) {
            // 2xx 范围内的状态码都会触发该函数。
            // 对响应数据做点什么
            return response;
        }, function (error) {
            // 超出 2xx 范围的状态码都会触发该函数。
            // 对响应错误做点什么
            return Promise.reject(error);
        });
        */
       
        axios.defaults.baseURL = "http://localhost:3000"

        const myAxios = axios.create()

        // axios的拦截器可以对请求或响应进行拦截，在请求发送前和响应读取前处理数据
        // 拦截器只对当前的实例有效
        // 添加请求拦截器(可以配置多个拦截器)
        axios.interceptors.request.use(//此时只有axios这个拦截器有用
            function (config) {
                // console.log("拦截器执行了")
                // config 表示axios中的配置对象
                // config.data.name = "猪哈哈" //一般不会这样去使用
                // 使用拦截器在请求发送之前为他们加上token(也可以直接在axios默认配置进行设置)
                config.headers["Authorization"] = `Bearer ${localStorage.getItem("token")}`

                // 在发送请求之前做些什么
                return config
            },
            function (error) {
                // 对请求错误做些什么
                return Promise.reject(error)
            }
        )

        document.getElementById("btn1").onclick = () => {
            axios({
                url: "students",
                method: "post",
                data: { name: "猪八戒" }
            })
                .then((res) => console.log(res.data))
                .catch((err) => {
                    console.log("出错了", err)
                })
        }
    </script>
</body>

</html>
```

![uTools_1679651600118](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679651600118.png)

**清除拦截器**

![uTools_1679652089284](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679652089284.png)

## 10.Nginx

![uTools_1692349129453](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692349129453.png)

![uTools_1692349143311](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692349143311.png)

![uTools_1692349159039](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692349159039.png)
