# 1.小满路由教学

## 1.什么是路由

![image-20230701182533859](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701182533859.png)



## 2.安装与简单使用

**前言**

router 路由

应为 vue 是单页应用不会有那么多 html 让我们跳转 所有要使用路由做页面的跳转

Vue 路由允许我们通过不同的 URL 访问不同的内容。通过 Vue 可以实现多视图的单页 Web 应用

```
npm i vue-router --save
//注意Vue2与Vue3的路由是互不兼容的，使用Vue3请使用Router4
```

**安装**

构建 前端项目

```
npm init vue@latest
//或者
npm init vite@latest
```

使用 Vue3 安装对应的 router4 版本 使用 Vue2 安装对应的 router3 版本

```
npm install vue-router@4
```

在 src 目录下面新建 router 文件 然后在 router 文件夹下面新建 index.ts

```typescript
//引入路由对象
import { createRouter, createWebHistory, createWebHashHistory, createMemoryHistory, RouteRecordRaw } from 'vue-router'

//vue2 mode history vue3 createWebHistory
//vue2 mode  hash  vue3  createWebHashHistory
//vue2 mode abstact vue3  createMemoryHistory

//路由数组的类型 RouteRecordRaw
// 定义一些路由
// 每个路由都需要映射到一个组件。
const routes: Array<RouteRecordRaw> = [{
  path: '/',
  component: () => import('../components/Login.vue') //lazy 懒加载
}, {
  path: '/register',
  component: () => import('../components/Register.vue')
}]



const router = createRouter({
  history: createWebHistory(),
  routes
})

//导出router
export default router
```

### 1.router-link

**router-link称为声明式导航和导航链接  可以高亮显示也可以进行动态传参**

请注意，我们没有使用常规的 a 标签，而是使用一个自定义组件 `router-link` 来创建链接。 这使得 Vue Router 可以在不重新加载页面的情况下更改 URL，处理 URL 的生成以及编码。我们将在后面看到如何从这些功能中获益。

`router-view#` router-view 将显示与 url 对应的组件。你可以把它放在任何地方，以适应你的布局。

```vue
<template>
  <div>
    <h1>小满最骚</h1>
    <div>
    <!--使用 router-link 组件进行导航 -->
    <!--通过传递 `to` 来指定链接 -->
    <!--`<router-link>` 将呈现一个带有正确 `href` 属性的 `<a>` 标签-->
      <router-link tag="div" to="/">跳转a</router-link>
      <router-link tag="div" style="margin-left:200px" to="/register">跳转b</router-link>
    </div>
    <hr />
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </div>
</template>
```

最后在 main.ts 挂载

```typescript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
createApp(App).use(router).mount('#app')
```



## 3.路由的跳转方式

   1. 普通的通过path跳转()

   2. name 命名跳转

   ![uTools_1688207515922](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1688207515922.png)

   3. 编程式导航

   ​     ![image-20230701203443904](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701203443904.png)

      4. a标签也可以直接跳转

![uTools_1688214931738](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1688214931738.png)



## 4.replace 不保存历史记录路由

![image-20230701204134706](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701204134706.png)

## ![image-20230701204144692](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701204144692.png)



## 5.路由传参

### 1.query

![image-20230701205508671](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701205508671.png)

![image-20230701205520457](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701205520457.png)

**不足的地方是--传值会出现在地址栏**



### 2.动态路由传参(根据不同用户的身份跳转)

**假设要访问http://xx/id**

![image-20230701205708480](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701205708480.png)

![image-20230701205728788](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701205728788.png)

**在router-link中进行动态跳转**

![image-20230701210216273](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701210216273.png)



## 6.嵌套路由(父子路由)

index.ts

![image-20230701210553608](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701210553608.png)

footer.vue

![image-20230701210618223](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701210618223.png)

**如果父路由的path参数为"/"时 就不用带前缀/user**



## 7.命名视图(类似插槽)

![image-20230701210956531](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701210956531.png)

**此时根据具体的需求会走不同的出口，走哪个出口就展示哪个组件，默认走default**

![image-20230701211041529](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211041529.png)

跳转后就会走不同的出口 user1有出口  user2也有出口

![image-20230701211205140](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211205140.png)



## 8.重定向

![image-20230701211441469](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211441469.png)

配置方式

![image-20230701211457813](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211457813.png)

![image-20230701211511130](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211511130.png)

![image-20230701211527927](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211527927.png)

**to这个参数带的信息就是父路由的信息**

**重定向时可以参数，重定向后会出现在url地址栏中**

![image-20230701211732933](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211732933.png)



**为路由起别名**

![image-20230701211759689](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701211759689.png)

### 1.例子：不同用户不同跳转

![image-20230715003445174](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715003445174.png)



## 9.前置导航路由(beforeEach)

main.ts

```ts
import { createApp } from 'vue'
// import './style.css'
import App from './App.vue'
import router from './router'
import ElementUi from 'element-plus'
import 'element-plus/dist/index.css'

const app = createApp(App)


app.use(router)
app.use(ElementUi)

const whiteList = ['/']

//全局前置守卫
router.beforeEach((to, from, next) => {
  let token = localStorage.getItem('token')
  //白名单 有值 或者登陆过存储了token信息可以跳转 否则就去登录页面
  if (whiteList.includes(to.path) || token) { //token每次都要跟后端校验一下是否过期
    //另外说一下beforeEach可以定义不止一个，vue会收集你所有定义的路由钩子，所以next的作用不应该是跳转，而是使步骤进行到下一个你定义的钩子
    next()
  } else {
    next('/')
  }
})


app.mount('#app')
```

App.vue

```vue
<template>
  <router-view></router-view>

</template>

<script setup lang='ts'>
import { ref, reactive } from 'vue'

</script>

<style>
* {
  padding: 0;
  margin: 0;
}

html,
body,
#app {
  height: 100%;
  overflow: hidden;
}
</style>
```

views/Login.vue

```vue
<template>

  <div class="login">
    <!-- ref用于给组件命名 -->
    <el-form ref="form" :rules="rules" :model="formInline" class="demo-form-inline">
      <el-form-item prop="user" label="账号：">
        <!-- element-ui中的form提供了表单验证功能，只需要通过rules属性传入约定的验证规则，
        并将form-item中的prop属性设置成需校验的字段名即可。 -->
        <el-input v-model="formInline.user" placeholder="请输入账号" />
      </el-form-item>
      <el-form-item prop="password" label="密码：">
        <el-input v-model="formInline.password" placeholder="请输入密码" type="password" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">登陆</el-button>
      </el-form-item>
    </el-form>
  </div>

</template>
<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'
import router from '../router';
import { ElMessage, FormRules, FormInstance } from 'element-plus'


const formInline = reactive({
  user: '',
  password: '',
})


const form = ref<FormInstance>()

const rules: FormRules = reactive({
  user: [{
    required: true,
    message: "请输入账号",
    type: "string"
  }],
  password: [{
    required: true,
    message: "请输入密码",
    type: "string"
  }]
})

const onSubmit = () => {
  console.log('submit!', form.value)
    //validate饿了么ui内置的验证函数
  form.value?.validate((validate) => {
      //判断是否通过验证
    if (validate) {
        //登录后跳转
      router.push('/index')
      localStorage.setItem('token', '1')
    } else {
      ElMessage.error('请输入完整')
    }
  })

}
</script>

<style lang='less' scoped>
.login {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
```

views/index.vue

```vue
<template>

  <div>
    哈哈，我进来了
  </div>

</template>

<script setup lang='ts'>
import { ref, reactive } from 'vue'

</script>

<style lang='less' scoped>

</style>
```

router/index.ts

```ts
//引入路由对象
import { createRouter, createWebHistory, createWebHashHistory, createMemoryHistory, RouteRecordRaw } from 'vue-router'

const routes: Array<RouteRecordRaw> = []


const router = createRouter({
  history: createWebHistory(),
  routes: [//配置信息
    {
      path: '/',
      component: () => import('@/views/Login.vue')
    },
    {
      path: '/index',
      component: () => import('@/views/index.vue')
    }
  ]
})

//导出router
export default router
```



## 10.后置导航路由(afterEach)

src/main.ts

```ts
import { createApp, createVNode, render } from 'vue'
// import './style.css'
import App from './App.vue'
import router from './router'
import ElementUi from 'element-plus'
import 'element-plus/dist/index.css'
import loadingBarVue from './components/loadingBar.vue'

console.log(loadingBarVue); //不能直接使用
// createVNode函数创建dom节点
const Vnode = createVNode(loadingBarVue) //转成虚拟Dom
// render用来将dom元素挂载到body上(挂载上了才能使用该元素带的方法)
render(Vnode, document.body) //挂载


const app = createApp(App)


const whiteList = ['/']

//全局前置守卫
router.beforeEach((to, from, next) => {

  Vnode.component?.exposed?.startLoading() //loadingBar

  let token = localStorage.getItem('token')
  //白名单 有值 或者登陆过存储了token信息可以跳转 否则就去登录页面
  if (whiteList.includes(to.path) || token) { //token每次都要跟后端校验一下是否过期
  }
})

//全局后置守卫  切换之后调用
router.afterEach((to, from) => {
    // 跳转的时候走完后面的动画效果
  Vnode.component?.exposed?.endLoading()
})

app.mount('#app')
```

src/components/loadingBar.vue

```vue
<template>

  <div class="wraps">
    <div ref="bar" class="bar"></div>
  </div>

</template>

<script setup lang='ts'>
import { ref, reactive, onMounted } from 'vue'

let speed = ref<number>(1)
let bar = ref<HTMLElement>()
let timer = ref<number>(0) //设置id

const startLoading = () => {
  let dom = bar.value as HTMLElement
  speed.value = 1
  console.log(dom);
  timer.value = window.requestAnimationFrame(function fn() {//不用箭头函数的原因，递归
    if (speed.value < 90) {
      speed.value += 1;
      dom.style.width = speed.value + '%'
      timer.value = window.requestAnimationFrame(fn) //递归
    } else {
      speed.value = 1;
      window.cancelAnimationFrame(timer.value)
    }
  })

}
const endLoading = () => {
  let dom = bar.value as HTMLElement
  setTimeout(() => {
    window.requestAnimationFrame(() => {
      speed.value = 100;
      dom.style.width = speed.value + '%'
    })
  }, 1000)


}
// 放到全局导航守卫-后置守卫 后不需要了
// //只有在 onMounted 之后才能获取 DOM
// onMounted(() => {
//   startLoading()
//   endLoading()
// })

defineExpose({
  startLoading,
  endLoading,
})

</script>

<style lang='less' scoped>
.wraps {
  position: fixed;
  top: 0;
  width: 100%;
  height: 2px;

  .bar {
    height: inherit;
    width: 0;
    background: blue;
  }
}
</style>
```



## 11.路由元信息(meta)

![image-20230701212941163](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701212941163.png)

![image-20230701212953780](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701212953780.png)

![image-20230701213033900](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701213033900.png)

## 12.路由过渡动效

想要在你的路径组件上使用转场，并对导航进行动画处理，你需要使用 [v-slot API](https://router.vuejs.org/zh/api/#router-view-s-v-slot)：

使用 `animate.css`

main.ts

```ts
import 'animate.css'
```

src/App.vue

```vue
    //route就是当前的生效的路由 component就是Vnode
	<router-view #default="{route,Component}">//v-slot
        //${route.meta.transition} 会根据不同的值对不同的组件产生不同的效果
        <transition :enter-active-class="`animate__animated ${route.meta.transition}`">
            <component :is="Component"></component>
        </transition>
    </router-view>
```

上面的用法会对所有的路由使用相同的过渡。如果你想让每个路由的组件有不同的过渡，你可以将[元信息](https://router.vuejs.org/zh/guide/advanced/meta.html)和动态的 `name` 结合在一起，放在`<transition>` 上：

```ts
declare module 'vue-router'{
     interface RouteMeta {
        title:string,
        transition:string,
     }
}
 
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      component: () => import('@/views/Login.vue'),
      meta:{
         title:"登录页面",
          //不同的动态效果
         transition:"animate__fadeInUp",
      }
    },
    {
      path: '/index',
      component: () => import('@/views/Index.vue'),
      meta:{
         title:"首页！！！",
          //不同的动态效果
         transition:"animate__bounceIn",
      }
    }
  ]
})
```

## 13.鼠标滚动事件

![image-20230701213708804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230701213708804.png)

## 14.动态路由

我们一般使用动态路由都是后台会返回一个 路由表 )前端通过调接口拿到后处理(后端处理路由)

主要使用的方法就是 `router.addRoute`

**添加路由**

动态路由主要通过两个函数实现。`router.addRoute()` 和 `router.removeRoute()`。

它们只注册一个新的路由，也就是说，如果新增加的路由与当前位置相匹配，就需要你用 `router.push()` 或 `router.replace()` 来手动导航，才能显示该新路由

```
router.addRoute({ path: '/about', component: About })
```

**删除路由**

有几个不同的方法来删除现有的路由：

- 通过添加一个名称冲突的路由。如果添加与现有途径名称相同的途径，会先删除路由，再添加路由：

```
router.addRoute({ path: '/about', name: 'about', component: About })
// 这将会删除之前已经添加的路由，因为他们具有相同的名字且名字必须是唯一的
router.addRoute({ path: '/other', name: 'about', component: Other })
```

- 通过调用 `router.addRoute()` 返回的回调：

```
const removeRoute = router.addRoute(routeRecord)
removeRoute() // 删除路由如果存在的话
```

当路由没有名称时，这很有用。

- 通过使用 `router.removeRoute()` 按名称删除路由：

```
router.addRoute({ path: '/about', name: 'about', component: About })
// 删除路由
router.removeRoute('about')
```

需要注意的是，如果你想使用这个功能，但又想避免名字的冲突，可以在路由中使用 `Symbol` 作为名字。

当路由被删除时，**所有的别名和子路由也会被同时删除**

**查看现有路由**

Vue Router 提供了两个功能来查看现有的路由：

- [router.hasRoute()](https://router.vuejs.org/zh/api/#hasroute)：检查路由是否存在。
- [router.getRoutes()](https://router.vuejs.org/zh/api/#getroutes)：获取一个包含所有路由记录的数组。





## 15.动态路由例子

**前端接收数据**

需要安装 `npm install axios -S`

src/views/Login.vue

```vue
<template>
  <div class="login">

    <el-form ref="form" :rules="rules" :model="formInline" class="demo-form-inline">
      <el-form-item prop="user" label="账号：">
        <el-input v-model="formInline.user" placeholder="请输入账号" />
      </el-form-item>
      <el-form-item prop="password" label="密码：">
        <el-input v-model="formInline.password" placeholder="请输入密码" type="password" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">登陆</el-button>
      </el-form-item>
    </el-form>
  </div>

</template>


<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'
// import router from '../router';
import { ElMessage, FormRules, FormInstance } from 'element-plus'
import loadingBar from '../components/loadingBar.vue';
import axios from 'axios'
const router = useRouter()

const formInline = reactive({
  user: '',
  password: '',
})


const form = ref<FormInstance>()

const rules: FormRules = reactive({
  user: [{
    required: true,
    message: "请输入账号",
    type: "string"
  }],
  password: [{
    required: true,
    message: "请输入密码",
    type: "string"
  }]
})

const onSubmit = () => {
  console.log('submit!', form.value)
  form.value?.validate((validate) => {
    if (validate) {
      initRouter()

      // router.push('/index')
      localStorage.setItem('token', '1')
    } else {
      ElMessage.error('请输入完整')
    }
  })

}

/**
 * 一般是单独的ts页面编写，这里合起来了
 */
const initRouter = async () => {
  const result = await axios.get('http://localhost:9999/login', { params: formInline });

  const data = result.data //连起来不让写

  //要对结果作判断，返回路由还是错误提示
  if (data.code === 400) {
    alert(data.mesage)
    return
  }

  //进行动态分发路由
  //判断有没有数据 如果是正确的账号密码 就会为它分发除/和/index以外的路由
  data.route.forEach((v: any) => {
    router.addRoute({
      path: v.path,
      name: v.name,
      //这儿不能使用@  这里是拼接路由
      component: () => import(`@/views/${v.component}`)
    })
    router.push('/index')
  })

  console.log(router.getRoutes());

}

</script>

<style lang='less' >
.login {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
```

**后端发送数据**

需要安装 `npm install express -S`

启动 `npm run dev `

```ts
import express, { Express, Request, Response } from 'express'

const app: Express = express()

app.get('/login', (req: Request, res: Response) => {
  res.header("Access-Control-Allow-Origin", "*");
  if (req.query.user == 'admin' && req.query.password == '123456') {
    res.json({
      route: [
        {
          path: "/demo1",
          name: "Demo1",
          component: 'demo1.vue'
        },
        {
          path: "/demo2",
          name: "Demo2",
          component: 'demo2.vue'
        },
        {
          path: "/demo3",
          name: "Demo3",
          component: 'demo3.vue'
        }
      ]
    })
  } else {
    res.json({
      code: 400,
      mesage: "账号密码错误"
    })
  }
})

app.listen(9999, () => {
  console.log('http://localhost:9999');

})
```



# 2.补充

## 1.404路由

![image-20230715003959347](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715003959347.png)

![image-20230715003638152](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715003638152.png)

## 2.前置导航的应用例子

**切换路由时改变标题**

![image-20230715151721802](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715151721802.png)

![image-20230715151735981](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715151735981.png)

**用户权限**

![image-20230715152754881](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715152754881.png)

**跳转权限**

![image-20230715152851129](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715152851129.png)

## 3.使用中时需要导航

![image-20230715225522512](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715225522512.png)

![image-20230715225535212](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715225535212.png)

## 4.后置守卫

![image-20230715225648473](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715225648473.png)

## 5.其它

### 1.在组件中使用全局钩子

![image-20230715225833787](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715225833787.png)

### 2.独享钩子(路由定制钩子)

![image-20230715225950557](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715225950557.png)

![image-20230715230009969](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230009969.png)

### 3.组件内单独使用(非全局)

![image-20230715230205254](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230205254.png)

![image-20230715230239578](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230239578.png)



![image-20230715230258960](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230258960.png)



## 6.路由侦听

**watch**

![image-20230715230412237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230412237.png)

![image-20230715230430036](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230430036.png)

**watchEffect**

![image-20230715230615166](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715230615166.png)

## 7.express部署vue3+router项目

<img src="https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715231008274.png" alt="image-20230715231008274" style="zoom:33%;" />



## 8.关于路由器模式

**大部分情况下我们要用history模式，但是他部署容易出错，可以去官网看一下怎么调整部署**

![image-20230715231234130](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230715231234130.png)

## 9.$router和￥route

$router push replace 这些跳转方法

$route获取 params参数 query对象....

![image-20230924225037626](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230924225037626.png)