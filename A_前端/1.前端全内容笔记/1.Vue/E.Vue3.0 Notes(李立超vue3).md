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

const  = {
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

App.vue

```vue
<script setup>
import {ref} from "vue"
import {reactive} from "vue"
import TabList from "./components/TabList.vue";
import Tab from "./components/Tab.vue"

  //创建一个球员对象
  const players = reactive([
    {
    name:"梅西",
    img:"/images/messi.png",
    rate:"1",
    hot:4033330,
    },
    {
    name:"C罗",
    img:"/images/ronaldo.png",
    rate:"2",
    hot:2033330,
    },
    {
    name:"内马尔",
    img:"/images/neymar.png",
    rate:"3",
    hot:1033330,
    }
  ])

    //创建一个球队对象
    const teams = reactive(
    [{
    name:"法国",
    img:"/images/法国.jpg",
    rate:"1",
    hot:2033760,
    },
    {
    name:"巴西",
    img:"/images/巴西.jpg",
    rate:"2",
    hot:1053760,
    },
    {
    name:"荷兰",
    img:"/images/荷兰.jpg",
    rate:"3",
    hot:1023760,
    }
  ])

  //获取球员最高热度
  const playerMaxHot = players[0].hot
  const teamMaxHot = teams[0].hot

</script>

<template>
  <Tab>
    <!-- 这样可以直接把数据传给Tab 不用在经过app-tab-tablist -->
    <!-- 此时相当于是tablist就是app的子组件，而不是tab的子组件 -->
    <template #0><TabList :items="players" :max-hot="playerMaxHot"></TabList></template>
    <template #1><TabList :items="teams" :max-hot="teamMaxHot"></TabList></template>
  </Tab>
</template>

<style scoped>
</style>
```

HotBar.vue

```vue
<script setup>
import { computed } from '@vue/reactivity';
    const props = defineProps([
        "hot",
        "maxHot"
    ])
    const width = computed(()=>{
        //计算百分比
        return(props.hot / props.maxHot) * 100 + "%"
    })
    // 这是我一开始解决长度的方法手动设置百分比 动态设置width
    // <div class="inner" :style="{width:props.width}">{{props.hot}}热度</div>
    // item要传一个width
</script>

<template>
    <div class="hot-bar">
        <div class="inner">{{props.hot}}热度</div>
    </div>
</template>

<style scoped>
    .hot-bar{
    background-color:#032667;
    border-radius: 20px;
    /* 向内缩进0.5个字体 */
    text-indent: 0.5em;
    /* 不裁剪圆角会不生效 */
    overflow: hidden;
  }

  .inner{
    /* 动态设置宽度 */
    width: v-bind(width);
    /* 给内部的加上圆角 */
    border-radius: 20px;
    /* 忘记属性了 可以直接右键移入 vscode会自动引用mdn */
    /* 线性渐变默认从上往下变  90deg直接转成水平的*/
    /* 50%是设置第一个颜色平铺60%在变色 */
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));
    /* 文字不换行 这样宽度小了就不会被挤下来 */
    white-space: nowrap;
  }
</style>
```

Photo.vue

```vue
<script setup>
import { computed } from '@vue/reactivity';

    //传入参数
    const  props = defineProps([
    // props.src实际上对应的是 TableItem的item.img
        "src",
        "alt",
        "rate"
    ])
    // rate名次的颜色不一样
    // ❤动态的设置样式
    const color = computed(()=>{
        if(props.rate==1){
            return"rgb(254,45,70)"
        }else if(props.rate==2){
            return"rgb(245,102,1)"
        }else{
            return"rgb(247,167,1)"
        }
    })
</script>

<template>
    <!-- 图片 -->
    <div class="photo">
        <!-- 放在public下的图片的路径默认就是根路径/ -->
        <img :src="props.src" :alt="props.name">
        <span>{{props.rate}}</span>
    </div>
</template>

<style scoped>
    
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
    /* 动态设置样式 v-bind() */
    background-color: v-bind(color);
    font-size: 20px;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom-right-radius:20px;
  }
</style>
```

Tab.vue

```vue
<script setup>
import {ref} from 'vue'
  //创建变量记录小选项卡的状态
  const current = ref(0) //0表示球员 1表示球队
</script>

<!-- 
    Tab组件的作用是切换多个选项卡
        其中显示的主要内容是TabList，而TabList的数据位于App中
        如果还按照之前的方式编写代码，数据的传递比较麻烦
            App--Tab--TabList
-->


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
      <div v-show="current === 0">
        <!-- 球员 -->
        <!-- <TabList :items="players" :max-hot="playerMaxHot"></TabList> -->
        <slot name="0"></slot>
      </div>

      <div v-show="current === 1">
        <!-- 球队 -->
       <!-- <TabList :items="teams" :max-hot="teamMaxHot"></TabList> -->
       <slot name="1"></slot>
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




/* 
  .inner1{
    width: 5%;
    border-radius: 20px;
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));
    white-space: nowrap;
  }

  .inner2{
    width: 45%;
    border-radius: 20px;
    background-image: linear-gradient(90deg,rgb(187,3,52),60%,rgb(66,2,12));
    white-space: nowrap;
  } */


</style>
```

TabItem.vue

```vue
<script setup>
    import Photo from "./Photo.vue";
    import HotBar from "./HotBar.vue";

    /*
        子组件中的数据不会在子组件中直接定义，这样会导致数据和视图发生耦合
        子组件中的数据通常会在创建组件实例时确定(引入时父组件传入)
        父组件可以通过props来将数据传递给子组件

        使用props完成父子组件的通信：
            1.在子组件中定义props
            2.父组件创建ref或reactive对象
            3.注册组件并且传入数据 例如<TabItem :item="player1"></TabItem>】
            4.子组件使用父组件传回的数据渲染模板
    */ 

    // 宏定义 设置父组件要传入的值 使用时也不需要引入什么
    // 返回的props是一个代理对象 item就是父组件传回来给子组件的东西
    const props = defineProps(["item","max-hot"])
    // const props1 = defineProps({})

    // 定义一个item获取父组件传来的props.item
    const item = props.item
</script>


<template>
     <!-- 球员容器 -->
     <div class="tab-item">
            <!-- 引入图片组件 -->
            <Photo :src="item.img" :alt="item.name" :rate="item.rate"></Photo>

            <!-- 文字描述 -->
            <div class="desc">
              <span class="name">{{item.name}}</span>
              <!-- 可以直接在变量后进行计算 -->
              <!-- html用xxx-xxx 其它用xxxXXX -->
              <!-- <HotBar :hot="item.hot" :max-hot="item.hot*5"></HotBar> -->
              <!-- props.maxHot是从App传递到TableItem在传递到HotBar -->
              <HotBar :hot="item.hot" :max-hot="props.maxHot"></HotBar>
            </div>
    </div>
</template>

<style scoped>
  .tab-item{
    /* 开启弹性盒子 水平排列 */
    display: flex;
    margin-bottom: 40px;
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
 
</style>
```

TabList.vue

```vue
<!-- 用来专门显示列表的组件 -->
<script setup>
import TabItem from './TabItem.vue'
    //定义参数,接收app.vue传过来的球员和球队数据
    //真实开发中应该是通过ajax向服务器请求数据来进行加载
    const props = defineProps(["items","maxHot"])
</script>

<template>
    <div class="tab-list">
        <!-- 引入组件 给子组件的item属性传一个player1对象-->
        <!-- <TabItem :item="players[0]" :max-hot=" maxHot"></TabItem>
        <TabItem :item="players[1]" :max-hot=" maxHot"></TabItem>
        TabItem :item="players[2]" :max-hot=" maxHot"></TabItem> -->
        <!-- <TabItem v-for="player in players" :item="player" :max-hot="maxHot"></TabItem> -->
        <!-- <TabItem v-for="team in teams" :item="team" :max-hot="maxHot1"></TabItem> -->

        <TabItem v-for="item in props.items" :item="item" :max-hot="props.maxHot"></TabItem>

    </div>    
</template>

<style scoped>
  .tab-list{
    margin: 20px;
  }
</style>
```



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



#### 16.事件

```vue
<script setup>
import { ref } from "vue"

const count = ref(0)

//通过方法事件处理器调用
function clickHandler(event) {
    /* 
        事件对象的作用：
            方法事件处理器的回调函数，vue会将事件对象作为参数传递
            这个事件对象就是DOM中原生的事件对象，它里边包含了事件触发时的相关信息
            通过该对象，可以获取：触发事件的对象、触发事件时一些情况 ...
            同时通过该对象，也可以对事件进行一些配置：取消事件的传播、取消事件的默认行为...
    */
    console.log(event)//打印出原生的事件对象
}

//通过内联事件处理器调用
function clickHandler2(...args) {
    /* 
        内联事件处理器，回调函数由我们自己调用，参数也是我们自己传递的
            注意:在内联事件处理器中，可以使用$event来访问事件对象
    */
    console.log(args)//没传参打印出来是undefined
}

//原生方法解决事件的传播
function boxHandler(event, text) {
    // 可以通过事件对象来取消事件的传播
    // 原生的方法
    event.stopPropagation()
    alert(text)
}

//vue提供的解决事件的传播的方法
function boxHandler2(text) {
    // 可以通过事件对象来取消事件的传播
    event.stopPropagation()//这种方法已经被弃用了，这个event对象是window上的，所以我们没定义也可以访问
    //不建议使用window上的event来取消事件的传播，虽然可以用
    alert(text)
}
</script>

<template>
    <h1>{{ count }}</h1>
    <!-- 
        为元素绑定事件：
            ① 绑定事件使用v-on指令
                v-on:事件名
                简写 >> @事件名
            ② 绑定事件的两种方式
                a. 内联事件处理器（自己调用函数）
                    - 事件触发时，直接执行js语句
                    - 内联事件处理器，回调函数的参数由我们自己传递(你不传它就是空的)

                b. 方法事件处理器（vue帮我们调用函数）
                    - 事件触发时，vue会对事件的函数进行调用
                    - 方法事件处理器，回调函数的参数由vue帮我们传
                        - 参数就是事件对象

                vue如何区分两种处理器：
                    检查事件的值是否是合法的js标识符(变量名)或属性访问路径，
                    如果是，则表示它是方法事件处理器，否则，表示它是内联事件处理器
                            foo（方法）
                            foo.bar（方法:访问对象的属性）

                            foo++（内联:表达式）
                            foo()（内联:函数）
    -->
    <!-- <button v-on:click="count++">点我一下</button> -->
    <button @click="count++">点我一下</button>
    <hr />

    <!-- 相当于btn01.onclick = fn -->
    <button @click="clickHandler">方法事件处理器</button>
    <hr />

    <!-- 这种情况下是内联事件处理器 不是vue自动帮我们调用函数 -->
    <button @click="clickHandler2($event, 1, 2, 'hello')">
        内联事件处理器
    </button>

    <hr />
    <!-- 
    原生:
    <div class="box1" @click="boxHandler($event, '点击了box1')">
        box1
        <div class="box2" @click="boxHandler($event, '点击了box2')">
            box2
            <div class="box3" @click="boxHandler($event, '点击了box3')">box3</div>
        </div>
    </div> 
    -->

    <!-- vue提供的方法:通过 事件.修饰符 原理是vue自己调用了stopPropagation() -->
    <div class="box1" @click="boxHandler2('点击了box1')">
        box1
        <div class="box2" @click.stop="boxHandler2('点击了box2')">
            box2
            <div class="box3" @click.stop="boxHandler2('点击了box3')">box3</div>
        </div>
    </div>
</template>


<style scoped>
.box1 {
    width: 200px;
    height: 200px;
    background-color: #bfa;
}

.box2 {
    width: 100px;
    height: 100px;
    background-color: orange;
}

.box3 {
    width: 50px;
    height: 50px;
    background-color: tomato;
}
</style>
```

![uTools_1683030873414](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683030873414.png)



#### 17.事件修饰符

```vue
<script setup>
function clickHandler(text) {
    // event.stopPropagation()
    alert(text)
}
/* 
    事件修饰符：
        .stop 停止事件的传播？似乎stop只能停止冒泡
        .capture 在捕获阶段触发事件
        .prevent 取消默认行为
        .self 只有事件由自身触发时才会有效
        .once 绑定一个一次性的事件
        .passive 主要用于提升滚动事件的性能(滚动卡的时候可以加上)
            -加上以后会先滚动在执行绑定的函数 看起来就不卡了
            -浏览器目前开始要设置为默认行为了
*/
</script>
<template>
    <h1>Hello Vue</h1>
    <div @click.self="clickHandler('box1')" class="box1">
        <div @click="clickHandler('box2')" class="box2">
            <div @click="clickHandler('box3')" class="box3"></div>
        </div>
    </div>
</template>
<style scoped>
.box1 {
    width: 300px;
    height: 300px;
    background-color: yellowgreen;
}

.box2 {
    width: 200px;
    height: 200px;
    background-color: yellow;
}

.box3 {
    width: 100px;
    height: 100px;
    background-color: #bfa;
}
</style>
```

![uTools_1683032793679](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683032793679.png)

![uTools_1683032814254](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683032814254.png)

![uTools_1683032824899](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683032824899.png)

![uTools_1683032835999](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683032835999.png)

#### 18.属性透传

App.vue

```vue
<script setup>
import C from "./components/C.vue"
/* 
    透传属性
        - 在组件上设置属性，会自动传递给组件的根元素(注意是根元素)
        - 这样一来可以方便我们在父组件中为子组件来设置属性(作用)
        - 透传会发生在没有被声明为props()和emit的属性上
            -const props = defineProps(["name"])
        - 自动的透传只适用单根组件(多根的时候就不透传了)
*/
function showMsg() {
    alert("hello")
}
</script>

<template>
    <h1>属性的透传</h1>
    <h2 class="box1">我是h2</h2>
    <!-- style和click都可以透传 -->
    <C class="box2" style="color: red" @click="showMsg"></C>
    <!-- 转换后会显示<h2 class="box2" style="color: red" @click="showMsg">我是组件C</h2> -->
    ❤❤❤<!-- 如果c组件中还有其它组件 会一直向上透传找到根元素 -->
</template>
<style scoped></style>

```

C.vue

```vue
<script setup>
// 导入包
import { useAttrs } from "vue"

console.log($attrs); //会报错

/* 
    在脚本中$是不能被直接访问的，作用域不一样，只有在模板tem中才可以直接访问
    在script中，可以通过useAttrs()来获取透传过来的属性
*/
const attrs = useAttrs()
console.log(attrs)

</script>

<!-- 不想让c组件自动透传的解决方法 -->
<script>
export default {
    //属性不再进行自动透传,但还是可以手动设置
    inheritAttrs: false
}
</script>

<template>
    <h2 class="box3" style="font-size: 60px">我是组件C</h2>

    <!-- 在模板中，可以通过$attrs来访问透传过来的属性，可以手动指定透传过来的属性要添加到哪些元素(多根单根都行)-->
    {{ $attrs }}

    <h2 class="box3" :class="$attrs.class" style="font-size: 60px">
        我是组件C
    </h2>
    <h3 :class="$attrs.class" :style="$attrs.style">我也是组件C</h3>

    <!-- 这样可以直接把所有透传过来的属性都加上 -->
    <h3 :="$attrs">我是h3</h3>
</template>

```



#### 19.手动双向数据传递

**alt+shift+鼠标左键**

```vue
<!-- 纯手动进行双向数据绑定 -->
<script setup>
import { ref } from 'vue';

  let text = ref('')

  // 处理表单数据的函数 提交表单后触发该函数
  function submitHandler(){
    console.log(text.value);
    //将text提交给服务器，在根据服务器返回的数据做后续的操作
  }
</script>

<template>
  <h1>hello vue</h1>
  <!-- 
    由Vue来接管表单
      -我们将表单项的value属性和变量text做了绑定
        当value变化时，text变量随之变化(单向绑定)
        当value或text变化时，另一个随之变化(双向绑定)

        Vue.js 是一个 MVVM 框架，即数据双向绑定，即当数据发生变化的时候，视图也就发生变化，当视图发生变化的时候，数据也会跟着同步变化。
          双向绑定作用:
                1.当value变化时，text随之变化，让vue可以获取到text值
                2.当text变化时，value随之变化，vue可以影响input的值

                通过事件影响text的值，也可以通过text影响元素的值
   -->
  <form @submit.prevent="submitHandler">
    <input type="text" @input="(event) => (text = event.target.value)">
    <button>提交</button>
  </form>
</template>


<style scoped>

</style>
```

#### 20.v-model及修饰符

```vue
<script setup>
import { ref } from 'vue';

  const text = ref('')
  const bool = ref('是')
  const hobbies = ref([])
  const gender = ref('女')
  const friend1 = ref('')
  const friend2 = ref('[]')

  function submitHandler(){
    console.log(text.value);
    //将text提交给服务器，在根据服务器返回的数据做后续的操作
  }
</script>

<template>
  <h1>hello vue</h1>
  <form @submit.prevent="submitHandler">
    <div>
    <!-- 
        在vue中，为我们提供了v-model了可以快速完成表单的双向数据绑定
        <input type="text" v-model="text" /> 等价于下面那行
        <input type="text" :value="text" @input="event => text = event.target.value" />
    -->
    <!-- 
          v-model的修饰符
            .lazy 使用change来处理数据
            .trim 去除前后的空格
            .number 将数据转换为数值
      -->
        信息:<input type="text" v-model.lazy="text">
    </div>

    <div>
      是否:
        <!-- true-value="是" false-value="否" 可以设置特殊的布尔值 -->
        <input v-model="bool" type="checkbox" true-value="是" false-value="否">
    </div>
    <div>
        爱好:
        <input v-model="hobbies" type="checkbox" name="hobby" value="足球">足球
        <input v-model="hobbies" type="checkbox" name="hobby" value="篮球">篮球
        <input v-model="hobbies" type="checkbox" name="hobby" value="羽毛球">羽毛球
    </div>

    <div>
      性别:
      <input v-model="gender" type="radio" name="gender" value="男">男
      <input v-model="gender" type="radio" name="gender" value="女">女
    </div>

    <div>
      朋友:
        <select v-model="friend1">
          <!-- 
            在ios浏览器中 没有给下拉框设置默认值
              -会出现无法选择下拉框的情况
                -解决方法是加一个空的选项并禁用该选项
            如果设置了默认值就不会出现这种情况
           -->
          <option value="" disabled>请选择...</option>
          <option>孙悟空</option>
          <option>猪八戒</option>
          <option>沙和尚</option>
        </select>
    </div>

    <div>
      朋友:
      <!-- 下拉框多选的情况就要用数组 -->
        <select v-model="friend2" multiple>
          <option>孙悟空</option>
          <option>猪八戒</option>
          <option>沙和尚</option>
          <option>黄以</option>
          <option>黄宇</option>
          <option>死狗于</option>
        </select>
    </div>

    <button>提交</button>
  </form>
</template>

<style scoped>

</style>
```



#### 21.自定义事件 emits

App.vue

```vue
<script setup>
import { ref } from 'vue';
import StudentList from './components/StudentList.vue';

//发送请求来向服务器加载数据
//这里我们就直接在这里用了
const STU_ARR = ref([
    {id:1,name:"孙悟空",age:18,gender:"男",address:"花果山"},
    {id:2,name:"黄宇",age:28,gender:"男",address:"花果山"},
    {id:3,name:"许信",age:38,gender:"男",address:"花果山"},
    {id:4,name:"伟杰",age:28,gender:"男",address:"花果山"},
])

//定义一个删除学生的方法
const delStudentsByIndex = (index) => {
    STU_ARR.value.splice(index,1)
}

</script>

<template>
    <!-- <StudentList :students="STU_ARR" :fn="delStudentsByIndex"></StudentList> -->
    <!-- 可以将组件中的方法以自定义事件的形式发送给其它组件(方法用自定义事件传,数据用属性传) -->
    <StudentList :students="STU_ARR" @del-stu="delStudentsByIndex"></StudentList>
</template>
```

StudentsList.vue

```vue
<script setup>

//通过defineProps定义的属性在$attrs中就不存在了
//被我们自定义了,所以不会透传了
//使用自定义属性时最好用defineProps来指定,这样组件拥有什么属性更加清晰
//透传适合的场景我现在还不知道....
//通过defineProps来接收父组件的students属性
// const props = defineProps(["students","fn"])
const props = defineProps(["students"])

//定义自定义事件对象
//defineEmits用来接收父组件传过来的方法
const emits = defineEmits(["delStu"])


//定义一个删除学生的方法 这个方法调用delStu
const delStuHandler = (index) => {
    if (confirm("确认删除吗?")) {
        //前面我们提到了props的属性虽然可以修改,但是最好是只读的不要动它
        //因为直接修改了父组件对象中的数据
        //props.students.splice(index,1)
        
        //开发中要遵循一个原则 自己的事情自己做
        //所以删除App的数据要由App来做,App提供一个删除的方法让大家调用
        //第一种方法是在App定义一个属性传给StudentList(但是这样不好,正常属性都是传值)
        // props.fn(index)

        //第二种方法是通过自定义事件(自定义事件在js和模板都可以使用)
        emits('delStu',index)
    }
}
</script>

<template>
    <table>
        <caption>
            学生列表
        </caption>
        <thead>
            <tr>
                <th>学号</th>
                <th>性别</th>
                <th>年龄</th>
                <th>性别</th>
                <th>住址</th>
                <th>删除</th>
            </tr>
        </thead>
        <tbody>
            <!-- 
                不推荐使用透传这种方式
                    -会造成一个问题:使用我们组件的人不知道组件中
                        有一个自定的:students属性
                    -建议使用自定义属性,这样使用我们的组件时会有提示
            -->
            <!-- <tr v-for="stu in $attrs.students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
            </tr> -->

            <tr v-for="(stu,index) in props.students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
                <!--
                    父子组件中的通信通过props和emit来完成
                        -父组件传递给子组件
                            -父组件传递属性给子组件 props
                            -父组件传递方法给子组件 emits

                        -子组件传递给父组件
                            -子组件传递给父组件(更友好,不违反props的单向数据原则) emit
                 -->
                <td>
                    <!-- <a href="#" @click.prevent="delStuHandler(index)">删除</a> -->

                    <!-- 在模板中可以通过$emit()来触发自定义事件 -->
                    <!-- index作为参数传过来(这是直接使用的方式,但是不要这样,别的组件使用我们并组件不知道有这个属性) -->
                    <!-- <a href="#" @click.prevent="$emit('delStu',index,$event)">删除</a> -->

                    <!-- 直接使用自定义事件对象 -->
                    <!-- <a href="#" @click.prevent="emits('delStu',index)">删除</a> -->

                    <!-- 调用js方法 js方法使用了自定义事件对象 -->
                    <a href="#" @click.prevent="delStuHandler(index)">删除</a>
                </td>
            </tr>

        </tbody>
    </table>
</template>

<style scoped>
    table{
        width: 100%;
        border-collapse: collapse;
    }

    caption{
        font-size: 30px;
        font-weight: bold;
    }

    th,td{
        border: 1px solid black;
        text-align: center;
    }
</style>  
```

#### 22.自定义事件练习

**包括： 1.(App->List(接收数据传递)->Item定义变量接收传递) 2.(App->List->Item利用透传传递传递)**

app

```vue
<script setup>
import { ref } from 'vue';
import StudentList from './components/StudentList.vue';
import StudentForm from './components/StudentForm.vue';

//发送请求来向服务器加载数据
//这里我们就直接在这里用了
const STU_ARR = ref([
    {id:1,name:"孙悟空",age:18,gender:"男",address:"花果山"},
    {id:2,name:"黄宇",age:28,gender:"男",address:"花果山"},
    {id:3,name:"许信",age:38,gender:"男",address:"花果山"},
    {id:4,name:"伟杰",age:28,gender:"男",address:"花果山"},
])

//自己的事情自己做，自己的增删改查自己来，别的组件只能调用我的方法来改变我的数据

//定义一个删除学生的方法
const delStudentsByIndex = (index) => {
    STU_ARR.value.splice(index,1)
}

//定义一个添加学生的方法
const addNewStudent = (student)  => {
    //取最后一个元素的id(？判断存在 才能进行取值)
    const lastId = STU_ARR.value.at(-1)?.id
    //取到的值非空 进行加1
    const newId = !isNaN(lastId) ? lastId + 1 : 1
    //传进来的student.id就是新的id
    student.id = newId
    STU_ARR.value.push(student)
}

</script>

<template>
    <!-- <StudentList :students="STU_ARR" :fn="delStudentsByIndex"></StudentList> -->
    <!-- 可以将组件中的方法以自定义事件的形式发送给其它组件(方法用自定义事件传,数据用属性传) -->
    <StudentList :students="STU_ARR" @del-stu="delStudentsByIndex"></StudentList>

    <hr>
    <StudentForm @add-student="addNewStudent"></StudentForm>
</template>
```

StudenList

```vue
<script setup>
import StudentItem from './StudentItem.vue';

//通过defineProps定义的属性在$attrs中就不存在了
//被我们自定义了,所以不会透传了
//使用自定义属性时最好用defineProps来指定,这样组件拥有什么属性更加清晰
//透传适合的场景我现在还不知道....
//通过defineProps来接收父组件的students属性
// const props = defineProps(["students","fn"])
// const props = defineProps(["students"])
// const emits = defineEmits(["delStu"])

</script>

<template>
    <table>
        <caption>
            学生列表
        </caption>
        <thead>
            <tr>
                <th>学号</th>
                <th>性别</th>
                <th>年龄</th>
                <th>性别</th>
                <th>住址</th>
                <th>删除</th>
            </tr>
        </thead>
        <!-- 通过app传给list，在传给item 这种方式很麻烦 list要app这俩个数据根本没有用，还要先定义在传递 -->
        <!-- <StudentItem :students="props.students" @del-stu="emits('delStu',index)"></StudentItem> -->
        <!-- 我们使用透传也可实现这个效果,因为透传会一直往上找，找到item -->
        <!-- 注意事件的传递要加上$attrs.onXxxx -->
        <!-- 但是这样list还是要指定透传属性给item 太麻烦了 我们需要一个app直接传给item的东西 -->
        <StudentItem :students="$attrs.students" @del-stu="$attrs.onDelStu"></StudentItem>
    </table>
</template>

<style scoped>
    table{
        width: 100%;
        border-collapse: collapse;
    }

    caption{
        font-size: 30px;
        font-weight: bold;
    }

    th{
        border: 1px solid black;
        text-align: center;
    }
</style>
```

StudentItem

```vue
<script setup>
const props = defineProps(["students"])

//定义自定义事件对象
//defineEmits用来接收父组件传过来的方法
const emits = defineEmits(["delStu"])

//定义一个删除学生的方法
const delStuHandler = (index) => {
    if (confirm("确认删除吗?")) {
        //前面我们提到了props的属性虽然可以修改,但是最好是只读的不要动它
        //因为直接修改了父组件对象中的数据
        //props.students.splice(index,1)
        
        //开发中要遵循一个原则 自己的事情自己做
        //所以删除App的数据要由App来做,App提供一个删除的方法让大家调用
        //第一种方法是在App定义一个属性传给StudentList(但是这样不好,正常属性都是传值)
        // props.fn(index)

        //第二种方法是通过自定义事件(自定义事件在js和模板都可以使用)
        emits('delStu',index)
    }
}
</script>

<template>
            <tbody>
            <!-- 
                不推荐使用透传这种方式
                    -会造成一个问题:使用我们组件的人不知道组件中
                        有一个自定的:students属性
                    -建议使用自定义属性,这样使用我们的组件时会有提示
            -->
            <!-- <tr v-for="stu in $attrs.students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
            </tr> -->

            <tr v-for="(stu,index) in props.students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
                <!--
                    父子组件中的通信通过props和emit来完成
                        -父组件传递给子组件
                            -父组件传递属性给子组件 props
                            -父组件传递方法给子组件 emits

                        -子组件传递给父组件
                            -子组件传递给父组件(更友好,不违反props的单向数据原则) emit
                 -->
                <td>
                    <!-- <a href="#" @click.prevent="delStuHandler(index)">删除</a> -->

                    <!-- 在模板中可以通过$emit()来触发自定义事件 -->
                    <!-- index作为参数传过来(这是直接使用的方式,但是不要这样,别的组件使用我们并组件不知道有这个属性) -->
                    <!-- <a href="#" @click.prevent="$emit('delStu',index,$event)">删除</a> -->

                    <!-- 直接使用自定义事件对象 -->
                    <!-- <a href="#" @click.prevent="emits('delStu',index)">删除</a> -->

                    <!-- 调用js方法 js方法使用了自定义事件对象 -->
                    <a href="#" @click.prevent="delStuHandler(index)">删除</a>
                </td>
            </tr>
        </tbody>   
</template>

<style scoped>
    th,td{
        border: 1px solid black;
        text-align: center;
    }
</style>
```

StudentForm

```vue
<script setup>
import { ref } from 'vue';
    
    const emits = defineEmits(["addStudent"])
    //定义一个新的变量来存储新添加的数据
    const newStu = ref({
        name:"",
        age:1,
        gender:"男",
        address:""
    })
    const submitHandler = () => {
        //调用app添加数组的方法
        //为了避免响应式数据印象表单的数据，我们要对newStu转成非响应式对象
        //不处理的话，表单里的数据是响应式的，一变全部跟着变，浅复制只复制数据，不会复制响应式
        // emits("addStudent",Object.assign({},newStu.value))
        emits("addStudent",{...newStu.value})

        //添加以后重置(因为表单现在是我们自己处理了，不是以前的默认行为重置表单)
        newStu.value.name = ""
        newStu.value.age = 1
        newStu.value.gender = "男"
        newStu.value.address = ""
        
    }
</script>
<template>
    <form @submit.prevent="submitHandler">
        <div>
            姓名: <input type="text" v-model="newStu.name">
        </div>
        <div>
            性别: 
            <input type="radio" name="gender" value="男"  v-model="newStu.gender">男 
            <input type="radio" name="gender" value="女" v-model="newStu.gender">女
        </div>
        <div>
            年龄: <input type="number" v-model="newStu.age">
        </div>
        <div>
            住址: <input type="text" v-model="newStu.address">
        </div>
        <div>
            <button>添加</button>
        </div>
    </form>
</template>
```

#### 22.1v-model和v-bind

##### 1.Vue3.3defindeModel取代defineProps和defineEmits

`v-model`和`v-bind`都是Vue的指令，但它们有不同的作用。

`v-bind`指令用于绑定一个值到指定的HTML属性上，语法为`:attribute="value"`。例如：

```html
<img :src="imgSrc">
```

在这里，`imgSrc`是一个Vue实例中的属性，我们将其通过`v-bind`指令绑定到`src`属性上，这样当`imgSrc`的值发生变化时，图片的URL也会被更新。

而`v-model`指令用于在表单元素（如input、select、textarea等）上创建双向数据绑定，它相当于同时使用了`v-bind`和`v-on`指令。例如：

```html
<input v-model="message" />
```

这里，`message`是Vue实例中的一个属性，它会被绑定到输入框的值上，并且当输入框的值发生变化时，`message`的值也会随之更新。

需要注意的是，只有`<input>`、`<select>`和`<textarea>`等表单元素才能使用`v-model`指令。对于其他元素，你需要使用自定义指令或手动绑定事件来实现类似的功能。

总之，`v-bind`用于单向数据绑定，将Vue实例中的属性值绑定到DOM元素的属性上；`v-model`用于双向数据绑定，在表单元素上创建了一个值和输入框内容之间的双向绑定关系，可以同时监听用户的输入事件和修改属性的变化。

##### 2.通过练习来看

![uTools_1685082740558](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685082740558.png)

父组件

```vue
<script setup>
import { ref } from 'vue';
import A from './components/A.vue';
// 定义一个变量val传给子组件
const val = ref('')
</script>

<template>
变化的值:{{ val }}
<hr>
<!-- 设置v-model就是绑定了一个value属性和input事件 -->
<A v-model="val"></A>
</template>

```

子组件

```vue
<script setup>
// 子组件需要接收props
// 在Vue 3中，v-model指令默认绑定的属性是名为modelValue的属性。
import { defineProps } from 'vue';
import { defineEmits } from 'vue';
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])
function onInput(e) {
  emit('update:modelValue', e.target.value)
}
</script>

<template>
  <!-- 通过:value和@input接收来自父组件的数据 -->
  <input :value="modelValue" @input="onInput" />
</template>
```

原理

```css
这是一个使用Vue 3的组件通信方式——v-model，父组件和子组件共同维护了一个变量val。

在父组件中，定义了一个val变量，并将它传递给了子组件A，同时在模板中使用了v-model指令将val绑定到了A组件上。这个v-model指令实际上会自动展开为一个value属性和一个input事件的绑定，value属性的值会随着val的改变而改变，而input事件则会在用户输入时触发，从而更新val的值。
也就是说用户输入时val值会更新，value值也会随着改变。

在子组件中，使用defineProps定义了一个modelValue属性作为接收父组件传递进来的val变量的值，同时使用defineEmits定义了一个update:modelValue事件，用于向父组件发送更新val的请求。在模板中，使用:value="modelValue"将modelValue的值绑定到了input元素的value属性上，从而将父组件传递进来的val变量的值显示在了输入框中。当用户输入时，onInput方法会被调用，然后通过emit方法触发update:modelValue事件，最终将用户输入的值传递给父组件，从而完成了双向数据绑定的效果。
```

**在vue3.3中引入了defineModel来简化操作**

```vue
<script setup>
//子组件只需要这样就可以实现和上面一样的功能
import { defineModel } from 'vue';
// 子组件需要接收props
// 在Vue 3中，v-model指令默认绑定的属性是名为modelValue的属性。
// const props = defineProps(['modelValue'])
// const emit = defineEmits(['update:modelValue'])
// function onInput(e) {
//   emit('update:modelValue', e.target.value)
// }


const modelValue = defineModel()
</script>

<template>
  <input v-model="modelValue" />
</template>
```

![uTools_1685096966693](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685096966693.png)



#### 23.依赖注入(多层结构传递值 vue3)

```css
    依赖注入
        - 通过依赖注入，可以跨域多层组件向其他的组件传递数据
            -一定要是祖先后代的关系才可以开启依赖注入
            -兄弟元素读不到依赖注入 但是可以读取到一个你设置的默认值

        - 步骤：
            1. 设置依赖（provide） provide(name, value)  父组件导入包provide 子组件导入包inject  
            2. 注入数据 （inject） const value = inject(name, default)

        -注意：
            依赖注入谁近取谁  A-B-C AB都设置了name  C组件会读取到B组件的name 
```



#### 24.依赖注入改进练习

app

```vue
<script setup>
import { provide, ref } from 'vue';
import StudentList from './components/StudentList.vue';
import StudentForm from './components/StudentForm.vue';

//发送请求来向服务器加载数据
//这里我们就直接在这里用了
const STU_ARR = ref([
    {id:1,name:"孙悟空",age:18,gender:"男",address:"花果山"},
    {id:2,name:"黄宇",age:28,gender:"男",address:"花果山"},
    {id:3,name:"许信",age:38,gender:"男",address:"花果山"},
    {id:4,name:"伟杰",age:28,gender:"男",address:"花果山"},
])

//自己的事情自己做，自己的增删改查自己来，别的组件只能调用我的方法来改变我的数据

//定义一个删除学生的方法
const delStudentByIndex = (index) => {
    STU_ARR.value.splice(index,1)
}

//定义一个添加学生的方法
const addNewStudent = (student)  => {
    //取最后一个元素的id(？判断存在 才能进行取值)
    const lastId = STU_ARR.value.at(-1)?.id
    //取到的值非空 进行加1
    const newId = !isNaN(lastId) ? lastId + 1 : 1
    //传进来的student.id就是新的id
    student.id = newId
    STU_ARR.value.push(student)
}

//依赖注入
provide("student", {
    students: STU_ARR,
    delStudentByIndex,
    addNewStudent
})

</script>

<template>
    <!-- <StudentList :students="STU_ARR" :fn="delStudentsByIndex"></StudentList> -->
    <!-- 可以将组件中的方法以自定义事件的形式发送给其它组件(方法用自定义事件传,数据用属性传) -->
    <!-- <StudentList :students="STU_ARR" @del-stu="delStudentsByIndex"></StudentList> -->
    <StudentList></StudentList>
    <hr>
    <StudentForm></StudentForm>
    <!-- <StudentForm @add-student="addNewStudent"></StudentForm> -->
</template>
```

StudentList

```vue
<script setup>
import StudentItem from './StudentItem.vue';

//通过defineProps定义的属性在$attrs中就不存在了
//被我们自定义了,所以不会透传了
//使用自定义属性时最好用defineProps来指定,这样组件拥有什么属性更加清晰
//透传适合的场景我现在还不知道....
//通过defineProps来接收父组件的students属性
// const props = defineProps(["students","fn"])
// const props = defineProps(["students"])
// const emits = defineEmits(["delStu"])

</script>

<template>
    <table>
        <caption>
            学生列表
        </caption>
        <thead>
            <tr>
                <th>学号</th>
                <th>性别</th>
                <th>年龄</th>
                <th>性别</th>
                <th>住址</th>
                <th>删除</th>
            </tr>
        </thead>
        <!-- 通过app传给list，在传给item 这种方式很麻烦 list要app这俩个数据根本没有用，还要先定义在传递 -->
        <!-- <StudentItem :students="props.students" @del-stu="emits('delStu',index)"></StudentItem> -->
        <!-- 我们使用透传也可实现这个效果,因为透传会一直往上找，找到item -->
        <!-- 注意事件的传递要加上$attrs.onXxxx -->
        <!-- 但是这样list还是要指定透传属性给item 太麻烦了 我们需要一个app直接传给item的东西 -->
        <!-- <StudentItem :students="$attrs.students" @del-stu="$attrs.onDelStu"></StudentItem> -->

        <!-- 依赖注入以后 不需要list来传值了 -->
        <StudentItem></StudentItem>
    </table>
</template>

<style scoped>
    table{
        width: 100%;
        border-collapse: collapse;
    }

    caption{
        font-size: 30px;
        font-weight: bold;
    }

    th{
        border: 1px solid black;
        text-align: center;
    }
</style>
```

StudentItem

```vue
<script setup>
import { inject } from 'vue';

//通过解构获取依赖注入的值
const {students,delStudentByIndex} = inject("student")

// const props = defineProps(["students"])

//定义自定义事件对象
//defineEmits用来接收父组件传过来的方法
// const emits = defineEmits(["delStu"])

//定义一个删除学生的方法
const delStuHandler = (index) => {
    if (confirm("确认删除吗?")) {
        //前面我们提到了props的属性虽然可以修改,但是最好是只读的不要动它
        //因为直接修改了父组件对象中的数据
        //props.students.splice(index,1)
        
        //开发中要遵循一个原则 自己的事情自己做
        //所以删除App的数据要由App来做,App提供一个删除的方法让大家调用
        //第一种方法是在App定义一个属性传给StudentList(但是这样不好,正常属性都是传值)
        // props.fn(index)

        //第二种方法是通过自定义事件(自定义事件在js和模板都可以使用)
        // emits('delStu',index)
        delStudentByIndex(index)
    }
}
</script>

<template>
            <tbody>
            <!-- 
                不推荐使用透传这种方式
                    -会造成一个问题:使用我们组件的人不知道组件中
                        有一个自定的:students属性
                    -建议使用自定义属性,这样使用我们的组件时会有提示
            -->
            <!-- <tr v-for="stu in $attrs.students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
            </tr> -->

            <!-- <tr v-for="(stu,index) in props.students"> -->
            <tr v-for="(stu,index) in students">
                <td>{{stu.id}}</td>
                <td>{{stu.name}}</td>
                <td>{{stu.age}}</td>
                <td>{{stu.gender}}</td>
                <td>{{stu.address}}</td>
                <!--
                    父子组件中的通信通过props和emit来完成
                        -父组件传递给子组件
                            -父组件传递属性给子组件 props
                            -父组件传递方法给子组件 emits

                        -子组件传递给父组件
                            -子组件传递给父组件(更友好,不违反props的单向数据原则) emit
                 -->
                <td>
                    <!-- <a href="#" @click.prevent="delStuHandler(index)">删除</a> -->

                    <!-- 在模板中可以通过$emit()来触发自定义事件 -->
                    <!-- index作为参数传过来(这是直接使用的方式,但是不要这样,别的组件使用我们并组件不知道有这个属性) -->
                    <!-- <a href="#" @click.prevent="$emit('delStu',index,$event)">删除</a> -->

                    <!-- 直接使用自定义事件对象 -->
                    <!-- <a href="#" @click.prevent="emits('delStu',index)">删除</a> -->

                    <!-- 调用js方法 js方法使用了自定义事件对象 -->
                    <a href="#" @click.prevent="delStuHandler(index)">删除</a>
                </td>
            </tr>
        </tbody>   
</template>

<style scoped>
    th,td{
        border: 1px solid black;
        text-align: center;
    }
</style>
```

StudentFrom

```vue
<script setup>
import { ref } from 'vue';
import { inject } from 'vue';

//通过解构获取依赖注入的值
// const{students,delStudentByIndex} = inject()    

    // const emits = defineEmits(["addStudent"])

    const {addNewStudent} = inject("student")

    //定义一个新的变量来存储新添加的数据
    const newStu = ref({
        name:"",
        age:1,
        gender:"男",
        address:""
    })
    const submitHandler = () => {
        //调用app添加数组的方法
        //为了避免响应式数据印象表单的数据，我们要对newStu转成非响应式对象
        //不处理的话，表单里的数据是响应式的，一变全部跟着变，浅复制只复制数据，不会复制响应式
        // emits("addStudent",Object.assign({},newStu.value))
        // emits("addStudent",{...newStu.value})

        addNewStudent({...newStu.value})

        //添加以后重置(因为表单现在是我们自己处理了，不是以前的默认行为重置表单)
        newStu.value.name = ""
        newStu.value.age = 1
        newStu.value.gender = "男"
        newStu.value.address = ""
        
    }
</script>
<template>
    <form @submit.prevent="submitHandler">
        <div>
            姓名: <input type="text" v-model="newStu.name">
        </div>
        <div>
            性别: 
            <input type="radio" name="gender" value="男"  v-model="newStu.gender">男 
            <input type="radio" name="gender" value="女" v-model="newStu.gender">女
        </div>
        <div>
            年龄: <input type="number" v-model="newStu.age">
        </div>
        <div>
            住址: <input type="text" v-model="newStu.address">
        </div>
        <div>
            <button>添加</button>
        </div>
    </form>
</template>
```



#### 25.状态(state)

#### 1.状态提升()

```vue
App
<script setup>
import Root from "./components/Root.vue"
</script>
<template>
    <h1>Hello Vue</h1>
    <Root></Root>
</template>
Root
<script setup>
import { provide, ref } from "vue"
import ComponentA from "./ComponentA.vue"
import ComponentB from "./ComponentB.vue"

//祖先元素定义了状态(数据) 这样通过子组件依赖注入或者属性传递等方式就都能访问到
const count = ref(0)
const increment = () => {
    count.value++
}

//通过依赖注入 传给所有子元素(不要先给B在给C)
provide("count", {
    count,
    increment
})
</script>
<template>
    <h2>根组件</h2>
    <ul>
        <li><ComponentA></ComponentA></li>
        <li><ComponentB></ComponentB></li>
    </ul>
</template>

ComponentA
<script setup>
import { inject, ref } from "vue"
// import { countStore } from "@/store/count"
// 引入store钩子
import { useCountStore } from "../store/countStore"

// const {count, increment} = inject("count")

// 获取store实例
const countStore = useCountStore()

/* 
    状态管理
        - 状态（state）
            - 应用当中的数据就是状态
            - 状态即数据
        - 视图（view）
            - 视图用来呈现数据，用户通过视图访问数据
        - 交互（actions）
            - 用户的操作
            - 状态会根据用户在视图中的操作发生变化

        - 在这个练习中 ref就是状态 tem模板就是视图 按钮就是交互

    -在这个练习中，App引用Root，Root引用了A、B，B引用了C  
        这就导致了AC之间产生了隔离，没办法使用依赖注入，管理同一个数据
        我们希望AC共同用一个数据
          -解决办法：提升状态
            - 当有多个组件需要使用到同一个state时，可以将state提升到这些组件共同的祖先组件(AC共同的祖先为Root)中声明
                这样一来所有这些组件便都可以通过祖先元素来访问到这个state
*/
</script>
<template>
    <!-- <h3>
        ComponentA --
        {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button>
    </h3> -->

    <h3>
        ComponentA2 --
        {{ countStore.count }} -- {{ countStore.double }} --
        {{ countStore.name }} --
        <button @click="countStore.increment">按钮</button>
    </h3>
</template>

ComponentB
<script setup>
import { ref } from "vue"
import ComponentC from "./ComponentC.vue"

const isShow = ref(true)
</script>
<template>
    <h3>ComponentB</h3>
    <ul>
        <li v-if="isShow"><ComponentC></ComponentC></li>
    </ul>
</template>

ComponentC
<script setup>
import { ref, inject } from "vue"
// import { countStore } from "../store/count"
// const { count, increment } = inject("count")

import { useStudentStore } from "@/store/studentStore.js"
import { storeToRefs } from "pinia"

const stuStore = useStudentStore()
/* 
    store实例本身就是一个reactive对象，
        可以通过它直接访问state中的数据
    
    但是如果直接将state中数据解构出来，那么数据将会丧失响应性

    可以通过storeToRefs()来对store进行解构，
        它可以将state和getters中的属性解构为ref属性，从而保留其响应性

    state的修改：
        1. 直接修改
        2. 通过$patch
        3. 通过$patch传函数的形式的修改
        4. 直接替换state
        5. 重置state
*/
// const { name, age } = stuStore

const { name, age, title } = storeToRefs(stuStore)

// state中的属性（方法），都可以通过store对象直接访问

const clickHandler = () => {
    stuStore.$patch({
        name: "孙小圣",
        age: 20,
        skills: ["救命毫毛"]
    })

    // stuStore.$patch((state) => {
    //     state.skills.push("救命毫毛")
    // })

    // stuStore.skills.push("哈哈")

    // stuStore.$patch({ name: "孙小圣" })
    // stuStore.$state = { name: "孙小圣" }
}

/* 
    store的订阅
        - 当store中的state发生变化时，做一些响应的操作
        - store.$subscribe(函数, 配置对象)
*/
stuStore.$subscribe(
    (mutation, state) => {
        // mutation 表示修改的信息
        // console.log(mutation.events)
        // console.log(mutation.events[0] === mutation.events[1])
        // console.log(mutation.payload)
        // if(state.token){
        //     // 登录，向本地存储中添加内容
        // }else{
        //     // 登出，从本地存储中移除内容
        // }
        // console.log("state发生变化了", state)
        // 使用订阅时不要在回调函数中直接修改state
        // state.age++
    },
    { detached: true }
)

// $onAction 用来订阅action的调用
stuStore.$onAction(({ name, store, args, after, onError }) => {
    /* 
        name 调用的action的名字
        store store的实例
        args action接收到的参数
        after() 可以设置一个回调函数，函数会在action成功调用后触发
        onError() 可以设置一个回调函数，函数会在action调用失败后触发
    */

    after(() => {
        console.log(name + "成功执行！")
    })

    onError((err) => {
        console.log(name + "执行失败！", err)
    })
})
</script>
<template>
    <h4>
        ComponentC -- {{ name }} -- {{ age }} -- {{ title }} --
        {{ stuStore.double }} --
        {{ stuStore.skills }}
        <!-- {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button> -->

        <button @click="stuStore.growUp">长大</button>

        <hr />

        <button @click="stuStore.name = '孙大圣'">修改name</button>
        <button @click="clickHandler">patch修改</button>
        <button @click="stuStore.$reset()">重置</button>
    </h4>
</template>

```

#### 2.创建状态

```css
/*
利用单例设计模式来解决上面状态提升不足的一些问题
什么是单例设计模式：
	单例模式，是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例的特殊类。通过单例模式可以保证系统中，应用该模式的类一个类只有一个实例。即一个类只有一个对象实例。
	单例设计模式是设计模式中最简单的形式之一，这一模式的目的是使得类的一个对象，成为系统中的唯一实例，要实现这一点，可以从客户端对其进行实例化开始，因此需要用一种只允许生成对象类的唯一实例的机制，阻止所有想要生成对象的访问，使用工厂方法来限制实例化过程，这个方法应该是静态方法，让类的实例去生成另一个唯一实例毫无意义。
	♥♥这样我们就可以保证系统只有这一份数据，还容易使用，避免了传递。
*/
```

手动创建单例

![uTools_1683548038471](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683548038471.png)

使用

![uTools_1683548099058](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683548099058.png)

![uTools_1683548086731](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683548086731.png)

使用这种手动的方式需要注意

![image-20230508202013868](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230508202013868.png)

![uTools_1683548463665](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1683548463665.png)

**这种方式在开发大型项目不够规范，大家都有自己的习惯，于是vue推出了pinia库**

#### 3.pinia(状态管理库)

##### 1.简介

**官网：[Pinia | The intuitive store for Vue.js (vuejs.org)](https://pinia.vuejs.org/zh/)**

**支持vue2vue3，不过引入的方式和使用的方式不相同。**



##### 2.基本使用(类似选项式API)

main.js

```js
import { createApp } from 'vue'
import App from './App.vue'
import {createPinia} from 'pinia'

/* 
    使用pinia的步骤
        1.安装pinia:yarn add pinia
        2.在主文件引入createPinia()
        3.通过createPinia()创建pinia实例
        4.将pinia配置为vue的插件
        5.创建store.js
        6.引入函数defineStore()
        7.创建store: const useCountStore = defineStore()
        8.在需要store的组件中引入store
*/

//通过createPinia()创建实例
const pinia = createPinia()
const app = createApp(App)
// 配置中间件
app.use(pinia)
app.mount('#app')

```

countStore.js

```js
//引入函数 defineStore()

import { defineStore } from "pinia";

//通过函数来创建store 创建出来别人引用的时候以函数形式
//创建的是一个钩子函数(别人的数据被我钩子到这里，命名规范是usexxxx)
//defineStore("store的唯一id",配置对象{})
/*
    配置对象:
        1.state 是一个函数，将需要由pinia维护的数据以对象的形式返回
        2.getter 计算属性
        3.actions 方法
*/
export const useCountStore = defineStore("count",{
        // 数据
        state: () => ({
            count: 100,
            name: "猪八戒"
        }),
    
        // 计算属性
        getters: {
            double: (state) => state.count * 2
        },
    
        // 方法
        actions: {
            increment() {
                this.count++
            }
        }
})
```

commpentA.vue

```vue
<script setup>
import { inject, ref } from "vue"
// import { countStore } from "@/store/count"
// const {count, increment} = inject("count")

// 引入store钩子
import { useCountStore } from "../store/countStore"

// 获取store实例 引用时useCountStore() 
const countStore = useCountStore()

</script>
<template>
    <!-- <h3>
        ComponentA --
        {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button>
    </h3> -->

    <h3>
        ComponentA2 --
        {{ countStore.count }} -- {{ countStore.double }} --
        {{ countStore.name }} --
        <button @click="countStore.increment">按钮</button>
    </h3>
</template>
```

##### 3.组合状态(组合式API)

```js
import { defineStore } from "pinia";
export const useCountStore = defineStore("count", () => {
     // 定义数据
     const count = ref(50)
     const name = ref("孙悟空")
     const double = computed(() => count.value * 2)
     function increment() {
         count.value++
     }

     return { count, name, double, increment }
 })
```

##### 4.store的解构

```js
const stuStore = useStudentStore()
/* 
    store实例本身就是一个reactive对象，
        可以通过它直接访问state中的数据
    
    但是如果直接将state中数据解构出来，那么数据将会丧失响应性

    可以通过storeToRefs()来对store进行解构，
        它可以将state和getters中的属性解构为ref属性，从而保留其响应性
        但是action无法解构，解构出来访问到的是undefined
*/
// const { name, age } = stuStore

const { name, age, title } = storeToRefs(stuStore)
```

##### 5.state的修改

##### 6.store的修改

##### 7.getter和action



**以下是完整的笔记 完整pinia**

###### **1.5，6，7笔记**

```vue
<script setup>
import { ref, inject } from "vue"
// import { countStore } from "../store/count"
// const { count, increment } = inject("count")

import { useStudentStore } from "@/store/studentStore.js"
import { storeToRefs } from "pinia"

const stuStore = useStudentStore()
/* 
    store实例本身就是一个reactive对象，
        可以通过它直接访问state中的数据
    
    但是如果直接将state中数据解构出来，那么数据将会丧失响应性

    可以通过storeToRefs()来对store进行解构，
        它可以将state和getters中的属性解构为ref属性，从而保留其响应性

    state的修改：
        1. 直接修改
        2. 通过$patch(它是直接替换掉所有)
        3. 通过$patch传函数的形式的修改
        4. 直接替换state
        5. 重置state(所有值恢复到原始)
*/
// const { name, age } = stuStore

const { name, age, title } = storeToRefs(stuStore)

// state中的属性（方法），都可以通过store对象直接访问

const clickHandler = () => {
    stuStore.$patch({
        name: "孙小圣",
        age: 20,
        skills: ["救命毫毛"]
    })

    // stuStore.$patch((state) => {
    //     state.skills.push("救命毫毛")
    // })

    //直接修改
    // stuStore.skills.push("哈哈")

    // stuStore.$patch({ name: "孙小圣" })
    //直接替换
    // stuStore.$state = { name: "孙小圣" }
}

/* 
    store的订阅
        - 当store中的state发生变化时，做一些响应的操作
        - store.$subscribe(函数, 配置对象)
        - 没有配置对象的时候默认本组件卸载store也随着卸载(订阅就失效了)
        - 监视state和getter 因为他们俩个改了就会触发store的变化
*/
stuStore.$subscribe(
    (mutation, state) => {
        // mutation 表示修改的信息  mutation.type表示修改的类型  mutation.event表示修改事件
        //mutation.payload 可以读取到patch传递的参数
        // console.log(mutation.events)
        // console.log(mutation.events[0] === mutation.events[1])
        // console.log(mutation.payload)

        // if(state.token){
        //     // 登录，向本地存储中添加内容
        // }else{
        //     // 登出，从本地存储中移除内容
        // }
        // console.log("state发生变化了", state)
        // 使用订阅时不要在回调函数中直接修改state(修改state就会触发修改状态 进入死循环)
        // state.age++
    },
    { detached: true }
)

// $onAction 用来订阅action的调用
stuStore.$onAction(({ name, store, args, after, onError }) => {
    /* 
        name 调用的action的名字
        store store的实例
        args action接收到的参数
        after() 可以设置一个回调函数，函数会在action成功调用后触发
        onError() 可以设置一个回调函数，函数会在action调用失败后触发
    */

    after(() => {
        console.log(name + "成功执行！")
    })

    onError((err) => {
        console.log(name + "执行失败！", err)
    })
})
</script>
<template>
    <h4>
        ComponentC -- {{ name }} -- {{ age }} -- {{ title }} --
        {{ stuStore.double }} --
        {{ stuStore.skills }}
        <!-- {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button> -->

        <button @click="stuStore.growUp">长大</button>

        <hr />

        <button @click="stuStore.name = '孙大圣'">修改name</button>
        <button @click="clickHandler">patch修改</button>
        <!-- 重置state -->
        <button @click="stuStore.$reset()">重置</button>
    </h4>
</template>
```

```js
import { defineStore } from "pinia"

export const useStudentStore = defineStore("student", {
    state: () => ({
        name: "孙悟空",
        age: 18,
        gender: "男",
        address: "花果山",
        skills: ["七十二变", "筋斗云", "金箍棒"]
    }),

    getters: {
        title: (state) => {
            return "Mr. " + state.name
        },

        //也可以直接用函数 不用箭头函数
        double() {
            return this.age * 2
        }
    },

    actions: {
        //actions里面不要用箭头函数 用不了this
        growUp() {
            throw new Error("出错了！")
            this.age++
        }
    }
})
```





###### 2.完整笔记 例子

Main.js

```js
import { createPinia } from "pinia"
import { createApp } from "vue"
import App from "./App.vue"

/* 
    使用pinia的步骤
        1. 安装pinia
        2. 在main.js中引入createPinia()
        3. 通过createPinia()创建pinia实例
        4. 将pinia配置为vue的插件
*/

const pinia = createPinia()

const app = createApp(App)

// 将pinia设置为vue的插件
app.use(pinia)

app.mount("#app")
```

countStore.js

```js
// 引入函数 defineStore()
import { defineStore } from "pinia"
import { computed, ref } from "vue"

// 通过函数来创建store
//defineStore("store的唯一id",配置对象{})
//创建的是一个钩子函数(别人的数据被我钩子到这里，命名规范是usexxxx)
// defineStore("store的id", 配置对象)
// 配置对象：state，是一个函数，将需要由pinia维护的数据以对象的形式返回
export const useCountStore = defineStore("count", {
    // 数据
    state: () => ({
        count: 100,
        name: "猪八戒"
    }),

    // 计算属性
    getters: {
        double: (state) => state.count * 2
    },

    // 方法
    actions: {
        increment() {
            this.count++
        }
    }
})

// export const useCountStore = defineStore("count", () => {
//     // 定义数据
//     const count = ref(50)
//     const name = ref("孙悟空")
//     const double = computed(() => count.value * 2)
//     function increment() {
//         count.value++
//     }

//     return { count, name, double, increment }
// })

```

studentStore.js

```js
import { defineStore } from "pinia"

export const useStudentStore = defineStore("student", {
    state: () => ({
        name: "孙悟空",
        age: 18,
        gender: "男",
        address: "花果山",
        skills: ["七十二变", "筋斗云", "金箍棒"]
    }),

    getters: {
        title: (state) => {
            return "Mr. " + state.name
        },

        //也可以直接用函数 不用箭头函数
        double() {
            return this.age * 2
        }
    },

    actions: {
        //actions里面不要用箭头函数 用不了this
        growUp() {
            throw new Error("出错了！")
            this.age++
        }
    }
})
```

Root.vue

```vue
<script setup>
import { provide, ref } from "vue"
import ComponentA from "./ComponentA.vue"
import ComponentB from "./ComponentB.vue"

//祖先元素定义了状态(数据) 这样通过子组件依赖注入或者属性传递等方式就都能访问到
const count = ref(0)
const increment = () => {
    count.value++
}

//通过依赖注入 传给所有子元素(不要先给B在给C)
provide("count", {
    count,
    increment
})
</script>
<template>
    <h2>根组件</h2>
    <ul>
        <li><ComponentA></ComponentA></li>
        <li><ComponentB></ComponentB></li>
    </ul>
</template>
```

ComponentA.vue

```vue
<script setup>
import { inject, ref } from "vue"
// import { countStore } from "@/store/count"
// 引入store钩子
import { useCountStore } from "../store/countStore"

// const {count, increment} = inject("count")

// 获取store实例
const countStore = useCountStore()

/* 
    状态管理
        - 状态（state）
            - 应用当中的数据就是状态
            - 状态即数据
        - 视图（view）
            - 视图用来呈现数据，用户通过视图访问数据
        - 交互（actions）
            - 用户的操作
            - 状态会根据用户在视图中的操作发生变化

        - 在这个练习中 ref就是状态 tem模板就是视图 按钮就是交互

    -在这个练习中，App引用Root，Root引用了A、B，B引用了C  
        这就导致了AC之间产生了隔离，没办法使用依赖注入，管理同一个数据
        我们希望AC共同用一个数据
          -解决办法：提升状态
            - 当有多个组件需要使用到同一个state时，可以将state提升到这些组件共同的祖先组件(AC共同的祖先为Root)中声明
                这样一来所有这些组件便都可以通过祖先元素来访问到这个state
*/
</script>
<template>
    <!-- <h3>
        ComponentA --
        {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button>
    </h3> -->

    <h3>
        ComponentA2 --
        {{ countStore.count }} -- {{ countStore.double }} --
        {{ countStore.name }} --
        <button @click="countStore.increment">按钮</button>
    </h3>
</template>
```

ComponentB.vue

```VUE
<script setup>
import { ref } from "vue"
import ComponentC from "./ComponentC.vue"

const isShow = ref(true)
</script>
<template>
    <h3>ComponentB</h3>
    <ul>
        <li v-if="isShow"><ComponentC></ComponentC></li>
    </ul>
</template>

```

ComponentC.vue

```vue
<script setup>
import { ref, inject } from "vue"
// import { countStore } from "../store/count"
// const { count, increment } = inject("count")

import { useStudentStore } from "@/store/studentStore.js"
import { storeToRefs } from "pinia"

const stuStore = useStudentStore()
/* 
    store实例本身就是一个reactive对象，
        可以通过它直接访问state中的数据
    
    但是如果直接将state中数据解构出来，那么数据将会丧失响应性

    可以通过storeToRefs()来对store进行解构，
        它可以将state和getters中的属性解构为ref属性，从而保留其响应性

    state的修改：
        1. 直接修改
        2. 通过$patch(它是直接替换掉所有)
        3. 通过$patch传函数的形式的修改
        4. 直接替换state
        5. 重置state(所有值恢复到原始)
*/
// const { name, age } = stuStore

const { name, age, title } = storeToRefs(stuStore)

// state中的属性（方法），都可以通过store对象直接访问

const clickHandler = () => {
    stuStore.$patch({
        name: "孙小圣",
        age: 20,
        skills: ["救命毫毛"]
    })

    // stuStore.$patch((state) => {
    //     state.skills.push("救命毫毛")
    // })

    //直接修改
    // stuStore.skills.push("哈哈")

    // stuStore.$patch({ name: "孙小圣" })
    //直接替换
    // stuStore.$state = { name: "孙小圣" }
}

/* 
    store的订阅
        - 当store中的state发生变化时，做一些响应的操作
        - store.$subscribe(函数, 配置对象)
        - 没有配置对象的时候默认本组件卸载store也随着卸载(订阅就失效了)
        - 监视state和getter 因为他们俩个改了就会触发store的变化
*/
stuStore.$subscribe(
    (mutation, state) => {
        // mutation 表示修改的信息  mutation.type表示修改的类型  mutation.event表示修改事件
        //mutation.payload 可以读取到patch传递的参数
        // console.log(mutation.events)
        // console.log(mutation.events[0] === mutation.events[1])
        // console.log(mutation.payload)

        // if(state.token){
        //     // 登录，向本地存储中添加内容
        // }else{
        //     // 登出，从本地存储中移除内容
        // }
        // console.log("state发生变化了", state)
        // 使用订阅时不要在回调函数中直接修改state(修改state就会触发修改状态 进入死循环)
        // state.age++
    },
    { detached: true }
)

// $onAction 用来订阅action的调用
stuStore.$onAction(({ name, store, args, after, onError }) => {
    /* 
        name 调用的action的名字
        store store的实例
        args action接收到的参数
        after() 可以设置一个回调函数，函数会在action成功调用后触发
        onError() 可以设置一个回调函数，函数会在action调用失败后触发
    */

    after(() => {
        console.log(name + "成功执行！")
    })

    onError((err) => {
        console.log(name + "执行失败！", err)
    })
})
</script>
<template>
    <h4>
        ComponentC -- {{ name }} -- {{ age }} -- {{ title }} --
        {{ stuStore.double }} --
        {{ stuStore.skills }}
        <!-- {{ countStore.count }} --
        <button @click="countStore.increment">按钮</button> -->

        <button @click="stuStore.growUp">长大</button>

        <hr />

        <button @click="stuStore.name = '孙大圣'">修改name</button>
        <button @click="clickHandler">patch修改</button>
        <!-- 重置state -->
        <button @click="stuStore.$reset()">重置</button>
    </h4>
</template>
```



###### 3.getter补充

![uTools_1684405346729](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1684405346729.png)

![uTools_1684405365775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1684405365775.png)

#### 26.Teleport

```css
<Teleport> 是一个内置组件，它可以将一个组件内部的一部分模板“传送”到该组件的 DOM 结构外层的位置去。
```

![uTools_1685203491692](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685203491692.png)

![uTools_1685203588728](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685203588728.png)

![image-20230701230410098](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701230410098.png)



#### 27.Suspense

![image-20230701230724156](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701230724156.png)

![image-20230701230756566](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701230756566.png)

![image-20230701230844132](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701230844132.png)

![image-20230701230940353](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701230940353.png)



### 补充：ref的其它使用:用来挂载节点

![image-20230809152853471](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809152853471.png)

标准组件的写法中，子组件的数据和方法return以后，父组件可以通过`组件.value.数据`的方式直接操作子组件的数据

但是在语法糖的写法中，默认只能在模板中使用，要用defineExpose API暴露后才能使用

**没有有语法糖时的写法**

```vue
B1.vue
<template>
{{ childRef }}
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup(){
    const childRef = 10
    return{
      childRef
    }
  }
})
</script>

```

![image-20230809151928231](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809151928231.png)



**有语法糖时**

```vue
B1.vue
<template>
{{ msg }}
</template>

<script lang="ts" setup>
const msg = 'Hello World'

//可以通过defineExpose直接暴露父组件使用
defineExpose({
  msg
})
</script>

```



```vue
APP.vue
<template>
  <B1 ref="child"></B1>
  <br>
  {{ child?.msg }}
</template>

<script setup lang="ts">
import { ref } from 'vue'
import B1 from './components/x/B1.vue';
import { onMounted } from 'vue';
const child = ref<InstanceType<typeof B1>>()
onMounted(()=>{
   console.log(child.value?.childRef);
})

</script>
```















































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



**插槽是怎么实现的**

```bash
oop面向对象原则
 1.开闭原则(对修改关闭，对扩展开启)
 2.单一原则(一个组件处理一个问题)
```

