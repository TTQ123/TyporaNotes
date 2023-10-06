# Vue2

## 1.vue是什么

![image-20230814163453506](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814163453506.png)

![image-20230814163623307](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814163623307.png)



### 1.Vue实例

![image-20230814220326676](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814220326676.png)



### 2.差值表达式

![image-20230814221524306](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814221524306.png)



### 3.响应性数据

![image-20230814222849718](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814222849718.png)

![image-20230814222924906](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814222924906.png)



### 4.开发者调试工具

![image-20230814224246303](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814224246303.png)

**data的值不能是全中文的，不然在vue调试工具是不能显示的**

## 

## 2.vue指令

### 1.v-html

![image-20230814225503014](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814225503014.png)

![image-20230814225440172](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814225440172.png)



### 2.v-show和v-if

![image-20230814225938647](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814225938647.png)



### 3.v-else 和 v-else-if

![image-20230814230328875](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814230328875.png)

![image-20230814230341349](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814230341349.png)



### 4.v-on

![image-20230814231114383](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814231114383.png)

**vue2中，data声明的数据(选项式API)只能在模板中直接使用，无法在methods中使用，需要通过 `实例.数据` 或者 `this.数据` 来获取**

![image-20230814232043669](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814232043669.png)

**v-on参数传递**

![image-20230814233338386](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814233338386.png)





#### 1.vue2和vue3中this的区别

**VUE3中已经没有了this，因为他用的是组合式API，想要this可以用ref去代替获取到数据的值，或者是getCurrentInstance（）方法，这个方法返回了ctx和proxy**

![image-20230814232841350](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814232841350.png)

![image-20230814232924467](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814232924467.png)

![image-20230814232931803](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230814232931803.png)



### 5.v-bind

![image-20230815002417092](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815002417092.png)

**v-bind更多的还是用在父子组件传值**

#### 1.v-bind原理

![image-20230815204932840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815204932840.png)



### 6.v-for

![image-20230815193800694](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815193800694.png)

**`v-for`的默认行为会尝试原地修改元素(就地复用)**

![image-20230815202811035](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815202811035.png)

```bash
如果我们不加key，他会把最后一个删除，然后把其它的往前面推。
```



### 7.v-model

![image-20230815203439655](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815203439655.png)

![image-20230815203501447](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815203501447.png)

#### 1.vue2中v-model原理

![image-20230815204412500](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815204412500.png)

```apl
v-bind绑定了双向数据,这样完成第一步 数据变化-->视图更新
@input事件完成第二步 视图变化-->数据更新
```



#### 2.vue3中v-model原理

![image-20230815204432257](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815204432257.png)



### 8.第一天案例:记事本

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #app {
            width: 400px;
            margin: 50px auto;
        }
    </style>
</head>

<body>
    <div id="app">
        <header class="header">
            <h1>小黑记事本</h1>
            <input type="text" placeholder="请输入任务" class="new-todo" v-model="todoName">
            <button class="add" @click="add">添加任务</button>
        </header>
        <section class="main">
            <ul class="todo-list">
                <li class="todo" v-for="(item,index) in list">
                    <div class="view">
                        <!-- 用index不会影响序号 -->
                        <span class="index">{{index + 1}}</span> <label>{{item.name}}</label>
                        <button class="destroy" @click="del(item.id)">删除任务</button>
                    </div>
                </li>
            </ul>
        </section>
        <footer class="footer" v-show="list.length > 0">
            <div class="todo-count">
                合 计:<strong> {{list.length}} </strong>
                <button class="clear-complated" @click="delAll">清空任务</button>
            </div>
            
        </footer>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                todoName:'',
                list: [
                    { id: 1, name: '跑步一公里' },
                    { id: 2, name: '跳绳一百次' },
                    { id: 3, name: '跳远十次' }
                ]
            },
            methods: {
                del(id) {
                    this.list = this.list.filter(item => item.id !== id)
                },
                add(){
                    if (this.todoName.trim() === '') {
                        alert('请输入任务名称')
                        return
                    }
                    this.list.unshift({
                        id:new Date(),
                        name:this.todoName
                    })
                    this.todoName = ''
                },

                delAll(){
                    this.list = []
                }
            }
        })
    </script>
</body>

</html>
```



### 9.指令的修饰符

![image-20230815220627608](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815220627608.png)

**修饰符原理**

![image-20230815221048560](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815221048560.png)

**@事件名.stop的原理**

![image-20230815221341970](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815221341970.png)



### 10.v-bind对于css样式的控制(操作css和style)

#### 1.操作css

![image-20230815221829159](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815221829159.png)

**这个clss是在style样式里面声明了，可以直接拿来用**

**例子**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .active {
            color: pink;
        }
    </style>
</head>

<body>
    <div id="app">
       <ul>
        <li v-for="(item,index) in list" :key="item.id" @mouseover="activeIndex = index">
            <a :class="{active: index === activeIndex}">{{item.name}}</a>
        </li>
       </ul>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                activeIndex:0,
                list: [
                    { id: 1, name: '京东秒杀' },
                    { id: 2, name: '百度秒杀' },
                    { id: 3, name: '苦瓜秒杀' }
                ]
            },
            methods: {
               
            }
        })
    </script>
</body>

</html>
```



#### 2.操作style

![image-20230815223633057](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815223633057.png)

![image-20230815223603274](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815223603274.png)

### 11.v-model应用于其它表单元素

![image-20230815230255021](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815230255021.png)

![image-20230815230308602](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815230308602.png)

![image-20230815230322284](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815230322284.png)



## 3.vue计算属性

### 1.简介

![image-20230815231130840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815231130840.png)

![image-20230815231031536](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815231031536.png)



### 2.computer和methods的差异

![image-20230815231552012](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815231552012.png)

![image-20230815231415682](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815231415682.png)



### 3.计算属性的完整写法(读取和修改)

![image-20230815231733101](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230815231733101.png)

例子：计算属性的获取和修改

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <div id="app">
        <div>
            姓:<span>{{firstName}}</span>+名:<span>{{lastName}}</span> = {{fullName}}
            <br>
            <button  @click="changeName">改名</button>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
               firstName:'刘',
               lastName:'备'
            },
            methods: {
               changeName(){
                this.fullName = '张飞'
               }
            },
            computed:{
                fullName:{
                    get(){
                        return this.firstName + this.lastName
                    },
                    set(value){
                        // 当点击了事件changeName fullName将被修改同时传给set的value形参
                        this.firstName = value.slice(0,1)
                        this.lastName = value.slice(1)
                    }
                }

            }
        })
    </script>
</body>

</html>
```



### 4.第二天案例:成绩案例

![image-20230816002534273](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230816002534273.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="./index.css" />
    <title>Document</title>
</head>

<body>
    <div id="app" class="score-case">
        <div class="table">
            <table>
                <thead>
                    <tr>
                        <th>编号</th>
                        <th>科目</th>
                        <th>成绩</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody v-if="list.length > 0">
                    <tr v-for="(item,index) in list" :key="item.id">
                        <td>{{index+1}}</td>
                        <td>{{item.subject}}</td>
                        <td :class="{red: item.score < 60}">{{item.score}}</td>
                        <td><a @click.prevent="del(item.id)" href="#">删除</a></td>
                    </tr>
                </tbody>
                <tbody v-else>
                    <tr>
                        <td colspan="4">
                            <span class="none">暂无数据</span>
                        </td>
                    </tr>
                </tbody>

                <tfoot>
                    <tr>
                        <td colspan="4">
                            <span>总分:{{totalScore}}</span>
                            <span style="margin-left: 50px">平均分:{{totalAvg}}</span>
                        </td>
                    </tr>
                </tfoot>
            </table>
        </div>
        <div class="form">
            <div class="form-item">
                <div class="label">科目:</div>
                <div class="input">
                    <input type="text" placeholder="请输入科目" v-model.trim="subject" />
                </div>
            </div>
            <div class="form-item">
                <div class="label">分数:</div>
                <div class="input">
                    <input type="text" placeholder="请输入分数" v-model.number="score" />
                </div>
            </div>
            <div class="form-item">
                <div class="label"></div>
                <div class="input">
                    <button class="submit" @click="add">添加</button>
                </div>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

    <script>
        const app = new Vue({
            el: '#app',
            data: {
                list: [
                    { id: 1, subject: '语文', score: 20 },
                    { id: 7, subject: '数学', score: 99 },
                    { id: 12, subject: '英语', score: 70 },
                ],
                subject: '',
                score: ''
            },
            methods: {
                del(id) {
                    // item就是遍历的整个数组 相等的那个被删除了
                    this.list = this.list.filter(item => item.id !== id)
                },
                add() {
                    if (!this.subject) {
                        alert('请输入科目')
                    }
                    if (typeof this.score !== 'number') {
                        alert('请输入正确的内容')
                        return
                    }
                    this.list.unshift({
                        id: +new Date(),
                        subject: this.subject,
                        score: this.score
                    })
                    this.subject = ''
                    this.score = ''
                }
            },
            computed: {
                // 计算总分
                totalScore() {
                    // 第一项是计算总分，第二项是从0开始的意思
                    return this.list.reduce((sum, item) => sum + item.score, 0)
                },
                // 计算平均分
                totalAvg() {
                    // 总分为0 平均分也为0
                    if (this.totalScore === 0) {
                        return 0
                    }
                    return (this.totalScore / this.list.length).toFixed(2)
                }

            }
        })
    </script>
</body>

</html>
```



## 4.watch侦听器

### 1.watch简写 监听简单数据类型

![image-20230816004920526](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230816004920526.png)

### 2.watch完整写法 监听复杂类型

![uTools_1692118075672](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692118075672.png)

![uTools_1692118054267](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692118054267.png)

### 3.例子 实时翻译功能

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-size: 18px;
        }

        #app {
            padding: 10px 20px;
        }

        .query {
            margin: 10px 0;
        }

        .box {
            display: flex;
        }

        textarea {
            width: 300px;
            height: 160px;
            font-size: 18px;
            border: 1px solid #dedede;
            outline: none;
            resize: none;
            padding: 10px;
        }

        textarea:hover {
            border: 1px solid #1589f5;
        }

        .transbox {
            width: 300px;
            height: 160px;
            background-color: #f0f0f0;
            padding: 10px;
            border: none;
        }

        .tip-box {
            width: 300px;
            height: 25px;
            line-height: 25px;
            display: flex;
        }

        .tip-box span {
            flex: 1;
            text-align: center;
        }

        .query span {
            font-size: 18px;
        }

        .input-wrap {
            position: relative;
        }

        .input-wrap span {
            position: absolute;
            right: 15px;
            bottom: 15px;
            font-size: 12px;
        }

        .input-wrap i {
            font-size: 20px;
            font-style: normal;
        }
    </style>
</head>

<body>
    <div id="app">
        <!-- 条件选择框 -->
        <div class="query">
            <span>翻译成的语言：</span>
            <select v-model="obj.lang">
                <option value="italy">意大利</option>
                <option value="english">英语</option>
                <option value="german">德语</option>
            </select>
        </div>

        <!-- 翻译框 -->
        <div class="box">
            <div class="input-wrap">
                <textarea v-model="obj.words"></textarea>
                <span><i>⌨️</i>文档翻译</span>
            </div>
            <div class="output-wrap">
                <div class="transbox">{{ result }}</div>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script>
        // 需求：输入内容，修改语言，都实时翻译

        // 接口地址：https://applet-base-api-t.itheima.net/api/translate
        // 请求方式：get
        // 请求参数：
        // （1）words：需要被翻译的文本（必传）
        // （2）lang： 需要被翻译成的语言（可选）默认值-意大利

        const app = new Vue({
            el: '#app',
            data: {
                // 复杂数据类型 对象类型
                obj: {
                    words: '小黑',
                    lang: 'italy'
                },
                result: '', // 翻译结果
            },

            watch: {
                obj: {
                    deep: true,//深度监视
                    immediate: true, // 立刻执行，一进入页面handler就立刻执行一次
                    // 作用是给word一个默认值，第一次进页面不会自动翻译一次(handler不执行，数据变化了才执行)
                    handler(newValue) {
                        // 开启防抖:延迟执行(输入肯定有多次不要一直执行,一段时间后在执行)
                        clearTimeout(this.timer) //如果在300毫秒内输入了,那么我们要删除前面那个定时器
                        // 不然时间到了还是会执行，控制台会执行多次(我们只要一次)
                        this.timer = setTimeout(async () => {
                            // axios发送请求
                            const res = await axios({
                                url: 'https://applet-base-api-t.itheima.net/api/translate',
                                params: newValue //newValue其实就是整个obj对象,直接传给参数进行网络请求
                            })
                            this.result = res.data.data //获取到的值显示到翻译栏
                            console.log(res.data.data)
                        }, 300)
                    }
                }
            }
              // watch简单写法  
              // 'obj.words' (newValue) {
              //   clearTimeout(this.timer)
              //   this.timer = setTimeout(async () => {
              //     const res = await axios({
              //       url: 'https://applet-base-api-t.itheima.net/api/translate',
              //       params: {
              //         words: newValue
              //       }
              //     })
              //     this.result = res.data.data
              //     console.log(res.data.data)
              //   }, 300)
              // }
        })
    </script>
</body>

</html>
```



### 4.综合例子:购物商城

![image-20230816021746216](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230816021746216.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="./css/inputnumber.css" />
    <link rel="stylesheet" href="./css/index.css" />
    <title>购物车</title>
</head>

<body>
    <div class="app-container" id="app">
        <!-- 顶部banner -->
        <div class="banner-box"><img src="http://autumnfish.cn/static/fruit.jpg" alt="" /></div>
        <!-- 面包屑 -->
        <div class="breadcrumb">
            <span>🏠</span>
            /
            <span>购物车</span>
        </div>
        <!-- 购物车主体 -->
        <div class="main" v-if="fruitList.length > 0">
            <div class="table">
                <!-- 头部 -->
                <div class="thead">
                    <div class="tr">
                        <div class="th">选中</div>
                        <div class="th th-pic">图片</div>
                        <div class="th">单价</div>
                        <div class="th num-th">个数</div>
                        <div class="th">小计</div>
                        <div class="th">操作</div>
                    </div>
                </div>
                <!-- 身体 -->
                <div class="tbody">
                    <div class="tr" :class="{active:item.isChecked}" v-for="(item,index) in fruitList" :key="item.id">
                        <div class="td"><input type="checkbox" v-model="item.isChecked" /></div>
                        <div class="td"><img :src="item.icon" /></div>
                        <div class="td">{{ item.price }}</div>
                        <div class="td">
                            <div class="my-input-number">
                                <button class="decrease" @click="sub(item.id)" :disabled="item.num <= 1"> - </button>
                                <span class="my-input__inner">{{item.num}}</span>
                                <button class="increase" @click="add(item.id)"> + </button>
                            </div>
                        </div>
                        <div class="td"> {{ item.num * item.price }}</div>
                        <div class="td"><button @click="del(item.id)">删除</button></div>
                    </div>
                </div>
            </div>
            <!-- 底部 -->
            <div class="bottom">
                <!-- 全选 -->
                <label class="check-all">
                    <input type="checkbox" v-model="isAll" />
                    全选
                </label>
                <div class="right-box">
                    <!-- 所有商品总价 -->
                    <span class="price-box">总价&nbsp;&nbsp;:&nbsp;&nbsp;¥&nbsp;<span class="price">{{ totalPrice
                            }}</span></span>
                    <!-- 结算按钮 -->
                    <button class="pay">结算( {{ totalCount }} )</button>
                </div>
            </div>
        </div>
        <!-- 空车 -->
        <div class="empty" v-else>🛒空空如也</div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <script>
        // 默认的值
        const defaultArr = [
            {
                id: 1,
                icon: 'http://autumnfish.cn/static/火龙果.png',
                isChecked: true,
                num: 2,
                price: 6,
            },
            {
                id: 2,
                icon: 'http://autumnfish.cn/static/荔枝.png',
                isChecked: false,
                num: 7,
                price: 20,
            },
            {
                id: 3,
                icon: 'http://autumnfish.cn/static/榴莲.png',
                isChecked: false,
                num: 3,
                price: 40,
            },
            {
                id: 4,
                icon: 'http://autumnfish.cn/static/鸭梨.png',
                isChecked: true,
                num: 10,
                price: 3,
            },
            {
                id: 5,
                icon: 'http://autumnfish.cn/static/樱桃.png',
                isChecked: false,
                num: 20,
                price: 34,
            },
        ]
        const app = new Vue({
            el: '#app',
            data: {
                // 水果列表从本地存储去取(转为字符串) 没有值的时候就是被用户删除玩了 直接去取默认值
                fruitList: JSON.parse(localStorage.getItem('list')) || defaultArr
            },
            computed: {
                isAll: {
                    get() {
                        // 必须所有小选框都选择,全选按钮才选中 every
                        // 所有item.isChecked为true
                        return this.fruitList.every(item => item.isChecked)
                    },
                    // set可以拿到isAll被修改的值 当你重复勾选按钮就是在修改值传递给value
                    set(value) {
                        console.log(value);
                        // value拿到的就是isAll的值是true还是false
                        // foreach用来遍历整个数组执行一次cb函数
                        this.fruitList.forEach(item => item.isChecked = value)
                    }
                },
                // 统计选中的总数 reduce
                totalCount() {
                    return this.fruitList.reduce((sum, item) => {
                        if (item.isChecked) {
                            // 选中 → 需要累加
                            return sum + item.num
                        } else {
                            // 没选中 → 不需要累加
                            return sum
                        }
                    }, 0)
                },
                // 统计选中的总价
                totalPrice() {
                    return this.fruitList.reduce((sum, item) => {
                        if (item.isChecked) {
                            // 选中 → 需要累加
                            return sum + item.num * item.price
                        } else {
                            // 没选中 → 不需要累加
                            return sum
                        }
                    }, 0)
                }
            },
            watch: {
                fruitList:{
                    deep: true,
                    handler(newValue) {
                        // 将变化的newValue存入本地（转为JSON）
                        localStorage.setItem('list', JSON.stringify(newValue))
                    }
                }
            },

            methods: {
                del(id) {
                    this.fruitList = this.fruitList.filter(item => item.id !== id)
                },
                sub(id) {
                    //1.根据id 找到数组的对应项 find
                    const fruit = this.fruitList.find(item => item.id === id)
                    //2.修改num值
                    fruit.num--
                },
                add(id) {
                    //1.根据id 找到数组的对应项 find
                    const fruit = this.fruitList.find(item => item.id === id)
                    //2.修改num值
                    fruit.num++
                }
            }
        })
    </script>
</body>

</html>
```



## 5.vue2生命周期

### 1.简介

![image-20230817005605725](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817005605725.png)



### 2.生命周期钩子函数

![image-20230817010756925](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817010756925.png)

**例子**

![image-20230817011110254](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817011110254.png)

![image-20230817011430443](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817011430443.png)



### 3.created应用 进入页面就开始请求数据

![image-20230817011816505](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817011816505.png)

#### 1.补充:前端接收的数据

![image-20230817012040278](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817012040278.png)

![image-20230817012055209](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817012055209.png)



### 4.mounted 进入页面获取鼠标焦点

 ![image-20230817012523575](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817012523575.png)



### 5.例子:通过Echarts完成小黑记账清单

![image-20230817022832467](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20230817022832467.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <!-- CSS only -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" />
  <style>
    .red {
      color: red !important;
    }

    .search {
      width: 300px;
      margin: 20px 0;
    }

    .my-form {
      display: flex;
      margin: 20px 0;
    }

    .my-form input {
      flex: 1;
      margin-right: 20px;
    }

    .table> :not(:first-child) {
      border-top: none;
    }

    .contain {
      display: flex;
      padding: 10px;
    }

    .list-box {
      flex: 1;
      padding: 0 30px;
    }

    .list-box a {
      text-decoration: none;
    }

    .echarts-box {
      width: 600px;
      height: 400px;
      padding: 30px;
      margin: 0 auto;
      border: 1px solid #ccc;
    }

    tfoot {
      font-weight: bold;
    }

    @media screen and (max-width: 1000px) {
      .contain {
        flex-wrap: wrap;
      }

      .list-box {
        width: 100%;
      }

      .echarts-box {
        margin-top: 30px;
      }
    }
  </style>
</head>

<body>
  <div id="app">
    <div class="contain">
      <!-- 左侧列表 -->
      <div class="list-box">

        <!-- 添加资产 -->
        <form class="my-form">
          <input type="text" class="form-control" placeholder="消费名称" v-model.trim="name" />
          <input type="text" class="form-control" placeholder="消费价格"  v-model.number="price"/>
          <button type="button" class="btn btn-primary" @click="add">添加账单</button>
        </form>

        <table class="table table-hover">
          <thead>
            <tr>
              <th>编号</th>
              <th>消费名称</th>
              <th>消费价格</th>
              <th>操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item,index) in list" :key="item.id">
              <td>{{index+1}}</td>
              <td>{{item.name}}</td>
              <td :class="{red:item.price>500}">{{item.price.toFixed(2)}}</td>
              <td><a href="javascript:;" @click="del(item.id)">删除</a></td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <td colspan="4">消费总计： {{totalPrice}}</td>
            </tr>
          </tfoot>
        </table>
      </div>

      <!-- 右侧图表 -->
      <div class="echarts-box" id="main"></div>
    </div>
  </div>
  <script src="../echarts.min.js"></script>
  <script src="../vue.js"></script>
  <script src="../axios.js"></script>
  <script>
    /**
     * 接口文档地址：
     * https://www.apifox.cn/apidoc/shared-24459455-ebb1-4fdc-8df8-0aff8dc317a8/api-53371058
     * 
     * 功能需求：
     * 功能需求：
       * 1. 基本渲染
       *    (1) 立刻发送请求获取数据 created
       *    (2) 拿到数据，存到data的响应式数据中
       *    (3) 结合数据，进行渲染 v-for
       *    (4) 消费统计 => 计算属性
       * 2. 添加功能
       *    (1) 收集表单数据 v-model
       *    (2) 给添加按钮注册点击事件，发送添加请求
       *    (3) 需要重新渲染(前端发送了请求，后端数据增加，前端重新渲染)
       * 3. 删除功能
       *    (1) 注册点击事件，传参传 id
       *    (2) 根据 id 发送删除请求
       *    (3) 需要重新渲染
       * 4. 饼图渲染
       *    (1) 初始化一个饼图 echarts.init(dom)(官方文档看一下就都会了)  mounted钩子实现
       *    (2) 根据数据实时更新饼图 echarts.setOption({ ... })
     */
    const app = new Vue({
      el: '#app',
      data: {
        list: [],
        name:'',
        price:''
      },
      created() {
        // 第一次进入发送请求
       this.getList()
      },

      mounted () {
          //1. 操作dom生成echarts实例 
          //由于我们在发送完请求还要调用setOption方法,所以可以把myChart挂载到实例this上,方便拿到
          this.myChart = echarts.init(document.querySelector('#main'))

          //2 操作实例方法生成饼图的初次模板（初始化内容标题模板等等,当你要更新数据时在调一次setOption方法）
          // 可以对照文档来设置格式
          this.myChart.setOption({
            // 大标题
            title: {
              text: '消费账单列表',
              left: 'center'
            },
            // 提示框
            tooltip: {
              trigger: 'item'
            },
            // 图例
            legend: {
              orient: 'vertical',
              left: 'left'
            },
            // 数据项
            series: [
              {
                name: '消费账单',
                type: 'pie',
                radius: '50%', // 半径
                data: [
                // data就是要动态设置的数据
                ],
                emphasis: {
                  itemStyle: {
                    shadowBlur: 10,
                    shadowOffsetX: 0,
                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                  }
                }
              }
            ]
          })
        },
      computed:{
        totalPrice(){
          return this.list.reduce((sum,item) => sum + item.price,0)
        }
      },
      methods:{
        // 获取最新的列表是通用的方法统一封装
        async getList(){
          const res = await axios.get('https://applet-base-api-t.itheima.net/bill', {
          params: {
            creator: '黄老鼠'
          }
        })
        this.list = res.data.data
         
        // 发送完请求以后也要更新饼图 再调用一次setOption
        this.myChart.setOption({
          series:[
            {
              // 只有data是要更新的
              // {value:xx,name:xxx} 这是官网的data设置 所以我们通过map来转换处理数据
              data:this.list.map((item) => ({value:item.price,name:item.name}))
            }
          ]
        })

        },


        async add(){
          if (!this.name) {
            alert('请输入消费名称')
            return
          }
          if (!this.price) {
            alert('请输入消费价格')
            return
          }
          const res = await axios.post('https://applet-base-api-t.itheima.net/bill',{
            creator: '黄老鼠',
            name:this.name, //this.name就是表单输入的数据 因为做了双向数据绑定
            price:this.price
          })
          // 拉取后台最新的数据重新渲染
          this.getList()
          // 清空输入
          this.price = ''
          this.name = ''
        },
        // 删除方法
        async del(id){
          // 删除的方法参数直接在path上传递
          if(confirm('你确定删除吗')){
          const res = await axios.delete(`https://applet-base-api-t.itheima.net/bill/${id}`)
          }
          this.getList()
        }
      },


    })
  </script>
</body>

</html>
```



## 6.vue2工程化开发

### 1.vue2vue3工程化的不同点

```apl
vue3:vite->create-vue->pinia
vue2:webpack->vue-cli->vuex
```



### 2.基本使用(理解项目、如何创建项目)

**基于vue-cli创建项目**

![image-20230817173949222](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230817173949222.png)

![uTools_1692265492491](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692265492491.png)

**main.js入口文件**

![uTools_1692267039957](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692267039957.png)

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692267039957.png)

![uTools_1692265956688](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692265956688.png)



### 3.组件化开发

![image-20230818010057817](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818010057817.png)

![image-20230818010217040](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818010217040.png)

**vue2的template不能有多个，template里中也只能有一个根元素**

![image-20230818010449274](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818010449274.png)

![image-20230818010523377](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818010523377.png)



#### 1.普通组件的注册使用

##### 1.局部注册

**vscode中敲击<vue>一件生成组件三部分结构**

![image-20230818010821419](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818010821419.png)

![image-20230818011240088](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818011240088.png)

##### 2.全局注册

![image-20230818011409758](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818011409758.png)

![image-20230818011633721](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818011633721.png)

##### 3.vscode快捷键

```bash
1.1.shift+alt+左键多行编辑
2.大文件同时折叠 ctrl + k, ctrl + 0
3.2.大文件同时展开 ctrl + k, ctrl + j
4. ctrl+c 关闭项目运行
```



#### 4.案例

![image-20230818013752471](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818013752471.png)



#### 5.组件的三大组成部分

##### 1.scoped解决样式冲突

![image-20230818175205781](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818175205781.png)

![image-20230818175144209](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818175144209.png)

##### 2.组件的data函数

**根组件的data是一个对象，而子组件的data必须用函数。**

![image-20230822235556671](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230822235556671.png)



### 4.组件的通信

#### 1.父子组件通信

![image-20230822235854981](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230822235854981.png)

props父传子的流程

![image-20230823000121939](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823000121939.png)

$emits子传父通知更新(父组件更新了title会向下传递给子组件)

![image-20230823000255393](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823000255393.png)

![image-20230823010159161](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823010159161.png)

**这里newTitle拿到就是`changeTitle`事件带的参数 `传智教育`,我们要知道父组件传给子组件的props是只读的,所以不能直接在子组件中修改,要在父组件中修改**

**Vue3中类似的例子**

```vue
<!--app-->
<template>
  <Child1 @changeTitle="changeTitle" :title="myTitle"></Child1>
</template>

<script setup lang="ts">
import { Ref, ref } from "vue";
import Child1 from "./components/Child1.vue";
const myTitle = ref('我是修改前的标题')

const changeTitle = (res:string) => {
  console.log('接收到修改消息',res);
  myTitle.value = res
}

</script>

<!-- Child.vue -->
<template>
  {{ props.title }}
  <button @click="changeTitle">传递消息</button>
</template>

<script lang="ts" setup>
import { ref } from "vue"
const message = ref('我是被修改后的消息了,从子组件中来的')
const props = defineProps(['title'])
const emits = defineEmits(['changeTitle'])
const changeTitle = () => {
  emits('changeTitle',message)
}
</script>
```

![image-20230823004809491](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823004809491.png)



##### 1.什么是props

![image-20230823005141169](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823005141169.png)



##### 2.porps校验

![image-20230823005815328](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823005815328.png)



##### 3.prop要遵循单向数据流

**口诀:谁的数据谁负责**

![image-20230823010357836](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823010357836.png)

**Vscode   crtl+d获取单个单词**



##### 4.例子：拆分小黑记事本例子

![uTools_1692725042633](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692725042633.png)

![image-20230823012655965](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823012655965.png)

![image-20230823012759802](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823012759802.png)

![image-20230823012928562](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230823012928562.png)



#### 2.非父子通信 -> event bus 事件总线

**这种是一对多的关系，只要监听了该事件都能监听到**

![image-20230829164344345](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230829164344345.png)



event bus.js

![image-20230829225531566](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230829225531566.png)

```vue
App.vue
<template>
    <div>
      <A1Components></A1Components>
      <B1Components></B1Components>
    </div>
</template>

<script>
import A1Components from './components/A1Components.vue';
import B1Components from './components/B1Components.vue';
export default{
  components:{
    A1Components,
    B1Components
  }
}
</script>
A1
<template>
  <div>
    我是A组件(接收方)
    <p>我可以使用msg: {{ msg }}</p>
  </div>
</template>

<script >
import Bus from '../utils/EventBus.js'
export default {
    created(){
        // 2. 在组件A(接收方),进行监听Bus的事件(订阅消息) 监听Bus的sendMsg事件
        Bus.$on('sendMsg',(msg) => {  //Bus.$on表示订阅
            // console.log(msg); //msg可以接收到B1Components发送的消息
            console.log(this.msg);
            this.msg = msg
        })
    },
    data(){
      return{
        msg:''
      }
    }
}
</script>
B1
<template>
  <div>
    我是B组件(发送方)
    <button @click="clickSend">发送</button>
  </div>
</template>

<script>
import Bus from '../utils/EventBus.js'
export default {
    methods:{
        clickSend(){
            //3.B组件(发送方) 触发事件发送消息
            Bus.$emit('sendMsg','我已经开始发送消息')
        }
    }
}
</script>
```

#### 3.非父子通信 provide和inject

![image-20230829225712387](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230829225712387.png)

**注意这个响应式和非响应式**

![image-20230829231620955](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230829231620955.png)



### 5.原理解析

#### 1.v-model应用于模板的原理

`在vue的模板中，不能直接用e拿到事件对象，要用$event才能拿到事件形参 -> e`

![image-20230829233644426](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230829233644426.png)



#### 2.v-model应用于子组件

**`v-model不能直接在子组件绑定，因为子组件不能直接修改父组件传过来的props`**

![image-20230830000750568](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230830000750568.png)

```vue
App.vue
<template>
    <div>
      <A1Components :selectId="selectId" @changeId="selectId = $event"></A1Components>
    </div>
</template>

<script>
import A1Components from './components/A1Components.vue';

export default{
  components:{
    A1Components
  },
  data(){
    return{
      selectId:'101'  //父组件传递过去的props
    }
  }
}
</script>
A1
<template>
  <div>
    <!-- 子组件进行封装 -->
    <select :value="selectId" @change="handleChange">
      <option value="101">北京</option>
      <option value="102">广州</option>
      <option value="103">上海</option>
      <option value="104">天津</option>
      <option value="105">厦门</option>
    </select>
  </div>
</template>

<script >
export default {
props:{
  selectId:String
},
methods:{
  handleChange(e){
    this.$emit('changeId',e.target.value)
   }
 }
}
</script>
```



#### 3.v-model直接运用于父组件

![image-20230830001432563](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230830001432563.png)

```vue
app
<template>
    <div>
      <A1Components v-model="selectId"></A1Components>
    </div>
</template>

<script>
import A1Components from './components/A1Components.vue';

export default{
  components:{
    A1Components
  },
  data(){
    return{
      selectId:'101'  //父组件传递过去的props
    }
  }
}
</script>
a1
<template>
  <div>
    <!-- 子组件进行封装 -->
    <select :value="value" @change="handleChange">
      <option value="101">北京</option>
      <option value="102">广州</option>
      <option value="103">上海</option>
      <option value="104">天津</option>
      <option value="105">厦门</option>
    </select>
  </div>
</template>

<script >
export default {
props:{
  value:String
},
methods:{
  handleChange(e){
    this.$emit('input',e.target.value)
  }
}

}
</script>
```

![image-20230830001542674](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230830001542674.png)



#### 4.sync修饰符

![image-20230830041942369](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230830041942369.png)

```VUE
app
<template>
    <div>
      <button @click="isShow = true;is = false" v-show="is">退出</button>
      <!-- 相当于绑定了 :visible + @update:visible -->
      <A1Components :visible.sync="isShow"></A1Components>
    </div>
</template>

<script>
import A1Components from './components/A1Components.vue';

export default{
  components:{
    A1Components
  },
  data(){
    return{
      is:true,
      isShow:false//父组件传递过去的props
    }
  }
}
</script>

A1
<template>
  <div class="top">
    <div class="show" v-show="visible">
      <p>温馨提示 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<button @click="close">x</button></p>
      <br>
      <p>你确认退出系统吗!</p>
      <button @click="close">确认</button>
      <button @click="noClose">取消</button>
    </div>
    <div v-show="isShow2" class="top1">
      <p>退出成功</p>
    </div>
    <div v-show="isShow3" class="top2">
      <p>取消成功,刷新返回页面</p>
    </div>
  </div>
</template>

<script >
export default {
  data(){
    return{
      isShow1:true,
      isShow2:false,
      isShow3:false
    }
  },
props:{
  visible:Boolean
},
methods:{
  clickChange(){
    
  },
 close(){
  this.$emit('update:visible',false)
  this.isShow2 = true
 },
 noClose(){
  this.$emit('update:visible',false)
  this.isShow3 = true
 },
}

}
</script>

<style scoped>
.show{
  z-index:999;
  width: 500px;
  height: 300px;
  background:rgb(120, 119, 119);
}
.top1{
  z-index: 1000;
  width: 500px;
  height: 300px;
  background:rgb(120, 119, 119);
}
.top2{
  z-index: 1000;
  width: 500px;
  height: 300px;
  background:rgb(120, 119, 119);
}
</style>
```



#### 5.ref和$ref

1.获取DOM元素

![image-20230903212042625](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903212042625.png)

2.获取组件实例

![image-20230903212533972](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903212533972.png)

![image-20230903212456385](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903212456385.png)



#### 6.vue是异步更新，$nextTick

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903213432067.png)

![image-20230903213415092](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903213415092.png)

![image-20230903213507354](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903213507354.png)

##### 1.vue3获取DOM元素

![uTools_1693747936642](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1693747936642.png)



### 6.vue自定义指令

#### 1.概念

![image-20230903213958356](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903213958356.png)

inserted相当于一个生命周期钩子函数

![image-20230903214248928](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903214248928.png)

![image-20230903214602601](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903214602601.png)



#### 2.指令的值(传参)

![image-20230903214955313](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903214955313.png)

![image-20230903215220671](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903215220671.png)

![image-20230903215332741](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903215332741.png)



#### 3.例子:v-loading

![image-20230903215439844](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903215439844.png)

![image-20230903215559820](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903215559820.png)

![image-20230903222415721](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903222415721.png)

```vue
<template>
  <div class="main">
    <div class="box" v-loading="isLoading">
      <ul>
        <li v-for="item in list" :key="item.id" class="news">
          <div class="left">
            <div class="title">{{ item.title }}</div>
            <div class="info">
              <span>{{ item.source }}</span>
              <span>{{ item.time }}</span>
            </div>
          </div>

          <div class="right">
            <img :src="item.img" alt="">
          </div>
        </li>
      </ul>
    </div>
    <div class="box2" v-loading="isLoading">
    </div>
  </div>
</template>

<script>
// 安装axios =>  yarn add axios
import axios from 'axios'


// 接口地址：http://hmajax.itheima.net/api/news
// 请求方式：get
export default {
  data () {
    return {
      list: [],
      isLoading:true
    }
  },

  async created () {
    // 1. 发送请求获取数据
    const res = await axios.get('http://hmajax.itheima.net/api/news')
    
    setTimeout(() => {
      // 2. 更新到 list 中
      this.list = res.data.data
      this.isLoading = false
    }, 2000)
  },
  directives:{
    loading:{
        inserted(el,binding) {
          //el 拿到就是v-loading指令绑定的元素
          // binding.value 拿到的就是isLoading
          binding.value ? el.classList.add('loading') : el.classList.remove('loading')
        },
        update(el,binding){
          binding.value ? el.classList.add('loading') : el.classList.remove('loading')
        }
      }
  }
}
</script>

<style>
/* 伪类 - 蒙层效果 */
.loading:before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #fff url('./loading.gif') no-repeat center;
}

.box2 {  子绝父相
  width: 400px;
  height: 400px;
  border: 2px solid #000;
  position: relative;
} 

.box {
  width: 800px;
  min-height: 500px;
  border: 3px solid orange;
  border-radius: 5px;
  position: relative;
}
.news {
  display: flex;
  height: 120px;
  width: 600px;
  margin: 0 auto;
  padding: 20px 0;
  cursor: pointer;
}
.news .left {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding-right: 10px;
}
.news .left .title {
  font-size: 20px;
}
.news .left .info {
  color: #999999;
}
.news .left .info span {
  margin-right: 20px;
}
.news .right {
  width: 160px;
  height: 120px;
}
.news .right img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
```



### 7.插槽

#### 1.默认插槽

我们这里用父子通信实际上是不方便的，还要触发了事件才能去修改组件样式

![image-20230903223306077](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223306077.png)

![image-20230903223327240](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223327240.png)

![image-20230903223128475](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223128475.png)

![image-20230903223159193](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223159193.png)



#### 2.插槽默认内容

![image-20230903223554510](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223554510.png)



#### 3.具名插槽

![image-20230903223812611](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223812611.png)

![image-20230903223848220](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903223848220.png)

**v-slot也是操作dom元素的，可以证明vue指令就是在操作dom元素**



#### 4.作用域插槽

![image-20230903224306566](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903224306566.png)

![image-20230903224432163](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903224432163.png)

**操作需要定制，然后在删除时需要用到id，我们可以在插槽中传入id值，使得其可以进行删除**



##### 1.具体使用

![image-20230903224620176](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230903224620176.png)

```vue
app
<template>
  <div>
    <A1Components :data="list">
      <!-- 通过 插槽名='对象名' 来接收 -->
      <template #default="obj">
        <button @click="del(obj.item.id)">删除</button>
      </template>
    </A1Components>
    <A1Components :data="list2">
      <!-- 可以解构赋值 -->
      <template #default="{ item }"> 
        <button @click="show(item)">查看</button>
      </template>
    </A1Components>
  </div>
</template>

<script>
import A1Components from './components/A1Components.vue';
export default {
  data () {
    return {
      list: [
        { id: 1, name: '张小花', age: 18 },
        { id: 2, name: '孙大明', age: 19 },
        { id: 3, name: '刘德忠', age: 17 },
      ],
      list2: [
        { id: 1, name: '赵小云', age: 18 },
        { id: 2, name: '刘蓓蓓', age: 19 },
        { id: 3, name: '姜肖泰', age: 17 },
      ]
    }
  },
  components: {
    A1Components
  },
  methods:{
    del(id){
      this.list = this.list.filter(item => item.id !== id)
    },
    show(item){
      alert(`我是${item.name},我${item.age}岁`)
    }

  }
}
</script>

A1
<template>
  <table class="my-table">
    <thead>
      <tr>
        <th>序号</th>
        <th>姓名</th>
        <th>年纪</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item,index) in data" :key="item.id">
        <td>{{ index+1 }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.age }}</td>
        <td>
          <!-- 把item,msg传给父组件使用 -->
          <!-- 传过去的内容会包在一个对象中 -->
          <slot :item="item" msg="我是测试消息"></slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    data: Array,
  },
}
</script>

<style scoped>
.my-table {
  width: 450px;
  text-align: center;
  border: 1px solid #ccc;
  font-size: 24px;
  margin: 30px auto;
}
.my-table thead {
  background-color: #1f74ff;
  color: #fff;
}
.my-table thead th {
  font-weight: normal;
}
.my-table thead tr {
  line-height: 40px;
}
.my-table th,
.my-table td {
  border-bottom: 1px solid #ccc;
  border-right: 1px solid #ccc;
}
.my-table td:last-child {
  border-right: none;
}
.my-table tr:last-child td {
  border-bottom: none;
}
.my-table button {
  width: 65px;
  height: 35px;
  font-size: 18px;
  border: 1px solid #ccc;
  outline: none;
  border-radius: 3px;
  cursor: pointer;
  background-color: #ffffff;
  margin-left: 5px;
}
</style>
```



#### 5.综合案例(练习自定义指令、插槽)

##### 1.APP.VUE

```vue
<template>
  <div class="table-case">
    <!-- 利用了具名插槽和作用域插槽 -->
    <MyTable :data="goods">
      <template #head>
        <th>编号</th>
          <th>名称</th>
          <th>图片</th>
          <th width="100px">标签</th>
      </template>
      <template #body="{ item,index }">
        <td>{{ index+1 }}</td>
          <td>{{item.name}}</td>
          <td>
            <img :src="item.picture" />
          </td>
          <td>
           <MyTag v-model="item.tag"></MyTag>
          </td>
      </template>
    </MyTable>
  </div>
</template>

<script>
// my-tag 标签组件的封装
// 1. 创建组件 - 初始化
// 2. 实现功能
//    (1) 双击显示，并且自动聚焦
//        v-if v-else @dbclick 操作 isEdit
//        自动聚焦：
//        1. $nextTick => $refs 获取到dom，进行focus获取焦点
//        2. 封装v-focus指令

//    (2) 失去焦点，隐藏输入框
//        @blur 操作 isEdit 即可

//    (3) 回显标签信息
//        回显的标签信息是父组件传递过来的
//        v-model实现功能 (简化代码)  v-model => :value 和 @input
//        组件内部通过props接收, :value设置给输入框

//    (4) 内容修改了，回车 => 修改标签信息
//        @keyup.enter, 触发事件 $emit('input', e.target.value)

// ---------------------------------------------------------------------

// my-table 表格组件的封装
// 1. 数据不能写死，动态传递表格渲染的数据  props
// 2. 结构不能写死 - 多处结构自定义 【具名插槽】
//    (1) 表头支持自定义
//    (2) 主体支持自定义
import MyTag from './components/MyTag.vue';
import MyTable from './components/MyTable.vue';
export default {
  name: 'TableCase',
  data() {
    return {
      text:'水杯',
      goods: [
        {
          id: 101,
          picture:
            'https://yanxuan-item.nosdn.127.net/f8c37ffa41ab1eb84bff499e1f6acfc7.jpg',
          name: '梨皮朱泥三绝清代小品壶经典款紫砂壶',
          tag: '茶具',
        },
        {
          id: 102,
          picture:
            'https://yanxuan-item.nosdn.127.net/221317c85274a188174352474b859d7b.jpg',
          name: '全防水HABU旋钮牛皮户外徒步鞋山宁泰抗菌',
          tag: '男鞋',
        },
        {
          id: 103,
          picture:
            'https://yanxuan-item.nosdn.127.net/cd4b840751ef4f7505c85004f0bebcb5.png',
          name: '毛茸茸小熊出没，儿童羊羔绒背心73-90cm',
          tag: '儿童服饰',
        },
        {
          id: 104,
          picture:
            'https://yanxuan-item.nosdn.127.net/56eb25a38d7a630e76a608a9360eec6b.jpg',
          name: '基础百搭，儿童套头针织毛衣1-9岁',
          tag: '儿童服饰',
        },
      ],
    }
  },
  components:{
    MyTable,MyTag
  }
}
</script>

<style lang="less" scoped>
.table-case {
  width: 1000px;
  margin: 50px auto;
  img {
    width: 100px;
    height: 100px;
    object-fit: contain;
    vertical-align: middle;
  }
}
</style>
```

##### 2.MyTag

```vue
<template>
     <div class="my-tag">
        <input 
            v-if="isEdit"
            :value="value"
            @keyup.enter="handEnter"
            v-focus
            class="input"
            type="text" 
            placeholder="输入标签"
            @blur="isEdit = false" 
        />
        <!-- blur失去焦点事件 -->
        <div
         class="text"
         @dblclick="handleClick"
         v-else
        >
         {{ value }}
        </div>
      </div>
</template>

<script>
export default{
    props:{
        value:String
    },
    data(){
        return{
            isEdit:false
        }
    },
    methods:{
        // 点击标签事件
        handleClick(){
            this.isEdit = true //双击显示
        },
        // 标签回车事件
        handEnter(e){
            // 输入为空不可以保存
            if(e.target.value.trim() === ''){
                return alert('输入不可以为空')
            }
            // 回车时提醒父组件更新值(通过v-model绑定了父组件 props接收父组件数据 emit提醒父组件更新)
            this.$emit('input',e.target.value)
            // 回车以后自动失去焦点
            this.isEdit = false
        }
    }
}
</script>

<style scoped lang="less">
.my-tag {
    cursor: pointer;
    .input {
      appearance: none;
      outline: none;
      border: 1px solid #ccc;
      width: 100px;
      height: 40px;
      box-sizing: border-box;
      padding: 10px;
      color: #666;
      &::placeholder {
        color: #666;
      }
    }
  }
</style>
```

##### 3.MyTable

```vue
<template>
  <table class="my-table">
      <thead>
        <tr>
            <slot name="head"></slot>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,index) in data" :key="item.id">
            <!-- 给父组件传递了俩个参数 分别是item和index，这俩个会变成一个对象传递给父组件 -->
          <slot name="body" :item="item" :index="index"></slot>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default {
    props:{
        data:{
            type:Array,
            required:true
        }
        
    }
}
</script>

<style lang="less" scoped>
    .my-table {
    width: 100%;
    border-spacing: 0;
    img {
      width: 100px;
      height: 100px;
      object-fit: contain;
      vertical-align: middle;
    }
    th {
      background: #f5f5f5;
      border-bottom: 2px solid #069;
    }
    td {
      border-bottom: 1px dashed #ccc;
    }
    td,
    th {
      text-align: center;
      padding: 10px;
      transition: all 0.5s;
      &.red {
        color: red;
      }
    }
    .none {
      height: 100px;
      line-height: 100px;
      color: #999;
    }
  }
</style>
```

##### 4.main.js

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

// 封装全局指令
Vue.directive('focus',{
  // 指令所在的dom元素，被插入到页面中时触发
  inserted(el){
    el.focus()
  }
})

new Vue({
  render: h => h(App),
}).$mount('#app')

```



### 8.Vue Router

#### 1.单页和多页应用程序

**Vue主要用于构建单页面应用程序,React主要用于构建多页面应用程序(大项目)**

`vue3构建多页面应用程序:`https://blog.csdn.net/snowball_li/article/details/132154902

![image-20230905160004799](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905160004799.png)

![image-20230905160054164](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905160054164.png)



#### 2.router简介

router就是为了实现单页面应用程序的按需更新。

![image-20230905160214871](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905160214871.png)

![image-20230905160248147](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905160248147.png)



#### 3.基本使用(5+2的)

##### 1.5个基本步骤

![image-20230905205322490](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905205322490.png)

![image-20230905205719002](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905205719002.png)

`现在vue3更多的用pinia`



##### 2.2个核心步骤

![image-20230905210708433](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905210708433.png)

路由就是组件和路径映射关系

![image-20230905212054854](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905212054854.png)



##### 3.组件存放目录的问题

![image-20230905212308272](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905212308272.png)

![image-20230905212343006](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905212343006.png)

![image-20230905212358878](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905212358878.png)

![image-20230905212420730](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905212420730.png)



#### 4.路由进阶

##### 1.路由模块封装

![image-20230905214308623](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905214308623.png)

```js
/src/router/index.js
// 路由入口文件
import Vue from 'vue'

// 为了避免层次问题 vue提供了@标识符 表示从src出发
import Find from '@/views/Find.vue'
import My from '@/views/My.vue'

import VueRouter from 'vue-router'
Vue.use(VueRouter)

const router = new VueRouter({
  routes:[
    {path:'/find',component:Find},
    {path:'/my',component:My}
  ]
})

export default router

main.js
import Vue from 'vue'
import App from './App.vue'
import router from './router/index.js'

Vue.config.productionTip = false


new Vue({
  render: h => h(App),
  router:router
}).$mount('#app')
```



##### 2.router-link(声明式导航)高亮实现

![image-20230905215028762](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905215028762.png)

![image-20230905215106911](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905215106911.png)

![image-20230905215508409](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905215508409.png)

**定制routerlink的俩个类名**

![image-20230905215831616](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230905215831616.png)



##### 3.router-link 跳转传参

###### 1.查询参数传参

![image-20230906205045647](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205045647.png)

![image-20230906204954602](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906204954602.png)

###### 2.动态路由传参

![image-20230906205251558](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205251558.png)

![image-20230906205446990](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205446990.png)

![image-20230906205502990](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205502990.png)

**配置了动态路由以后,表示搜索必须要在路径后面传参，不传参就不会显示,可以使用?参数可选符来解决**

![image-20230906205927134](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205927134.png)



###### 3.总结

![image-20230906205628481](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906205628481.png)



#### 4.路由重定向

![image-20230906210246277](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906210246277.png)



#### 5.404路由

![image-20230906210518930](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906210518930.png)



#### 6.路由模式设置

![image-20230906210642492](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906210642492.png)



#### 7.编程式导航

`传统js代码跳转使用location.href,但是在vue中不适合，因为vue是单页应用程序,不能跳转网页`



##### 1.基本使用

###### route和router、query和params

```js
1.route是用来获取路由信息的，router是用来操作路由的。
2.route对象是一个路由信息对象，里面主要包含路由的一些基本信息，包含当前的路径，参数，query对象等。而router对象则是用来定义路由表，实现页面跳转等功能。
3.query和params属性都是用来传递参数的。其中，params(动态路由传参)是在路由路径上直接绑定的，形式是 /path/:paramName，而query(查询参数传参)则是通过 ?key=value 的形式添加在路由地址后面 。
```



分为俩种编程式导航: 通过路径跳转、通过名字跳转

![image-20230906215022021](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906215022021.png)

![image-20230906215004403](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906215004403.png)



##### 2.编程式导航路由传参

###### 1.path的路径跳转传参 --> 查询参数传参

![image-20230906215209797](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906215209797.png)





###### 2.path的路径跳转传参:动态路由传参

![image-20230906215235414](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906215235414.png)

配置的路由例子

![image-20231006185204264](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006185204264.png)



实际操作

查询参数传参query

![image-20230906215545185](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906215545185.png)

动态路由传参params

![image-20231006185439924](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006185439924.png)



###### 3.name命名路由跳转传参查询参数传参

![image-20230906220202157](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906220202157.png)



###### 4.name命名路由跳转传参动态路由传参

特殊:因为动态路由传参是直接在路径中传参，而name跳转的方式没有书写路径，所以我们通过params来同时接收和发送

![image-20230906220235685](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906220235685.png)



###### 5.总结

![image-20230906220526962](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906220526962.png)

![image-20230906220542827](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230906220542827.png)

`path适合路径简单，name适合路径复杂，query适合多个参数，动态路由参数适合单个参数`



#### 8.综合案例 面经详情

**需求分析**

![image-20230907162321491](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907162321491.png)

##### 1.嵌套路由(子路由)

![image-20230907163641037](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907163641037.png)

![image-20230907163701466](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907163701466.png)

##### 2.index.js

```js
// 路由入口文件
import Vue from 'vue'
import VueRouter from 'vue-router'
Vue.use(VueRouter)

import Layout from '@/views/Layout'
import ArticleDetail  from '@/views/ArticleDetail'
import Article from '@/views/Article'
import Collect from '@/views/Collect'
import Like from '@/views/Like'
import User from '@/views/User'

const router = new VueRouter({
  routes:[
    {
      path:'/',
      component:Layout,
      redirect:'',
      children:[
        {
          path:'/article',
          component:Article
        },
        {
          path:'/collect',
          component:Collect
        },
        {
          path:'/like',
          component:Like
        },
        {
          path:'/user',
          component:User
        },
      ]
    },
    {
      path:'/detail/:id',
      component:ArticleDetail
    }
  ]
})

export default router
```

##### 3.ArticleDetail

```vue
<template>
  <div class="article-detail-page" v-if="article.id">
    <nav class="nav"> <span @click="$router.back()" class="back">&lt;</span> 面经详情</nav>
    <header class="header">
      <h1>{{ article.stem }}</h1>
      <p>{{ article.createdAt }} | {{ article.views }} 浏览量 | {{ article.likeCount }} 点赞数</p>
      <p>
        <img :src="article.creatorAvatar" alt=""> 
        <span>{{ article.creatorName }}</span> 
      </p>
    </header>
    <main class="body">  
      {{ article.content }}
    </main>
  </div>
</template>

<script>
import axios from 'axios'
// 请求地址: https://mock.boxuegu.com/mock/3083/articles/:id
// 请求方式: get
export default {
  name: "ArticleDetailPage",
  data() {
    return {
      article:{}
    }
  },
  async created(){
    //const id  = this.$route.query.id
    // 1.第一步获取传过来的参数
    const id = this.$route.params.id
    // 2.发送请求
    const {data} = await axios.get(`https://mock.boxuegu.com/mock/3083/articles/${id}`)
    this.article = data.result 
  }
}
</script>

<style lang="less" scoped>
.article-detail-page {
  .nav {
    height: 44px;
    border-bottom: 1px solid #e4e4e4;
    line-height: 44px;
    text-align: center;
    .back {
      font-size: 18px;
      color: #666;
      position: absolute;
      left: 10px;
      top: 0;
      transform: scale(1, 1.5);
    }
  }
  .header {
    padding: 0 15px;
    p {
      color: #999;
      font-size: 12px;
      display: flex;
      align-items: center;
    }
    img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      overflow: hidden;
    }
  }
  .body {
    padding: 0 15px;
  }
}
</style>
```

##### 4.Article

```vue
<template>
  <!-- v-if优化了一下请求等待时间 -->
  <div class="article-page" v-if="articles">
    //v-for渲染 并注册点击事件跳转到面经详情(记得传参数)
    //@click="$router.push(`/detail?id=${item.id}`)"
    <div
      v-for="item in articles"
      :key="item.id"
      @click="$router.push(`/detail/${item.id}`)"
      class="article-item">
      <div class="head">
        <img :src="item.creatorAvatar" alt="" />
        <div class="con">
          <p class="title">{{ item.stem }}</p>
          <p class="other">{{ item.creatorName }} | {{ item.createdAt }}</p>
        </div>
      </div>
      <div class="body">
        {{ item.content }}
      </div>
      <div class="foot">点赞 {{ item.likeCount }} | 浏览 {{ item.views }}</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

// 首页请求渲染
// 1. 安装 axios   yarn add axios
// 2. 看接口文档，确认请求方式，请求地址，请求参数
//    请求地址: https://mock.boxuegu.com/mock/3083/articles
//    请求方式: get
// 3. created中发请求，获取数据，存起来
// 4. 页面动态渲染

// 跳转详情页传参 → 渲染
// 1. 查询参数传参 (更适合多个参数)
//    ?参数=参数值    =>  this.$route.query.参数名
// 2. 动态路由传参 (单个参数更优雅方便)
//    改造路由 => /路径/参数  =>  this.$route.params.参数名
//    细节优化：
//    (1) 访问 / 重定向到 /article   (redirect)
//    (2) 返回上一页 $router.back()
//    (3) 下一页  $router.next()
export default {
  name: 'ArticlePage',
  data () {
    return {
      articles:[]
    }
  },
  async created(){
    //1.axios发请求拿到数据
    const res = await axios.get('https://mock.boxuegu.com/mock/3083/articles')
    // 2.将得到的数据存起来准备渲染
    this.articles = res.data.result.rows
  }
}
</script>

<style lang="less" scoped>
.article-page {
  background: #f5f5f5;
}
.article-item {
  margin-bottom: 10px;
  background: #fff;
  padding: 10px 15px;
  .head {
    display: flex;
    img {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      overflow: hidden;
    }
    .con {
      flex: 1;
      overflow: hidden;
      padding-left: 15px;
      p {
        margin: 0;
        line-height: 1.5;
        &.title {
          text-overflow: ellipsis;
          overflow: hidden;
          width: 100%;
          white-space: nowrap;
        }
        &.other {
          font-size: 10px;
          color: #999;
        }
      }
    }
  }
  .body {
    font-size: 14px;
    color: #666;
    line-height: 1.6;
    margin-top: 10px;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }
  .foot {
    font-size: 12px;
    color: #999;
    margin-top: 10px;
  }
}
</style>
```

##### 5.Layout

```vue
<template>
  <div class="h5-wrapper">
    <div class="content">
      <router-view></router-view>
    </div>
    <nav class="tabbar">
      <router-link to="/article">面经</router-link>
      <router-link to="/collect">收藏</router-link>
      <router-link to="/like">喜欢</router-link>
      <router-link to="/user">我的</router-link>
    </nav>
  </div>
</template>

<script>
export default {
  // 组件名(如果没有配置 name，才会找文件名作为组件名)
  name: 'LayoutPage',
  // 组件缓存了，就不会执行组件的created，mounted，destroyed等钩子
  // 所以提供了 actived 和 deactived
  created () {
    console.log('created 组件被加载了');
  },
  mounted () {
    console.log('mounted dom渲染完了');
  },
  destroyed () {
    console.log('destroyed 组件被销毁了');
  },

  activated () {
    alert('你好，欢迎回到首页')
    console.log('activated 组件被激活了，看到页面了');
  },
  deactivated () {
    console.log('deactivated 组件失活，离开页面了');
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
<style lang="less" scoped>
.h5-wrapper {
  .content {
    margin-bottom: 51px;
  }
  .tabbar {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 50px;
    line-height: 50px;
    text-align: center;
    display: flex;
    background: #fff;
    border-top: 1px solid #e4e4e4;
    a {
      flex: 1;
      text-decoration: none;
      font-size: 14px;
      color: #333;
      -webkit-tap-highlight-color: transparent;
    }
  }
}
</style>
```

##### 6.App

```vue
<template>
  <div class="h5-wrapper">
    <!-- 包裹了keep-alive 一级路由匹配的组件都会被缓存
      LayoutPage组件(被缓存) - 多两个生命周期钩子
          - actived 激活时，组件被看到时触发
          - deactived 失活时，离开页面组件看不见触发
          ArticleDetailPage组件(未被缓存)

         需求：只希望Layout被缓存，include配置
         :include="组件名数组"
    -->
    <keep-alive :include="keepArr">
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: "h5-wrapper",
  data(){
    return{
      keepArr:['LayoutPage']
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
<style lang="less" scoped>
.h5-wrapper {
  .content {
    margin-bottom: 51px;
  }
  .tabbar {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 50px;
    line-height: 50px;
    text-align: center;
    display: flex;
    background: #fff;
    border-top: 1px solid #e4e4e4;
    a {
      flex: 1;
      text-decoration: none;
      font-size: 14px;
      color: #333;
      -webkit-tap-highlight-color: transparent;
      &.router-link-active {
        color: #fa0;
      }
    }
  }
}
</style>
```

#### 9.路由前置守卫

![image-20230918210141971](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918210141971.png)

![image-20230918211222115](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918211222115.png)

to里面有俩个path

![image-20230918211514451](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918211514451.png)

path**是不带参数的**

**例子**

```js
// 我们配置的所有路由在真正被访问到之前(解析渲染对应页面时),都必须先经过全局前置路由守卫
// 只有放行了,才能去到想访问的地方

// to:    到哪里去的完整路由信息对象(路径,参数) 比如你在/下点击按钮跳转到/cart -此时to就是/cart
// from:  从哪里来的完整路由信息对象(路径,参数) 比如你在/下点击按钮跳转到/cart -此时from就是/
// next(): 是否放行
//    1.next() 直接放行 会放行到to去
//    2.next(路径) 进行拦截,拦截到next配置的路径

// 定义一个数组,专门存放需要权限访问的页面(商城项目这种页面少)
const authUrls = ['/pay', '/myorder']

router.beforeEach((to, from, next) => {
  // 1.第一个判断 是否正在访问权限页面
  if (!authUrls.includes(to.path)) {
    next()
    return
  }
  // 2.第二个判断 是否有token
  const token = store.getters.token
  if (token) {
    // 如果有token 则放行
    next()
  } else {
    // 没有token自动跳去登录
    next('/login')
  }
})
export default router
```







### 9.vue-cli和ESlint

#### 1.vue-cli创建自定义项目

```bash
1.vue create 项目名
2.选择自定义创建(自己选)
3.cd 目录
4.npm run serve 或者 yarn serve
```

![image-20230907213754903](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907213754903.png)



#### 2.ESlint代码规范

![image-20230907214203795](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907214203795.png)

`俩个等号会触发隐式转换,不要使用`

![image-20230907214248667](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907214248667.png)

![image-20230907214513590](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230907214513590.png)



#### 3.解决代码规范

![image-20230908112149584](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230908112149584.png)





### 10.Vuex

#### 1.Vuex是什么

![image-20230908112509667](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230908112509667.png)



#### 2.基本使用

![image-20230908113307432](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230908113307432.png)



#### 3.访问和修改仓库数据

##### 1.使用store直接访问

![image-20230910201247689](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910201247689.png)

##### 2.通过辅助函数mapState

![image-20230910201805815](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910201805815.png)



##### 3.mutations(修改仓库的数据)

![image-20230910202157306](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910202157306.png)



##### 4.如何使用mutations来修改数据

![1694349364078](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1694349364078.png)



##### 5.mutations可以提交参数

![image-20230910205500951](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910205500951.png)



例子

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  // 提供公共访问的数据仓库
  state: {
    count: 1,
    title: '你好'
  },
  // mutations的第一个参数都是state,第二个参数是提交载荷(传过来的参数)
  // 只能传递一个载荷(需要多个参数就要包装成一个对象)
  mutations: {
    addCount (state, n) {
      state.count += n
    },
    changeTitle (state) {
      state.title = '更新标题'
    },
    changeCount (state, newCount) {
      state.count = newCount
    }
  }
})
// js模块中直接访问
console.log(store.state.count)

export default store
```



```vue
<template>
  <div>
    <!-- 模板中访问 -->
    <p>{{ $store.state.count }}</p>
    <br>
    <button @click="handleAdd(3)"> 值 + 3 </button>
    <input type="text" @input="inp" :value="count">
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'app',
  created () {
    // 组件逻辑中访问
    console.log(this.$store.state.count)
  },
  computed: {
    ...mapState(['count', 'title'])
  },
  methods: {
    // 提交给仓库更新的消息
    handleAdd (n) {
      this.$store.commit('addCount', n)
      // 传递复杂化参数
      // this.$store.commit('addCount', {
      //   count: 100,
      //   title: '123'
      // })
    },
    inp (e) {
      const msg = +e.target.value
      this.$store.commit('changeCount', msg)
    }
  }
}
</script>
```



##### 6.mapMutations辅助函数

![image-20230910211122601](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910211122601.png)

**更多的是直接模板中直接调用**



##### 7.actions异步修改数据

![image-20230910211532773](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910211532773.png)

![image-20230910211617254](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910211617254.png)



##### 8.mapActions辅助函数

![image-20230910212937921](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910212937921.png)



##### 9.getters

![image-20230910213820657](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230910213820657.png)



##### 10.使用总结

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  // 提供公共访问的数据仓库
  state: {
    count: 1,
    title: '你好',
    list: [1, 2, 3, 4, 5, 6, 7]
  },
  // 类似于计算属性(但是没有set修改 还是要通过mutations修改)
  getters: {
    // 1.getters函数的第一个函数是 state
    // 2.getters函数必须要有返回值
    // getters也是响应式的 也有计算属性的缓存特性
    filterList (state) {
      return state.list.filter(item => item > 5)
    }
  },
  // mutations的第一个参数都是state,第二个参数是提交载荷(传过来的参数)
  // 只能传递一个载荷(需要多个参数就要包装成一个对象)
  mutations: {
    addCount (state, n) {
      state.count += n
    },
    changeTitle (state) {
      state.title = '更新标题'
    },
    changeCount (state, newCount) {
      state.count = newCount
    }
  },
  // actions用来配合处理异步(不能直接操作state,还是要commit 调用mutations的方法来修改)
  actions: {
    // context 上下文(state仓库)  num 要修改成的值
    changeCountAsync (context, num) {
      // 异步操作(更多的是发请求)
      setTimeout(() => {
        // context.commit(‘mutation方法’,额外参数)
        context.commit('changeCount', num)
      }, 1000)
    }
  }
})
// js模块中直接访问
console.log(store.state.count)

export default store
```

```vue
<template>
  <div>
    <!-- 模板中访问 -->
    <p>{{ $store.state.count }}</p>
    <br>
    <button @click="handleAdd(3)"> 值 + 3 </button>
    <input type="text" @input="inp" :value="count">
    <button @click="handleChange666">一秒后修改为666</button>
    <button @click="changeCountAsync(888)">一秒以后改为888</button>

    <hr>
    <!-- 模板中直接使用 -->
    <div>{{ $store.getters.filterList }}</div>
  </div>
</template>

<script>
import { mapActions, mapGetters, mapMutations, mapState } from 'vuex'

export default {
  name: 'app',
  created () {
    // 组件逻辑中访问
    console.log(this.$store.state.count)
  },
  computed: {
    ...mapState(['count', 'title']),
    ...mapGetters(['filterList'])
  },
  methods: {
    ...mapMutations(['changeTitle']),
    ...mapActions(['changeCountAsync']),
    // 提交给仓库更新的消息
    handleAdd (n) {
      this.$store.commit('addCount', n)
      // 传递复杂化参数
      // this.$store.commit('addCount', {
      //   count: 100,
      //   title: '123'
      // })
    },
    inp (e) {
      const msg = +e.target.value
      this.$store.commit('changeCount', msg)
    },
    handleChange666 () {
      // 注意这里调用的action(action自己会去调mutations)
      // 666就是num
      this.$store.dispatch('changeCountAsync', 666)
    }
  }
}
</script>
```



#### 4.vuex分模块(多个仓库)

**应用大型的时候，不分多个仓库容易使得项目难以维护。** 

`但是整个vuex还是单一状态树，子对象也是挂载在父亲节点的state上的`

![image-20230911213209955](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911213209955.png)



##### 1.访问子模块的state

![image-20230911213350842](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911213350842.png)

·映射子模块的具体属性·

![image-20230911214051143](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911214051143.png)



![image-20230911213523362](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911213523362.png)

`整个子模块直接映射`

![image-20230911213639113](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911213639113.png)



##### 2.访问子模块的getters

![image-20230911214252817](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911214252817.png)

![image-20230911214424840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911214424840.png)



**为什么要这样访问呢,打印this.$store.getters**

![image-20230911214623010](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911214623010.png)

```bash
1.我们要挂载带有特殊符号的对象键名要用 对象['user/id']  (原理是相当于把键名包成一个字符串  '') 
2.不能直接  对象.user/id 会报错
```



**通过映射访问更快捷**

![image-20230911215424069](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911215424069.png)



##### 3.访问子模块的mutation

![image-20230911215051324](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911215051324.png)

![image-20230911215517375](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911215517375.png)



##### 4.访问子模块的actions

![image-20230911215707397](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911215707397.png)

![image-20230911220039034](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911220039034.png)



##### 5.案例

index.js

```js
import Vue from 'vue'
import Vuex from 'vuex'
import user from './modules/user'
import work from './modules/work'

Vue.use(Vuex)

const store = new Vuex.Store({
  // 提供公共访问的数据仓库
  state: {
    count: 1,
    title: '你好',
    list: [1, 2, 3, 4, 5, 6, 7]
  },
  // 类似于计算属性(但是没有set修改 还是要通过mutations修改)
  getters: {
    // 1.getters函数的第一个函数是 state
    // 2.getters函数必须要有返回值
    // getters也是响应式的 也有计算属性的缓存特性
    filterList (state) {
      return state.list.filter(item => item > 5)
    }
  },
  // mutations的第一个参数都是state,第二个参数是提交载荷(传过来的参数)
  // 只能传递一个载荷(需要多个参数就要包装成一个对象)
  mutations: {
    addCount (state, n) {
      state.count += n
    },
    changeTitle (state) {
      state.title = '更新标题'
    },
    changeCount (state, newCount) {
      state.count = newCount
    }
  },
  // actions用来配合处理异步(不能直接操作state,还是要commit 调用mutations的方法来修改)
  actions: {
    // context 上下文(state仓库)  num 要修改成的值
    changeCountAsync (context, num) {
      // 异步操作(更多的是发请求)
      setTimeout(() => {
        // context.commit(‘mutation方法’,额外参数)
        context.commit('changeCount', num)
      }, 1000)
    }
  },
  modules: {
    // 挂载
    user, work
  }
})
// js模块中直接访问
console.log(store.state.count)

export default store
```

work.js

```js
const state = {
  user: {
    name: '我是黄宇',
    age: 18
  }
}

const mutations = {
  // 提供一个更新的方法
  changeUserCount (state, obj) {
    state.user.name = obj.name
    state.user.age = obj.age
  }
}

const actions = {
  // 一秒以后才会更新
  // context是当前仓库(子模块)的state 所以是上下文(默认提交的是自己的state)
  // newUser 就是 App 传过来的参数
  asyncChange (context, newUser) {
    setTimeout(() => {
      // 异步操作后提交
      context.commit('changeUserCount', newUser)
    }, 1000)
  }
}

const getters = {}

export default {
  // 开启命名空间
  namespaced: true,
  state,
  mutations,
  actions,
  getters
}
```

APP

```vue
<template>
  <div>
    <!-- 模板中访问 -->
    <p>{{ $store.state.count }}</p>
    <br>
    <button @click="handleAdd(3)"> 值 + 3 </button>
    <input type="text" @input="inp" :value="count">
    <button @click="handleChange666">一秒后修改为666</button>
    <button @click="changeCountAsync(888)">一秒以后改为888</button>

    <hr>
    <!-- 模板中直接使用 -->
    <div>{{ $store.getters.filterList }}</div>

    <hr>

    <div>{{ user }}</div>
    <button @click="fn">一秒就给黄宇改名</button>
    <button @click="asyncChange({
      name: '死狗更新' , age: 55
    })">map映射给死狗改名</button>
  </div>
</template>

<script>
import { mapActions, mapGetters, mapMutations, mapState } from 'vuex'

export default {
  name: 'app',
  created () {
    // 组件逻辑中访问
    console.log(this.$store.state.count)
  },
  computed: {
    ...mapState(['count', 'title']),
    ...mapGetters(['filterList']),
    // 通过 模块名  映射 模块内的数据
    ...mapState('work', ['user'])
  },
  methods: {
    ...mapMutations(['changeTitle']),
    ...mapActions(['changeCountAsync']),
    ...mapActions('work', ['asyncChange']),
    // 提交给仓库更新的消息
    handleAdd (n) {
      this.$store.commit('addCount', n)
      // 传递复杂化参数
      // this.$store.commit('addCount', {
      //   count: 100,
      //   title: '123'
      // })
    },
    inp (e) {
      const msg = +e.target.value
      this.$store.commit('changeCount', msg)
    },
    handleChange666 () {
      // 注意这里调用的action(action自己会去调mutations)
      // 666就是num
      this.$store.dispatch('changeCountAsync', 666)
    },
    fn () {
      this.$store.dispatch('work/asyncChange', {
        name: '死狗宇', age: 28
      })
    }
  }
}
</script>

<style>

</style>

```



#### 5.综合案例购物车 练习Vuex

##### 1.分析项目

![image-20230911222524217](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230911222524217.png)



##### 2.准备后端接口数据(json-server)

![image-20230913214939913](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230913214939913.png)



##### 3.分析

![1694613066502](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1694613066502.png)



##### 4.完整案例 VUE2->vue_cart

index.js 

```js
import Vue from 'vue'
import Vuex from 'vuex'
import cart from './modules/cart'
Vue.use(Vuex)

const store = new Vuex.Store({
  modules: {
    cart
  }
})

export default store
```

cart.js

```js
import axios from 'axios'

export default {
  namespaced: true,
  state () {
    return {
      // 购物车数据
      list: []
    }
  },
  mutations: {
    // 1. 设置方法获取最新的list
    updateList (state, newList) {
      state.list = newList
    },
    // 更新数量的方法 (对象 {id: xx , newCount: xx})
    updateCount (state, obj) {
      // 找到对应的项find
      const goods = state.list.find(item => item.id === obj.id)
      // 更新它的count
      goods.count = obj.newCount
    }
  },
  actions: {
    // 2.异步获取数据
    async getList (context) {
      const res = await axios.get('http://localhost:3000/cart')
      // 4.调用mutations方法存到list数组
      // console.log(res)
      context.commit('updateList', res.data)
    },

    // 提供一个函数向后台提交修改数据
    async updateCountAsync (context, obj) {
      // 1.后台更新
      await axios.patch(`http://localhost:3000/cart/${obj.id}`, {
        // 将对应id的count更新
        count: obj.newCount
      })
      // 2.前端更新(mutations函数)
      context.commit('updateCount', {
        id: obj.id,
        newCount: obj.newCount
      })
    }
  },
  getters: {
    // 依赖于state 相当于计算属性
    total (state) {
      // 必须返回
      return state.list.reduce((sum, item) => sum + item.count, 0)
    },
    totalPrice (state) {
      return state.list.reduce((sum, item) => sum + item.count * item.price, 0)
    }
  }
}
```

app

```vue
<template>
  <div class="app-container">
    <!-- Header 区域 -->
    <cart-header></cart-header>

    <!-- 商品 Item 项组件 -->    <!-- item也要传过去 -->
    <cart-item v-for="item in list" :key="item.id" :item="item"></cart-item>

    <!-- Foote 区域 -->
    <cart-footer>123</cart-footer>
  </div>
</template>

<script>
import CartHeader from '@/components/cart-header.vue'
import CartFooter from '@/components/cart-footer.vue'
import CartItem from '@/components/cart-item.vue'
import { mapState } from 'vuex'

export default {
  name: 'App',
  created () {
    // 3.页面调用actions获取数据
    this.$store.dispatch('cart/getList')
  },
  computed: {
    // 5.利用辅助函数映射到computed
    ...mapState('cart', ['list'])
  },
  components: {
    CartHeader,
    CartFooter,
    CartItem
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding: 50px 0;
  font-size: 14px;
}
</style>
```

cart-item

```vue
<template>
  <div class="goods-container">
    <!-- 左侧图片区域 -->
    <div class="left">
      <img :src="item.thumb" class="avatar" alt="">
    </div>
    <!-- 右侧商品区域 -->
    <div class="right">
      <!-- 标题 -->
      <div class="title">{{ item.name }}</div>
      <div class="info">
        <!-- 单价 -->
        <span class="price">￥{{ item.price }}</span>
        <div class="btns">
          <!-- 按钮区域 -->
          <button class="btn btn-light" @click="btnClick(-1)">-</button>
          <span class="count">{{ item.count }}</span>
          <button class="btn btn-light"  @click="btnClick(1)">+</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CartItem',
  methods: {
    btnClick (step) {
      const newCount = this.item.count + step
      const id = this.item.id
      if (newCount < 1) return
      // 调用更新的异步方法
      this.$store.dispatch('cart/updateCountAsync', {
        id, newCount
      })
    }
  },
  props: {
    item: {
      type: Object,
      require: true
    }
  }
}
</script>

<style lang="less" scoped>
.goods-container {
  display: flex;
  padding: 10px;
  + .goods-container {
    border-top: 1px solid #f8f8f8;
  }
  .left {
    .avatar {
      width: 100px;
      height: 100px;
    }
    margin-right: 10px;
  }
  .right {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .title {
      font-weight: bold;
    }
    .info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      .price {
        color: red;
        font-weight: bold;
      }
      .btns {
        .count {
          display: inline-block;
          width: 30px;
          text-align: center;
        }
      }
    }
  }
}

.custom-control-label::before,
.custom-control-label::after {
  top: 3.6rem;
}
</style>
```



footer

```vue
<template>
  <div class="footer-container">
    <!-- 中间的合计 -->
    <div>
      <span>共 {{ total }}件商品，合计：</span>
      <span class="price">￥{{ totalPrice }}</span>
    </div>
    <!-- 右侧结算按钮 -->
    <button class="btn btn-success btn-settle">结算</button>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'CartFooter',
  computed: {
    ...mapGetters('cart', ['total', 'totalPrice'])
  }
}
</script>

<style lang="less" scoped>
.footer-container {
  background-color: white;
  height: 50px;
  border-top: 1px solid #f8f8f8;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 0 10px;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  z-index: 999;
}

.price {
  color: red;
  font-size: 13px;
  font-weight: bold;
  margin-right: 10px;
}

.btn-settle {
  height: 30px;
  min-width: 80px;
  margin-right: 20px;
  border-radius: 20px;
  background: #42b983;
  border: none;
  color: white;
}
</style>

```



#### 6.黑马购物车项目

##### 1.vant-ui

`vant2支持vue2  vant3和vant4支持vue3`

##### 2.组件库

![image-20230914161720819](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914161720819.png)



##### 3.组件库的基本使用步骤

最好使用按需导入(移动端最在意的是性能)

1. 全部导入

![image-20230914162155941](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914162155941.png)

2. 按需导入

![image-20230914164316158](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914164316158.png)

![image-20230914162808252](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914162808252.png)

`把vant按需导入的代码抽离成js文件,在main文件导入，这样好维护`



##### 4.移动端vw适配(适合vant使用)

**100vw是整个屏幕的宽**

![image-20230914165145987](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914165145987.png)

配置文件 适配1.1.1版本 不同版本配置看vant官网

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-px-to-viewport': {
      // vw适配的标准屏幕宽度
      // 设计图750调成1倍 => 适配375px
      // 设计图640调成1倍 => 适配320px
      // 可以使用蓝狐工具进行调倍数
      viewportWidth: 375,
    },
  },
};
```

设置盒子为300px后,浏览器生效样式80vw   自动计算    计算公式: `300 / 375 * 100vw`

`https://fotoflexer.com/editor/  在线修改比例及修图`



##### 5.路由配置

![image-20230914191712548](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914191712548.png)

![image-20230914191638761](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914191638761.png)



底部导航

![image-20230914194417043](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914194417043.png)



2级路由(在layout提供2级路由出口)

![image-20230914200549274](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914200549274.png)



开启vant按钮的路由模式(相当于变成了router-link)

![image-20230914200139892](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230914200139892.png)



##### 6.登录页

1.静态布局

![image-20230916143659080](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230916143659080.png)

头部组件直接用的vant组件库  导航的颜色样式提取到了公共的样式表中



2.封装request模块

![image-20230916144027013](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230916144027013.png)

**接口文档：[10. 获取图形验证码 - 智慧商城-实战项目 (apifox.com)](https://apifox.com/apidoc/shared-12ab6b18-adc2-444c-ad11-0e60f5693f66/api-70224089)**

编写接口文档: `用swagger自动生成，然后导入ApiFox生成文档`



3.图形验证码渲染

![image-20230916151329232](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230916151329232.png)



##### 7.api接口模块

![image-20230916152504414](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230916152504414.png)

**因为请求总是重复的，而且也不是页面逻辑，所以建议都分离出去**



##### 8.vant toast提示框

![image-20230917122147374](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917122147374.png)

原型挂载以后，vue和他创建的实例都可以访问到  组件就是vue创建出来的一个个实例



##### 9.登录页短信验证码

![image-20230917135428650](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917135428650.png)



##### 10.登录页登录功能

![image-20230917140938627](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917140938627.png)



##### 11.响应拦截器(所有错误统一处理)

![image-20230917203440730](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917203440730.png)



##### 12.登录权证存储(token和userid)

![image-20230917211129348](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917211129348.png)



##### 13.storage存储模块

![image-20230917211530417](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230917211530417.png)



##### 14.请求loading效果

![image-20230918204723299](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918204723299.png)

![image-20230918205858500](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918205858500.png)

![image-20230918205909798](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918205909798.png)



##### 15.页面访问拦截

![image-20230918210010594](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918210010594.png)

利用全局前置守卫



##### 16.home页面 首页

![image-20230918221605389](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230918221605389.png)



##### 17.搜索页面历史记录

![image-20230920201444734](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230920201444734.png)

一般不用往数据库存，如果要考虑多端同步才需要存数据库(一般是浏览器记录、视频音频才需要)



##### 18.搜索列表页

![image-20230920221126335](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230920221126335.png)



##### 19.商品详情

![image-20230921200037792](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921200037792.png)



##### 20加入购物车 立即购买弹窗

![image-20230921205204275](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921205204275.png)



##### 21.数字框组件

![image-20230921205315899](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921205315899.png)



##### 22.加入购物车

![image-20230921214628767](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921214628767.png)

![image-20230921214643838](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921214643838.png)



##### 23.购物车页面模块

![image-20230924104251400](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230924104251400.png)



##### 24.订单结算页面

![image-20230924195158794](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230924195158794.png)



##### 25.确认订单信息--购物车结算

![image-20230924213941689](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230924213941689.png)



##### 26.立即购买结算

![image-20231006174551950](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006174551950.png)



混入mixins

```js
// 混入的原理就相当于展开运算符  (obj1,...obj2) 把obj2展开塞到obj1中
// 混入的使用场景为 提取页面的公共业务逻辑(多组件跨组件使用) 比如弹出登录提示
export default {
  // 此处编写的就是 Vue组件实例的 配置项，通过一定语法，可以直接混入到组件内部
  // data methods computed 生命周期函数 ...
  // 注意点：
  // 1. 如果此处 和 组件内，提供了同名的 data 或 methods， 则组件内优先级更高
  // 2. 如果编写了生命周期函数，则mixins中的生命周期函数 和 页面的生命周期函数，会用数组管理，统一执行
  // created () {
  //   // console.log('嘎嘎')
  // },
  // data () {
  //   return {
  //     title: '标题'
  //   }
  // },
  methods: {
    // 该方法根据登录状态，判断是否需要显示登录确认框
    // 如果是未登录 返回true
    // 如果已经登录 放回false
    loginConfirm () {
      // 判断token是否存在
      // 1.token存在  继续操作
      // 2.token不存在  弹出确认框
      if (!this.$store.getters.token) {
        // 利用vant的弹出框
        this.$dialog.confirm({
          title: '温馨提示',
          message: '请先登录才能继续操作哦',
          confirmButtonText: '去登录',
          cancelButtonText: '在逛逛'
          // then表示确认
          // 如果希望跳转到登录以后能回跳回当前页面(这样用户体验好)
          // 需要在跳转前携带当前的路径地址
          // fullPath存在this.$route  他会携带查询参数 整个路径的内容
        }).then(() => {
          // 路由跳转 $router对象 要用replace 不留历史记录 这样以后回退是去商品列表页
          this.$router.replace({
            path: '/login', // 跳转到登录页
            query: {
              backUrl: this.$route.fullPath
            }
          })
        }
        ).catch(() => {})
        // catch表示取消 什么也不干
        return true
      }
      return false
    }
  }
}

```



##### 27.支付订单

![image-20231006194006942](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006194006942.png)



##### 28.订单管理--个人中心

![image-20231006204938364](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006204938364.png)



跨模块访问

![1696594977039](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1696594977039.png)



##### 29.项目打包发布

![image-20231006205142427](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006205142427.png)



配置：如果不配置项目无法访问到对的路径

如果没有配置,这个项目必须放在服务器根目录下才可以进行访问，也不能本地双击打开，配置以后可以放在服务器的任意位置，因为使用的是相对路径

![image-20231006205736592](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006205736592.png)



打包优化 通过路由访问原则来分模块 按需加载进行优化

![image-20231006210331281](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231006210331281.png)

此时打包以后会生成更多的js和css 在我们访问到新路由时在按需加载
