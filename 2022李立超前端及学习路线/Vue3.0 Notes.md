#  Vue

![uTools_1680429283424](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680429283424.png)

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

**创建后:**

main.js

```js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

index.html

```html
<!DOCTYPE html>
<html lang="zh">

<head>
  <meta charset="UTF-8">
  <link rel="icon" href="/favicon.ico">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Vite App</title>
</head>

<body>
  <div id="app"></div>
  <script type="module" src="/src/main.js"></script>
</body>

</html>
```

App.vue

```vue
<script setup>

</script>

<template>
    <div class="app">
    </div>
</template>

<style scoped>

</style>
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

#### 2.setup快速写法

```vue
<script setup>  //加上setup表示纯使用组合式api
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



#### 3.reactive和shallowReactive和ref响应式变量原理

```vue
<script setup>
import { reactive, ref } from "vue"
import { $ref } from "vue/macros" //避免编辑器弹出警告
/* 
    reactive()
        - 返回一个对象的响应式代理
        - 返回的是一个深层响应式对象
        - 也可以使用shallowReactive()创建一个浅层响应式对象
        - 缺点：
            - 只能返回对象的响应式代理！不能处理原始值

    ref()
        - 接收一个任意值，并返回它的响应式代理
*/
const stu = reactive({
    name: "孙悟空"
})

// ref在生成响应式代理时，它是将值(原始值和对象都会)包装成一个对象 0(0无法直接创建代理)  --> {value:0}
// 访问ref对象时，必须通过 对象.value 来访问其中的值
// 在模板中，ref对象会被自动解包
let count = $ref(0) // 生成一个0的响应式代理

// count = 10 // 改变量只会影响到变量自己，在js中，无法实现对一个变量的代理
console.log(count)

// vue给我们提供了一个语法糖，使得ref对象在script标签中也可以自动解包
// $是一个实验性的属性，需要在vite插件中做一些配置 reactivityTransform:true
function fn() {
    // count自增
    count.value++; //没有进行插件配置
    // count++ //进行了插件配置可以省略value 目前好像不支持了
}
</script>
<template>
    <h1>组合式的API</h1>
    <h2 @click="fn">{{ count }}</h2>
</template>
```

**实例**

```js
import { reactive, ref } from "vue"

const stu = reactive({ name: "孙悟空" })

const count = ref(0) // {value:0}

const person = ref({ name: "猪八戒", age: 18 }) // {value:{ name: "猪八戒", age: 18 }}

console.log(person.value.name)
```

**vite.config.js配置**

```js
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { reactive } from 'vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue(
    reactivityTransform:true
  )],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})
```



#### 4.ref对象补充

```vue
<script setup>
import { ref, reactive, computed } from "vue"

const msg = ref("Hello Vue")

// {value: obj} 整个obj对象是响应式的
// 访问obj.value.name
const obj = ref({
    name: "孙悟空",
    age: 18
})

// obj2的属性是响应式的
// 访问obj2.name.value
const obj2 = {
    name: ref("孙悟空"), // {value:"孙悟空"}
    age: ref(18) // // {value:18}
}


const { name, age } = obj2 //创建一个新对象 将obj2赋值给新对象，此时新对象为响应式对象(访问时直接 name age 就可以)

const changeMsgHandler = () => {
    // 修改ref对象时，必须通过value
    // 但是不需要this.msg了 这就是组合式api新的地方
    // msg.value = "哈哈"
    name.value = "你看我变不变"
}

// computed 用来生成计算属性
const newMsg = computed(() => {
    return msg.value + "-我爱Vue！"
})
</script>

<template>
    <!-- ref对象在模板中可以自动解包（要求ref对象必须是顶层对象） -->
    <h1>{{ msg }}</h1>
    <h1>{{ newMsg }}</h1>

    <!-- obj会自动解包 -->
    <h2>{{ obj.name }}</h2>
    <!-- name不是顶层响应式对象，所以不能自动解包 -->
    <!-- <h2>{{ obj2.name.value }}</h2> -->

    <h2>{{ name }}</h2>
    <hr />

    <h2>{{ obj.age + 1 }}</h2>
    <!-- <h2>{{ obj2.age.value + 1 }}</h2> -->

    <h2>{{ age + 1 }}</h2>

    <button @click="changeMsgHandler">点我一下</button>

</template>
```



#### 5.模板的语法(v-text、v-html)

```vue
<script setup>
const msg = "我爱vue"
const html = `<h2>我是一段html代码</h2>`

const fn = () => {
    console.log("哈哈哈")
}
</script>

<template>
    <!-- 
    - 在模板中，可以直接访问到组件中声明的变量
    - 除了组件中的变量外，vue也为我们提供了一些全局对象可以访问：
        比如：Date、Math、RegExp ...
        除此之外，也可以通过app对象来向vue中添加一些全局变量
        app.config.globalProperties
    - 使用插值(双大括号)，只能使用表达式
        表达式，就是有返回值的语句(比如if语句就写不了一点)
    - 插值实际上就是在修改元素的textContent，
        textContent的特点是：如果内容中含有标签，标签会被转义显示，不会作为标签生效(innerHtml就不会转义)

    指令：
      - 指令模板中为标签设置的一些特殊属性，它可以用来设置标签如何显示内容
      - 指令使用v-开头
        v-text 将表达式的值作为元素的textContent插入，作用同{{}}
          使用指令时，不需要通过{{}}来指定表达式
        v-html 将表达式的值作为元素的innerHTML插入，有xss攻击的风险


  -->
    <h1>{{ "hello" + "world" }}</h1>
    <!-- <h2>{{ if(1+1==2){console.log(123)} }}</h2> -->
    <h1>{{a>b?0:1}}</h1>
    <div>{{ html }}</div>
    <!-- 将html作为标签的textContent值插入 如同<div>{{ html }}</div> -->
    <div v-text="html"></div>
    <div v-html="html"></div>
</template>
```

**main.js**

```js
import { createApp } from "vue"
import App from "./App.vue"

const app = createApp(App)

// app.config.globalProperties.hello = "你好，我是全局的属性"
app.config.globalProperties.alert = alert.bind(window) //将alert的this绑定为window(在全局作用域中this代表window)

app.mount("#app")
```



#### 6.v-bind指令

```vue
<script setup>
import { ref } from "vue"

//public打包后会直接出现在项目根目录dist下  / 表示根目录
const imgPath = ref("/images/messi.png")

const changeImg = () => {
    imgPath.value = "/images/neymar.png"
}

const attrs = {
    id: "box1",
    class: "hello"
}

const attrName = "title"
const attrValue = "这是一个title属性"

const color = "red"

const isDisabled = ""
</script>

<template>
	<!-- 双大括号不能在 HTML attributes 中使用。想要响应式地绑定一个 attribute(属性)，应该使用 v-bind 指令 -->
    <!-- 
      当我们需要为标签动态的设置属性时，需要使用v-bind指令,
        v-bind可以简写为 :
      当我们为一个布尔值设置属性时，
        如果值为true，则元素上有该属性（转换后为true，也算true）
        如果值为false，则元素没有该属性（转换后为false，也算false）
        特殊情况："" 空串，在这里会被当成真值(面试考点)
  -->

    <!-- <button @click="changeImg">切换图片</button> -->
    <!-- <img :src="imgPath" alt="梅西" /> -->

    <!-- 可以直接传对象 -->
    <img :src="{}" alt="">

    <!-- 不仅属性值可以是动态的，属性也可以是动态的 -->
    <img :[attrName]="attrValue" :src="imgPath" alt="梅西" />

	<!-- 设置了id和class -->
    <div :="attrs"></div>

    <!-- 动态设置样式 -->
    <div :style="{}"></div>
    <div :style="color"></div>

	<!-- 绑定对象 isActive为真时设置active类 -->
	<div :class="{ active: isActive }"></div>

	<!-- 为按钮设置一个动态的类名 当current为0时设置active -->
    <div @click="current=0" class="tab-button" :class="{active:current === 0}">热门球队</div>
    <div @click="current=1" class="tab-button" :class="{active:current === 1}">热门球员</div>



    <input type="text" :disabled="isDisabled" />
</template>

<!-- 可以直接计算取5倍的hot -->
<template>
	<HotBar :hot="item.hot" :max-hot="item.hot*5"></HotBar>
</template>
```

![uTools_1681717002124](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681717002124.png)



**在组件上使用**

![uTools_1681716146206](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681716146206.png)

![uTools_1681716233317](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681716233317.png)



#### 7.样式

**设置了deep后**

![uTools_1681388000639](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681388000639.png)

##### 1.vue的scoped

```vue
<script setup>
//code安装了Vue Language Features (Volar)插件后 会自动引入注册
import MyBox from "./components/MyBox.vue"
</script>

<template>
    <div class="app">
        <h1>今天天气真不错！</h1>
        <div class="box1">App中的box1</div>
        <MyBox></MyBox>
    </div>
</template>

<!-- 
  可以直接通过style标签来编写样式，
    如果直接通过style标签写样式，此时编写的样式是全局样式
    会影响到所有的组件
-->

<!-- 全局样式 -->
<!-- <style>
h1 {
    background-color: #bfa;
}

.box1 {
    width: 200px;
    height: 200px;
    background-color: yellowgreen;
}
</style> -->

<!--  可以为style标签添加一个scoped属性，
   这样样式将成为局部样式，只对当前组件生效 
如何实现的？
   - 当我们在组件中使用scoped样式时，
     vue会自动为组件中的所有元素生成一个随机不重复的属性
     形如：data-v-7a7a37b1
     生成后，所有的选择器都会在最后添加一个 [data-v-7a7a37b1]
       h1 -> h1[data-v-7a7a37b1]
       .box1 -> .box1[data-v-7a7a37b1]
       样式选中时使用属性选择器，实现了只对当前组件生效

  - 注意：
      - 随机生成的属性，除了会添加到当前组件内的所有元素上，
        也会添加到当前组件引入的其他组件的根元素上，这样设计
        是为了，可以通过父组件来为子组件设置一些样式
        (如果MyBox1只有一个h1为根元素，这时候就会影响它的样式)
-->
<style scoped>
h1 {
    background-color: orange;
}
.box1 {
    width: 200px;
    height: 200px;
    background-color: #bfa;
}

/* 
正常情况下俩个组件是不要耦合的

特殊情况下:
    1.将组件中所有的 h2的字体颜色设置为黄色
    2.当前组件就是要修改引入组件的样式

    我们对h2进行设置后：
        选择器最终的效果：.app h2 --> .app h2[xxxxx]
        无法对其产生作用,因为[xxxxx]是随机的 此时需要用到deep

        .app h2[data-v-7a7a37b1] 没用deep生成的最终样式

        .app[data-v-7a7a37b1] h2 用了deep生成的最终样式
        这样变成只要是app里的h2，就会被影响
*/

/* 强行修改所有h2 */
.app :deep(h2) {
    color: yellow;
}


/* 
    所有h2变色
    :deep(h2){
    background-color: blue;
  } */

/* 
   有些情况我们需要有些样式全局生效，有些局部生效，此时也可以用:global() 
  :global() 全局选择器
*/
:global(div) {
    border: 1px red solid;
}
</style>


<!-- 有些情况我们需要有些样式全局生效，有些局部生效，此时可以用俩个style，一个加scoped一个不加 -->
<style>
div {
    border: 1px red solid;
}
</style>
```

##### 2.css模块化

```vue
<script setup>
import MyBox from "./components/MyBox.vue"
</script>

<template>
    <div class="app">
        <h1>今天天气真不错！</h1>
        <!-- 默认使用时$style.类名 -->
        <!-- <div :class="$style.box1"></div> -->
        <div :class="classes.box1">App中的box1</div>
        <MyBox></MyBox>
    </div>
</template>

<!-- 
  css 模块(类似js模块)
    - 自动的对模块中的类名进行hash化来确保类名的唯一性
    - 在模板中可以通过 $style.类名 使用(每个组件的$style都是不一样的，不会重复)
    - 也可以通过module的属性值来指定变量名
-->

<style module="classes">
.box1 {
    background-color: #bfa;
}
</style>
```

##### 3.类名(属性)的动态设置和内联样式

```vue
<script setup>
// 动态设置类名
const arr = ["box1", "box2", "box3"]
//可以直接传对象,true表示生效,false不生效
const arr2 = [{ box1: true }, { box2: false }, { box3: true }]
const style = {
    color: "red",
    backgroundColor: "#bfa"
}
</script>
<template>
    <!-- 可以直接设置类名，和网页一样 -->
    <h1 class="header">我爱Vue</h1>
    <!-- 设置了box1和box3 设置了内联样式-->
    <div :class="arr2" :style="style">我是div</div>
</template>
<style scoped>
.header {
    background-color: orange;
}
</style>
```



#### 8.props

**MyButton.vue**

```vue
<script setup>
/* 
        父组件可以通过props来向子组件传递数据
        注意：父组件传递给子组件的props都是只读的，无法修改(单向数据流：只能读)
            ❤我们使用ref和reactive创建响应式数据时要确保数据只能在创建的地方修改(数据安全性)
            即使可以修改，我们也尽量不要在子组件中去修改父组件的数据
            如果非得要改，具体方法后边再讲（自定义事件）
            直接修改的方式是：
                通过在父组件中定义对象 修改对象的属性 因为props锁定的是变量名

        属性名(const props = defineProps(["count", "obj", "maxLength"]))
            - 定义属性名时，属性名要遵循驼峰命名法      
            - 传参的时候有俩种命名方法:
                    1.max-length = xxx   vue推荐 因为模板可以直接在网页引用，为了兼容网页的语法规范
                        网页里使用vue模板
                            1.直接在script中 new Vue()创建后在使用{{}}
                            2.在script引入组件后 直接使用{{}}
                    2.maxLength = xxx

        使用props完成父子组件的通信：
            1.在子组件中定义props
            2.父组件创建ref或reactive对象传值
                 -也可以直接进行传值 例如<TabItem:item="player1"  max=10></TabItem:item=>
            3.注册组件并且传入数据 例如<TabItem :item="player1"></TabItem>
            4.子组件使用父组件传回的数据渲染模板            
    */
// 定义props
// count = 0
// obj = {count = 0}
// const props = defineProps(["count", "obj", "maxLength"])

const props = defineProps({
    //通过对象来做类型限制
    count: Number,
    obj: Object,
    //默认值是false 没传isCheck就是false
    isCheck: Boolean,
    // 对象中的属性也可以做配置
    maxLength: {
        type: String, //类型
        required: true, //必须的 必须有这个属性
        default: "哈哈",//默认值 没传参数时使用默认值
        //检查参数是否合法 value是父组件传过来的值
        validator(value) {
            // value不等于嘻嘻返回true 参数合法
            return value !== "嘻嘻"
        }
    }
})

console.log(props)
</script>

<template>
    <div>
        <h1>{{ props.maxLength }}</h1>
        <h2>我是子组件 MyBox {{ props.obj.count }}</h2>
        <button @click="props.obj.count++">MB的按钮</button>
        <hr />
    </div>
</template>

<style scoped>
div {
    color: tomato;
}
</style>
```

**设置了对象来进行类型检测:只在开发时提示开发者，不符合规定项目页会运行，控制台会报错提示不合法**

![uTools_1681739421125](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681739421125.png)





**子组件直接修改父组件的数据(不要这样去做，这里是做扩展)**

```css
props锁定的是变量，所以说我们可以通过在父组件创建对象的方式来实现修改

修改父组件传入的对象的属性就可以达到子组件直接修改父组件的数据
```



![uTools_1681738502457](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681738502457.png)

**修改了obj对象的count属性**

![uTools_1681738657828](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1681738657828.png)





#### 9.练习

##### 1.单组件实现

```vue
<script setup>
  import {ref} from "vue"
  //创建变量记录小选项卡的状态
  const current = ref(0) //0表示球员 1表示球队
</script>

<template>
  <!-- 外部容器 -->
  <div class="tab-wrapper">

    <!-- 选项卡的头部 -->
    <header class="tab-head">
      <!-- 定义俩个按钮 -->
      <!-- 为按钮设置一个动态的类名 当current为0时设置active -->
      <div @click="current=0" class="tab-button" :class="{active:current === 0}">热门球员</div>
      <div @click="current=1" class="tab-button" :class="{active:current === 1}">热门球队</div>
    </header>

    <!-- 选项卡的主题 -->
    <div class="main">
      <!-- 
        v-show指令用来设置一个内容是否显示
           ——原理是通过display来设置一个元素是否显示的(js原生写法)
       -->
      <div v-show="current === 0">
        <!-- 球员外层容器 -->
        <div class="tab-list">
          <!-- 球员容器 -->
          <div class="tab-item">
            <!-- 图片 -->
            <div class="photo">
              <!-- 放在public下的图片的路径默认就是根路径/ -->
              <img src="/images/messi.png" alt="梅西">
              <span>1</span>
            </div>
            <!-- 文字描述 -->
            <div class="desc">
              <span class="name">梅西</span>
              <!-- 热度条 每个球员不一样 -->
              <div class="hot-bar">
                <div class="inner">433760热度</div>
              </div>
            </div>
          </div>
          <div class="tab-item">
            <!-- 图片 -->
            <div class="photo">
              <!-- 放在public下的图片的路径默认就是根路径/ -->
              <img src="/images/ronaldo.png" alt="梅西">
              <span>1</span>
            </div>
            <!-- 文字描述 -->
            <div class="desc">
              <span class="name">C罗</span>
              <!-- 热度条 每个球员不一样 -->
              <div class="hot-bar">
                <div class="inner1">133760热度</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div v-show="current === 1">
        <!-- 球队外层容器 -->
        <div class="tab-list">
          <!-- 球员容器 -->
          <div class="tab-item">
            <!-- 图片 -->
            <div class="photo">
              <!-- 放在public下的图片的路径默认就是根路径/ -->
              <img src="/images/法国.jpg" alt="法国">
              <span>1</span>
            </div>
            <!-- 文字描述 -->
            <div class="desc">
              <span class="name">法国</span>
              <!-- 热度条 每个球员不一样 -->
              <div class="hot-bar">
                <div class="inner">333760热度</div>
              </div>
            </div>
          </div>
          <!-- 球员容器 -->
          <div class="tab-item">
            <!-- 图片 -->
            <div class="photo">
              <!-- 放在public下的图片的路径默认就是根路径/ -->
              <img src="/images/巴西.jpg" alt="法国">
              <span>1</span>
            </div>
            <!-- 文字描述 -->
            <div class="desc">
              <span class="name">巴西</span>
              <!-- 热度条 每个球员不一样 -->
              <div class="hot-bar">
                <div class="inner2">233760热度</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .tab-wrapper{
    box-sizing: border-box;
    width: 800px;
    padding: 20px;
    background-color: rgb(45,83,211);
  }
  .tab-head{
    display: flex;
    border-radius: 10px;
    /* 子元素溢出 无法显示圆角 开启裁剪 */
    overflow: hidden;
  }

  .tab-button{
    background-color:#fff;
    font-size: 30px;
    padding: 10px 0;
    text-align: center;
    /* 弹性系数 自动伸缩 */
    flex:auto;
    /* 鼠标移入的样式变成手指 */
    cursor: pointer;
    transition: 0.3s;
  }

  .tab-button:not(.active):hover{
    /* 鼠标移入字体变色 被选中的按钮不变色 */
    color: rgb(187, 3, 52);
  }

  .active{
    background-color: rgb(187, 3, 52);
    color: #fff;
  }

  /* 以下设置选项卡下的样式 */
  .tab-list{
    margin: 20px;
  }

  .tab-item{
    /* 开启弹性盒子 水平排列 */
    display: flex;
    margin-bottom: 40px;
  }

  .photo{
    width: 150px;
    background-color: #fff;
    border-radius: 20px;
    /* 不裁剪的时候 上面无法显示圆角 */
    overflow: hidden;
    position: relative;
  }

  .photo img{
    /* 和容器一样100% */
    width: 100%;
    /* 解决图片和底部不对齐的bug */
    vertical-align: top;
  }

  .photo span{
    position: absolute;
    top: 0;
    left: 0;
    width: 50px;
    height: 50px;
    background-color: #f36601;
    font-size: 20px;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom-right-radius:20px;
  }

  .desc{
    font-size: 30px;
    color: #fff;
    display: flex;
    /* 弹性盒子垂直排列 */
    flex-flow: column;
    /* 对齐方式 */
    justify-content: space-evenly;
    /* 弹性盒子自动伸缩撑满原始 */
    flex: auto;
    margin-left: 30px;
  }
  .hot-bar{
    background-color:#032667;
    border-radius: 20px;
    /* 向内缩进0.5个字体 */
    text-indent: 0.5em;
    /* 不裁剪圆角会不生效 */
    overflow: hidden;
  }

  .inner{
    width: 65%;
    /* 给内部的加上圆角 */
    border-radius: 20px;
    /* 忘记属性了 可以直接右键移入 vscode会自动引用mdn */
    /* 线性渐变默认从上往下变  90deg直接转成水平的*/
    /* 50%是设置第一个颜色平铺60%在变色 */
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));

    /* 文字不换行 这样宽度小了就不会被挤下来 */
    white-space: nowrap;
  }

  .inner1{
    width: 35%;
    border-radius: 20px;
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));
    white-space: nowrap;
  }

  .inner2{
    width: 45%;
    border-radius: 20px;
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));
    white-space: nowrap;
  }
</style>
```

##### 2.多组件实现(还有样式的动态引入)





#### 10.v-show和v-if

```vue
<script setup>
import { ref } from "vue"

const isShow = ref(true)
</script>
<template>
    <h1>App组件</h1>
    <button @click="isShow = !isShow">切换</button>

    <!-- 
      v-show 可以根据值来决定元素是否显示（通过display来切换元素的显示状态）
      v-if 可以根据表达式的值来决定是否显示元素（会直接将元素删除）

        - 1.v-show通过css来切换组件的显示与否，切换时不会涉及到组件的重新渲染
            切换的性能比较高。
          2.但是初始化时，需要对所有组件进行初始化（即使组件暂时不显示）
            所以它的初始化的性能要差一些！

        - 1.v-if通过删除添加元素的方式来切换元素的显示，切换时需要反复的渲染组件，
            切换的性能比较差。(显示的时候才加载)
          2.v-if只会初始化需要用到的组件，所以它的初始化性能比较好
          3.v-if可以和 v-else-if 和 v-else结合使用
          4.v-if可以配合template使用，template1不会显示，用div包会显示div(v-if加在哪个标签就是控制哪个标签)
            v-show不能配合template使用，因为template不会显示，它没有地方加display:none

      如何选择:
         1.组件加载速度较快，v-show和v-if都可以
         2.需要很快的切换效果，用v-show
         3.组件较大，选择v-if好一点
         4.球员球队练习适合用v-show(组件不大，需要切换速度快)    

      补充：回答v-if和v-show的区别，不可以说回流(重排重绘没什么关系)
    -->

    <!-- <div v-if="isShow">
        <h2>我是if中的内容</h2>
    </div>
    <div v-else>
        <h2>我是else中的内容！</h2>
    </div> -->

    <!-- 渲染后template不会显示 -->
    <template v-if="isShow">
        <h2>我是一个h2</h2>
        <h3>我是h3</h3>
    </template>
</template>
```



#### 11.component

```vue
<script setup>
import { ref } from "vue"
import A from "./components/A.vue"
import B from "./components/B.vue"

const isShow = ref(true)
</script>
<template>
    <!-- 
        component 是一个动态组件
            - component最终以什么标签呈现由is属性决定
    -->
    <button @click="isShow = !isShow">切换</button>
    <component :is="isShow ? A : B"></component>
</template>
```



#### 12.v-for介绍

```vue
<script setup>
import { ref } from "vue"
const arr = ref(["孙悟空", "猪八戒", "沙和尚", "唐僧"])
</script>
<template>
    <ul>
        <!-- name就是取名变量:取值的方式就是arr[0],arr[1],arr[2] -->
        <li v-for="name in arr">{{ name }}</li>
        <li v-for="name of arr">{{ name }}</li>   in和of效果一样
     </ul>
</template>
```

#### 13.v-for补充

```vue
<script setup>
import { ref } from "vue"
const arr = ref(["孙悟空", "猪八戒", "沙和尚", "唐僧"])
const arr2 = ref([
    {
        id: 1,
        name: "孙悟空",
        age: 18
    },
    {
        id: 2,
        name: "猪八戒",
        age: 28
    },
    {
        id: 3,
        name: "沙和尚",
        age: 38
    }
])
</script>

<template>
    <button @click="arr.push('白骨精')">点我一下</button>

    <!-- 向最后添加 只会修改最后一个li -->
    <button @click="arr2.push({ id: 4, name: '唐僧', age: 16 })">
        点我一下2
    </button>

    <!-- 向前面添加，会修改所有的li -->
    <button @click="arr2.unshift({ id: 4, name: '唐僧', age: 16 })">
        点我一下2
    </button>

    <ul>
        <li v-for="name of arr">{{ name }}</li>
    </ul>

    <!-- 遍历时可以遍历index(参数:下标 取什么名称都行) -->
    <ul>
        <li v-for="(name, index) in arr">{{ index }} - {{ name }}</li>
    </ul>

    <div v-for="obj in arr2">{{ obj.id }} --{{obj.name}} -- {{ obj.age }}</div>
    <hr />

    <!-- 通过template遍历时外层不会嵌套标签 -->
    <template v-for="obj in arr2">{{ obj.id }} --{{obj.name}} -- {{ obj.age }}</template>

    <!-- 
        我们在使用v-for遍历时，旧的结构和新的结构是按照顺序进行对比的
        <div>孙悟空</div>
        <div>猪八戒</div>
        <div>沙和尚</div>

        默认情况下：vue采取diff比较算法，按顺序进行比较，发生了变化才修改元素
        <div>孙悟空</div>
        <div>猪八戒</div>
        <div>沙和尚</div>
        <div>唐僧</div>

        unshift添加在前面，于是4个li都发生了修改
        <div>唐僧</div>
        <div>孙悟空</div>
        <div>猪八戒</div>
        <div>沙和尚</div>

        其实修改4个li对性能的影响不大，最主要的我们
            要预防按顺序比较时元素不是互相对应的，导致元素错位

        解决方法:在使用v-for时，可以为元素指定一个唯一的key
            有了key以后，元素再比较时就会按照相同的key去比较而不是顺序

        <div key=1>孙悟空</div>
        <div key=2>猪八戒</div>
        <div key=3>沙和尚</div>

        <div key=4>唐僧</div>
        <div key=1>孙悟空</div>
        <div key=2>猪八戒</div>
        <div key=3>沙和尚</div>
        
    -->
    <ul>
        <!-- ({解构赋值},index) -->
        <!-- 传入对象当中的唯一标识id 此时是按id来对比的 -->
        <li v-for="({ id, name, age }, index) in arr2" :key="id">
            {{ name }} -- {{ age }}
            <input type="text" />
        </li>
    </ul>
</template>
```

##### 1.当元素后面还带一些其它不变的元素时，错位就会影响数据的对应

![uTools_1682344701097](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682344701097.png)

![uTools_1682344709753](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682344709753.png)

![uTools_1682345102384](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682345102384.png)

##### 2.v-for和v-if同时使用时

![uTools_1682345200804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682345200804.png)

##### 2.在组件中直接使用v-for

![uTools_1682345456511](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682345456511.png)



#### 14.插槽

App.vue

```vue
<script setup>
import MyButton from "./components/MyButton.vue"
import A from "./components/A.vue"
import MyWrapper from "./components/MyWrapper.vue"

const name = "孙悟空"
</script>
<template>
    <h1>App组件</h1>
    <!-- 
        希望在父组件中指定子组件中的内容
            - 之前我们的解决方法是，为父组件指定props，然后在子组件接收
              在子组件中我们用props.text来代替写死的text
              但是这种写法不够好，我们通过props属性指定的是按钮中的文字

            - 限制我们可以通过插槽（slot）来实现该需求
                插槽中可以放置任意的内容，不止是文字，还可以是标签或者是其它组件等
        
	   父组件中:
	   	   <MyButton>插槽的入口</MyButton>

        子组件中:
            <button>
                <slot></slot>  插槽的出口
            </button>
    -->
    <!--
    在插槽中插入A组件
    <MyButton>
        <A :name="name"></A>
	    //A组件也是app组件的子组件，mybutton组件和A组件没上面关系
		// 通过插槽引入组件，位于父组件的作用域中
		//A组件能访问到app中定义的name
		//A组件不能访问MyButton中的内容 俩者不认识
    </MyButton>
    -->

    <MyWrapper>
        <!-- 使用template外层不会套标签 -->
        <!-- 具名插槽的入口 -->
        <template v-slot:aa>一级标题</template>
        <!-- 插槽的简写为# -->
        <template #bb>二级标题</template>
    </MyWrapper>
</template>
```

MyButton.vue

```vue
<script setup>
const age = 18
</script>
<template>
    <button>
        <!-- slot标签，会被组件的标签体所替换 -->
        <slot></slot>
    </button>
</template>
<style scoped>
/* button {
    width: 200px;
    height: 100px;
    font-size: 26px;
} */
</style>
```

A.vue

```vue
<script setup>
const props = defineProps(["name"])
</script>
<template>
    <h1>A组件 {{ props.name }}</h1>
</template>
```

MyWrapper.vue

```vue
<template>
    <div>
        <!-- 通过具名(命名)插槽为h1和h2传入不同的内容 -->
        <h1><slot name="aa"></slot></h1>
        <h2><slot name="bb"></slot></h2>
    </div>
</template>
```



#### 15.插槽补充

app

```vue
<script setup>
import A from "./components/A.vue"
import SlotDemo from "./components/SlotDemo.vue"

const name = "猪八戒"
</script>
<template>
    <h1>App组件</h1>
    <!-- 接收App的name -->
    <A :name="name"></A>
    
    <!-- 直接写在组件中内容是默认插槽的内容，只会出现在默认插槽中（没有name属性的插槽，没被具名的） -->
    <SlotDemo>
        <!-- SlotDemo和A是兄弟元素 要把SlotDemo的值传给A需要特殊处理 -->
        <template #s1>s1插槽</template>

        <!-- 用slotProps接收SlotDemo传递过来的参数 -->
        <!-- <template v-slot:S2="slotProps">{{slotProps}}</template> -->
        <!-- <template v-slot:S2="slotProps"><A :name="slotProps.name"></A></template> -->

        <!-- 解构赋值可以直接访问 -->
        <template v-slot:s2="{ stuName, age, gender }">
            <A :name="age"></A>
        </template>
    </SlotDemo>
</template>
```

slotdemo

```vue
<script setup>
const stu = {
    name: "孙悟空",
    age: 18,
    gender: "男"
}

const stuName = "孙悟空"
const age = 18
const gender = "男"
</script>
<template>
    <div>
        slotDemo组件
        <!-- 可以在slot中指定一个默认内容，默认会在组件中没有内容时显示-->
        <!-- <h1><slot>插槽的默认内容</slot></h1> -->

        <h1><slot name="s1"></slot></h1>
        <div>
            <!-- 插槽中可以设置参数 -->
            <!-- 这个slot其实就是A组件了 此时可以把SlotDemo的内容传给A -->
            <slot name="s2" :gender="gender" :age="age" :stuName="stuName" :stu="stu"></slot>
        </div>

        <!-- 不指定name属性的插槽是默认插槽（default） -->
        <h3><slot></slot></h3>
    </div>
</template>
```

a

```vue
<script setup>
const props = defineProps(["name"])
</script>
<template>
    <h1>A组件 {{ props.name }}</h1>
</template>
```

**补充**

![uTools_1682517005814](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682517005814.png)

















### 补充：网页的渲染

-   浏览器在渲染页面时，做了哪些事情:                                                                                                                                                                                                  

    1. 加载页面的 html 和 css（源码）
    2. html 转换为 DOM(文档对象模型,一组对象)，css 转换为 CSSOM(样式对象)
    3. 将 DOM 和 CSSOM 构建成一棵渲染树
    4. 对渲染树(网页)进行 reflow（回流、重排）（计算元素的位置）
    5. 对网页进行绘制 repaint（重绘）
-   渲染树（Render Tree）

    -   从根元素开始检查那些元素可见，以及他们的样式
    -   忽略那些不可见的元素（display:none） [visibility：hidden等方式会进入树中，因为它们占用网页位置]
-   重排、回流

    -   计算渲染树中元素的大小和位置
    -   当页面中的元素的大小或位置发生变化时，便会触发页面的重排（回流）
    -   重排时一定会触发重绘
    -   width、height、margin、font-size 、padding......
    -   注意：每次修改这类样式都会触发一次重排！所以如果分次修改多个样式会触发重排多次，而重排是非常耗费系统资源的操作（昂贵），重排次数过多后，会导致网页的显示性能变差，在开发时我们应该尽量的减少重排的次数
    -   在现代的前端框架中，这些东西都已经被框架优化过了！所以使用 vue、react 这些框架这些框架开发时，几乎不需要考虑这些问题，唯独需要注意的时，尽量减少在框架中直接操作 DOM(直接操作DOM就会容易触发重排)
    -   Vue中修改组件其实修改的是虚拟DOM，等操作完成后将虚拟DOM移交给DOM对象，这样只会重排一次
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
              
  		    //把样式设置在class中
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
                  
                  // 发生3次重排
                  box1.style.width = "300px"
                  box1.style.height = "400px"
                  box1.style.fontSize = "20px"
                  
                  //可以通过修改class来间接的影响样式，来减少重排的次数
                  box1.classList.add("box3")
                  
                  // 这种方式可以减少重排次数，只会发生俩次
                  box1.style.display = "none"
                  box1.style.width = "300px"
                  box1.style.height = "400px"
                  box1.style.fontSize = "20px"
                  div.style.display = "block"
              }
          </script>
      </body>
  </html>
  ```
  





























### 补充：学完vue3后把vue3和vue2的官方文档看一下



插槽是怎么实现的

```bash
oop面向对象原则
 1.开闭原则(对修改关闭，对扩展开启)
 2.单一原则(一个组件处理一个问题)
```

