#  Vue

```css
1.传统服务器要进行加载数据，渲染页面，并且将页面返回给前端
2.这样造成的问题是:前后端不分离(耦合)，服务器压力大，开发成本高(不同运行环境要开发不一样的服务器)
3.我们希望一个服务器可以为大多数客户端服务，于是就产生了Rest风格的服务器(只返回JSON数据)
4.以前我们用AJAX拿到数据以后，用dom创建对象等方式将数据加载到页面中
5.后面产生了MVC的处理方式，以及MVC的变形MVVM
```

```CSS
原生开发的代码被称为命令式，我们输入一个个命令。Vue采用的是声明式的，直接编写想要显示的代码样式，Vue会自己将代码转换为一行行实现效果的代码。
对这行代码:要在网页里插入一个<h1>1234</h1>
	命令式:1.获取body对象  2.创建一个h1对象 3.设置innerHtml 4.将h1插入到body中
	声明式:<h1>1234</h1>
Vue是组件化的编程模型(组件可大可小，增强复用性。)
Vue是渐进式的js框架，适合大小项目，也可以嵌套在用了其它框架的项目中。(项目升级想要用Vue的一些特性，可以局部替换。)
```

![uTools_1680429283424](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680429283424.png)

## 1.Vue简介

-   vue 是一个前端的框架，主要负责帮助我们构建用户的界面
-   MVVM：Model - View - View Model
-   vue 负责 vm 的工作（视图模型,将视图和模型连接），通过 vue 可以将视图和模型相关联。
    -   当模型发生变化时，视图会自动更新
    -   也可以通过视图去操作模型
-   vue 思想：
    -   组件化开发
    -   声明式的编程

### 1.HelloWorld

1. 直接在网页中使用（像 jQuery 一样）

   - `        <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>`

3. 代码：

   ```javascript
   // 组件，就是一个普通js对象
   const App = {}
   
   // 创建应用
   const app = createApp(App)
   
   // 挂载到页面
   app.mount("#root")
   ```

4. 实例

   ```vue
    <div id="app"></div>
   
       <script>
           //Vue 一切皆是组件
           //创建一个根组件(在vue3中一切组件都一样，根组件代表的是最外层的，相当于html标签)
           //组件就是一个普通的js对象，创建一个组件以后Vue会自己生成一个组件实例
           //组件是组件实例的模板
           //组件 ---> 组件创建组件实例 ---> 虚拟DOM(Vue用来提升性能的) ---> DOM
           //为什么不直接拿组件来用？  为了复用！在哪里用就在拿生成一个实例。
   
           const Root = {//Root创建出来的组件实例就属于VM视图模型
               data(){
                   return{
                       message:"Vue好棒!"//data方法返回的对象，其中的属性会自动添加到组件实例中
                   }
               },//data是一个函数，需要一个对象作为返回值
   
               //在模板中可以直接访问组件实例中的属性
               //在模板中可以通过{{属性名}}，来访问带组件实例中的属性
               template: "<h1>Hello Vue,{{message}}</h1>"  //希望组件在页面中呈现的样子
           }
   
           //创建app实例(应用实例，要传入一个根组件作为参数)
           // const app = Vue.createApp(Root)
   
           //将实例在页面中挂载
           // app.mount("#app")
   
           //简洁写法
           Vue.createApp(Root).mount("#app")
       </script>
   ```

6. 按钮练习

   ```vue
       <div id="app"></div>
   
       <script>
   
           const Root = {
               data() {
                   return {
                       count: 0
                       //data中的数据模型会自动和使用它的视图绑定，数据变化视图会自动刷新
                   }
               },
               //修改count就是修改了模型，以前我们需要操作dom，判断点击以后在+1
               template: "<button @click='count++'>点击</button>  -- 点了{{count}}次"  //希望组件在页面中呈现的样子
           }
   
           Vue.createApp(Root).mount("#app")
       </script>
   ```

   5.模板template
   
   ```html
    <div id="app">
           <!-- <button @click='count++'>点击</button> -- 点了{{count}}次 -->
           <!-- 如果直接将模板定义到网页种，此时模板必须符合html的规范 -->
           <!-- 比如html不区分大小写，会自动把大写的标签名转为小写，这样我们使用自定义的大写组件就使用不了 -->
           <!-- 开发中运用的场景很少，一般是其它项目想引入Vue，渐进式的作用 -->
   
           <p>xxxxx</p>
           <!-- 如果在组件中定义了template，则会优先使用其作为模板，同时根元素中的所有内容都会被替换 -->
           <!-- 如果在组件中没有定义template，则会使用根元素的innerHTML -->
       </div>
   
       <script>
   
           const Root = {
               data() {
                   return {
                       count: 0
                       //data中的数据模型会自动和使用它的视图绑定，数据变化视图会自动刷新
                   }
               },
               //template时模板，它决定了组件最终的样子
               /*
                   定义模板的方式有3种
                       1.在组件中通过template属性去指定
                       2.直接在网页的根元素指定
                       3.组件中通过render()直接渲染[回到了命令式编程，特殊情况会用，类似react]
               */
   
               //修改count就是修改了模型，以前我们需要操作dom，判断点击以后在+1
               template: "<button @click='count++'>点击</button>  -- 点了{{count}}次"  //希望组件在页面中呈现的样子
           }
   
           Vue.createApp(Root).mount("#app")
       </script>
   ```
   
   

### 2.使用vite管理(手动管理)

```bash
1.初始化项目  yarn init -y
2.安装vite yarn add -D vite
3.安装Vue yarn add vue(项目依赖不要加-D)
4.创建index.html模板，创建index.js模板
5.配置package.json(vite --open  可以自动打开)
6.运行 yarn dev
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hello vue</title>
    <script type="module" src="./src/index.js"></script>
</head>

<body>
    <div id="app"></div>

</body>

</html>
```

```js
// 引入vue
// import {createApp} from "vue" //引入创建实例的函数
//这样引入的vue，默认不支持通过template属性来设置模板(版本低性能差)
import {createApp} from "vue/dist/vue.esm-bundler.js"

// 创建一个根组件
const App = {
    data(){
        return{
            message:"123"
        }
    },
    template:"<h1>{{message}}</h1>"
}

//创建应用挂载到页面
const vm = createApp(App).mount("#app")
//mount()的返回值是根组件的实例
```

```json
 package.json

"scripts": {
    "dev":"vite --open",
    "build":"vite build",
    "preview":"vite preview"
  }
```



### 3.分模块和Vue组件化

**实例用大写开头，index.js是主入口文件**

index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hello vue</title>
    <script type="module" src="./src/index.js"></script>
</head>

<body>
    <div id="root">
        <h1>{{msg}}</h1>
        <!--解析的顺序是浏览器解析然后才是VUE解析，所以在浏览器直接使用模板要遵循html规范(不区分大小写的html)-->
        <!--所以放在浏览器直接用的要用小写  这种方式并不好-->
        <my-button></my-button>
    </div>

</body>

</html>
```

index.js

```js
import {createApp} from "vue/dist/vue.esm-bundler.js"
import App from "./App.js"


//创建应用挂载到页面
const vm = createApp(App).mount("#root")
```

App.js

```js
//引入组件
import MyButton from "./components/MyButton.js"

export default{
    data(){
        return{
          msg:"这是一个Vue网页"
        }
    },

    //在组件中注册子组件(在哪里用就在哪里注册)
    components:{
        // MyButton:MyButton(注册组件的名字:引入的组件)
        //2个一样可以简写
        MyButton,
        // MB:MyButton

        //如果希望组件能用到网页中(template要注销，因为会优先使用组件这个模板)
        "my-button":MyButton
    },

    //创建了3个组件实例
    template:`
    <h1>{{msg}}</h1>
    <MyButton></MyButton>
    <MyButton></MyButton>
    <MyButton></MyButton>
    <MyButton></MyButton>
    `
}
```

MyButton.js(子组件通常放在src下的components文件夹下)

```js
//封装一个自定义的按钮组件
export default{
    data(){
        return{
            count:0
        }
    },
    template:`
    <div>
    <h2>子组件</h2>
    <button @click="count++">点击</button>  <Span>{{count}}</span>  
    </div>

    `
}
```



### 4.单文件组件(解决模板用字符串写的问题)

index.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hello vue</title>
    <script type="module" src="./src/index.js"></script>
</head>

<body>
    <div id="root">
    </div>
</body>

</html>
```

index.js

```js
import {createApp} from "vue"
import App from "./App.vue"
//创建应用挂载到页面
const vm = createApp(App).mount("#root")
```

**引入Vue文件来解决这个问题，使用Vue文件需要安装插件** `yarn add -D @vitejs/plugin-vue` 执行 `yarn dev`

配置vite.config.js

```js
import vue from "@vitejs/plugin-vue"
export default{
    plugins:[vue()]
}
```

App.vue

```vue
<script>
    //引入MyButton.vue
    import MyButton from './components/MyButton.vue';

    // 编写单组件(主要为了模板好写)的代码
    export default{
        data(){
            return{
            msg:"这是一个Vue网页"
            }
        },
        //引入MyButton组件
        components:{
            MyButton
        }
    }
</script>

<!-- 单文件组件在打包的时候就已经编译成一个函数了，性能比那种写在App.js的好 -->
<template>
    <div>
        <h1>{{msg}}</h1>
        <!--使用MyButton组件-->
        <!--打包工具会预先转为函数，所以可以用大写 不用考虑浏览器-->
        <MyButton></MyButton>
    </div>
</template>

<!-- 
解决template报错问题:
//正确写法
<template>
    <div>
        <h2>我是h2</h2>
        <h2>我是h2</h2>
        <h2>我是helloWorld</h2>
    </div>
</template>
//错误写法,会报错。
<template>
    <h2>我是h2</h2>
    <h2>我是h2</h2>
    <h2>我是helloWorld</h2>
</template>

报错原因:根模板必须有一个准确的元素。
    -在vue组件中会使用template标签，在template中，
    还需要一个标签元素将其他标签元素包裹起来，
    因为template标签是不会被DOM解析，
    生成DOM元素的时候会被隐藏，
    而组件又必须只能有一个根节点。
 -->
```

MyButton.vue

```vue
<script>
    export default{
        data(){
            return{
                count:0
            }
        }
    }
</script>

<template>
    <div>
        <button @click="count++">点击</button>&nbsp;&nbsp;&nbsp;<span>{{count}}</span>
    </div>
</template>
```





### 4.使用vite(自动构建)

cd .. 返回上一级

![uTools_1680503241959](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680503241959.png)

```bash
1.yarn create vue 创建项目
2.进入项目文件夹
3.yarn 安装依赖
4.yarn dev 运行项目
5.删除一些没用的东西

补充: yarn create vue at 2  创建vue2项目
```

### 5.代码理解

main.js主文件

```js
import { createApp } from 'vue'
import App from './App.vue'
/* 
    App.vue是根组件
        - createApp(App) 将根组件关联到应用上
            - 一个应用只能只能挂载一个应用实例(App),有且只有一个，相当于是整个项目的根
            - 其它组件在哪里用就在哪里引用
            - 会返回一个应用的实例

        - app.mount("#app") 将应用挂载到页面中
            - 挂载以后原来的id为add的标签中的内容会被清除
            - 会返回一个根组件的实例，组件的实例通常可以命名为vm(viewmodel)
            - 组件实例是一个Proxy对象（代理对象）
            - 2种访问方式
                1.main.js
                    const app = createApp(App)
                    const vm = app.mount('#app')
                2.在App.vue的组件对象中的data中的this    
*/

const app = createApp(App)
const vm = app.mount('#app')
console.log(app);//应用实例
console.log(vm);//组件实例


// 可以创建多个应用实例，运用场景:在一个网页中局部地方使用Vue，正常项目不会这样用
// const app = createApp(App)
// const app2 = createApp(App)

// vue默认使用的js自带的es模块化标准，在es模块下，一个js是一个单独的执行环境，所以无法直接通过命令行访问
// 将vm，app设为全局变量,就可以在命令行模式下直接俄访问vm组件实例并且对其进行修改(证明响应式数据)
window.vm = vm
window.app = app
```

App.vue

```vue
<script>
  //组件，一个组件可以创建多个组件实例，相当于组件的模板
  //组件就是一个普通的js对象
  export default{
    //data是一个函数(组件的方法)
    //如果使用箭头函数，则无法通过this来访问组件实例
    //在data中，this就是当前的组件实例vm
    data(){
      // console.log(this);
      //直接向组件实例中添加的属性不会被vue所代理，不是响应数据，修改后页面不会同步变化
      this.name = "孙悟空"

      //data会返回一个对象作为返回值，vue会对该对象进行代理
      //从而将其转换为响应式数据，响应式数据可以直接通过组件实例访问 vm.msg
      //这样我们修改数据就可以直接在网页中显示，不用操作dom对象进行赋值操作
      return{
        msg:"我爱Vue"
      }
    }
  }
  
  // //解决方法：将vm作为函数的第一个参数传进来
  // 但是这种方式不好，使用vue时减少使用箭头函数
  // data:vm=>{
  //   console.log(vm);
  // }
</script>

<template>
  <div>
    <!-- h2直接修改是无法同时修改页面的，只有修改了vm实例才会重新显示 -->
    <h1>{{msg}}</h1>
    <h2>{{name}}</h2>
  </div>
</template>
```

**vue在底层执行例如data这些函数时会为其绑定this(实例对象)，而箭头函数天生没有this**

**因为js的函数的this不固定，所以vue就在底层先绑定好**

![uTools_1680772127570](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680772127570.png)

**解决：不过不建议这样子搞**

![uTools_1680772160241](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680772160241.png)



### 6.代理对象(Proxy对象)原理

```js
//组件实例就是一个代理对象(组件就是被代理的对象)
/* 
    如果直接修改对象的属性，那么就是仅仅修改了属性，没有办法去做其他的事情，
    这种操作只会影响对象自身，不会导致元素的重新的渲染
    
    希望在修改一个属性的同时，可以进行一些其他的操作，比如触发元素重新渲染！

    要实现这个目的，必须要对对象进行改造，vue3中使用的是的代理模式来完成对象的改造

    设置代理时不会对原对象产生影响！(创建时不会影响被代理对象，修改才会改变它)
*/
// 只能修改，没法进行其它操作
// obj.name = "猪八戒"

// 创建一个对象
const obj = {
    name: "孙悟空",
    age: 18
}

// 来为对象创建一个代理
const handler = {
    // get用来指定读取数据时的行为，它的返回值就是最终读取到的值
    // 指定get后，在通过代理读取对象属性时，就会调用get方法来获取值
    get(target, prop, receiver) {

        // 返回值之前做一些其他的操作...
        // 在vue中，data()返回的对象会被vue所代理
        // vue代理后，当我们通过代理去读取属性时，返回值之前，它会先做一个跟踪的操作
        // 当我们通过代理去修改属性时，修改后，会通知之前所有用到该值的位置进行更新

        // track() 追踪谁用了我这个属性
        /* 
            三个参数：
                target 被代理的对象
                prop 读取的属性
                receiver 代理对象
        */
        return target[prop]
    },

    // set会在通过代理修改对象时调用
    set(target, prop, value, receiver){
        // value是我们传入修改属性的值
        // console.log(target, prop, value, receiver);
        target[prop] = value

        // trigger() 触发所有的使用该值的位置进行更新
        // 值修改之后做一些其他的操作
    }
} // handler 用来指定代理的行为

// 创建代理 代理类(被代理的对象,代理对象)
const proxy = new Proxy(obj, handler)

// 修改代理的属性
proxy.age = 28 //就是value

console.log(proxy.age)
```



### 7.代理对象补充

App.vue

```vue
<!-- 总结 没有通过代理去修改对象时是不会有刷新的效果的，没调set -->
<!-- 直接改原对象obj是没有用的，要调用代理去改 -->

<script>
 const obj = {
     msg:"哈哈，我是obj"
 }
window.obj = obj

export default {


    data() {
        // 直接向组件实例中添加的属性不会被vue所代理，不是响应数据，修改后页面不会发生变化
        // this.name = "孙悟空"
        // 可以通过created(){this.$data.name = "孙悟空"}来使其变为响应对象

        // vm.$data 是实际的代理对象，通过vm可以直接访问到$data中的属性
        // vm.$data.msg 等价于 vm.msg
        

        // data会返回一个对象作为返回值，vue会对该对象进行代理
        //  从而将其转换为响应式数据，响应式数据可以直接通过组件实例访问
        //return {
           // msg: "我爱Vue"
       // }  这种方式函数的返回值，每一次都返回一个新的对象

        return obj //这种定义方式每次返回的都是obj对象(演示代理对象时的用法，开发不可以)
    },

    created(){
        // 会在组件创建完毕后调用
        // 可以通过vm.$data动态的向组件中添加响应式数据，但是不建议这么做(数据结构混乱)
        this.$data.name = "孙悟空"
    }
}
</script>

<template>
    <h1>{{ msg }}</h1>
    <h2>{{ name }}</h2>
</template>

```

**面试：vue2(defineProperty)和vue3的区别，代理问题的不同(用的代理对象不同)**

**proxy不兼容IE，因为ie不支持proxy**



### 8.data详情

**将data设置成函数的意义在于，每次可以返回一个新对象，这样使得每个组件实例都是独立的。如果直接返回对象，那所有代理代理的都是同一个对象，修改一个按钮等于修改了全部按钮。**

![uTools_1680769824681](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680769824681.png)

**vue的响应式数据不是仅仅针对根对象的，而是把对象中的属性也设置成响应式的属性**

![uTools_1680770809145](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680770809145.png)

**某些场景下我们不需要深层响应式对象，可以使用浅层响应式对象(只把根对象设置成响应式对象)**

1. ![uTools_1680770967952](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680770967952.png)
2. ![uTools_1680770912873](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680770912873.png)

**关于 this.$data.xxx = ""造成数据结构混乱的解决方法(提前占位，然后可以直接通过组件实例去修改。)**

![uTools_1680771192870](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680771192870.png)



### 9.methods

**vue中的组件其实相当于一个构建类，data用来设置类的属性，methods用来设置类的方法**

```vue
<script>
import MyButton from "./components/MyButton.vue"
import { shallowReactive } from "vue"

export default {
    // data用来指定实例对象中的响应式属性
    data() {
        return {
            msg: "今天天气真不错！"
        }
    },

    /* 
        methods 用来指定实例对象中的方法 
            - 它是一个对象，可以在它里边定义多个方法
            - 这些方法最终将会被挂载到组件实例上
            - 可以直接通过组件实例来调用这些方法    
            - 所有组件实例上的属性都可以在模板中直接访问
            - methods中函数的this会被自动绑定为组件实例(在vue中尽量不要同箭头函数)
    */
    methods: {
        sum(a, b){
            // console.log(this) // 组件实例 vm
            return a + b
        },
        changeMsg(){
            this.msg = "新的消息！"//调用方法后更改msg的值
        }
    }
}
</script>
<template>
    <h1>{{ msg }}</h1>
    <h2>{{ sum(2, 5) }}</h2>
    <button @click="changeMsg">点我一下</button>
</template>
```

**使用了箭头函数 获取不到组件实例**

![uTools_1680771864701](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680771864701.png)





### 10.计算属性

**有返回值的语句就是表达式，例如三元运算符，if语句没有返回值，不是表达式**

**{{表达式}}   模板中可以嵌套表达式，但是不能嵌套if语句**

```vue
<script>

export default {
    // data用来指定实例对象中的响应式属性
    data() {
        return {
            msg: "今天天气真不错",
            stu: {
                name: "孙悟空",
                age: 18,
                gender: "男"
            },
            firstName: "悟空",
            lastName: "孙",
            // 数组也是响应式数据
            arr: ["孙悟空", "猪八戒", "沙和尚"]
        }
    },

    methods: {
        updateAge() {
            if (this.stu.age === 18) {
                this.stu.age = 17
            } else {
                this.stu.age = 18
            }
        },
        //methods中的方法,每次组件重新渲染都会调用
        getInfo(){
          return this.stu.age>=18?"你是一个成年人":"你是一个未成年人"
        }
    },

    /* 
        computed 用来指定计算属性
        {
            属性名:getter
        }
        - 计算属性，只在其依赖的数据发生变化时才会重新执行(不会直接重新渲染)
        - 会对数据进行缓存，性能更好，不会在没用的时候执行
    */
   //比data的好处是可以返回一个函数(可以进行判断)
    computed: {
      // info:function(){}
      info(){
        //在计算属性的getter中，尽量只做读取相关的逻辑
        //不要执行那些会产生作用的代码(重新渲染性能不好)
        console.log("函数被调用了!");
        return this.stu.age>=18?"你是一个成年人":"你是一个未成年人"
      },
      //当只有getter时计算属性可以简写
      // name(){
      //   return this.lastName + this.firstName
      // }
      // 可以为计算属性设置setter，使得计算属性科协，但是不建议这样去做
      nameTest:{
        get(){
          return this.lastName + this.firstName
        },
        //没有setter时计算属性是只读的
        set(value){//value来指定参数(vm.name)
          this.lastName = value[0]
          this.firstName = value.slice(1)
        }
      }
    }
}
</script>
<template>
  <div>
    <p>{{ msg }}</p>
    <h1>{{ stu.name }} -- {{ stu.age }} -- {{ stu.gender }}</h1>
    <!-- <h2>{{stu.age>=18?"你是一个成年人":"你是一个未成年人"}}</h2> -->
    <!-- 调用不用加() -->
    <h2>评语：{{ info }}</h2> 
    <!-- 调用要加() -->
    <h2>methods:{{getInfo()}}</h2>
    <button @click="updateAge">减龄</button>
    <hr>
    <p>{{msg}}</p>
    <hr>
    <h2>{{nameTest}}</h2>
    <hr>
    <!-- 修改vm.arr[0].xxx="" -->
    <h2>{{arr[0]---arr[1]---arr[2]}}</h2>
  </div>
   
</template>
```

### 11.安装Vue的调试工具

goole应用商店

## 2.Vue3.0

### 1.组合式API

#### 1.原始方法

**过去Vue2.0使用的是选项式API，需要什么功能就进行什么功能的配置，比较麻烦。**

```vue
<!-- 组合式开发() -->
<script>
    //导入Reactive可以创建响应式变量 
    import { reactive } from "vue"
    export default{
        /*
            传统写法会有俩个问题
                1.在对象里写东西，只能写对象里可以写的，例如const a就不能写，有限制
                2.对象本身没有作用域，是它外部的作用域
        */
       /*
            setup钩子函数解决了这俩个问题
               -setup函数可以向设置要向外界暴露的内容，设置以后会直接挂载在vue上 
               -在setup()中可以通过返回值来指定哪些内容要暴露给外界，暴露后可以直接在模板中使用
       */
       setup(){
            //定义变量
            //在组合式api中直接声明的变量等，就是一个普通变量，不是响应式属性
            //修改这些属性不会在视图中产生效果
            let msg = "今天天气真不错" 
            let count =10


            //通过Reactive()来创建一个响应式的对象
            const stu = reactive({
                //这样就可以同步显示
                a:0,
                name:"孙悟空",
                age:18
            })

            //需要暴露的函数(避免了以前需要this)
            //可以直接修改，因为stu此时不是对象的属性，而是一个局部变量
            function changeAge(){
                // this.stu.age = 28
                stu.age = 28
            }

            //暴露给外部的值
            return {
                msg,
                count,
                stu,
                changeAge //暴露函数
            }
       }
            
    }
</script>

<template>
    <h1>{{msg}}</h1>
    <button @click="count++">点击</button>
    <!-- 无法同步显示 -->
    <h2>{{count}}</h2>
    <hr>
    <h3>{{stu.a}}</h3>
</template>
```

#### 2.快速写法

```vue
<script setup>
import { reactive } from "vue"

const msg = "我爱Vue"
const count = 0 //还是无法直接修改的
//放在reactive里可以同步修改
const stu = reactive({
    name: "孙悟空"
})

function fn() {
    alert("哈哈哈，好快乐！")
}
</script>
<template>
    <h1 @click="fn">组合式的API</h1>
    <h2>{{ msg }} -- {{ count }}</h2>
    <h3>{{ stu.name }}</h3>
</template>
```





## 网页的渲染

-   浏览器在渲染页面时，做了那些事：

    1. 加载页面的 html 和 css（源码）
    2. html 转换为 DOM，css 转换为 CSSOM
    3. 将 DOM 和 CSSOM 构建成一课渲染树
    4. 对渲染树进行 reflow（回流、重排）（计算元素的位置）
    5. 对网页进行绘制 repaint（重绘）
-   渲染树（Render Tree）

    -   从根元素开始检查那些元素可见，以及他们的样式
    -   忽略那些不可见的元素（display:none）
-   重排、回流

    -   计算渲染树中元素的大小和位置
    -   当页面中的元素的大小或位置发生变化时，便会触发页面的重排（回流）
    -   width、height、margin、font-size ......
    -   注意：每次修改这类样式都会触发一次重排！所以如果分词修改多个样式会触发重排多次，而重排是非常耗费系统资源的操作（昂贵），重排次数过多后，会导致网页的显示性能变差，在开发时我们应该尽量的减少重排的次数
    -   在现代的前端框架中，这些东西都已经被框架优化过了！所以使用 vue、react 这些框架这些框架开发时，几乎不需要考虑这些问题，唯独需要注意的时，尽量减少在框架中直接操作 DOM
-   重绘

    -   绘制页面
    -   当页面发生变化时，浏览器就会对页面进行重新的绘制
-   例子

- ```html
  <!DOCTYPE html>
  <html lang="zh">
      <head>
          <meta charset="UTF-8" />
          <meta http-equiv="X-UA-Compatible" content="IE=edge" />
          <meta
              name="viewport"
              content="width=device-width, initial-scale=1.0"
          />
          <title>Document</title>
          <style>
              .box1 {
                  width: 200px;
                  height: 200px;
                  background-color: orange;
              }
  
              .box2 {
                  background-color: tomato;
              }
  
              .box3 {
                  width: 300px;
                  height: 400px;
                  font-size: 20px;
              }
          </style>
      </head>
      <body>
          <button id="btn">点我一下</button>
          <hr />
          <div id="box1" class="box1"></div>
          <script>
              btn.onclick = () => {
                  // box1.classList.add("box2")
                  // 可以通过修改class来间接的影响样式，来减少重排的次数
                  // box1.style.width = "300px"
                  // box1.style.height = "400px"
                  // box1.style.fontSize = "20px"
                  // box1.classList.add("box3")
                  // box1.style.display = "none"
                  // box1.style.width = "300px"
                  // box1.style.height = "400px"
                  // box1.style.fontSize = "20px"
                  // div.style.display = "block"
              }
          </script>
      </body>
  </html>
  ```

  

