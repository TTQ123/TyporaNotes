# Vue3和React之间的区别

**很明显的一个区别是 vue拥抱前端三剑客  react则是拥抱js(大部分情况都交给js完成)**

```js
1.模版语法的不同 vue基于html的模版语法 react函数式组件(jsx)
2.俩个框架都是采用Proxy作为响应式系统的核心 但是vue3的响应式更完整
3.性能优化：Vue3在编译阶段进行了一些优化，如静态树提升、静态属性提升等，
使得其构建出的代码更加高效。React18通过引入并发模式和懒加载等技术来提高性能。
4.组件通信的实现不一样
5.状态管理使用的库原理类似
```

**总结**

```bash
1.vue对新手更为友好 有很多插件和最佳实践标准 
2.react 做项目需要自己思考的事情很多，react 的 api 其实很少，它很灵活，只关注核心能力比如数据驱动视图、jsx等，其他的全权交给开发者处理。
3.Vue3更加注重开发体验和响应式系统的性能优化，适合开发小型应用或单页面应用；而React18更加注重开发效率和性能的提升，适合开发大型应用或多个页面的应用。
```



## 区别详解

### 1.vue组件和react组件

![image-20230928193011952](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193011952.png)

```vue
<template>
  <div class=my-component>
    <!-- HTML模板 -->
  </div>
</template>

<script>
export default {
  // JavaScript代码
}
</script>

<style>
.my-component {
  /* CSS样式 */
}
</style>
```

```react
import React from 'react';
import './MyComponent.css';

function MyComponent() {
  // JavaScript代码
  return (
    <div className=my-component>
      {/* HTML模板 */}
    </div>
  );
}

export default MyComponent;
```

`总结：这两种框架它们的最终趋势都是函数式编程，不管是 `Vue` 还是 `React` 都是推荐我们引入大量内置的函数或者是 use 函数来进行组合并且完成我们的开发需求。而简化使用面向对象或者是配置的写法，能简化我们使用 `this` 的场景从而提升代码的灵活度和简易度。`





### 2.模版语法

1. `Vue` 采用 `<template>` 字符串模板。更贴近 `HTML`，学习成本低，但有时候不灵活。
2. `React` 采用 `JSX` 语法，更类似于 `js` ，限制比较多，（像一些关键字 `class`、`for`，单标签要闭合、属性要驼峰、组件名要大写等等这些都要注意），但是可以跟模板语法很好的进行结合

![image-20230928192847649](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928192847649.png)

![image-20230928191302668](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191302668.png)





### 3.响应式

![image-20230928193924815](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193924815.png)

![image-20230928191342185](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191342185.png)



### 4.性能优化

![image-20230928191401191](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191401191.png)



### 5.组件通信

vue3

![image-20230928191436567](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191436567.png)

react18

![image-20230928191456671](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191456671.png)



### 6.状态管理

![image-20230928191516276](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191516276.png)

![image-20230928191525444](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928191525444.png)

**对比**

![image-20230928193455669](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193455669.png)



### 7.指令

`vue中的指令是为了用于在HTML模板中添加DOM元素、属性、事件，react中没有，但是我们可以通过自己封装来实现`

![image-20230928192433694](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928192433694.png)

#### 1.if指令

```react
function App({ children }) {
  return (
    {
        awesome && <>React is awesome too!</>
    }
    {
        !awesome && <>Oh no  </>
    }
    // 或
    {
        awesome ? <>React is awesome too!</> : <>Oh no  </>
    }
  );
}
```

#### 2.for指令

```react
function App({ children }) {
  return (
    {
        [1, 2, 3].map(item => {
            return <div key={item}>{item}</div>
        })
    }
  );
}
```



### 8.事件

![image-20230928192633315](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928192633315.png)

![image-20230928192658546](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928192658546.png)

**对比**

![image-20230928193738053](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193738053.png)

![image-20230928193746648](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193746648.png)



### 9.路由

![image-20230928193301795](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193301795.png)

#### 1.vue路由实例

![image-20230928193324934](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193324934.png)

![image-20230928193334987](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193334987.png)

#### 2.react路由实例

```react
import React from 'react'
import { BrowserRouter as Router, Switch, Route, Link, useParams, useHistory } from 'react-router-dom'
import Home from './components/Home'
import About from './components/About'

const App = () => {
  return (
    <Router>
      <div>
        <ul>
          <li><Link to=/>Home</Link></li>
          <li><Link to=/about>About</Link></li>
        </ul>

        <hr/>

        <Switch>
          <Route exact path=/>
            <Home />
          </Route>
          <Route path=/about>
            <About />
          </Route>
        </Switch>
      </div>
    </Router>
  )
}

const Home = () => {
  const history = useHistory()
  const handleClick = () => {
    history.push('/about')
  }
  return (
    <div>
      <h1>Home Page</h1>
      <button onClick={handleClick}>Go to About Page</button>
    </div>
  )
}

const About = () => {
  const { id } = useParams()
  return (
    <div>
      <h1>About Page</h1>
      <p>Param: {id}</p>
      <Link to=/>Go to Home Page</Link>
    </div>
  )
}

export default App
```



### 10.其它细节

#### 1.模板和样式对比

![image-20230928193810255](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193810255.png)



#### 2.表单和组件通信

![image-20230928193829722](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193829722.png)



#### 3.逻辑复用和内容分发(文本自定义)、DOM操作

![image-20230928193858735](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928193858735.png)



#### 4.处理副作用

**副作用指的是与组件渲染结果无关的任何操作，例如：发送网络请求、修改DOM元素、访问本地存储、订阅或取消订阅事件、改变组件状态外的变量等。这些操作会影响组件的行为和状态，但是并不会直接影响渲染结果。我们应该将副作用分离出来，以便更好地控制组件的行为和状态。**

`vue使用，watchEffect()         react使用，useEffect()`

都是处理副作用的方法，用法上还是有很大区别的。

![image-20230928194339692](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928194339692.png)

watchEffect会自动根据所依赖的值进行重渲染，而useEffect要明确指定对应的值才能进行重渲染，React团队已经给出在未来的版本中可能会改成根据所依赖的值自动进行重渲染的操作，但暂时还不行。

watchEffect在更新前和卸载前触发的方式是通过回调函数的参数被调用来实现的，而useEffect是通过return的返回值来指定的。

![image-20230928194135796](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230928194135796.png)