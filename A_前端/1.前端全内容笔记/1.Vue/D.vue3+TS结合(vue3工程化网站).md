# Vue3入门指南与实战案例

## 1.前端工程化入门教程

### 1.了解前端工程化

#### ①不用前端工程化的弊端

1. 如本案例，可能存在同名的变量声明，引起变量冲突
2. 引入多个资源文件时，比如有多个 JS 文件，在其中一个 JS 文件里面使用了在别处声明的变量，无法快速找到是在哪里声明的，大型项目难以维护
3. 类似第 1 、 2 点提到的问题无法轻松预先感知，很依赖开发人员人工定位原因
4. 大部分代码缺乏分割，比如一个工具函数库，很多时候需要整包引入到 HTML 里，文件很大，然而实际上只需要用到其中一两个方法
5. 由第 4 点大文件延伸出的问题， script 的加载从上到下，容易阻塞页面渲染
6. 不同页面的资源引用都需要手动管理，容易造成依赖混乱，难以维护
7. 如果要压缩 CSS 、混淆 JS 代码，也是要人力操作使用工具去一个个处理后替换，容易出错



#### ②工程化带来的优势

**1.开发层面**

1. 引入了模块化和包的概念，作用域隔离，解决了代码冲突的问题
2. 按需导出和导入机制，让编码过程更容易定位问题
3. 自动化的代码检测流程，有问题的代码在开发过程中就可以被发现
4. 编译打包机制可以让使用开发效率更高的编码方式，比如 Vue 组件、 CSS 的各种预处理器
5. 引入了代码兼容处理的方案（ e.g. Babel ），可以让自由使用更先进的 JavaScript 语句，而无需顾忌浏览器兼容性，因为最终会帮转换为浏览器兼容的实现版本
6. 引入了 Tree Shaking 机制，清理没有用到的代码，减少项目构建后的体积



**2.团队协作的优势**

1. 统一的项目结构

![uTools_1685369649369](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685369649369.png)

2. 统一的代码风格(比如vue的模板语句)
3. 可复用的模块和组件
4. 代码的健壮性
5. 团队开发效率高



#### ③Vue3.js与工程化

###### **1.vue单网页使用**

```vue
<!-- 这是使用 Vue 实现的 demo -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello Vue</title>
    <script src="https://unpkg.com/vue@3"></script>
  </head>
  <body>
    <div id="app">
      <!-- 通过 `{{ 变量名 }}` 语法渲染响应式变量 -->
      <p>Hello {{ name }}!</p>

      <!-- 通过 `v-model` 双向绑定响应式变量 -->
      <!-- 通过 `@input` 给输入框绑定输入事件 -->
      <input
        type="text"
        v-model="name"
        placeholder="输入名称打招呼"
        @input="printLog"
      />

      <!-- 通过 `@click` 给按钮绑定点击事件 -->
      <button @click="reset">重置</button>
    </div>

    <script>
      const { createApp, ref } = Vue
      createApp({
        // `setup` 是一个生命周期钩子
        setup() {
          // 默认值
          const DEFAULT_NAME = 'World'

          // 用于双向绑定的响应式变量
          const name = ref(DEFAULT_NAME)

          // 打印响应式变量的值到控制台
          function printLog() {
            // `ref` 变量需要通过 `.value` 操作值
            console.log(name.value)
          }

          // 重置响应式变量为默认值
          function reset() {
            name.value = DEFAULT_NAME
            printLog()
          }

          // 需要 `return` 出去才可以被模板使用
          return { name, printLog, reset }
        },
      }).mount('#app')
    </script>
  </body>
</html>
```

![uTools_1685369889003](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685369889003.png)

###### 2.vue与工程化之间的关联

```css
在已经对 Vue 做了初步了解之后，可能有读者会问：“既然 Vue 的使用方式也非常简单，可以像 jQuery 这些经典类库一样在 HTML 引入使用，那么 Vue 和工程化有什么关联呢？”

Vue.js 是一个框架，框架除了简化编码过程中的复杂度之外，面对不同的业务需求还提供了通用的解决方案，而这些解决方案，通常是将前端工程化里的很多种技术栈组合起来串成一条条技术链，一环扣一环，串起来就是一个完整的工程化项目。

举一个常见的例子，比如上一节内容 了解 Vue.js 与全新的 3.0 版本 里的 demo 是一个简单的 HTML 页面，如果业务稍微复杂一点，比如区分了 “首页” 、 “列表页” 、 “内容页” 这样涉及到多个页面，传统的开发方案是通过 A 标签跳转到另外一个页面，在跳转期间会产生 “新页面需要重新加载资源、会有短暂白屏” 等情况，用户体验不太好。

Vue 提供了 Vue Router 实现路由功能，利用 History API 实现单页面模式（可在 现代化的开发概念 部分了解区别），在一个 HTML 页面里也可以体验 “页面跳转” 这样的体验，但如果页面很多，所有代码都堆积在一个 HTML 页面里，就很难维护。

借助前端工程化的构建工具，开发者可以编写 .vue 单组件文件，将多个页面的代码根据其功能模块进行划分，可拆分到多个单组件文件里维护并进行合理复用，最终通过构建工具编译再合并，最终生成浏览器能访问的 HTML / CSS / JS 文件，这样的开发过程，用户体验没有影响，但开发体验大大提升。

类似这样一个个业务场景会积少成多，把 Vue 和工程化结合起来，处理问题更高效更简单。
```



#### ④现代化开发的概念

##### 1.MPA和SPA

![uTools_1685370080006](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1685370080006.png)

MPA

```bash
# 传统的页面跳转过程

从用户点击跳转开始：
---> 浏览器打开新的页面
---> 请求【所有】资源
---> 加载 HTML 、CSS 、 JS 、 图片等资源
---> 完成新页面的渲染
```

MPA的优点

1. 首页加载速度快

2. SEO友好，容易被搜索引擎收录(TKD三要素好)

   ```bash
   网页的 TKD 三要素是指一个网页的三个关键信息，含义如下：
   
   T ，指 Title ，网站的标题，即网页的 <title>网站的标题</title> 标签。
   
   K ，指 Keywords ，网站的关键词，即网页的 <meta name="Keywords" content="关键词1,关键词2,关键词3" /> 标签。
   
   D ，指 Description ，网站的描述，即网页的 <meta name="description" content="网站的描述" /> 标签。
   
   这三个要素标签都位于 HTML 文件的 <head /> 标签内。
   ```

3. 容易与服务端语言结合

```css
由于传统的页面都是由服务端直出，所以可以使用 PHP 、 JSP 、 ASP 、 Python 等非前端语言或技术栈来编写页面模板，最终输出 HTML 页面到浏览器访问。
```

MPA的缺点

1. 页面之间跳转访问速度慢
2. 用户体验不够友好
3. 开发成本高

SPA简介

```css
正因为传统的多页面应用存在了很多无法解决的开发问题和用户体验问题，催生了现代化的 SPA 单页面应用技术的诞生。

SPA 单页面应用是现代化的网站体验，与 MPA 相反，不论站点内有多少个页面，在 SPA 项目实际上只有一个 HTML 文件，也就是 index.html 首页文件。

它只有第一次访问的时候才需要经历一次完整的页面请求过程，之后的每个内部跳转或者数据更新操作，都是通过 AJAX 技术来获取需要呈现的内容并只更新指定的网页位置。

AJAX 技术（ Asynchronous JavaScript and XML ）是指在不离开页面的情况下，通过 JavaScript 发出 HTTP 请求，让网页通过增量更新的方式呈现给用户界面，而不需要刷新整个页面来重新加载，是一种 “无刷体验” 。


SPA 在页面跳转的时候，地址栏也会发生变化，主要有以下两种方式：
   1.通过修改 Location:hash 修改 URL 的 Hash 值（也就是 # 号后面部分），例如从 https://example.com/#/foo 变成 https://example.com/#/bar
   2.通过 History API 的 pushState 方法更新 URL ，例如从 https://example.com/foo 变成 https://example.com/bar
这两个方式的共同特点是更新地址栏 URL 的时候，均不会刷新页面，只是单纯的变更地址栏的访问地址，而网页的内容则通过 AJAX 更新，配合起来就形成了一种网页的 “前进 / 后退” 等行为效果。


Vue Router 默认提供了这两种 URL 改变方式的支持，分别是 createWebHashHistory 的 Hash 模式和 createWebHistory 对应的 History 模式，在 路由的使用 一章可以学习更多 Vue 路由的使用。
```

SPA

```bash
# SPA 页面跳转过程

从用户点击跳转开始：
---> 浏览器通过 `pushState` 等方法更新 URL
---> 请求接口数据（如果有涉及到前后端交互）
---> 通过 JavaScript 处理数据，拼接 HTML 片段
---> 把 HTML 片段渲染到指定位置，完成页面的 “刷新”
```

SPA的优点

- 只有一次完全请求的等待时间（首屏加载）
- 用户体验好，内部跳转的时候可以实现 “无刷切换”
- 因为不需要重新请求整个页面，所以切换页面的时候速度更快
- 因为没有脱离当前页面，所以 “页” 与 “页” 之间在切换过程中支持动画效果
- 脱离了页面跳页面的框架，让整个网站形成一个 Web App ，更接近原生 App 的访问体验
- 开发效率高，前后端分离，后端负责 API 接口，前端负责界面和联调，同步进行缩短工期

SPA 的缺点

- 首屏加载相对较慢

由于 SPA 应用的路由是由前端控制， SPA 在打开首页后，还要根据当前的路由再执行一次内容渲染，相对于 MPA 应用从服务端直出 HTML ，首屏渲染所花费的时间会更长。

- 不利于 SEO 优化

由于 SPA 应用全程是由 JavaScript 控制内容的渲染，因此唯一的一个 HTML 页面 `index.html` 通常是一个空的页面，只有最基础的 HTML 结构，不仅无法设置每个路由页面的 TDK ，页面内容也无法呈现在 HTML 代码里，因此对搜索引擎来说，网站的内容再丰富，依然只是一个 “空壳” ，无法让搜索引擎进行内容爬取。



##### 2.CSR和SSR

![image-20230529223226058](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529223226058.png)

**SPA单页面就是基于CSR客户端渲染的**



SSR服务端渲染(使用node.js实现)

![image-20230529223844818](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529223844818.png)

**SSR在服务器端动态生成页面内容并将完整的HTML页面返回给浏览器，而不是仅返回一个空白的HTML模板和JavaScript代码。相比之下，SPA应用只在浏览器中(客户端CSR渲染)动态生成HTML内容，这对于搜索引擎爬虫来说很难解析和索引。**

###### 1.vue的SSR

Vue 的 SSR 支持非常好， Vue 官方不仅提供了一个 [Vue.js 服务器端渲染指南](https://cn.vuejs.org/guide/scaling-up/ssr.html) 介绍了基于 Vue 的 SSR 入门实践，还有基于 Vue 的 [Nuxt.js](https://github.com/nuxt/framework) 、 [Quasar](https://github.com/quasarframework/quasar) 框架帮助开发者更简单的落地 SSR 开发，构建工具 Vite 也有内置的 [Vue SSR](https://cn.vitejs.dev/guide/ssr.html) 支持。



###### 2.SSR的缺点(后面俩个方案)

![image-20230529224242164](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529224242164.png)

###### 3.预渲染

![image-20230529224618299](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529224618299.png)

预渲染的优缺点、实现

![image-20230529224721694](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529224721694.png)

预渲染的原理

![image-20230529224738910](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529224738910.png)

说简单点就是在构建的时候启用没有用户图形页面的浏览器，使用代码通过编程代码来控制浏览器，让他预先加载一下需要预加载的内容。

###### 4.SSG

![image-20230529224957954](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529224957954.png)

**做一个总结，VUE通过CSR实现SPA单页面应用，然后优化为SSR服务端渲染，然后通过预加载等技术在进行优化**

##### 3.ISR和DPR

![image-20230529225339596](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529225339596.png)

#### ⑤.工程化不止于前端

1. 服务端开发(Node)

![image-20230529225720948](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529225720948.png)

2. APP开发

```css
原本的Native APP(原生app)原生开发开发

常规的 Native App 原生开发需要配备两条技术线的支持：使用 Java / Kotlin 语言开发 Android 版本，使用 Objective-C / Swift 语言开发 iOS 版本，这对于创业团队或者个人开发者来说都是一个比较高的开发成本。

前端开发者在项目组里对 App 的作用通常是做一些活动页面、工具页面内嵌到 App 的 WebView 里，如果是在一些产品比较少的团队里，例如只有一个 App 产品，那么前端的存在感会比较低。

而 Hybrid App 的出现，使得前端开发者也可以使用 JavaScript / TypeScript 来编写混合 App ，只需要了解简单的打包知识，就可以参与到一个 App 的开发工作中。

开发 Hybrid App 的过程通常称为混合开发，最大的特色就是一套代码可以运行到多个平台，这是因为整个 App 只有一个基座，里面的 App 页面都是使用 UI WebView 来渲染的 Web 界面，因此混合开发的开发成本相对于原生开发是非常低的，通常只需要一个人 / 一个小团队就可以输出双平台的 App ，并且整个 App 的开发周期也会更短。
```

![image-20230529225921738](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529225921738.png)

3. 桌面程序开发(基于Electro框架)

![image-20230529230453144](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529230453144.png)

![image-20230529230618756](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529230618756.png)

Chromium是浏览器运行引擎

4. 开发脚本(pkg打包工具)

![image-20230529230813977](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529230813977.png)

#### ⑥实践工程化

![image-20230529230948996](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529230948996.png)

###### 1.nodejs

![image-20230529231249730](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529231249730.png)

**node就是可以让js脱离浏览器运行的环境，我好像可以理解成java虚拟机的跨平台**

![image-20230529231431624](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529231431624.png)



###### 2.通过node演出生的构建工具

```css
为什么要使用构建工具？
	1.js版本经常更新，需要构建工具转换为浏览器可以接收的版本
	2.将ts转为浏览器认识的js
	3.构建工具通常集 “语言转换 / 编译” 、 “资源解析” 、 “代码分析” 、 “错误检查” 、 “任务队列” 等非常多的功能于一身。
	4.整合资源，压缩代码....
```

5. 兼容老代码

![image-20230529231909274](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20230529231909274.png)

由于polyfill的代码复杂臃肿，人工维护不可能，通常使用babel来实现兼容。(Babel也是一种构建工具)

6. 其它

![image-20230529232130396](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529232130396.png)



###### 3.webpack和vite

+ webpack全部打包好在启动开服服务器
+ vite直接启动开发服务器，请求到对应的模块的时候再进行编译

![image-20230529232804585](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529232804585.png)

###### 4.开发环境和生产环境

![image-20230529232910146](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529232910146.png)

![image-20230529232938546](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529232938546.png)

**判断开发环境**

![image-20230529233024208](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230529233024208.png)



### 2.工程化的前期准备

#### 1.让一个项目成为node项目

##### 1.初始化项目

```bash
npm init -y 或者 yarn init -y
```

##### 2.如何发布

![image-20230531224242950](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531224242950.png)

**注意事项**

语义化版本号管理(发布的版本要按这个)

![image-20230531224334866](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531224334866.png)

##### 3.如何运行项目

```bash
#在script做了配置后
npm  run dev or npm run build
```

![image-20230601214244681](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230601214244681.png)

##### 4.Hello Node

```bash
#创建项目文件夹
mkdir hello-node

#进入项目目录
cd hello-node

#项目初始化
npm init -y

#创建index.js文件(程序入口)  "dev":"node index",

#运行项目
npm run dev

#如果使用了cjs文件 配置script"dev:cjs": "node src/cjs/index.cjs"
npm run dev:cjs
```

补充(如果要使用cjs)

![image-20230601214811335](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230601214811335.png)

![image-20230601215036605](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230601215036605.png)

如果要用Esm

![image-20230601215101877](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230601215101877.png)

![image-20230601215157750](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230601215157750.png)







#### 2.CommonJS和Es Moudle

**ES目前是推荐使用的 Vue vite ts用的都是它为默认**

##### 1.commjs语法

创建

```js
function foo() {
  console.log('Hello World from foo.')
}

const bar = 'Hello World from bar.'

//暴露
module.exports = {
  foo,
  bar,
}
```

引用

```js
1.const m = require('./module.cjs')
2.解构
const { foo, bar } = require('./module.cjs')
```

访问

```js
1.m.foo()  m.bar
2.foo() bar
```



##### 2.EsM

```js
//创建
export default function foo() {
  console.log('Hello World')
}
//引入
import m from './module.mjs'
//访问
m()

//无法直接使用解构赋值
import { foo } from './module.mjs'
//这样会报错
```

**解决方案**

```js
//解决方案
export function foo() {
  console.log('Hello World from foo.')
}

export const bar = 'Hello World from bar.'

//此时可以直接
import { foo, bar } from './module.mjs'

//访问
foo()
console.log(bar)

//改变引入的方式,访问格式变化
import * as m from './module.mjs'

//访问
console.log(typeof m)
console.log(Object.keys(m))
m.foo()
console.log(m.bar)
```

##### 3.在浏览器中使用ESM

1. 编写代码启动node服务器来访问

![image-20230531230104989](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531230104989.png)

![image-20230531230327321](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531230327321.png)

2. 内联的EsM

![image-20230531230412367](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531230412367.png)

总的来说，现阶段在浏览器使用 ES Module 并不是一个很好的选择，建议开发者还是使用构建工具来开发，工具可以抹平这些浏览器差异化问题，降低开发成本。



#### 3.认识组件化

##### 1.什么是组件化

在前端工程项目里，页面可以理解为一个积木作品，组件则是用来搭建这个作品的一块又一块积木。

##### 2.组件化是怎么实现的

![image-20230531230755231](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531230755231.png)

#### 4.什么是包和node_modules

![image-20230531231154112](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531231154112.png)

![image-20230531231534021](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531231534021.png)

#### 5.生产依赖和开发依赖

生产依赖 项目上线了还要用 -S

开发依赖 开发便利 -D

#### 6.全局安装

![image-20230531231658953](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531231658953.png)

版本控制 更新 卸载

安装npm包时 有些包要依赖其它包，所以他会装很多个包

使用包

![image-20230531232117734](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230531232117734.png)



### 3.typescript

#### 1.创建项目

```java
1.进入项目文件夹 安装依赖 npm install -D typescript ts-node
//typescript 这个包是用 TypeScript 编程的语言依赖包
//ts-node 是让 Node 可以运行 TypeScript 的执行环境
2.创建src > ts > index.ts
3.在package.json的script字段中添加"dev:ts": "ts-node src/ts/index.ts",
4.运行项目 npm run dev:ts
```

**如何编译ts为js**

**1.手动编译**

```js
1.在 package.json 里增加一个 build script:
"build": "tsc src/ts/index.ts --outDir dist --target es6",
//--outDir dist 编译文件放的地方
//--target es6 控制js的版本
```

**2.自动编译**

```js
1.全局安装ts npm install -g typescript(上面是开发依赖)
2.输入tsc --init  会创建一个tsconfig.json文件
3.配置tsconfig.json文件
{
  "compilerOptions": {
    "target": "es6",
    "module": "es6",
    "outDir": "./dist"
  }
}

4.在命令行运行 tsc 即可打包成功
```



#### 2.语法开始

##### 1.原始数据类型和数组

```typescript
// 字符串
const str: string = 'Hello World'

// 数值
const num: number = 1

// 布尔值
const bool: boolean = true

//总结:如果已经初始定义了值 可以缺省 :类型 ts会进行自动类型推导

// 这样也不会报错，因为 TS 会推导它们的类型
const str = 'Hello World'
const num = 1
const bool = true



// 字符串数组
const strs: string[] = ['Hello World', 'Hi World']

// 数值数组
const nums: number[] = [1, 2, 3]

// 布尔值数组
const bools: boolean[] = [true, true, false]

// 这种有初始项目的数组， TS 也会推导它们的类型
const strs = ['Hello World', 'Hi World']
const nums = [1, 2, 3]
const bools = [true, true, false]

//如果一开始为空
const nums = [] //会触发any[]或never[](表示永远不会有值的一种类型，任何类型都不能赋值给 never 类型的变量)
```

##### 2.对象(接口)

```typescript
//1 type写法
type userItem = {
    //
}

//2 接口写法
interface UserItem {
  // ...
}

// 定义用户对象的类型
interface UserItem {
  name: string
  age: number
}

// 在声明变量的时候将其关联到类型上
const petter: UserItem = {
  name: 'Petter',
  age: 20,
}

//定义可选属性
interface UserItem {
  name: string
  age?: number //?表示可选
}
```

**调用自身接口的属性**

如果一些属性的结构跟本身一致，也可以直接引用，比如下面例子里的 `friendList` 属性，用户的好友列表，它就可以继续使用 `UserItem` 这个接口作为数组的类型：

```typescript
interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  // 这个属性引用了本身的类型
  friendList: UserItem[]
}

const petter: UserItem = {
  name: 'Petter',
  age: 18,
  enjoyFoods: ['rice', 'noodle', 'pizza'],
  friendList: [
    {
      name: 'Marry',
      age: 16,
      enjoyFoods: ['pizza', 'ice cream'],
      friendList: [],
    },
    {
      name: 'Tom',
      age: 20,
      enjoyFoods: ['chicken', 'cake'],
      friendList: [],
    }
  ],
}
```

**接口的继承**

```typescript
// 这里继承了 UserItem 的所有属性类型，并追加了一个权限等级属性
interface Admin extends UserItem {
  permissionLevel: number
}

//可以在继承时舍弃一些属性
interface Admin extends Omit<UserItem, 'enjoyFoods' | 'friendList'> { //舍弃了'enjoyFoods' 'friendList'
  permissionLevel: number
}

```



##### 3.类

```typescript
// 定义一个类
class User {
  // constructor 上的数据需要先这样定好类型
  name: string

  // 入参也要定义类型
  constructor(userName: string) {
    this.name = userName
  }

  getName() {
    console.log(this.name)
  }
}

// 通过 new 这个类得到的变量，它的类型就是这个类
const petter: User = new User('Petter')
petter.getName() // Petter

//类之间可以继承
// 这是另外一个类，继承自基础类
class User extends UserBase {
  getName() {
    console.log(this.name)
  }
}

//类也可以被接口继承
// 这是一个接口，可以继承自类
interface User extends UserBase {
  age: number
}
```

如果类上面本身有方法存在，接口在继承的时候也要相应的实现，当然也可以借助在 [对象（接口）](http://vue3.chengpeiquan.com/typescript.html#对象-接口) 提到的 `Omit` 帮助类型来去掉这些方法。

```typescript
// 接口继承类的时候也可以去掉类上面的方法
interface User extends Omit<UserBase, 'getName'> {
  age: number
}
```



##### 4.联合类型

```typescript
//当一个变量可能出现多种类型的值的时候，可以使用联合类型来定义它，类型之间用 | 符号分隔。
function counter(count: number | string) {
  console.log(`The current count is: ${count}.`)
}

// 不论传数值还是字符串，都可以达到的目的
counter(1)  // The current count is: 1.
counter('2')  // The current count is: 2.
```



##### 5.函数

###### 1.基本写法

```typescript
// 写法一：函数声明
function sum1(x: number, y: number): number {
  return x + y
}

// 写法二：函数表达式
const sum2 = function(x: number, y: number): number {
  return x + y
}

// 写法三：箭头函数
const sum3 = (x: number, y: number): number => x + y

// 写法四：对象上的方法
const obj = {
  sum4(x: number, y: number): number {
    return x + y
  }
}

//际业务中会遇到有一些函数入参是可选，可以用和 对象（接口） 一样，用 ? 来定义：
function sum(x: number, y: number, isDouble?: boolean): number {
  return isDouble ? (x + y) * 2 : x + y
}

// 这样传参都不会报错，因为第三个参数是可选的
sum(1, 2) // 3
sum(1, 2, true) // 6
```



###### 2.无返回值的函数( void)

```typescript
// 注意这里的返回值类型
function sayHi(name: string): void {
  console.log(`Hi, ${name}!`)
}

sayHi('Petter') // Hi, Petter!

//需要注意的是， void 和 null 、 undefined 不可以混用，如果的函数返回值类型是 null ，那么是真的需要 return 一个 null 值：
// 只有返回 null 值才能定义返回类型为 null
function sayHi(name: string): null {
  console.log(`Hi, ${name}!`)
  return null
}

//有时候要判断参数是否合法，不符合要求时需要提前终止执行（比如在做一些表单校验的时候），这种情况下也可以用 void ：
function sayHi(name: string): void {
  // 这里判断参数不符合要求则提前终止运行，但它没有返回值
  if (!name) return

  // 否则正常运行
  console.log(`Hi, ${name}!`)
}
```



###### 3.异步函数的返回值

对于异步函数，需要用 `Promise<T>` 类型来定义它的返回值，这里的 `T` 是泛型，取决于的函数最终返回一个什么样的值（ `async / await` 也适用这个类型）。

```typescript
//这是一个异步函数，会 resolve 一个字符串，所以它的返回类型是 Promise<string> （假如没有 resolve 数据，那么就是 Promise<void> ）。
// 注意这里的返回值类型
function queryData(): Promise<string> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Hello World')
    }, 3000)
  })
}

queryData().then((data) => console.log(data))
```



###### 4.函数本身的类型

```typescript
// 这里的 sum ，确实是没有指定类型（因为进行自动类型推导）
const sum = (x: number, y: number): number => x + y

//完整写法
const sum: (x:number,y:number) => number = (x: number, y: number): number => x + y
// 1. const sum: (x: number, y: number) => number 是这个函数的名称和本身类型
// 2. = (x: number, y: number) 这里是指明了函数的入参和类型
// 3. : number => x + y 这里是函数的返回值和类型
```



TypeScript 的函数类型是以 `() => void` 这样的形式来写的：左侧圆括号是函数的入参类型，如果没有参数，就只有一个圆括号，如果有参数，就按照参数的类型写进去；右侧则是函数的返回值。

事实上由于 TypeScript 会推导函数类型，所以很少会显式的去写出来，除非在给对象定义方法：

```typescript
// 对象的接口
interface Obj {
  // 上面的方法就需要显式的定义出来
  sum: (x: number, y: number) => number
}

// 声明一个对象
const obj: Obj = {
  sum(x: number, y: number): number {
    return x + y
  }
}
```



###### 5.函数重载

```typescript
// 对单人或者多人打招呼
function greet(name: string | string[]): string | string[] {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

//在这种情况下 如果要强制确认类型，需要用类型断言 as关键字
const greeting = greet('Petter') as string  //greeting是string类型
const greetings = greet(['Petter', 'Tom', 'Jimmy']) as string[] //greetings是string[]类型


// 这一次用了函数重载
function greet(name: string): string  // TS 类型
function greet(name: string[]): string[]  // TS 类型
function greet(name: string | string[]) {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

// 单个问候语，此时只有一个类型 string
const greeting = greet('Petter')
console.log(greeting) // Welcome, Petter!

// 多个问候语，此时只有一个类型 string[]
const greetings = greet(['Petter', 'Tom', 'Jimmy'])
console.log(greetings)
// [ 'Welcome, Petter!', 'Welcome, Tom!', 'Welcome, Jimmy!' ]
```

上面是利用函数重载优化后的代码，可以看到一共写了 3 行 `function greet …` ，区别如下：

第 1 行是函数的 TS 类型，告知 TypeScript ，当入参为 `string` 类型时，返回值也是 `string` ;

第 2 行也是函数的 TS 类型，告知 TypeScript ，当入参为 `string[]` 类型时，返回值也是 `string[]` ;

第 3 行开始才是真正的函数体，这里的函数入参需要把可能涉及到的类型都写出来，用以匹配前两行的类型，并且这种情况下，函数的返回值类型可以省略，因为在第 1 、 2 行里已经定义过返回类型了。



###### 6.any类型或never类型

```typescript
//如果实在不知道应该如何定义一个变量的类型， TypeScript 也允许使用任意值。
// 这里的入参显式指定了 any
function getFirstWord(msg: any) {
  // 这里使用了 String 来避免程序报错
  console.log(String(msg).split(' ')[0])
}

getFirstWord('Hello World')

getFirstWord(123)
```



## 2.vue3工程化创建管理项目

### 补充：vue2vue3构建工具的不同

![uTools_1692267549766](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692267549766.png)

![uTools_1692267562099](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1692267562099.png)

### 1.创建项目的三种方法(npm 管理基于vite)

创建项目要有node环境和npm

#### 1.create vite

```bash
1.npm create vite(然后根据提示选择想要的扩展)
2.npm install(项目创建完成后进入终端，安装项目依赖)
3.npm run dev(运行项目)
```



#### 2.create vue(基于vite)❥

```bash
1.npm init vue@3(然后根据提示选择想要的扩展)
2.npm install(项目创建完成后进入终端，安装项目依赖)
3.npm run dev(运行项目)
```



#### 3.简单使用create preset(1)

```bash
1.npm create preset(然后根据提示选择想要的扩展)
2.npm install(项目创建完成后进入终端，安装项目依赖)
3.npm run dev(运行项目)
```



#### 4.全局使用create preset(2)

```bash
1.npm install -g create-preset
2.preset init hello-vue3 --template vue3-ts-vite
3.npm install(项目创建完成后进入终端，安装项目依赖)
4.npm run dev(运行项目)
```



#### 5.通过create-vite  创建

```bash
1.npm install -g create-vite  
2.create-vite my-vue-app --template vue  
3.npm install  
4.npm run dev
```



### 2.创建项目(npm 管理基于vue cli)

```bash
1.更新vue cli脚手架 npm install -g @vue/cli
2.构建3.0项目 vue create hello-vue3(然后需要手动配置依赖)
3.安装依赖 npm install
4.运行项目npm run serve
```



### 3.各种文件说明

#### 1.调整TS Config

![image-20230607201915313](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607201915313.png)

假设在 vite.config.ts 里配置了这些 alias ：

```typescript
export default defineConfig({
  // ...
  resolve: {
    alias: {
      '@': resolve('src'), // 源码根目录
      '@img': resolve('src/assets/img'), // 图片
      '@less': resolve('src/assets/less'), // 预处理器
      '@libs': resolve('src/libs'), // 本地库
      '@plugins': resolve('src/plugins'), // 本地插件
      '@cp': resolve('src/components'), // 公共组件
      '@views': resolve('src/views'), // 路由组件
    },
  },
  // ...
})
```

那么在该项目的 tsconfig.json 文件里就需要相应的加上这些 paths ：

```typescript
{
  "compilerOptions": {
    // ...
    "paths": {
      "@/*": ["src/*"],
      "@img/*": ["src/assets/img/*"],
      "@less/*": ["src/assets/less/*"],
      "@libs/*": ["src/libs/*"],
      "@plugins/*": ["src/plugins/*"],
      "@cp/*": ["src/components/*"],
      "@views/*": ["src/views/*"]
    },
    // ...
  },
  // ...
}
```



#### 2.添加写作规范

##### 1.Editor Config

在项目根目录下再增加一个名为 `.editorconfig` 的文件。

这个文件的作用是强制编辑器以该配置来进行编码，比如缩进统一为空格而不是 Tab ，每次缩进都是 2 个空格而不是 4 个等等。

```typescript
# http://editorconfig.org
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 2
indent_style = space
insert_final_newline = true
max_line_length = 80
trim_trailing_whitespace = true

[*.md]
max_line_length = 0
trim_trailing_whitespace = false
```

![image-20230607202111116](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202111116.png)

##### 2.Prettier

![image-20230607202208049](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202208049.png)

```typescript
{
  "semi": false,
  "singleQuote": true
}
```

![image-20230607202231281](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202231281.png)

##### 3.ESLint

![image-20230607202319058](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202319058.png)

```typescript
module.exports = {
  root: true,
  env: {
    node: true,
    browser: true,
  },
  extends: ['plugin:vue/vue3-essential', 'eslint:recommended', 'prettier'],
  parser: 'vue-eslint-parser',
  parserOptions: {
    parser: '@typescript-eslint/parser',
    ecmaVersion: 2020,
    sourceType: 'module',
  },
  plugins: ['@typescript-eslint', 'prettier'],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'prettier/prettier': 'warn',
    'vue/multi-word-component-names': 'off',
  },
  globals: {
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly',
  },
}
```

![image-20230607202340089](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202340089.png)

![image-20230607202352156](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230607202352156.png)



**vue-router笔记分写出去了**



## 3.vue3插件管理

**什么是插件：插件是功能的实现或者是组件的封装**

![image-20230716204359166](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204359166.png)

**主流包管理器：npm  cnpm yarn pnpm(后起之秀)**



**引入插件**

![image-20230716204653832](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204653832.png)

### 1.vue专属插件

![image-20230716204753334](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204753334.png)

#### 1.全局插件的使用

![image-20230716204835975](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204835975.png)

**用法**

![image-20230716204850146](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204850146.png)



#### 2.单组件插件的使用

![image-20230716204936479](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716204936479.png)



### 2.通用JS/TS插件

#### 1.普通插件的组件内引入(推荐，按需引入)

![image-20230716205303685](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205303685.png)

#### 2.普通插件的全局引入(不推荐)

![image-20230716205345140](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205345140.png)

![image-20230716205420529](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205420529.png)

![image-20230716205451621](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205451621.png)

### 3.本地插件

**本地插件就是一些我们经常需要用到的业务功能，我们可以自己封装起来**

![image-20230716205720540](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205720540.png)

#### 1.开发本地通用JS/TS插件

![image-20230716205857852](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205857852.png)

![image-20230716205924567](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205924567.png)

**例子1:只有一个默认功能**

![image-20230716210024611](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210024611.png)

**例子：工具合集**

![image-20230716210209477](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210209477.png)

![image-20230716210233273](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210233273.png)

![image-20230716210140871](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210140871.png)

**例子：包含工具及辅助函数**

![image-20230716210342008](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210342008.png)

![image-20230716210523271](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210523271.png)

**在es中 greet默认 { praise } 是具名导出**

### 4.开发本地vue专属插件

![image-20230716210652448](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210652448.png)

![image-20230716210914601](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210914601.png)

![image-20230716210936450](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210936450.png)

![image-20230716210951209](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716210951209.png)



**例子：如何编写一个全局本地vue专属插件**

编写插件

```typescript
// src/plugins/directive.ts
import type { App } from 'vue'

// 插件选项的类型
interface Options {
  // 文本高亮选项
  highlight?: {
    // 默认背景色
    backgroundColor: string
  }
}

/**
 * 自定义指令
 * @description 保证插件单一职责，当前插件只用于添加自定义指令
 */
export default {
  install: (app: App, options?: Options) => {
    /**
     * 权限控制
     * @description 用于在功能按钮上绑定权限，没权限时会销毁或隐藏对应 DOM 节点
     * @tips 指令传入的值是管理员的组别 id
     * @example <div v-permission="1" />
     */
    app.directive('permission', (el, binding) => {
      // 假设 1 是管理员组别的 id ，则无需处理
      if (binding.value === 1) return

      // 其他情况认为没有权限，需要隐藏掉界面上的 DOM 元素
      if (el.parentNode) {
        el.parentNode.removeChild(el)
      } else {
        el.style.display = 'none'
      }
    })

    /**
     * 文本高亮
     * @description 用于给指定的 DOM 节点添加背景色，搭配文本内容形成高亮效果
     * @tips 指令传入的值需要是合法的 CSS 颜色名称或者 Hex 值
     * @example <div v-highlight="`cyan`" />
     */
    app.directive('highlight', (el, binding) => {
      // 获取默认颜色
      let defaultColor = 'unset'
      if (
        Object.prototype.toString.call(options) === '[object Object]' &&
        options?.highlight?.backgroundColor
      ) {
        defaultColor = options.highlight.backgroundColor
      }

      // 设置背景色
      el.style.backgroundColor =
        typeof binding.value === 'string' ? binding.value : defaultColor
    })
  },
}
```

启用插件

![image-20230716213322590](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716213322590.png)

使用插件

![image-20230716213335667](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716213335667.png)

### 5.全局API挂载

![image-20230716205345140](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205345140.png)

![image-20230716205420529](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205420529.png)

![image-20230716205451621](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230716205451621.png)



### 6.开发一个基于vite的npm包

![image-20230717155622990](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717155622990.png)

#### 1.例子:开发npm包的前期准备

```bash
# 创建一个项目文件夹
mkdir hello-lib

# 进入项目文件夹
cd hello-lib

# 执行初始化，使其成为一个 Node 项目
npm init -y

# 配置包信息(package.json)

# 添加 -D 选项将其安装到 devDependencies
npm i -D vite

# 配置vite.config.ts文件

# 添加入口文件 src/index.ts

# 执行打包命令查看结果
npm run build
```

package.json 

![image-20230717225115419](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717225115419.png)

```json
{
  "name": "@learning-vue3/lib", // 包名
  "version": "1.0.0", // 版本号
  "description": "A library demo for learning-vue3.", // 描述
  "author": "chengpeiquan <chengpeiquan@chengpeiquan.com>", // 作者信息
  "homepage": "https://github.com/learning-vue3/hello-lib", // 主页链接
  "repository": {
    "type": "git", // 仓库类型
    "url": "git+https://github.com/learning-vue3/hello-lib.git" // 仓库链接
  },
  "license": "MIT", // 许可证
  "files": ["dist"], // 需要包含在发布中的文件或目录
  "main": "dist/index.cjs", // CommonJS 模块的入口文件路径
  "module": "dist/index.mjs", // ES 模块的入口文件路径
  "browser": "dist/index.min.js", // 在浏览器环境下使用的入口文件路径
  "types": "dist/index.d.ts", // TypeScript 类型定义文件路径
  "keywords": ["library", "demo", "example"], // 关键词
  "scripts": {
    "build": "vite build" // 构建命令
  }
}
```

![image-20230717225300229](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717225300229.png)

![image-20230717225434284](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717225434284.png)

vite.config.ts

```typescript
// vite.config.ts
import { defineConfig } from 'vite'

// https://cn.vitejs.dev/config/
export default defineConfig({
  build: {
    // 输出目录
    outDir: 'dist',
    // 构建 npm 包时需要开启 “库模式”
    lib: {
      // 指定入口文件
      entry: 'src/index.ts',
      // 输出 UMD 格式时，需要指定一个全局变量的名称
      name: 'hello',
      // 最终输出的格式，这里指定了三种
      formats: ['es', 'cjs', 'umd'],
      // 针对不同输出格式对应的文件名
      fileName: (format) => {
        switch (format) {
          // ES Module 格式的文件名
          case 'es':
            return 'index.mjs'
          // CommonJS 格式的文件名
          case 'cjs':
            return 'index.cjs'
          // UMD 格式的文件名
          default:
            return 'index.min.js'
        }
      },
    },
    // 压缩混淆构建后的文件代码
    minify: true,
  },
})
```

src/index.ts

![image-20230717225549762](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717225549762.png)



#### 2.在本地进行测试npm包

**编写完ts文件后，统一在index.ts中作为入口导出个构建工具**

![image-20230717230401264](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230717230401264.png)

1.先在 src 目录下创建一个名为 utils.ts 的文件，写入以下内容(功能函数)：

```ts
// src/utils.ts

/**
 * 生成随机数
 * @param min - 最小值
 * @param max - 最大值
 * @param roundingType - 四舍五入类型
 * @returns 范围内的随机数
 */
export function getRandomNumber(
  min: number = 0,
  max: number = 100,
  roundingType: 'round' | 'ceil' | 'floor' = 'round'
) {
  return Math[roundingType](Math.random() * (max - min) + min)
}

/**
 * 生成随机布尔值
 */
export function getRandomBoolean() {
  const index = getRandomNumber(0, 1)
  return [true, false][index]
}
```

2.在入口文件统一导出

![image-20230718154637436](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718154637436.png)

3.创建本地软连接

```bash
# 进入 npm 包项目所在的目录(你写的包)
cd url

# 创建 npm 包的本地软链接
npm link

# 查看全局安装目录
npm prefix -g
```

4.创建项目进行调试

```bash
# 进入调试项目所在的目录
cd url

# 包名就是package.json的name字段
# 通过 npm 包的包名称关联本地软链接(假设包名交my-library)
npm link my-library
```

![image-20230718154935999](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718154935999.png)

5.测试

![image-20230718154954738](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718154954738.png)

#### 3.添加版权注释

![image-20230718155028748](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155028748.png)

![image-20230718155047551](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155047551.png)

#### 4.生成npm包的类型声明(ts需要类型声明才能完全兼容 js不用)

![image-20230718155147777](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155147777.png)

![image-20230718155206976](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155206976.png)

**进行类型声明1：DTS文件**

![image-20230718155240479](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155240479.png)

![image-20230718155307237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155307237.png)

![image-20230718155329231](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155329231.png)

**此时npm run build通过**

**但是这种方法会产生很多.d.ts文件**

**进行类型声明2：DTS  Bundle文件**

![image-20230718155449997](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155449997.png)

![image-20230718155503222](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155503222.png)

```js
// scripts/buildTypes.mjs
import { writeFileSync } from 'fs'
import { dirname, resolve } from 'path'
import { fileURLToPath } from 'url'
import { generateDtsBundle } from 'dts-bundle-generator'

async function run() {
  // 默认情况下 `.mjs` 文件需要自己声明 __dirname 变量
  const __filename = fileURLToPath(import.meta.url)
  const __dirname = dirname(__filename)

  // 获取项目的根目录路径
  const rootPath = resolve(__dirname, '..')

  // 添加构建选项
  // 插件要求是一个数组选项，支持多个入口文件
  const options = [
    {
      filePath: resolve(rootPath, `./src/index.ts`),
      output: {
        noBanner: true,
      },
    },
  ]

  // 生成 DTS 文件内容
  // 插件返回一个数组，返回的文件内容顺序同选项顺序
  const dtses = generateDtsBundle(options, {
    preferredConfigPath: resolve(rootPath, `./tsconfig.json`),
  })
  if (!Array.isArray(dtses) || !dtses.length) return

  // 将 DTS Bundle 的内容输出成 `.d.ts` 文件保存到 dist 目录下
  // 当前只有一个文件要保存，所以只取第一个下标的数据
  const dts = dtses[0]
  const output = resolve(rootPath, `./dist/index.d.ts`)
  writeFileSync(output, dts)
}
run().catch((e) => {
  console.log(e)
})
```

![image-20230718155536015](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155536015.png)

![image-20230718155545652](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230718155545652.png)

### 5.添加说明文档

README 模板

```bash
# 项目名称

写上项目用途的一句话简介。

## 功能介绍

1. 功能 1 一句话介绍
2. 功能 2 一句话介绍
3. 功能 3 一句话介绍

## 在线演示

如果有部署在线 demo ，可放上 demo 的访问地址。

## 安装方法

使用 npm ： `npm install package-name`

使用 CDN ： `https://example.com/package-name`

## 用法

告诉使用者如何使用 npm 包。

## 插件选项

如果 npm 包是一个插件，并支持传递插件选项，在这里可以使用表格介绍选项的作用。

| 选项名称 |  类型  |    作用    |
| :------: | :----: | :--------: |
|   foo    | string | 一句话介绍 |
|   bar    | number | 一句话介绍 |

更多内容请根据实际情况补充。
```



### 6.发布包

在发布 npm 包之前，请先在 npm 官网上注册一个账号：[点击注册](https://www.npmjs.com/signup) 。

接下来需要在命令行上登录该账号以操作发布命令，打开命令行工具，输入以下命令进行登录：

```bash
npm login
```

按照命令行的提示输入在 npmjs 网站上注册的账号和密码即可完成登录，可以通过以下命令查看当前登录的账号名称，验证是否登录成功：

```bash
npm whoami
```

在登录成功之后，命令行会记住账号的登录状态，以后的操作就无需每次都执行登录命令了。

TIP

以上操作也可以实用 `npm adduser` 命令代替，直接在命令行完成注册和登录。

#### 将包发布到 npmjs[](http://vue3.chengpeiquan.com/plugin.html#将包发布到-npmjs)

在 npm 上发布私有包需要进行付费，因此这里只使用公共包的发布作为演示和讲解，如果开发的是公司内部使用的 npm 包，只要源代码是私有仓库，也可以使用这种方式来发布，当前在这样做之前请先获得公司的同意。

对于一个普通命名的包，要发布到 npmjs 上非常简单，只需要执行 npm 包管理器自带的一个命令即可：

```bash
npm publish
```

它默认会将这个包作为一个公共包发布，如果包名称合法并且没有冲突，则发布成功，可以在 [npmjs](https://www.npmjs.com/) 查询到，否则会返回错误信息告知原因，如果因为包名冲突导致的失败，可以尝试修改别的名称再次发布。

如果打算使用像 [@vue/cli](https://www.npmjs.com/package/@vue/cli) 、 [@vue/compiler-sfc](https://www.npmjs.com/package/@vue/compiler-sfc) 这样带有 @scope 前缀的作用域包名，需要先在 npmjs 的 [创建新组织](https://www.npmjs.com/org/create) 页面创建一个组织，或者确保自己拥有 @scope 对应的组织发布权限。

@scope 作用域包默认会作为私有包发布，因此在执行发布命令的时候还需要加上一个 `--access` 选项，将其指定为 `public` 允许公开访问才可以发布成功：

```bash
npm publish --access public
```

当前的 hello-lib 项目已发布到 npmjs ，可以查看该包的主页 [@learning-vue3/lib](https://www.npmjs.com/package/@learning-vue3/lib) ，也可以通过 npm 安装到项目里使用了：

```bash
npm i @learning-vue3/lib
```

并且发布到 npmjs 上的包，都同时获得热门 CDN 服务的自动同步，可以通过包名称获取到 CDN 链接并通过 `<script />` 标签引入到 HTML 页面里：

```bash
# 使用 jsDelivr CDN
https://cdn.jsdelivr.net/npm/@learning-vue3/lib

# 使用 UNPKG CDN
https://unpkg.com/@learning-vue3/lib
```

此时 CDN 地址对应的 npm 包文件内容，就如前文所述，调用了 package.json 里 browser 字段指定的 UMD 规范文件 `dist/index.min.js` 。

#### 给 npm 包打 Tag[](http://vue3.chengpeiquan.com/plugin.html#给-npm-包打-tag)

细心的开发者还会留意到，例如像 Vue 这样的包，在 npmjs 上的 [版本列表](https://www.npmjs.com/package/vue?activeTab=versions) 里有 Current Tags 和 Version History 的版本分类，其中 Version History 是默认的版本发布历史列表，而 Current Tags 则是在发布 npm 包的时候指定打的标签。

![Vue 在 npmjs 上的版本列表](http://vue3.chengpeiquan.com/assets/img/vue-versions-on-npmjs.jpg)

Vue 在 npmjs 上的版本列表

标签的好处是可以让使用者无需记住对应的版本号，而是使用一些更具备语义化的单词来安装指定版本，例如：

```bash
# 安装最新版的 Vue 3 ，即截图里对应的 3.2.40 版本
npm i vue@latest

# 安装最新版的 Vue 2 ，即截图里对应的 2.7.10 版本
npm i vue@v2-latest

# 如果后续有功能更新的测试版，也可以通过标签安装
npm i vue@beta
```

除了减少寻找版本号的麻烦外，一旦后续有版本更新，再次使用相同的标签安装，可以重新安装到该标签对应的最新版本，例如从 `1.0.0-beta.1` 升级到 `1.0.0-beta.2` ，可以使用 `@beta` 标签再次安装来达到升级的目的。

在标签列表里，有一个 `latest` 的标签是发布 npm 包时自带的，对应该包最新的正式版本，安装 npm 包时如果不指定标签，则默认使用 `latest` 标签，以下两个安装操作是等价的：

```bash
# 隐式安装 latest 标签对应的版本
npm i vue

# 显式安装 latest 标签对应的版本
npm i vue@latest
```

同样的，当发布 npm 包时不指定标签，则该版本也会在发布后作为 `@latest` 标签对应的版本号。

其他标签则需要在发布时配合发布命令，使用 `--tag` 作为选项手动指定，以下命令将为普通包打上名为 `alpha` 的 Tag ：

```bash
npm publish --tag alpha
```

同理，如果是 @scope 作用域包也是在使用 `--access` 选项的情况下，继续追加一条 `--tag` 选项指定包的标签。

```bash
npm publish --access public --tag alpha
```



TIP

请注意，如果是 Alpha 或者 Beta 版本，通常会在版本号上增加 `-alpha.0` 、 `-alpha.1` 这样的 [版本标识符](http://vue3.chengpeiquan.com/guide.html#版本标识符)，以便在发布正式版本的时候可以使用无标识符的相同版本号，以保证版本号在遵循 [升级规则](http://vue3.chengpeiquan.com/guide.html#基本格式与升级规则) 下的连续性。





## 4.组件之间的通信

1. 首先，分为四种场景之下的组件通信

![image-20230724153110325](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230724153110325.png)

2. 父子组件之间的通信方法

   ![image-20230728001814110](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728001814110.png)

### 1.父子组件通信

#### 1.props+emits

**这里使用的是没有setup语法糖的模式，传递的是props的属性**

**关于props和attrs的区别**

![uTools_1690396683766](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1690396683766.png)

```vue
Father
<template>
  <div>
    <C
    title="用户信息"
    :index="1"
    :uid="userInfo.id"
    :user-name="userInfo.name"
  />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import C from './components/test/C.vue';

interface Member {
  id: number
  name: string
}
export default defineComponent({
 components:{
  C
 },

 // 定义一些数据并 `return` 给 `<template />` 用
 setup() {
    const userInfo: Member = {
      id: 1,
      name: 'Petter',
    }

    // 不要忘记 `return` ，否则 `<template />` 拿不到数据
    return {
      userInfo,
    }

  }
})
</script>

```

```vue
<!-- Child.vue -->
<template>
  <p>标题：{{ title }}</p>
  <p>索引：{{ index }}</p>
  <p>用户id：{{ uid }}</p>
  <p>用户名：{{ userName }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// Child.vue
export default defineComponent({
    //获取props
  props: {
    // 可选，并提供默认值
    title: {
      type: String,
      required: false,
      default: '默认标题',
    },

    // 默认可选，单类型
    index: Number,

    // 添加一些自定义校验
    userName: {
      type: String,

      // 在这里校验用户名必须至少 3 个字
      validator: (v:string) => v.length >= 3,
    },

    // 默认可选，但允许多种类型
    uid: [Number, String],
  },

  // 在这里需要添加一个入参
  setup(props) {
    // 该入参包含了当前组件定义的所有 props
    console.log(props)
  }
})
</script>

```



**传递非props属性**

```vue
<!-- Father.vue -->
<template>
  <C
    id="child-component"
    class="class-name-from-father"
    :keys="['foo', 'bar']"
    :obj="{ foo: 'bar' }"
    data-hash="b10a8db164e0754105b7a99be72e3fe5"
  />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import C from './components/test/C.vue';


export default defineComponent({
 components:{
  C
 },

})
</script>

```

```vue
<!-- Child.vue -->
<template>
  <div class="child">子组件</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup() {
    return {}
  },
})
</script>

<style scoped>
.child {
  width: 100%;
}
</style>

```

![image-20230728004522524](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728004522524.png)

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728004538024.png)

**获取attrs**

![image-20230728004815948](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728004815948.png)

![image-20230728004858513](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728004858513.png)

![image-20230728004906556](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728004906556.png)

**绑定 emits**

> 注：这一小节的步骤是在 Father.vue 里操作。

如果父组件 Father.vue 需要获取子组件 Child.vue 的数据更新情况，可以由子组件通过 emits 进行通知，下面这个更新用户年龄的例子可以学习如何给子组件绑定 emit 事件。

事件的逻辑是由父组件决定的，因此需要在父组件 Father.vue 的 `<script />` 里先声明数据变量和一个更新函数，并且这个更新函数通常会有一个入参作为数据的新值接收。

在本例子里，父组件声明了一个 `updateAge` 方法，它接受一个入参 `newAge` ，代表新的年龄数据，这个入参的值将由子组件 Child.vue 在触发 emits 时传入。

因为还需要在 `<template />` 部分绑定给子组件，所以请记得 return 出来。

```ts
// Father.vue
import { defineComponent, reactive } from 'vue'
import Child from '@cp/Child.vue'

interface Member {
  id: number
  name: string
  age: number
}

export default defineComponent({
  components: {
    Child,
  },
  setup() {
    const userInfo: Member = reactive({
      id: 1,
      name: 'Petter',
      age: 0,
    })

    /**
     * 声明一个更新年龄的方法
     * @param newAge - 新的年龄，由子组件触发 emits 时传递
     */
    function updateAge(newAge: number) {
      userInfo.age = newAge
    }

    return {
      userInfo,
      updateAge,
    }
  },
})
```

再看 Father.vue 的 `<template />` 部分，和 Click 事件使用 `@click` 一样，自定义的 emits 事件也是通过 `v-on` 或者是 `@` 来绑定：

```vue
<!-- Father.vue -->
<template>
  <Child @update-age="updateAge" />
</template>
```

和 props 一样，官方文档也推荐将 camelCase 风格（小驼峰）命名的函数，在绑定时使用 kebab-case 风格（短横线），例如使用 `update-age` 代替 `updateAge` 传递。

**接收并调用 emits**

> 注：这一小节的步骤是在 Child.vue 里操作。

和 props 一样，可以指定是一个数组，把要接收的 `emit` 事件名称写进去：

```ts
// Child.vue
export default defineComponent({
  emits: ['update-age'],
})
```

和 props 不同，通常情况下 emits 这样配置就足够使用了。

接下来如果子组件需要更新数据并通知父组件，可以使用 `setup` 第二个参数 `context` 里的 `emit` 方法触发：

```ts
// Child.vue
export default defineComponent({
  emits: ['update-age'],
  setup(props, { emit }) {
    // 通知父组件将年龄设置为 `2`
    emit('update-age', 2)
  },
})
```

`emit` 方法最少要传递一个参数：事件名称。

事件名称是指父组件 Father.vue 绑定事件时 `@update-age="updateAge"` 里的 `update-age` ，如果改成 `@hello="updateAge"` ，那么事件名称就需要使用 `hello` ，一般情况下事件名称和更新函数的名称会保持一致，方便维护。

对于需要更新数据的情况， `emit` 还支持传递更多的参数，对应更新函数里的入参，所以可以看到上面例子里的 `emit('update-age', 2)` 有第二个参数，传递了一个 `2` 的数值，就是作为父组件 `updateAge` 的入参 `newAge` 传递。

如果需要通信的数据很多，建议第二个入参使用一个对象来管理数据，例如父组件调整为：

```ts
// Father.vue
function updateInfo({ name, age }: Member) {
  // 当 `name` 变化时更新 `name` 的值
  if (name && name !== userInfo.name) {
    userInfo.name = name
  }

  // 当 `age` 变化并且新值在正确的范围内时，更新 `age` 的值
  if (age > 0 && age !== userInfo.age) {
    userInfo.age = age
  }
}
```

子组件在传递新数据时，就应该使用对象的形式传递：

```ts
// Child.vue
emit('update-info', {
  name: 'Tom',
  age: 18,
})
```

这对于更新表单等数据量较多的场景非常好用。

**接收 emits 时做一些校验**

> 注：这一小节的步骤是在 Child.vue 里操作。

和 props 一样，子组件在接收 emits 时也可以对这些事件做一些验证，这个时候就需要将 emits 配置为对象，然后把事件名称作为 `key` ， `value` 则对应为一个用来校验的方法。

还是用回上文那个更新年龄的方法，如果需要增加一个条件：当达到成年人的年龄时才会更新父组件的数据，那么就可以将 emits 调整为：

```ts
// Child.vue
export default defineComponent({
  emits: {
    // 需要校验
    'update-age': (age: number) => {
      // 写一些条件拦截，返回 `false` 表示验证不通过
      if (age < 18) {
        console.log('未成年人不允许参与')
        return false
      }

      // 通过则返回 `true`
      return true
    },

    // 一些无需校验的，设置为 `null` 即可
    'update-name': null,
  },
})
```

接下来如果提交 `emit('update-age', 2)` ，因为不满足验证条件，浏览器控制台将会出现一段 `[Vue warn]: Invalid event arguments: event validation failed for event "update-age".` 这样的警告信息。



##### **1.补充：使用了setup语法糖时要怎么设inheritAttrs**

![uTools_1690396758739](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1690396758739.png)

##### 2.补充：使用了setup语法糖时要怎么获取attrs

![uTools_1690397050901](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1690397050901.png)





#### 2.v-model+emits

**v-model一般用来单个组件实现双向绑定，这里拿来父子组件通信比较少用**

**原理**

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230727181109646.png)

##### 1.vue2的用法 利用data来完成父子通信

```vue
/*APP.vue*/
<script lang="ts">
import Childx from '../src/components/comp1/Childx.vue'
import { reactive } from 'vue';
export default {
  components: { Childx },

  //没有使用setup语法糖时 data用来指定实例对象中的响应式属性（vue2写法）
  data() {
     interface M  {
       id:number,
       name:string,
       age:number
     }
     const userInfo:M = {
       id:1,
       name:'petter',
       age:28
     }
     return {
       userInfo
     }
   }

}
</script>

<template>
  <Childx
    v-model:uid="userInfo.id"
    v-model:username="userInfo.name"
    v-model:age="userInfo.age"
  />
  <br>
  {{ userInfo.id }}
  <br>
  {{ userInfo.name }}
  <br>
  {{ userInfo.age }}
</template> 

/*Childx.vue*/

<script>
export default {
  props: {
    uid: Number,
    username: String,
    age: Number,
  },
  emits: ['update:username']
}
</script>

<template>
  <input
    :value="username"
     //正常是要@input="checkInput" 这样好一点
    @input="$emit('update:username', $event.target.value)"
  />
</template>

```



##### 2.vue3的写法 没有语法糖的写法

```vue
/*APP.VUE*/
<script lang="ts">
import Childx from '../src/components/comp1/Childx.vue'
import { reactive } from 'vue';
export default {
  components: { Childx },

  //这是vue3的写法
  setup(){
    interface M  {
      id:number,
      name:string,
      age:number
    }
    const userInfo:M = reactive({
      id:1,
      name:'petter',
      age:28
    })
    return{
      userInfo
    }
  }

}
</script>

<template>
  <Childx
    v-model:uid="userInfo.id"
    v-model:username="userInfo.name"
    v-model:age="userInfo.age"
  />
  <br>
  {{ userInfo.id }}
  <br>
  {{ userInfo.name }}
  <br>
  {{ userInfo.age }}
</template> 

/*Childx.vue*/

<script>
export default {
  props: {
    uid: Number,
    username: String,
    age: Number,
  },
  emits: ['update:username']
}
</script>

<template>
  <input
    :value="username"
     //正常是要@input="checkInput" 这样好一点
    @input="$emit('update:username', $event.target.value)"
  />
</template>
```



##### 3.有语法糖的写法

```vue
/*app.vue*/
<script lang="ts" setup>
import {ref} from 'vue'
import CustomInput from '@/components/comp1/CustomInput.vue'

const value = ref('')
</script>

<template>
<CustomInput v-model="value"></CustomInput>
{{ value }}
</template>
/CustomInput.vue*/
<!-- CustomInput.vue -->
<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    />
    <br>
</template>

```



#### 3.ref+emits

##### 1.父组件到子组件 使用ref属性

```vue
App.vue
<!-- Father.vue -->
<template>
  <Child ref="child" />
</template>

<script lang="ts">
// Father.vue
import { defineComponent, onMounted, ref } from 'vue'
import Child from '@/components/child.vue'

export default defineComponent({
  components: {
    Child,
  },

  setup() {
    // 给子组件定义一个 `ref` 变量
    const child = ref<InstanceType<typeof Child>>()

    // 请保证视图渲染完毕后再执行操作
    onMounted(async () => {
      // 执行子组件里面的 AJAX 请求函数 父组件调用子组件的方法
      await child.value!.queryList()
      // 显示子组件里面的弹窗(修改子组件的数据)
      child.value!.isShowDialog = true

    })

    // 必须 `return` 出去才可以给到 `<template />` 使用
    return {
      child,
    }
  },

})
</script>

```

```vue
child.vue
<!-- Child.vue -->
<template>
  <div>
  <h2>我是子组件</h2>
 <hr>
  <button @click="queryList">点击按钮显示dialog</button>
  <div v-if="isShowDialog">
  This is a dialog.
  </div>
  </div>
  </template>

  <script lang="ts">
  import { defineComponent, ref } from 'vue'

  export default defineComponent({
  setup() {
    // 一开始不显示
    const isShowDialog = ref(false)

    const queryList = async () => {
    // 执行 AJAX 请求的逻辑
    // ...

    // 模拟异步请求延迟
    await new Promise(resolve => setTimeout(resolve, 1000))

    // 异步请求完成后，显示弹窗
    isShowDialog.value = true
  }

  return {
    isShowDialog,
    queryList,
    }
  },
  })
  </script>
```

##### 2.子到父 使用emits

```vue
child.vue
<template>
  <div>
    <h2>Child Component</h2>
    <button @click="queryList">Query List</button>
    <div v-if="isShowDialog">
      This is a dialog.
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  emits: ['eventFromChild'], // 定义一个名为 'eventFromChild' 的自定义事件

  setup(_, { emit }) {
    const isShowDialog = ref(false)

    const queryList = async () => {
      // 执行 AJAX 请求的逻辑
      // ...

      // 模拟异步请求延迟
      await new Promise(resolve => setTimeout(resolve, 1000))
      
      // 异步请求完成后，显示弹窗
      isShowDialog.value = true

      // 触发自定义事件，并将数据作为参数传递给父组件
      emit('eventFromChild', isShowDialog.value)
    }

    return {
      isShowDialog,
      queryList,
    }
  },
})
</script>
```

```vue
Father.vue
<template>
  <div>
    <h2>Parent Component</h2>
    <Child @eventFromChild="handleEventFromChild" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Child from './components/child.vue';
export default defineComponent({
  methods: {
    handleEventFromChild(data:string) {
      // 在这里处理来自子组件的数据
      console.log('Received data from child component:', data)
    }
  },
})
</script>

```



### 2.爷孙组件通信

爷孙组件通信方式

![image-20230728002022286](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230728002022286.png)

provide例子

![image-20230804025251699](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804025251699.png)

接收inject例子

![image-20230804025315025](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804025315025.png)

![image-20230804025326849](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804025326849.png)

![image-20230804025343402](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804025343402.png)

**可以传入第三个参数**

### 3.兄弟组件通信

![image-20230804025419079](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804025419079.png)

#### 1.全局组件通信

1. eventBus
2. Reative State

APP.VUE

```VUE
<template>
<B1></B1>
<br>
<A1></A1>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import B1 from './components/x/B1.vue';
import A1 from './components/x/A1.vue';
import { state } from '@/state'
export default defineComponent({
  components:{B1,A1},
  setup(){
    return{
      state
    }
  }
})
</script>

```

A1.VUE

```vue
<template>
  {{ state.message }}
</template>

  <script lang="ts">
  import { state } from '@/state'
  import { defineComponent,watch } from 'vue'
  export default defineComponent({
    setup(){
      console.log(state.message)
    // Hello World

    // 因为是响应式数据，所以可以侦听数据变化
    watch(
      () => state.message,
      (val) => {
        console.log('Message 发生变化：', val)
      }
    )

    setTimeout(() => {
      state.setMessage('Hello Hello')
      // Message 发生变化： Hello Hello
    }, 1000)

    setTimeout(() => {
      state.message = 'Hi Hi'
      // Message 发生变化： Hi Hi
    }, 2000)

    return{
      state
    }
    }
  })
  </script>
```

![image-20230804134353346](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804134353346.png)

B1.VUE

```vue
<template>
  {{ state.message }}
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import A1 from './A1.vue'
import { state } from '@/state'
export default defineComponent({
  components:{A1},
  setup(){
    return{
      state
    }
  }
})
</script>

```

src/state/index.ts

```ts
// src/state/index.ts
import { reactive } from 'vue'

// 如果有多个不同业务的内部状态共享
// 使用具名导出更容易维护
export const state = reactive({
  // 设置一个属性并赋予初始值
  message: 'Hello World',

  // 添加一个更新数据的方法
  setMessage(msg: string) {
    this.message = msg
  },
})
```



3. Vuex

![image-20230804135932186](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804135932186.png)

![image-20230804135947007](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804135947007.png)

![image-20230804135958016](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804135958016.png)

例子：

```vue
<template>
{{ store.state }}
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import { useStore } from 'vuex'

export default defineComponent({
  setup() {
    // 需要创建一个 store 变量
    const store = useStore()

    // 再使用 store 去操作 Vuex 的 API
    // ...

    return{
      store
    }
  },
})
</script>
```



4. Pinia(vue3适配)



### 4.pinia

#### 1.单个store

```vue
<!-- app -->
<template>
{{ store1.message }}
<br>
{{ message1 }}
</template>

<script lang="ts">
import { defineComponent,computed,toRefs,ref,toRef} from 'vue'
// 导入状态
import { useStore } from '@/stores'
import { storeToRefs } from 'pinia'
export default defineComponent({
  setup(){
    // 定义变量拿到实例
    const store1 = useStore()

    // 直接更新message的值
    // store.message = 'New Messages'

    // 可以通过计算属性拿到message的值 但是这种方法无法直接更新message的值
    const message1 = computed({
      // 需要通过getter和setter来操作数据
      get:() => store1.message,
      // 更新message的值
      set(newValue){
        store1.message = newValue
      }
  })
    message1.value = '我设置了computed的get和set后可以直接修改了'

    // pinia的state默认是一个reactive对象 无法直接解构赋值 可以使用torefs等api来使得它可以解构赋值同时不失去响应性
    // const {message} = storeToRefs(store1)
    const {message} = toRefs(store1)
    // const message = toRef(store, 'message')
    message.value = 'hh'

    //批量更新state
    // 1.传入一个对象
    store1.$patch({
      message: 'New Message',
      randomMessages: ['msg1', 'msg2', 'msg3'],
    })
    // 2.传入一个函数
    store1.$patch((state) => {
    state.message = 'New Message'

    // 数组改成用追加的方式，而不是重新赋值
    for (let i = 0; i < 3; i++) {
      state.randomMessages.push(`msg${i + 1}`)
    }

    // 全部更新
    store1.$state = {
    message: 'New Message',
    randomMessages: ['msg1', 'msg2', 'msg3'],
  }
  // 重置
  // 3s 后重置状态02
  setTimeout(() => {
      store1.$reset()
      console.log(store1.message) // 输出最开始的 Hello World
    }, 3000)
})

  // 订阅
  // $subscribe(
  //   callback: SubscriptionCallback<S>,
  //   options?: { detached?: boolean } & WatchOptions
  // ): () => void
  // a(value) : () => void 表示定义了一个接受一个参数 value 的函数，并且没有返回值。

  // 可以在 state 出现变化时，更新本地持久化存储的数据
  store1.$subscribe((mutation, state) => {
    // 更新本地持久化存储的数据
    localStorage.setItem('store', JSON.stringify(state))
  })

  //调用getter
  // 通过变量定义一个值
  const signedMessage = store1.signedMessage('Petter')
  console.log('signedMessage', signedMessage)
  // Petter say: "The message is Hello World".

  // 2s 后改变 message
  setTimeout(() => {
    store1.message = 'New Message'

    // signedMessage 不会变
    console.log('signedMessage', signedMessage)
    // Petter say: "The message is Hello World".

    // 必须这样再次执行才能拿到更新后的值
    console.log('signedMessage', store1.signedMessage('Petter'))
    // Petter say: "The message is New Message".
  }, 2000)


  // 调用action
   // 立即执行
   console.log(store1.updateMessageSync('New message by sync.'))

  // 3s 后执行
  store1.updateMessage('New message by async.').then((res) => console.log(res))

    // 这种方式需要把整个 store 给到 template 去渲染数据
    return{
      store1,message1,message
    }
  }
})
</script>
```

```ts
// src/stores/index.ts
import { defineStore } from 'pinia'

export const useStore = defineStore('main', {

  // 先定义一个最基本的 message 数据
  state: () => ({
    // 定义数据时可以指定他们的类型
    message: 'Hello World' as string,
    randomMessages:[] as string[]
  }),
  getters:{
    fullMessage:(state) => `这条消息是${state.message}`,

    // 这个getter返回了另外一个getter的结果
    emojMessage() : string {
      return ` ${this.fullMessage}`
    },

    // 给getter传递参数 本身不支持 但是支持返回一个具备入参的函数
     // 定义一个接收入参的函数作为返回值
    //  这种方式会使得变量失去响应性 我们可以通过computed来保持响应性
     signedMessage: (state) => {
      return (name: string) => `${name} say: "The message is ${state.message}".`
    },
  },

  actions:{
    //异步更新message
    async updateMessage(newMessage:string) : Promise<string>{
      return new Promise((resolve)=>{// 创建一个Promise对象，使用resolve来表示成功的状态
        setTimeout(() => {
          this.message = newMessage// 将this.message更新为newMessage
          resolve('Async done.')// 调用resolve来表示异步操作完成，并传递一个成功的消息
        },3000)
      })
    },
    // 同步更新 message
    updateMessageSync(newMessage: string): string {
      // 这里的 this 是当前的 Store 实例
      this.message = newMessage
      return 'Sync done.'
    }
  }
})

```

#### 2.多个store

![image-20230804234346832](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804234346832.png)

![image-20230804234400679](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804234400679.png)



![image-20230804234657459](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804234657459.png)

![image-20230804234724890](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804234724890.png)

![image-20230804234734039](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230804234734039.png)

#### 3.pinia的插件系统

Pinia 拥有非常灵活的可扩展性，有专属插件可以开箱即用满足更多的需求场景。

详情：[全局状态管理 | Vue3 入门指南与实战案例 (chengpeiquan.com)](http://vue3.chengpeiquan.com/pinia.html#专属插件的使用-new)

## 

## 3.高效开发

![image-20230805145008950](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230805145008950.png)

![image-20230805145020068](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230805145020068.png)

于是产生了新的特性

![image-20230805145056584](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230805145056584.png)

![image-20230805145141374](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230805145141374.png)

**在编译的时候相当于自动转成没有语法糖的标准组件，目前还不支持那种局部的vue文件，因为需要工程化的东西转换。**



### 1.全局编译器宏

```bash
1.defineProps 用来替代props传递的
2.definEmits 用来替代Emits的
3.definerExpose 在语法糖模式下,默认return的只能在模板中使用，使用defineExpose后可以在父组件script中使用
4.withDefaults 用来对defineProps进行TS类型限制时进行默认值设置
```



### 2.JSX/TSX语法

```vue
<script setup lang="ts">
import { defineProps } from 'vue';

interface Props {
  title: string;
}

const props = defineProps<Props>();

const HelloWorld = () => {
  return (
    <div>
      <h1>{props.title}</h1>
      <p>This is a TypeScript JSX component in Vue.</p>
    </div>
  );
};
</script>

<template>
  <HelloWorld title="Hello, World!" />
</template>

<style scoped>
h1 {
  color: blue;
}
</style>
```

```react
import React from 'react';

interface Props {
  title: string;
}

const HelloWorld: React.FC<Props> = ({ title }) => {
  return (
    <div>
      <h1>{title}</h1>
      <p>This is a TypeScript JSX component in React.</p>
    </div>
  );
};

export default HelloWorld;
```



### 3.新特性语法糖的好处

```bash
template操作简化(变量无需return,子组件无需注册)
```



### 4.props接收方式

![image-20230805154116284](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230805154116284.png)

**不指定的意思是父组件直接传给子组件的属性，不是子组件所必须的属性。**

![image-20230809163635133](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809163635133.png)

![image-20230809163649353](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809163649353.png)

![image-20230809163705759](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809163705759.png)



### 5.withDefaults的基本用法

![image-20230809163745686](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809163745686.png)



### 6.emits的接收方式

```VUE
A1.VUE
<template>
  <!-- 点击以后触发事件handleButtonClick -->
  <button @click="handleButtonClick">点击改变名字</button>
</template>

<script setup lang="ts">
import { useAttrs } from 'vue'
import { ref } from 'vue';

// 定义一个事件来改变消息  用途:组件中有时候需要用户点击才改变组件
const emits = defineEmits(['update-message'])
const message = ref('我是一开始的消息')

// 子组件中要定义一个函数来处理事件
const handleButtonClick = () => {
  message.value = '我是改变的消息'
  emits('update-message',message)
}

</script>
```

```VUE
APP.VUE
<template>
  <!-- 父组件引用子组件时需要传值 -->
  <A1 @update-message="getUpdateMessage"></A1>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import A1 from './components/x/A1.vue';

// 父组件要定义一个函数来处理和update-message绑定的事件 参数可以拿到子组件的值
const getUpdateMessage = (msg:string) => {
  console.log('接收到子组件的值',msg);
}

</script>
```



### 7.useAttrs的基础用法

```ts
import { useAttrs } from 'vue'

// 获取 attrs
const attrs = useAttrs()

// attrs 是个对象，和 props 一样，需要通过 `key` 来得到对应的单个 attr
console.log(attrs.msg)
```



### 8.slots的接收方式

![image-20230809164415006](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809164415006.png)

如果是新语法糖模式下要要用useSlots来渲染



### 9.子组件插槽也可以像组件一样给父组件传递东西

```vue
<script setup>
import MyComponent from './MyComponent.vue'
</script>

<template>
	<MyComponent v-slot="slotProps">
  	{{ slotProps.text }} {{ slotProps.count }}
  </MyComponent>
</template>
```

```vue
<script setup>
const greetingMessage = 'hello'
</script>

<template>
  <div>
  	<slot :text="greetingMessage" :count="1"></slot>
	</div>
</template>
```



### 10.ref的通信方式

![image-20230809164830460](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809164830460.png)

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



### 11.await支持

![image-20230809164845561](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809164845561.png)



### 12.命名技巧

```java
1.vue路由组件放在src/views目录下，以单个名词或动词进行命名，有多个的要用s或list
2.公共组件组件通常存放在 src/components目录,以大驼峰命名法命名(为了和基本HTML元素区别)
3.公共方法一般放在src/libs目录下，以一个名词或者动词作为文件命名(例如常用的正则表达式，可以归类到 regexp.ts)
4.对于经常用到的 TypeScript 类型，也可以抽离成公共文件，笔者习惯在 src/types 目录管理公共类型，统一使用 .ts 作为扩展名并在里面导出 TS 类型，而不使用 .d.ts 这个类型声明文件(这样做的好处是在使用到相应类型时，可以通过 import type 显式导入，在后期的项目维护过程中，可以很明确的知道类型来自于哪里，并且更接近从 npm 包里导入类型使用的开发方式。)
5.TS类型使用大驼峰命名法(方便和声明的变量作为区分，大部分情况下一看到 GameInfo 就知道是类型，而 gameInfo 则是一个变量)
6.变量和函数的命名就是小驼峰命名法
7.类的命名遵循大驼峰命名法
```

**4**

![image-20230809165504516](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165504516.png)

![image-20230809165514639](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165514639.png)

**6**

![image-20230809165722294](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165722294.png)

![image-20230809165735781](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165735781.png)

![image-20230809165746549](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165746549.png)



**函数**

![image-20230809165804650](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165804650.png)

![image-20230809165818481](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165818481.png)

**类**

![image-20230809165837316](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230809165837316.png)
