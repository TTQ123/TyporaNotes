# React 入门

## React 简介

### React 为何物

React：用于构建用户界面的 JavaScript 库。由 `Facebook` 开发且开源。

### 为何学习 React

原生 JavaScript 的痛点：

- 操作 DOM 繁琐、效率低
- 使用 JavaScript 直接操作 DOM，浏览器进行大量重绘重排
- 原生 JavaScript 没有组件化编码方案，代码复用率低

React 的特点：

- 采用组件化模式、声明式编码，提高开发效率和组件复用率
- 在 `React Native` 中可用 React 语法进行移动端开发
- 使用虚拟 DOM 和 Diffing 算法，减少与真实 DOM 的交互

## React 初体验

### 来一发 Hello React

相关 JS 库：

- `react.development.js` ：React 核心库
- `react-dom.development.js` ：提供 DOM 操作的 React 扩展库
- `babel.min.js` ：解析 JSX 语法，转换为 JS 代码

```html
<!-- 准备好一个“容器” -->
<div id="test"></div>

<!-- 引入react核心库 -->
<script type="text/javascript" src="../js/react.development.js"></script>
<!-- 引入react-dom，用于支持react操作DOM -->
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<!-- 引入babel，用于将jsx转为js -->
<script type="text/javascript" src="../js/babel.min.js"></script>

<!-- 此处一定要写babel，表示写的不是 JS，而是 JSX，并且靠 babel 翻译 -->
<script type="text/babel">
  //1.创建虚拟DOM
  // 不要写引号，因为不是字符串
  const VDOM = <h1>Hello,React</h1>

  //2.渲染虚拟DOM到页面
  // 导入核心库和扩展库后，会有 React 和 ReactDOM 两个对象
  ReactDOM.render(VDOM, document.getElementById('test'))
</script>
```

### 创建虚拟 DOM 的两种方式：JS 和 JSX

- 使用 JS 创建虚拟 DOM 比 JSX 繁琐
- JSX 可以让程序员更加简单地创建虚拟 DOM，相当于语法糖
- 最终 babel 会把 JSX 语法转换为 JS

```html
<script type="text/javascript">
  //1.使用 React 提供的 API 创建虚拟DOM
  const VDOM = React.createElement('h1', { id: 'title' }, React.createElement('span', {}, 'Hello,React'))
  //2.渲染虚拟DOM到页面
  ReactDOM.render(VDOM, document.getElementById('test'))
</script>
```

```html
<script type="text/babel">
  //1.创建虚拟DOM
  const VDOM = (
    <h1 id="title">
      <span>Hello,React</span>
    </h1>
  )
  //2.渲染虚拟DOM到页面
  ReactDOM.render(VDOM, document.getElementById('test'))
</script>
```

### 虚拟 DOM && 真实 DOM

关于虚拟 DOM：

1. 本质是 Object 类型的对象（一般对象）
2. 虚拟 DOM 比较“轻”，真实 DOM 比较“重”，因为虚拟 DOM 是 React 内部在用，无需真实 DOM 上那么多的属性。
3. 虚拟 DOM 最终会被 React 转化为真实 DOM，呈现在页面上。

```html
<script type="text/babel">
  const VDOM = (
    <h1 id="title">
      <span>Hello,React</span>
    </h1>
  )
  ReactDOM.render(VDOM, document.getElementById('test'))

  const TDOM = document.getElementById('demo')
  console.log('虚拟DOM', VDOM)
  console.log('真实DOM', TDOM)
</script>
```

## JSX

### JSX 简介

- 全称：JavaScript XML
- React 定义的类似于 XML 的 JS 扩展语法；本质是 `React.createElement()` 方法的语法糖
- 作用：简化创建虚拟 DOM

### JSX 语法规则

- 定义虚拟 DOM 时，不要写引号
- 标签中混入 JS 表达式需要使用 `{}`
- 指定类名不用 `class`，使用 `className`
- 内联样式，使用 `style={ { key: value } }` 的形式
- 只能有一个根标签
- 标签必须闭合，单标签结尾必须添加 `/`：`<input type="text" />`
- 标签首字母小写，则把标签转换为 HTML 对应的标签，若没有，则报错
- 标签首字母大写，则渲染对应组件，若没有定义组件，则报错

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>jsx语法规则</title>
    <style>
      .title {
        background-color: orange;
        width: 200px;
      }
    </style>
  </head>
  <body>
    <div id="test"></div>
    ...
    <script type="text/babel">
      const myId = 'aTgUiGu'
      const myData = 'HeLlo,rEaCt'

      const VDOM = (
        <div>
          <h2 className="title" id={myId.toLowerCase()}>
            <span style={{ color: 'white', fontSize: '19px' }}>{myData.toLowerCase()}</span>
          </h2>
          <input type="text" />
          // <good>very good</good>
          // <Child></Child>
        </div>
      )

      ReactDOM.render(VDOM, document.getElementById('test'))
    </script>
  </body>
</html>
```

### JSX 例子

注意区分：**JS 语句(代码)** 与 **JS 表达式**：

1. 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方

```js
a
a + b
demo(1)
arr.map()
function test() {}
```

2. 语句(代码)：

```js
if(){}
for(){}
switch(){case:xxxx}
```

```html
<script type="text/babel">
  let list = ['Angular', 'React', 'Vue'] const VDOM = (
  <div>
    <h1>前端js框架列表</h1>
    <ul>
      // React 会自动遍历数组
      {list.map((item, index) => {
        // Each child in a list should have a unique "key" prop.
        return <li key={index}>{item}</li>
      })}
    </ul>
  </div>
  ) ReactDOM.render(VDOM, document.getElementById('test'))
</script>
```

# React 面向组件编程

## 函数式组件

```
<script type="text/babel">
  //1.创建函数式组件
  function MyComponent() {
    //此处的 this 是 undefined，因为 babel 编译后开启了严格模式
    console.log(this)
    return <h2>我是用函数定义的组件(适用于【简单组件】的定义)</h2>
  }
  //2.渲染组件到页面
  ReactDOM.render(<MyComponent />, document.getElementById('test'))
</script>
```

要点：

- 组件名称首字母必须大写，否则会解析成普通标签导致报错，详见 JSX 语法规则
- 函数需返回一个虚拟 DOM
- 渲染组件时需要使用标签形式，同时标签必须闭合

渲染组件的过程：

- React 解析标签，寻找对应组件
- 发现组件是函数式组件，则调用函数，将返回的虚拟 DOM 转换为真实 DOM ，并渲染到页面中

## 类式组件

```
<script type="text/babel">
  // 创建类式组件
  class MyComponent extends React.Component {
    render() {
      console.log('render中的this：', this)
      return <h2>我是用类定义的组件(适用于【复杂组件】的定义)</h2>
    }
  }
  ReactDOM.render(<MyComponent />, document.getElementById('test'))
</script>
```

组件渲染过程：

- React 解析组件标签，寻找组件
- 发现是类式组件，则 `new` 该类的实例对象，通过实例调用原型上的 `render` 方法
- 将 `render` 返回的虚拟 DOM 转为真实 DOM ，渲染到页面上

## 组件实例核心属性 state

`state` 是组件实例对象最重要的属性，值为对象。又称为状态机，通过更新组件的 `state` 来更新对应的页面显示。

要点：

- 初始化 `state`
- React 中事件绑定
- `this` 指向问题
- `setState` 修改 `state` 状态
- `constructor` 、`render` 、自定义方法的调用次数

```
<script type="text/babel">
  class Weather extends React.Component {
    // 调用一次
    constructor(props) {
      super(props)
      // 初始化 state
      this.state = { isHot: true, wind: '微风' }
      // 解决 this 指向问题
      this.changeWeather = this.changeWeather.bind(this)
    }
    // 调用 1+N 次
    render() {
      // 读取状态
      const { isHot } = this.state
      return <h1 onClick={this.changeWeather}>今天天气 {isHot ? '炎热' : '凉爽'}</h1>
    }
    // 点一次调一次
    changeWeather() {
      const isHot = this.state.isHot
      // 对 state 的修改是一种合并而非替换，即 wind 依然存在
      this.setState({ isHot: !isHot })
    }
  }

  ReactDOM.render(<Weather />, document.getElementById('test'))
</script>
```

简化版：

```
<script>
  class Weather extends React.Component {
    state = { isHot: true, wind: '微风' }

    render() {
      const { isHot } = this.state
      return <h2 onClick={this.changeWeather}>天气{isHot ? '炎热' : '凉爽'}</h2>
    }

    // 采用箭头函数 + 赋值语句形式
    changeWeather = () => {
      const isHot = this.state.isHot
      this.setState = { isHot: !isHot }
    }
  }

  ReactDOM.render(<Weather />, document.getElementById('test'))
</script>
```

## 组件实例核心属性 props

每个组件对象都有 `props` 属性，组件标签的属性都保存在 `props` 中。

`props` 是只读的，不能修改。

### props 基本使用

```
<script type="text/babel">
  class Person extends React.Component {
    render() {
      const { name, age, sex } = this.props
      return (
        <ul>
          <li>姓名：{name}</li>
          <li>性别：{sex}</li>
          <li>年龄：{age}</li>
        </ul>
      )
    }
  }

  // 类似于标签属性传值
  ReactDOM.render(<Person name="Lily" age={19} sex="男" />, document.getElementById('test'))
</script>
```

### 批量传递 props

```
<script type="text/babel">
  class Person extends React.Component {
    render() {
      const { name, age, sex } = this.props
      return (
        <ul>
          <li>姓名：{name}</li>
          <li>性别：{sex}</li>
          <li>年龄：{age}</li>
        </ul>
      )
    }
  }

  const obj = { name: 'Ben', age: 21, sex: '女' }
  ReactDOM.render(<Person {...obj} />, document.getElementById('test'))
</script>
```

### 限制 props

在 `React 15.5` 以前，`React` 身上有一个 `PropTypes` 属性可直接使用，即 `name: React.PropTypes.string.isRequired` ，没有把 `PropTypes` 单独封装为一个模块。

从 `React 15.5` 开始，把 `PropTypes` 单独封装为一个模块，需要额外导入使用。

```
<!-- 引入prop-types，用于对组件标签属性进行限制 -->
<script type="text/javascript" src="../js/prop-types.js"></script>

<script type="text/babel">
  class Person extends React.Component {
    render() {
      const { name, age, sex } = this.props
      return (
        <ul>
          <li>姓名：{name}</li>
          <li>性别：{sex}</li>
          <li>年龄：{age}</li>
        </ul>
      )
    }
  }

  // 类型和必要性限制
  Person.propTypes = {
    name: PropTypes.string.isRequired,
    sex: PropTypes.string,
    age: PropTypes.number,
    // 限制 speak 为函数
    speak: PropTypes.func,
  }

  // 指定默认值
  Person.defaultProps = {
    sex: 'male',
    age: 19,
  }

  ReactDOM.render(<Person name="Vue" sex="male" age={11} speak={speak} />, document.getElementById('test'))

  function speak() {
    console.log('speaking...')
  }
</script>
```

### props 的简写形式

`Person.propTypes` 和 `Person.defaultProps` 可以看作在类身上添加属性，利用 `static` 关键词就能在类内部进行声明。因此所谓简写只是从类外部移到类内部。

```
<!-- 引入prop-types，用于对组件标签属性进行限制 -->
<script type="text/javascript" src="../js/prop-types.js"></script>

<script type="text/babel">
  class Person extends React.Component {
    static propTypes = {
      name: PropTypes.string.isRequired,
      sex: PropTypes.string,
      age: PropTypes.number,
      // 限制 speak 为函数
      speak: PropTypes.func,
    }
    static defaultProps = {
      sex: 'male',
      age: 19,
    }

    render() {
      const { name, age, sex } = this.props
      return (
        <ul>
          <li>姓名：{name}</li>
          <li>性别：{sex}</li>
          <li>年龄：{age}</li>
        </ul>
      )
    }
  }

  ReactDOM.render(<Person name="Vue" sex="male" age={11} speak={speak} />, document.getElementById('test'))

  function speak() {
    console.log('speaking...')
  }
</script>
```

### 类式组件的构造器与 props

[官网文档说明](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Freact-component.html%23constructor)

构造函数一般用在两种情况：

- 通过给 `this.state` 赋值对象来初始化内部 `state`
- 为事件处理函数绑定实例

```
constructor(props) {
  super(props)
  // 初始化 state
  this.state = { isHot: true, wind: '微风' }
  // 解决 this 指向问题
  this.changeWeather = this.changeWeather.bind(this)
}
```

因此构造器一般都不需要写。如果要在构造器内使用 `this.props` 才声明构造器，并且需要在最开始调用 `super(props)` ：

```
constructor(props) {
  super(props)
  console.log(this.props)
}
```

### 函数式组件使用 props

由于函数可以传递参数，因此函数式组件可以使用 `props` 。

```
<!-- 引入prop-types，用于对组件标签属性进行限制 -->
<script type="text/javascript" src="../js/prop-types.js"></script>

<script type="text/babel">
  function Person(props) {
    const { name, age, sex } = props
    return (
      <ul>
        <li>姓名：{name}</li>
        <li>性别：{sex}</li>
        <li>年龄：{age}</li>
      </ul>
    )
  }
  Person.propTypes = {
    name: PropTypes.string.isRequired,
    sex: PropTypes.string,
    age: PropTypes.number,
  }

  Person.defaultProps = {
    sex: '男',
    age: 18,
  }

  ReactDOM.render(<Person name="jerry" />, document.getElementById('test'))
</script>
```

## 组件实例核心属性 refs

通过定义 `ref` 属性可以给标签添加标识。

### 字符串形式的 ref

这种形式已过时，效率不高，[官方](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Frefs-and-the-dom.html%23legacy-api-string-refs)不建议使用。

```
<script type="text/babel">
  class Demo extends React.Component {
    showData = () => {
      const { input1 } = this.refs
      alert(input1.value)
    }
    render() {
      return (
        <div>
          <input ref="input1" type="text" placeholder="点击按钮提示数据" />
          &nbsp;
          <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        </div>
      )
    }
  }

  ReactDOM.render(<Demo />, document.getElementById('test'))
</script>
```

### 回调形式的 ref

要点：

- `c => this.input1 = c` 就是给组件实例添加 `input1` 属性，值为节点
- 由于是箭头函数，因此 `this` 是 `render` 函数里的 `this` ，即组件实例

```
<script type="text/babel">
  class Demo extends React.Component {
    showData = () => {
      const { input1 } = this
      alert(input1.value)
    }
    render() {
      return (
        <div>
          <input
            ref={(c) => {
              this.input1 = c
            }}
            type="text"
            placeholder="点击按钮提示数据"
          />
          &nbsp;
          <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        </div>
      )
    }
  }

  ReactDOM.render(<Demo />, document.getElementById('test'))
</script>
```

关于回调 `ref` 执行次数的问题，[官网](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Frefs-and-the-dom.html%23caveats-with-callback-refs)描述：

::: tip 如果 `ref` 回调函数是以内联函数的方式定义的，在更新过程中它会被执行两次，第一次传入参数 `null`，然后第二次会传入参数 DOM 元素。这是因为在每次渲染时会创建一个新的函数实例，所以 React 清空旧的 `ref` 并且设置新的。通过将 `ref` 的回调函数定义成 `class` 的绑定函数的方式可以避免上述问题，但是大多数情况下它是无关紧要的。 :::

即内联函数形式，在更新过程中 `ref` 回调会被执行两次，第一次传入 `null` ，第二次传入 DOM 元素。若是下述形式，则只执行一次。但是对功能实现没有影响，因此一般也是用内联函数形式。

```
<script type="text/babel">
  //创建组件
  class Demo extends React.Component {
    state = { isHot: false }

    changeWeather = () => {
      const { isHot } = this.state
      this.setState({ isHot: !isHot })
    }

    saveInput = (c) => {
      this.input1 = c
      console.log('@', c)
    }

    render() {
      const { isHot } = this.state
      return (
        <div>
          <h2>今天天气很{isHot ? '炎热' : '凉爽'}</h2>
          <input ref={this.saveInput} type="text" />
        </div>
      )
    }
  }

  ReactDOM.render(<Demo />, document.getElementById('test'))
</script>
```

### createRef API

该方式通过调用 `React.createRef` 返回一个容器用于存储节点，且一个容器只能存储一个节点。

```
<script type="text/babel">
  class Demo extends React.Component {
    myRef = React.createRef()
    myRef2 = React.createRef()

    showData = () => {
      alert(this.myRef.current.value)
    }

    showData2 = () => {
      alert(this.myRef2.current.value)
    }
    render() {
      return (
        <div>
          <input ref={this.myRef} type="text" placeholder="点击按钮提示数据" />
          &nbsp;
          <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
          <input onBlur={this.showData2} ref={this.myRef2} type="text" placeholder="失去焦点提示数据" />
          &nbsp;
        </div>
      )
    }
  }

  ReactDOM.render(<Demo />, document.getElementById('test'))
</script>
```

### 事件处理

- React 使用自定义事件，而非原生 DOM 事件，即 `onClick、onBlur` ：为了更好的兼容性
- React 的事件通过事件委托方式进行处理：为了高效
- 通过 `event.target` 可获取触发事件的 DOM 元素：勿过度使用 `ref`

当触发事件的元素和需要操作的元素为同一个时，可以不使用 `ref` ：

```
class Demo extends React.Component {
  showData2 = (event) => {
    alert(event.target.value)
  }

  render() {
    return (
      <div>
        <input onBlur={this.showData2} type="text" placeholder="失去焦点提示数据" />
        &nbsp;
      </div>
    )
  }
}
```

## 受控 & 非受控组件

包含表单的组件分类：

- 非受控组件：现用现取。即需要使用时，再获取节点得到数据
- 受控组件：类似于 Vue 双向绑定的从视图层绑定到数据层

尽量使用受控组件，因为非受控组件需要使用大量的 `ref` 。

```
// 非受控组件
class Login extends React.Component {
  handleSubmit = (event) => {
    event.preventDefault()
    const { username, password } = this
    alert(`用户名是：${username.value}, 密码是：${password.value}`)
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        用户名：
        <input ref={(c) => (this.username = c)} type="text" name="username" />
        密码：
        <input ref={(c) => (this.password = c)} type="password" name="password" />
        <button>登录</button>
      </form>
    )
  }
}
// 受控组件
class Login extends React.Component {
  state = {
    username: '',
    password: '',
  }

  saveUsername = (event) => {
    this.setState({ username: event.target.value })
  }

  savePassword = (event) => {
    this.setState({ password: event.target.value })
  }

  handleSubmit = (event) => {
    event.preventDefault()
    const { username, password } = this.state
    alert(`用户名是：${username}, 密码是：${password}`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        用户名：
        <input onChange={this.saveUsername} type="text" name="username" />
        密码：
        <input onChange={this.savePassword} type="password" name="password" />
        <button>登录</button>
      </form>
    )
  }
}
```

对上述受控组件的代码进行优化，希望把 `saveUsername` 和 `savePassword` 合并为一个函数。

要点：

- 高阶函数：参数为函数或者返回一个函数的函数，如 `Promise、setTimeout、Array.map()`
- 函数柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式

```
// 函数柯里化
function sum(a) {
  return (b) => {
    return (c) => {
      return a + b + c
    }
  }
}
// 使用高阶函数和柯里化写法
class Login extends React.Component {
  state = {
    username: '',
    password: '',
  }

  saveFormData = (dataType) => {
    return (event) => {
      this.setState({ [dataType]: event.target.value })
    }
  }

  handleSubmit = (event) => {
    event.preventDefault()
    const { username, password } = this.state
    alert(`用户名是：${username}, 密码是：${password}`)
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        用户名：
        <input onChange={this.saveFormData('username')} type="text" name="username" />
        密码：
        <input onChange={this.saveFormData('password')} type="password" name="password" />
        <button>登录</button>
      </form>
    )
  }
}
// 不使用柯里化写法
class Login extends React.Component {
  state = {
    username: '',
    password: '',
  }

  saveFormData = (dataType, event) => {
    this.setState({ [dataType]: event.target.value })
  }

  handleSubmit = (event) => {
    event.preventDefault()
    const { username, password } = this.state
    alert(`用户名是：${username}, 密码是：${password}`)
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        用户名：
        <input onChange={(event) => this.saveFormData('username', event)} type="text" name="username" />
        密码：
        <input onChange={(event) => this.saveFormData('password', event)} type="password" name="password" />
        <button>登录</button>
      </form>
    )
  }
}
```

## 生命周期

### 生命周期旧版

**初始化阶段**：`ReactDOM.render()` 触发的初次渲染

- `constructor`
- `componentWillMount`
- `render`
- `componentDidMount`

**更新阶段**

1. 父组件重新 `render` 触发的更新

- `componentWillReceiveProps`
- `shouldComponentUpdate` ：控制组件是否更新的阀门，返回值为布尔值，默认为 `true` 。若返回 `false` ，则后续流程不会进行。
- `componentWillUpdate`
- `render`
- `componentDidUpdate`

1. 组件内部调用 `this.setState()` 修改状态

- `shouldComponentUpdate`
- `componentWillUpdate`
- `render`
- `componentDidUpdate`

1. 组件内部调用 `this.forceUpdate()` 强制更新

- `componentWillUpdate`
- `render`
- `componentDidUpdate`

**卸载阶段**：`ReactDOM.unmountComponentAtNode()` 触发

- `componentWillUnmount`

![React Lifecycle](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/react-lifecyle-old.png)

### 生命周期新版

[更改内容](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fblog%2F2018%2F03%2F27%2Fupdate-on-async-rendering.html)：

- 废弃三个钩子：`componentWillMount` 、`componentWillReceiveProps` 、 `componentWillUpdate` 。在新版本中这三个钩子需要加 `UNSAFE_` 前缀才能使用，后续可能会废弃。
- 新增两个钩子（实际场景用得很少）：`getDerivedStateFromProps` 、`getSnapshotBeforeUpdate`

![React LIfecycle New](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/react-lifecycle-new.png)

[static getDerivedStateFromProps(props, state)](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Freact-component.html%23static-getderivedstatefromprops)：

- 需使用 `static` 修饰
- 需返回一个对象更新 `state` 或返回 `null`
- 适用于如下情况：`state` 的值任何时候都取决于 `props`

[getSnapshotBeforeUpdate(prevProps, prevState)](https://gitee.com/link?target=https%3A%2F%2Fzh-hans.reactjs.org%2Fdocs%2Freact-component.html%23getsnapshotbeforeupdate)：

- 在组件更新之前获取快照
- 得组件能在发生更改之前从 DOM 中捕获一些信息（如滚动位置）
- 返回值将作为参数传递给 `componentDidUpdate()`

```
static getDerivedStateFromProps(props,state){
  console.log('getDerivedStateFromProps',props,state);
  return null
}

getSnapshotBeforeUpdate(){
  console.log('getSnapshotBeforeUpdate');
  return 'atguigu'
}

componentDidUpdate(preProps,preState,snapshotValue){
  console.log('componentDidUpdate',preProps,preState,snapshotValue);
}
// getSnapshotBeforeUpdate 案例
class NewsList extends React.Component {
  state = { newsArr: [] }

  componentDidMount() {
    setInterval(() => {
      //获取原状态
      const { newsArr } = this.state
      //模拟一条新闻
      const news = '新闻' + (newsArr.length + 1)
      //更新状态
      this.setState({ newsArr: [news, ...newsArr] })
    }, 1000)
  }

  getSnapshotBeforeUpdate() {
    return this.refs.list.scrollHeight
  }

  componentDidUpdate(preProps, preState, height) {
    this.refs.list.scrollTop += this.refs.list.scrollHeight - height
  }

  render() {
    return (
      <div className="list" ref="list">
        {this.state.newsArr.map((n, index) => {
          return (
            <div key={index} className="news">
              {n}
            </div>
          )
        })}
      </div>
    )
  }
}
ReactDOM.render(<NewsList />, document.getElementById('test'))
```

### 最重要的三个钩子

- `render` ：初始化渲染和更新渲染
- `componentDidMount` ：进行初始化，如开启定时器、发送网络请求、订阅消息
- `componentWillUnmount` ：进行收尾，如关闭定时器、取消订阅消息

## 虚拟 DOM 与 Diff 算法

![Diff](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/Diff.png)

**`key` 的作用：**

`key` 是虚拟 DOM 对象的标识，可提高页面更新渲染的效率。

当状态中的数据发生变化时，React 会根据新数据生成新的虚拟 DOM ，接着对新旧虚拟 DOM 进行 Diff 比较，规则如下：

- 旧虚拟 DOM 找到和新虚拟 DOM 相同的 key：
  - 若内容没变，直接复用真实 DOM
  - 若内容改变，则生成新的真实 DOM ，替换页面中之前的真实 DOM
- 旧虚拟 DOM 未找到和新虚拟 DOM 相同的 key：根据数据创建新的真实 DOM ，渲染到页面

**使用 `index` 作为 `key` 可能引发的问题：**

- 若对数据进行逆序添加、逆序删除等破坏顺序的操作，会进行没有必要的真实 DOM 更新。界面效果没问题，但效率低下。
- 如果结构中包含输入类的 DOM（如 input 输入框） ，则会产生错误的 DOM 更新。
- 若不存在对数据逆序添加、逆序删除等破坏顺序的操作，则没有问题。

```
// 使用 index 作为 key 引发的问题
class Person extends React.Component {
  state = {
    persons: [
      { id: 1, name: '小张', age: 18 },
      { id: 2, name: '小李', age: 19 },
    ],
  }

  add = () => {
    const { persons } = this.state
    const p = { id: persons.length + 1, name: '小王', age: 20 }
    this.setState({ persons: [p, ...persons] })
  }

  render() {
    return (
      <div>
        <h2>展示人员信息</h2>
        <button onClick={this.add}>添加小王</button>
        <h3>使用index作为key</h3>
        <ul>
          {this.state.persons.map((personObj, index) => {
            return (
              <li key={index}>
                {personObj.name}---{personObj.age}
                <input type="text" />
              </li>
            )
          })}
      </div>
    )
  }
}
```

# React 脚手架

## 创建 React 项目

- 全局安装 React 脚手架：`npm i -g create-react-app`
- 创建项目：`create-react-app 项目名称`
- 进入文件夹：`cd 项目名称`
- 启动项目：`npm start`

上述方式已经过时，改用下方命令。详见[官方说明](https://gitee.com/link?target=https%3A%2F%2Fcreate-react-app.dev%2Fdocs%2Fgetting-started)。

```
npx create-react-app my-app
cd my-app
npm start
```

## React 脚手架项目结构

`public` ：静态资源文件

- `manifest.json` ：应用加壳（把网页变成安卓/IOS 软件）的配置文件
- `robots.txt` ：爬虫协议文件

`src` ：源码文件

- `App.test.js` ：用于给 `App` 组件做测试，一般不用
- `index.js` ：入口文件
- `reportWebVitals.js` ：页面性能分析文件，需要 `web-vitals` 库支持
- `setupTests.js` ：组件单元测试文件，需要 `jest-dom` 库支持

![React-cli structure](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/React-cli.png)

`index.html` 代码分析：

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <!-- %PUBLIC_URL% 代表 public 文件夹的路径 -->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <!-- 开启理想视口，用于做移动端网页的适配 -->
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- 用于配置浏览器页签+地址栏的颜色(仅支持安卓手机浏览器) -->
    <meta name="theme-color" content="red" />
    <!-- 网站描述 -->
    <meta name="description" content="Web site created using create-react-app" />
    <!-- 用于指定网页添加到手机主屏幕后的图标 -->
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <!-- 应用加壳时的配置文件 -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
  </head>
  <body>
    <!-- 若浏览器不支持 js 则展示标签中的内容 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

## 样式的模块化

样式的模块化可用于解决样式冲突的问题。该方法比较麻烦，实际开发用的比较少。用 `less` 就能解决了。

`component/Hello` 文件下的 `index.css` 改名为 `index.module.css` 。

```
.title {
  background-color: orange;
}
```

`Hello` 组件导入样式：

```
import { Component } from 'react'
import hello from './index.module.css'

export default class Hello extends Component {
  render() {
    return <h2 className={hello.title}>Hello,React!</h2>
  }
}
```

## TodoList 案例总结

1. 拆分组件、实现静态组件，注意：`className` 、`style` 的写法
2. 动态初始化列表，如何确定将数据放在哪个组件的 `state` 中？

- 某个组件使用：放在其自身的 `state` 中
- 某些组件使用：放在他们共同的父组件 `state` 中，即**状态提升**

1. 关于父子之间通信：

- 父传子：直接通过 `props` 传递
- 子传父：父组件通过 `props` 给子组件传递一个函数，子组件调用该函数

```
// 父组件
class Father extends Component {
  state: {
    todos: [{ id: '001', name: '吃饭', done: true }],
    flag: true,
  }

  addTodo = (todo) => {
    const { todos } = this.state
    const newTodos = [todo, ...todos]
    this.setState({ todos: newTodos })
  }

  render() {
    return <List todos={this.state.todos} addTodo={this.addTodo} />
  }
}

// 子组件
class Son extends Component {
  // 由于 addTodo 是箭头函数，this 指向父组件实例对象，因此子组件调用它相当于父组件实例在调用
  handleClick = () => {
    this.props.addTodo({ id: '002', name: '敲代码', done: false })
  }

  render() {
    return <button onClick={this.handleClick}>添加</button>
  }
}
```

1. 注意 `defaultChecked` 和 `checked` 的区别，类似的还有：`defaultValue` 和 `value`
2. 状态在哪里，操作状态的方法就在哪里

# React 网络请求

## React 脚手架配置代理

方法一：

在 `package.json` 文件中进行配置：

```
"proxy": "http://localhost:5000"
```

- 优点：配置简单，前端请求资源可不加前缀
- 缺点：不能配置多个代理
- 工作方式：当请求了 3000 端口号（本机）不存在的资源时，就会把请求转发给 5000 端口号服务器

方法二：

在 `src` 目录下创建代理配置文件 `setupProxy.js` ，进行配置：

```
const proxy = require('http-proxy-middleware')

module.exports = function (app) {
  app.use(
    //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
    proxy('/api1', {
      //配置转发目标地址(能返回数据的服务器地址)
      target: 'http://localhost:5000',
      //控制服务器接收到的请求头中host字段的值
      /*
      changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
      changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
      changeOrigin默认值为false，但一般将changeOrigin改为true
      */
      changeOrigin: true,

      //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
      pathRewrite: { '^/api1': '' },
    }),
    proxy('/api2', {
      target: 'http://localhost:5001',
      changeOrigin: true,
      pathRewrite: { '^/api2': '' },
    })
  )
}
```

## 消息订阅-发布机制

即 React 中兄弟组件或任意组件之间的通信方式。

使用的工具库：[PubSubJS](https://gitee.com/link?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fpubsub-js)

下载安装 `PubSubJS` ：`npm install pubsub-js --save`

基础用法：

```
import PubSub from 'pubsub-js'

// 订阅消息
var token = PubSub.subscribe('topic', (msg, data) => {
  console.log(msg, data)
})

// 发布消息
PubSub.publish('topic', 'hello react')

// 取消订阅
PubSub.unsubscribe(token)
```

## Github 搜索框案例知识点总结

1. 设计状态时要考虑全面，例如带有网络请求的组件，要考虑请求失败怎么办。
2. ES6 知识点：解构赋值 + 重命名

```
let obj = { a: { b: 1 } }

//传统解构赋值
const { a } = obj

//连续解构赋值
const {
  a: { b },
} = obj

//连续解构赋值 + 重命名
const {
  a: { b: value },
} = obj
```

1. 消息订阅与发布机制

- 先订阅，再发布（隔空对话）
- 适用于任意组件间通信
- 要在 `componentWillUnmount` 钩子中取消订阅

1. `fetch` 发送请求（**关注分离**的设计思想）

```
try {
  // 先看服务器是否联系得上
  const response = await fetch(`/api1/search/users2?q=${keyWord}`)
  // 再获取数据
  const data = await response.json()
  console.log(data)
} catch (error) {
  console.log('请求出错', error)
}
```

# React 路由

## 路由的理解

何为路由？

- 一个路由是一个映射关系
- `key` 为路径，`value` 可能是 `function` 或 组件

后端路由：

- `value` 是 `function` ，用于处理客户端的请求
- 注册路由：`router.get(path, function(req, res))`
- 工作过程：Node 接收到请求，根据路径匹配路由，调用对应函数处理请求，返回响应数据

前端路由：

- `value` 是组件
- 注册路由：`<Route path="/test" component={Test}>`
- 工作过程：浏览器路径变为 `/test` ，展示 `Test` 组件

## 路由基本使用

安装 `react-router-dom` ：

```
// 安装 5.X 版本路由
npm install react-router-dom@5.2.0 -S

// 最新已经 6.X 版本，用法和 5.X 有所不同
npm install react-router-dom -S
```

`6.x` 版本的用法参考[文章](https://gitee.com/link?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F191419879)

以 `5.x` 版本为例展示基本使用：

导航区使用 `<Link>`，展示区使用 `<Route>`。

```
// App.jsx
import React, { Component } from 'react'
import { Link, Route } from 'react-router-dom'
import Home from './components/Home'
import About from './components/About'

export default class App extends Component {
  render() {
    return (
      <div>
        <div className="list-group">
          <Link className="list-group-item" to="/about">
            About
          </Link>
          <Link className="list-group-item" to="/home">
            Home
          </Link>
        </div>
        <div className="panel-body">
          <Route path="/about" component={About} />
          <Route path="/home" component={Home} />
        </div>
      </div>
    )
  }
}
```

`<App>` 的最外侧包裹 `<BrowserRouter>` 或 `<HashRouter>` ：

```
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
)
```

## 路由组件和一般组件

1. 写法不同：

- 一般组件：`<Demo/>`
- 路由组件：`<Route path="/demo" component={Demo}/>`

1. 存放位置不同：

- 一般组件：`components`
- 路由组件：`pages`

1. 接收到的 `props` 不同：

- 一般组件：标签属性传递
- 路由组件：接收到三个固定的属性

```
history:
  go: ƒ go(n)
  goBack: ƒ goBack()
  goForward: ƒ goForward()
  push: ƒ push(path, state)
  replace: ƒ replace(path, state)

location:
  pathname: "/home/message/detail/2/hello"
  search: ""
  state: undefined

match:
  params: {}
  path: "/home/message/detail/:id/:title"
  url: "/home/message/detail/2/hello"
```

## NavLink 的使用

`NavLink` 可以实现路由链接的高亮，通过 `activeClassName` 指定样式名，默认追加类名为 `active` 。

```
<NavLink activeClassName="demo" to="/about">About</NavLink>

<NavLink activeClassName="demo" to="/home">Home</NavLink>
```

封装 `NavLink` 组件：由于 `NavLink` 组件中重复的代码太多，因此进行二次封装。

※ 细节点：组件标签的内容会传递到 `this.props.children` 属性中，反过来通过指定标签的 `children` 属性可以修改组件标签内容

```
// MyNavLink 组件
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'

export default class MyNavLink extends Component {
  render() {
    // this.props.children 可以取到标签内容，如 About, Home
    // 反过来通过指定标签的 children 属性可以修改标签内容
    return <NavLink activeClassName="demo" className="list-group-item" {...this.props} />
  }
}
<MyNavLink to="/about">About</MyNavLink>

<MyNavLink to="/home">Home</MyNavLink>
```

## Switch 的使用

`Switch` 可以提高路由匹配效率，如果匹配成功，则不再继续匹配后面的路由，即单一匹配。

```
<!-- 只会展示 Home 组件 -->
<Switch>
  <Route path="/about" component="{About}" />
  <Route path="/home" component="{Home}" />
  <Route path="/home" component="{Test}" />
</Switch>
```

## 解决多级路径刷新页面样式丢失的问题

- `public/index.html` 中 引入样式时不写 `./` 写 `/` （常用）
- `public/index.html` 中 引入样式时不写 `./` 写 `%PUBLIC_URL%` （常用）
- 使用 `HashRouter`

```
<link rel="stylesheet" href="/css/bootstrap.css" />

<link rel="stylesheet" href="%PUBLIC_URL%/css/bootstrap.css" />
```

## 路由的严格匹配与模糊匹配

- 默认使用模糊匹配（输入的路径必须包含要匹配的路径，且顺序一致）
- 开启严格匹配：`<Route exact path="/about" component={About}/>`
- 严格匹配需要再开，开启可能会导致无法继续匹配二级路由

## Redirect 的使用

- 一般写在所有路由注册的最下方，当所有路由都无法匹配时，跳转到 Redirect 指定的路由

```
<Switch>
  <Route path="/about" component="{About}" />
  <Route path="/home" component="{Home}" />
  <Redirect to="/about" />
</Switch>
```

## 嵌套路由

- 注册子路由需写上父路由的 `path`
- 路由的匹配是按照注册路由的顺序进行的

```
<!-- 父组件 -->
<MyNavLink to="/about">About</MyNavLink>
<MyNavLink to="/home">Home</MyNavLink>

<Switch>
  <Route path="/about" component="{About}" />
  <Route path="/home" component="{Home}" />
  <Redirect to="/about" />
</Switch>
<!-- 子组件 -->
<ul className="nav nav-tabs">
  <li>
    <MyNavLink to="/home/news">News</MyNavLink>
  </li>
  <li>
    <MyNavLink to="/home/message">Message</MyNavLink>
  </li>
</ul>

<Switch>
  <Route path="/home/news" component="{News}" />
  <Route path="/home/message" component="{Message}" />
  <Redirect to="/home/news" />
</Switch>
```

## 路由传参

三种方式：`params, search, state` 参数

三种方式对比：

- `state` 方式当前页面刷新可保留参数，但在新页面打开不能保留。前两种方式由于参数保存在 URL 地址上，因此都能保留参数。
- `params` 和 `search` 参数都会变成字符串

```
<!-- 路由链接 -->
<Link to='/home/message/detail/Bruce/21'>params</Link>
<Link to={`/home/message/detail/${item.name}/${item.age}`}>{item.name}</Link>

<Link to='/home/message/detail/?name=Bruce&age=21'>search</Link>
<Link to={`/home/message/detail/?id=${item.name}&title=${item.age}`}>{item.name}</Link>

<Link to={{pathname: '/home/message/detail', state: {name: 'Bruce', age: 21}}}>state</Link>

<!-- 注册路由 -->
<Route path='/home/message/detail/:name/:age' component={Detail} />
<!-- search 和 state 按正常注册即可 -->
<Route path='/home/message/detail' component={Detail} />
//接收参数
const { name, age } = this.props.match.params

import qs from 'querystring'
const { search } = this.props.location
const { name, age } = qs.parse(search.slice(1))

const { name, age } = this.props.location.state
```

## 编程式导航

编程式导航是使用路由组件 `this.props.history` 提供的 API 进行路由跳转：

```
this.props.history.push(path, state)
this.props.history.replace(path, state)
this.props.history.goForward()
this.props.history.goBack()
this.props.history.go(n)
// 编程式导航传参
this.props.history.push(`/home/message/detail/${id}/${title}`)
this.props.history.push(`/home/message/detail?id=${id}&title=${title}`)
this.props.history.push(`/home/message/detail`, { id: id, title: title })
```

## withRouter 的使用

`withRouter` 的作用：加工一般组件，让其拥有路由组件的 API ，如 `this.props.history.push` 等。

```
import React, {Component} from 'react'
import {withRouter} from 'react-router-dom'

class Header extends Component {
  ...
}

export default withRouter(Header)
```

## BrowserRouter 和 HashRouter

底层原理不一样：

- `BrowserRouter` 使用的是 H5 的 history API，不兼容 IE9 及以下版本。
- `HashRouter` 使用的是 URL 的哈希值。

路径表现形式不一样

- `BrowserRouter` 的路径中没有 `#` ，如：`localhost:3000/demo/test`
- `HashRouter` 的路径包含#，如：`localhost:3000/#/demo/test`

刷新后对路由 `state` 参数的影响

- `BrowserRouter` 没有影响，因为 `state` 保存在 `history` 对象中。
- `HashRouter` 刷新后会导致路由 `state` 参数的丢失！

备注：`HashRouter` 可以用于解决一些路径错误相关的[问题](https://gitee.com/brucecai55520/bruceblog/blob/master/docs/notes/react/react-router5.md#解决多级路径刷新页面样式丢失的问题)。

# React UI 组件库

## Ant Design 配置按需引入和自定义主题

> 以下配置是 `3.x` 版本，`4.x` 版本见[官网](https://gitee.com/link?target=https%3A%2F%2F3x.ant.design%2Findex-cn)

1. 安装依赖：

```
npm install react-app-rewired customize-cra babel-plugin-import less less-loader
```

1. 修改 `package.json`

```
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test",
  "eject": "react-scripts eject"
}
```

1. 根目录下创建 `config-overrides.js`

```
//配置具体的修改规则
const { override, fixBabelImports, addLessLoader } = require('customize-cra')

module.exports = override(
  fixBabelImports('import', {
    libraryName: 'antd',
    libraryDirectory: 'es',
    style: true,
  }),
  addLessLoader({
    lessOptions: {
      javascriptEnabled: true,
      modifyVars: { '@primary-color': 'green' },
    },
  })
)
```

1. 备注：不用在组件里引入样式，`import 'antd/dist/antd.css'` 删掉

# Redux

[官网](https://gitee.com/link?target=https%3A%2F%2Fredux.js.org%2F)

[中文文档](https://gitee.com/link?target=https%3A%2F%2Fwww.redux.org.cn%2F)

## Redux 概述

Redux 为何物

- Redux 是用于做 **状态管理** 的 JS 库
- 可用于 React、Angular、Vue 等项目中，常用于 React
- 集中式管理 React 应用多个组件共享的状态

何时用 Redux

- 某个组件的状态，需要让其他组件拿到（状态共享）
- 一个组件需要改变另一个组件的状态（通信）
- 使用原则：不到万不得已不要轻易动用

Redux 工作流程

![redux 工作流程图](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/redux.png)

- 组件想操作 Redux 中的状态：把动作类型和数据告诉 `Action Creators`
- `Action Creators` 创建 `action` ：同步 `action` 是一个普通对象，异步 `action` 是一个函数
- `Store` 调用 `dispatch()` 分发 `action` 给 `Reducers` 执行
- `Reducers` 接收 `previousState` 、`action` 两个参数，对状态进行加工后返回新状态
- `Store` 调用 `getState()` 把状态传给组件

## 核心概念

**`action`** ：

- 表示动作的对象，包含 2 个属性
- `type` ：标识属性，值为字符串，唯一，必须属性
- `data` ：数据属性，类型任意，可选属性
- `{type: 'increment', data: 2}`

**`reducer`** ：

- 用于初始化状态、加工状态
- 根据旧状态和 `action` 产生新状态
- 是**纯函数**

> 纯函数：输入同样的实参，必定得到同样的输出
>
> - 不能改写参数数据
> - 不产生副作用，如网络请求、输入输出设备（网络请求不稳定）
> - 不能调用 `Date.now()` 、`Math.random()` 等不纯方法

**`store`** ：

- Redux 核心对象，内部维护着 `state` 和 `reducer`
- 核心 API
  - `store.getState()` ：获取状态
  - `store.dispatch(action)` ：分发任务，触发 `reducer` 调用，产生新状态
  - `store.subscribe(func)` ：注册监听函数，当状态改变自动调用

## 一个求和案例

```
// App.jsx

import React, { Component } from 'react'
import Count from './components/Count'

export default class App extends Component {
  render() {
    return (
      <div>
        <Count />
      </div>
    )
  }
}
// index.js

import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import store from './redux/store'

ReactDOM.render(<App />, document.getElementById('root'))

// 状态改变重新渲染 App 组件
store.subscribe(() => {
  ReactDOM.render(<App />, document.getElementById('root'))
})
// redux/constant.js

// 保存常量值
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
// redux/count_reducer.js

import { INCREMENT, DECREMENT } from './constant'

//初始化状态
const initState = 0
export default function countReducer(preState = initState, action) {
  const { type, data } = action
  switch (type) {
    case INCREMENT:
      return preState + data
    case DECREMENT:
      return preState - data
    default:
      return preState
  }
}
// redux/store.js

import { createStore } from 'redux'
//引入为 Count 组件服务的 reducer
import countReducer from './count_reducer'

export default createStore(countReducer)
// redux/count_action.js

import { INCREMENT, DECREMENT } from './constant'

export const createIncrementAction = (data) => ({ type: INCREMENT, data })
export const createDecrementAction = (data) => ({ type: DECREMENT, data })
// components/Count/index.jsx

import React, { Component } from 'react'
import store from '../../redux/store'
import { createIncrementAction, createDecrementAction } from '../../redux/count_action'

export default class Count extends Component {
  // 可在组件单独监听 Redux 状态变化
  // componentDidMount() {
  // 	store.subscribe(() => {
  // 		this.setState({})
  // 	})
  // }

  increment = () => {
    const { value } = this.selectNumber
    // 将 value 转为数值
    // 手动写 Action 对象
    store.dispatch({ type: 'increment', data: value * 1 })
    // 专门创建 Action 对象
    store.dispatch(createIncrementAction(value * 1))
  }

  decrement = () => {
    const { value } = this.selectNumber
    store.dispatch(createDecrementAction(value * 1))
  }

  incrementAsync = () => {
    const { value } = this.selectNumber
    setTimeout(() => {
      store.dispatch(createIncrementAction(value * 1))
    }, 500)
  }

  render() {
    return (
      <div>
        <h1>当前求和为：{store.getState()}</h1>
        <select ref={(c) => (this.selectNumber = c)}>
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
        <button onClick={this.increment}>+</button>
        <button onClick={this.decrement}>-</button>
        <button onClick={this.incrementAsync}>异步加</button>
      </div>
    )
  }
}
```

- redux 只负责管理状态，状态改变驱动页面展示要自己写
- 可以在 `index.js` 中统一监听状态变化，也可以在组件中单独监听。注意不能直接 `this.render()` 调用 `render` 函数，要通过 `this.setState({})` 间接调用
- `reducer` 由 `store` 自动触发首次调用，传递的 `preState` 为 `undefined` ，`action` 为 `{type: '@@REDUX/ININT_a.5.v.9'}` 类似的东东，只有 `type`

## Redux 异步编程

安装异步中间件：

```
npm install redux-thunk -S
```

要点：

- 延迟的动作不想交给组件，而是 `action`
- 当操作状态所需数据要靠异步任务返回时，可用异步 `action`
- 创建 `action` 的函数返回一个函数，该函数中写异步任务
- 异步任务完成后，分发一个同步 `action` 操作状态
- 异步 `action` 不是必要的，完全可以在组件中等待异步任务结果返回在分发同步 `action`

```
// store.js
import { createStore, applyMiddleware } from 'redux'
import countReducer from './count_reducer'
import thunk from 'redux-thunk'

export default createStore(countReducer, applyMiddleware(thunk))
// count_action.js
import { INCREMENT, DECREMENT } from './constant.js'

export const createIncrementAction = (data) => ({ type: INCREMENT, data })
export const createDecrementAction = (data) => ({ type: DECREMENT, data })

// 异步 action 返回一个函数
export const createIncrementAsyncAction = (data, time) => {
  return (dispatch) => {
    setTimeout(() => {
      dispatch(createIncrementAction(data))
    }, time)
  }
}
// Count.jsx
incrementAsync = () => {
  const { value } = this.selectNumber
  store.dispatch(createIncrementAsyncAction(value * 1))
}
```

整个过程简单理解：`store` 在分发 `action` 时，发现返回一个函数，那它知道这是个异步 `action` 。因此 `store` 勉为其难地帮忙执行这个函数，同时给这个函数传递 `dispatch` 方法，等待异步任务完成取到数据后，直接调用 `dispatch` 方法分发同步 `action` 。

# React-Redux

> React-Redux 是一个插件库，用于简化 React 中使用 Redux 。

![React-Redux模型图](https://gitee.com/brucecai55520/bruceblog/raw/master/docs/notes/react/images/react-redux.png)

React-Redux 将组件分为两类：

- UI 组件
  - 只负责 UI 呈现，不带有业务逻辑
  - 通过 `props` 接收数据
  - 不能使用 Redux 的 API
  - 保存在 `components` 文件夹下
- 容器组件
  - 负责管理数据和业务逻辑，和 Redux 通信，将结果交给 UI 组件
  - 可使用 Redux 的 API
  - 保存在 `containers` 文件夹下

## React-Redux 基本使用

要点：

- `connect()()` ：创建容器组件
- `mapStateToProps(state)` ：映射状态为 UI 组件标签属性，即传递状态
- `mapDispatchToProps(dispatch)` ：传递操作状态的方法
- 容器组件中的 `store` 是靠 `props` 传进去，而不是在容器组件中直接引入

```
// containers/Count/index.jsx
// Count 容器组件

import CountUI from '../../components/Count'
import { connect } from 'react-redux'

import { createIncrementAction, createDecrementAction, createIncrementAsyncAction } from '../../redux/count_action'

function mapStateToProps(state) {
  return {
    count: state,
  }
}

function mapDispatchToProps(dispatch) {
  return {
    add: (number) => dispatch(createIncrementAction(number)),
    sub: (number) => dispatch(createDecrementAction(number)),
    addAsync: (number) => dispatch(createIncrementAsyncAction(number, time)),
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(CountUI)
// App.jsx
import React, { Component } from 'react'
import Count from './containers/Count'
import store from './redux/store.js'

export default class App extends Component {
  render() {
    return (
      <div>
        <Count store={store} />
      </div>
    )
  }
}
// components/Count/index.jsx
// Count UI 组件

increment = () => {
  const { value } = this.selectNumber
  this.props.add(value * 1)
}

decrement = () => {
  const { value } = this.selectNumber
  this.props.sub(value * 1)
}

incrementAsync = () => {
  const { value } = this.selectNumber
  this.props.addAsync(value * 1, 500)
}
```

## 优化写法

`mapDispatchToProps` 可以写成对象形式，React-Redux 底层会帮助自动分发。

```
// 函数写法
export default connect(
  state => ({count:state}),
  dispatch => ({
    add: number => dispatch(createIncrementAction(number)),
    sub: number => dispatch(createDecrementAction(number)),
    addAsync: (number,time) => dispatch(createIncrementAsyncAction(number,time)),
  })
)(CountUI)

// 对象写法
export default connect(
  state => ({ count: state }),
  {
    add: createIncrementAction,
    sub: createDecrementAction,
    addAsync: createIncrementAsyncAction,
  }
)(CountUI)
```

React-Redux 容器组件可以自动监测 Redux 状态变化，因此 `index.js` 不需要手动监听：

```
store.subscribe(() => {
  ReactDOM.render(<App />, document.getElementById('root'))
})
```

`Provider` 组件的使用：让所有组件都能获得状态数据，不必一个一个传递

```
// index.js

import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import { Provider } from 'react-redux'
import store from './redux/store'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

整合容器组件和 UI 组件为一个文件：

```
import React, { Component } from 'react'
import {
	createIncrementAction,
	createDecrementAction,
} from '../../redux/count_action'
import {connect} from 'react-redux'

// 定义 UI 组件
class Count extends Component {
  ...
}

// 创建容器组件
export default connect(
  state => ({count: state}),
  {
    add: createIncrementAction,
    sub: createDecrementAction
  }
)(Count)
```

## 多个组件数据共享

首先规范化文件结构，容器组件和 UI 组件合为一体后放在 `containers` 文件夹。`redux` 文件夹新建 `actions` 和 `reducers` 文件夹分别用于存放每个组件对应的 `action` 和 `reducer` 。

新建 `Person` 组件对应的 `action` 和 `reducer` ：

```
// redux/actions/person.js

import { ADD_PERSON } from '../constant.js'

export const createAddPersonAction = (personObj) => ({ type: ADD_PERSON, data: personObj })
// redux/reducers/person.js

import { ADD_PERSON } from '../constant.js'

const initState = [{ id: 'lsfd', name: 'china', age: '9999' }]
export default function personReducer(preState = initState, action) {
  const { type, data } = action
  switch (type) {
    case ADD_PERSON:
      return [data, ...preState]
    default:
      return preState
  }
}
```

关键步骤：在 `store.js` 中使用 `combineReducers()` 整合多个 `reducer` 来创建 `store` 对象。

这样 Redux 中就以对象的形式存储着每个组件的数据。类似于这样：

```
{
  total: 0,
  personList: []
}
// redux/store.js

import { createStore, applyMiddleware, combineReducers } from 'redux'
import countReducer from './reducers/count'
import personReducer from './reducers/person'
import thunk from 'redux-thunk'

const Reducers = combineReducers({
  total: countReducer,
  personList: personReducer,
})

export default createStore(Reducers, applyMiddleware(thunk))
```

`Person` 组件中获取 Redux 保存的状态，包括其他组件的数据。

```
import React, { Component } from 'react'
import { connect } from 'react-redux'
import { createAddPersonAction } from '../../redux/actions/person'
import { nanoid } from 'nanoid'

class Person extends Component {
  addPerson = () => {
    const name = this.nameInput.value
    const age = this.ageInput.value
    const personObj = { id: nanoid(), name, age }
    this.props.addPerson(personObj)
    this.nameInput.value = ''
    this.ageInput.value = ''
  }

  render() {
    return (
      <div>
        <h2>在Person组件拿到Count组件的数据：{this.props.count}</h2>
        <input type="text" ref={(c) => (this.nameInput = c)} placeholder="Please input name" />
        <input type="text" ref={(c) => (this.ageInput = c)} placeholder="Please input age" />
        <button onClick={this.addPerson}>添加</button>
        <ul>
          {this.props.personList.map((item) => {
            return (
              <li key={item.id}>
                {item.name} -- {item.age}
              </li>
            )
          })}
        </ul>
      </div>
    )
  }
}

export default connect(
  // state 是 Redux 保存的状态对象
  // 容器组件从 Redux 中取出需要的状态，并传递给 UI 组件
  state => ({personList: state.personList, count: state.total}),
  {
    addPerson: createAddPersonAction
    // 这一行凑数的，为了保持代码格式
    addPerson2: createAddPersonAction
  }
)(Person)
```

一个细节，在 `personReducer` 中，是按如下方式修改状态的，而没有使用 `unshift` 方法。在第二种方式，React 会认为状态没有变化从而不会重新渲染页面，因为 `preState` 保存的是数组地址值，返回的地址和之前的地址是一样的，尽管数组内容发生了改变。而第一种方式返回一个新的数组的地址值，和之前不一样，因此会重新渲染页面。

```
// 方式一
switch (type) {
  case ADD_PERSON:
    return [data, ...preState]
  default:
    return preState
}

// 方式二
switch (type) {
  case ADD_PERSON:
    preState.unshift(data)
    return preState
  default:
    return preState
}
```

## 纯函数

概念：输入同样的参数，返回同样的输出。

约束：

- 不能修改参数数据
- 不产生任何副作用，如网络请求、输入和输出设备
- 不能调用 `Date.now()` 或 `Math.random()` 等不纯的方法

`reducer` 的函数必须是纯函数。

## Redux 开发者工具

Chrome 安装 Redux DevTools 开发者工具，项目下载依赖包 `npm i redux-devtools-extension --save-dev`，最后在 `store.js` 进行配置：

```
import { composeWithDevTools } from 'redux-devtools-extension'
...
export default createStore(Reducers, composeWithDevTools(applyMiddleware(thunk)))
// 不需要异步中间件
export default createStore(Reducers, composeWithDevTools())
```

## 项目打包运行

运行命令：`npm run build` 进行项目打包，生成 `build` 文件夹存放着打包完成的文件。

运行命令：`npm i serve -g` 全局安装 `serve` ，它能够以当前目录为根目录开启一台服务器，进入 `build` 文件夹所在目录，运行 `serve` 命令即可开启服务器查看项目效果。

# React 扩展内容

## setState 更新状态的两种写法

对象式：`setState(stateChange, [callback])`

- `stateChange` 为状态改变对象(该对象可以体现出状态的更改)
- `callback` 是可选的回调函数, 它在状态更新完毕、界面也更新后才被调用

函数式：`setState(updater, [callback])`

- updater 为返回 stateChange 对象的函数。
- updater 可以接收到 state 和 props。

说明：

- React 状态更新是异步的。下述代码打印的 `count` 值是上一次的值，而非更新后的。可在第二个参数回调中获取更新后的状态。

```
add = () => {
  this.setState({ count: this.state.count + 1 })
  console.log(this.state.count)
}

add = () => {
  this.setState({ count: this.state.count + 1 }, () => {
    console.log(this.state.count)
  })
}
```

- `callback` 回调在 `componentDidMount` 钩子之后执行
- 对象式写法可以看做函数式写法的语法糖

```
add = () => {
  this.setState((state, props) => {
    return { count: state.count + props.step }
  })
}
```

## 路由组件懒加载 lazyLoad

```
import React, { Component, lazy, Suspense } from 'react'
import Loading from './Loading'

// 通过 lazy 函数配合 import() 函数动态加载路由组件
// 路由组件代码会被分开打包
const Home = lazy(() => import('./Home'))
const About = lazy(() => import('./About'))

export default Demo extends Component {
  render() {
    return (
      <div>
        <h1>Demo 组件</h1>
        <Link to="/home">Home</Link>
        <Link to="/about">About</Link>

        // 通过 <Suspense> 指定在加载得到路由打包文件前显示一个自定义 Loading 界面
        <Suspense fallback={Loading}>
          <Switch>
            <Route path="/home" component={Home}>
            <Route path="/about" component={About}>
          </Switch>
        </Suspense>
      </div>
    )
  }
}
```

## React Hook

> Hook 是 React 16.8.0 增加的新特性，让我们能在函数式组件中使用 `state` 和其他特性

### State Hook

- `State Hook` 让函数式组件也可拥有 `state` 状态。

- 语法：`const [Xxx, setXxx] = React.useState(initValue)`

- `useState()` 参数：状态初始化值；返回值：包含 2 个元素的数组，分别为状态值和状态更新函数

- ```
  setXxx()
  ```

   

  的 2 种用法：

  - `setXxx(newValue)`
  - `setXxx(value => newValue)`
  - 注意！新状态值会**覆盖**原状态值！因此若有多个状态，只能多次调用 `React.useState` ，不能使用对象！

```
const [count, setCount] = React.useState(0)
const [name, setName] = React.useState('Tom')

function add() {
  setCount(count + 1)
  setCount((count) => count + 1)
}
```

### Effect Hook

- `Effect Hook` 让我们能在函数式组件中执行副作用操作（就是模拟生命周期钩子）
- 副作用操作：发送 Ajax 请求、定时器、手动更改真实 DOM
- `Effect Hook` 可以模拟三个钩子：`componentDidMount`、`componentDidUpdate`、`componentWillUnmount`
- `React.useEffect` 第一个参数 `return` 的函数相当于 `componentWillUnmount` ，若有多个会按顺序执行

```
// 语法
React.useEffect(() => {
  ...
  return () => {
    // 组件卸载前执行，即 componentWillUnmount 钩子
    ...
  }
}, [stateValue])

// 模拟 componentDidMount
// 第二个参数数组为空，表示不监听任何状态的更新
// 因此只有页面首次渲染会执行输出
React.useEffect(() => {
  console.log('DidMount')
  return () => {
    console.log('WillUnmount 1')
  }
}, [])

// 模拟全部状态 componentDidUpdate
// 若第二个参数不写，表示监听所有状态的更新
React.useEffect(() => {
  console.log('All DidUpdate')
  return () => {
    console.log('WillUnmount 2')
  }
})

// 模拟部分状态 componentDidUpdate
// 第二个参数数组写上状态，表示只监听这些状态的更新
React.useEffect(() => {
  console.log('Part DidUpdate')
  return () => {
    console.log('WillUnmount 3')
  }
}, [count, name])

// 若调用 ReactDOM.unmountComponentAtNode(document.getElementById('root'))
// 会输出 WillUnmount 1、2、3
```

### Ref Hook

- `Ref Hook` 可以在函数式组件存储或查找组件内的标签或其他数据
- 语法：`const refContainer = React.useRef()`
- 保存标签对象的容器，和 `React.createRef()` 类似，也是专人专用

```
function Demo() {
  const myRef = React.useRef()

  function show() {
    console.log(myRef.current.value)
  }

  return (
    <div>
      <input type="text" ref={myRef} />
      <button onClick={show}>展示数据</button>
    </div>
  )
}
```

## Fragment

- `Fragment` 标签本身不会被渲染成一个真实 DOM 标签，有点像 Vue 的 `template`。
- 用空标签也有相同效果，但是空标签不能传递任何属性，`Fragment` 标签可以传递 `key` 属性，遍历时候可用。

```
import React, { Component, Fragment } from 'react'

export default class Demo extends Component {
  render() {
    return (
      <Fragment key={1}>
        <input type="text" />
        <input type="text" />
      </Fragment>
    )

    // 或
    return (
      <>
        <input type="text" />
        <input type="text" />
      </>
    )
  }
}
```

## Context

Context 是一种组件间通信方式，常用于祖父组件与子孙组件。实际开发一般不用，一般用 React-Redux

用法说明：

```
1) 创建Context容器对象：
const XxxContext = React.createContext()

2) 渲染子组时，外面包裹xxxContext.Provider, 通过value属性给后代组件传递数据：
<XxxContext.Provider value={数据}>
  子组件
</XxxContext.Provider>

3) 后代组件读取数据：

// 第一种方式：仅适用于类组件
// 声明接收context
static contextType = xxxContext
// 读取context中的value数据
this.context

//第二种方式: 可用于函数组件与类组件
<XxxContext.Consumer>
  {
    // value就是context中的value数据
    value => (
      ...
    )
  }
</XxxContext.Consumer>
```

举个栗子：

```
// context.js

import React from 'react'
export const MyContext = React.createContext()
export const { Provider, Consumer } = MyContext
// A.jsx

import React, { Component } from 'react'
import B from './B.jsx'
import { Provider } from './context.js'

export default class A extends Component {
  state = { username: 'tom', age: 18 }

  render() {
    const { username, age } = this.state
    return (
      <div>
        <h3>A组件</h3>
        <h4>用户名是:{username}</h4>
        <Provider value={{ username, age }}>
          <B />
        </Provider>
      </div>
    )
  }
}
// B.jsx

import React, { Component } from 'react'
import C from './C.jsx'

export default class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件</h3>
        <C />
      </div>
    )
  }
}
// C.jsx

import React, { Component } from 'react'
import { MyContext } from './context.js'

export default class C extends Component {
  static contextType = MyContext
  render() {
    const { username, age } = this.context
    return (
      <div>
        <h3>C组件</h3>
        <h4>
          从A组件接收到的用户名:{username},年龄:{age}
        </h4>
      </div>
    )
  }
}
// C.jsx 为函数式组件

import { Consumer } from './context.js'
export default function C() {
  return (
    <div>
      <h3>我是C组件</h3>
      <h4>
        从A组件接收到的用户名:
        <Consumer>{(value) => `${value.username},年龄是${value.age}`}</Consumer>
      </h4>
    </div>
  )
}
```

## 组件渲染优化

问题：

- 只要调用 `setState()` ，即使没有修改状态，组件也会重新 `render()`
- 只要父组件重新渲染，即使子组件没有使用父组件的状态，也会重新 `render()`

原因：

- `shouldComponentUpdate()` 钩子默认总是返回 `true`

改进：

- 只有组件的 `state` 或 `props` 的数据发生改变时才重新渲染

方式：

1. 手动重写 `shouldComponentUpdate(nextProps, nextState)` 的逻辑，只有数据发生改变才返回 `true`
2. 使用 `PureComponent` ，它重写了 `shouldComponentUpdate()` ， 只有 `state` 或 `props` 数据有变化才返回 `true`

:::tip

- 它只是进行 `state` 和 `props` 数据的浅比较, 如果只是数据对象内部数据变了, 返回 `false`。即对于引用数据类型，比较的是地址引用
- 不要直接修改 `state` 数据, 而是要产生新数据 :::

```
import React, { PureComponent } from 'react'

class Demo extends PureComponent {
  ...
  addStu = () => {
    // 不会渲染
    const { stus } = this.state
    stus.unshift('小刘')
    this.setState({ stus })

    // 重新渲染
    const { stus } = this.state
    this.setState({ stus: ['小刘', ...stus] })
  }
  ...
}
```

## render props (插槽)

> 类似于 Vue 中的插槽技术

如何向组件内部动态传入带内容的结构（即标签或组件）？

- Vue：插槽技术
- React：
  - 使用 `children props`：通过组件标签体传入结构
  - 使用 `render props`：通过组件标签属性传入结构，可携带数据

`children props` 方式：

- 组件标签体内容会存储到 `this.props.children` 中
- 缺点：A 组件无法向 B 组件传递数据

```
import React, { Component } from 'react'

export default class Parent extends Component {
  render() {
    return (
      <div>
        <h3>Parent组件</h3>
        <A>
          <B />
        </A>
      </div>
    )
  }
}

class A extends Component {
  state = { name: 'tom' }
  render() {
    return (
      <div>
        <h3>A组件</h3>
        {this.props.children}
      </div>
    )
  }
}

class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件</h3>
      </div>
    )
  }
}
```

`render props` 方式：

- `<A render={(name) => <B name={name} />} />`
- `{this.props.render(name)}`

```
import React, { Component } from 'react'

export default class Parent extends Component {
  render() {
    return (
      <div>
        <h3>Parent组件</h3>
        <A render={(name) => <B name={name} />} />
      </div>
    )
  }
}

class A extends Component {
  state = { name: 'tom' }
  render() {
    const { name } = this.state
    return (
      <div>
        <h3>A组件</h3>
        {this.props.render(name)}
      </div>
    )
  }
}

class B extends Component {
  render() {
    return (
      <div>
        <h3>B组件,{this.props.name}</h3>
      </div>
    )
  }
}
```

## 错误边界

:::tip 错误边界(Error boundary)：用来捕获后代组件错误，渲染出备用页面。

注意：只在生产环境（项目上线）起效 :::

特点：

- 只能捕获**后代组件生命周期**产生的错误，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误
- 简单理解就是只能捕获后代组件生命周期钩子里面代码的错误

```
import React, { Component } from 'react'
import Child from './Child'

export default class Parent extends Component {
  state = {
    //用于标识子组件是否产生错误
    hasError: '',
  }

  // 当子组件出现错误，会触发调用，并携带错误信息
  static getDerivedStateFromError(error) {
    // render 之前触发
    // 返回新的 state
    return { hasError: error }
  }

  // 子组件产生错误时调用该钩子
  componentDidCatch(error, info) {
    console.log(error, info)
    console.log('此处统计错误，反馈给服务器')
  }

  render() {
    return (
      <div>
        <h2>Parent组件</h2>
        {this.state.hasError ? <h2>网络不稳定，稍后再试</h2> : <Child />}
      </div>
    )
  }
}
```

## 组件通信方式总结

- `props`
- 消息订阅发布：`pubs-sub`
- 集中管理：Redux、dva 等
- [conText](https://gitee.com/brucecai55520/bruceblog/blob/master/docs/notes/react/react-extensions.md#context)

推荐搭配：

- 父子组件：`props`
- 兄弟组件：消息订阅-发布、集中式管理
- 祖孙组件(跨级组件)：消息订阅-发布、集中式管理、`conText`(开发用的少，封装插件用的多即 React-Redux)

# React Router 6

## 概述

React Router 发布了三个不同的包：

- `react-router`：路由核心库，提供许多组件、钩子
- `react-router-dom`：包括了 `react-router` 所有内容，同时添加了用于 DOM 的组件，如 `<BrowserRouter>`
- `react-router-native`：包括了 `react-router` 所有内容，同时添加了用于 ReactNative 的 API，如 `<NativeRouter>`

与 React Router 5.x 版本的区别：

- 内置组件的变化：移除 `<Switch/>`，新增 `<Routes/>`……
- 语法变化：`component={About}` 变成 `element={<About/>}`……
- 新增 hook：`useParams`、`useNavigate`、`useMatch`……
- 官方明确表示推荐使用函数式组件

## 基本使用

安装 6 版本的 React Router。

```
npm install react-router-dom
```

`index.js` 文件引入 `<BrowserRouter>`。

```
// 从 react-dom/client 引入 ReactDOM
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

// React 18 的语法发生改变了
ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

`App.js` 设置路由链接和注册路由。`<Route caseSensitive>` 属性用于指定匹配时是否区分大小写（默认为 false）。

```
import { NavLink, Routes, Route } from 'react-router-dom'
import About from './components/About/About'
import Hello from './components/Hello/Hello'

// React 18 默认使用函数式组件了
export default function App() {
  return (
    <div>
      <NavLink to="/about">About</NavLink>
      <NavLink to="/hello">Hello</NavLink>
      <hr />
      <Routes>
        <Route path="/about" element={<About />}></Route>
        <Route path="/hello" element={<Hello />}></Route>
      </Routes>
    </div>
  )
}
```

## `<BrowserRouter>`

`<BrowserRouter> `用于包裹整个应用。

```
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

## `<HashRouter>`

作用与 `<BrowserRouter>` 一样，但 `<HashRouter>` 修改的是地址栏的 hash 值。

6.x 版本中 `<HashRouter>`、`<BrowserRouter>` 的用法与 5.x 相同。

## `<Routes/>`

6 版本中移出了 `<Switch>`，引入了新的替代者：`<Routes>`。

`<Routes>` 和 `<Route>` 要配合使用，且必须要用 `<Routes>` 包裹 `<Route>`。

## `<Navigate>` 重定向

只要 `<Navigate>` 组件被渲染，就会修改路径，切换视图。可用于路由重定向。

`replace` 属性用于控制跳转模式（push 或 replace，默认是 push）。

```
import { NavLink, Routes, Route, Navigate } from 'react-router-dom'
import About from './components/About/About'
import Hello from './components/Hello/Hello'

export default function App() {
  return (
    <div>
      <NavLink to="/about">About</NavLink>
      <NavLink to="/hello">Hello</NavLink>
      <hr />
      <Routes>
        <Route path="/about" element={<About />}></Route>
        <Route path="/hello" element={<Hello />}></Route>
        <Route path="/" element={<Navigate to="/about" />}></Route>
      </Routes>
    </div>
  )
}
import React, { useState } from 'react'
import { Navigate } from 'react-router-dom'

export default function Home() {
  const [sum, setSum] = useState(1)
  return (
    <div>
      <h1>Home</h1>
      {/* 根据sum的值决定是否切换视图 */}
      {sum === 1 ? <h4>sum的值为{sum}</h4> : <Navigate to="/about" replace={true} />}
      <button onClick={() => setSum(2)}>将sum变为 2</button>
    </div>
  )
}
```

## `useRoutes()` 路由表

路由规则可以单独抽出一个模块。

```
// 路由表
// routes/index.js
import { Navigate } from 'react-router-dom'
import About from '../components/About/About'
import Hello from '../components/Hello/Hello'

const routes = [
  {
    path: '/about',
    element: <About />,
  },
  {
    path: '/hello',
    element: <Hello />,
  },
  {
    path: '/',
    element: <Navigate to="/about" />,
  },
]

export default routes
// 引入路由表
// App.js
import { NavLink, useRoutes } from 'react-router-dom'
import routes from './routes'

export default function App() {
  // 生成路由规则
  const element = useRoutes(routes)

  return (
    <div>
      <NavLink to="/about">About</NavLink>
      <NavLink to="/hello">Hello</NavLink>
      <hr />
      {element}
    </div>
  )
}
```

## `<Outlet>` 嵌套路由

- 嵌套路由中，需要使用 `<Outlet>` 设置子路由的路由出口，即在何处渲染子路由。
- 设置二级路由链接时，可以是 `to="news"`、`to="./news"`，但不能是 `to="/news"`。

不使用路由表的嵌套路由：

```
// App.js
export default function App() {
  return (
    <div>
      <NavLink to="about">About</NavLink>
      <NavLink to="hello">Hello</NavLink>
      <hr />
      <Routes>
        <Route path="about" element={<About />} />
        <Route path="hello" element={<Hello />}>
          <Route path="news" element={<News />} />
          <Route path="message" element={<Message />} />
        </Route>
        <Route path="/" element={<Navigate to="about" />} />
      </Routes>
    </div>
  )
}
```

使用路由表的嵌套路由：

```
// 路由表
const routes = [
  {
    path: '/about',
    element: <About />,
  },
  {
    path: '/hello',
    element: <Hello />,
    // 定义二级路由，注意不要加 /
    children: [
      {
        path: 'news',
        element: <News />,
      },
      {
        path: 'message',
        element: <Message />,
      },
    ],
  },
  {
    path: '/',
    element: <Navigate to="/about" />,
  },
]
// Hello 子组件
import React, { Fragment } from 'react'
import { NavLink, Outlet } from 'react-router-dom'

export default function Hello() {
  return (
    <Fragment>
      <h2>I am Hello!</h2>
      {/* 子路由链接 */}
      <NavLink to="news">News</NavLink>
      <NavLink to="message">Message</NavLink>
      <hr />
      {/* 子路由出口 */}
      <Outlet></Outlet>
    </Fragment>
  )
}
```

## `<NavLink>` 路由高亮

实现导航的 “高亮” 效果，6 版本不能直接指定高亮类名，需要通过函数返回。该函数传入一个对象，类似于 `{isActive: true}` 标识路由是否被激活。

默认情况下，当 `Home` 的子组件匹配成功，`Home` 的导航也会高亮，`end` 属性可移除该效果。

```
// NavLink 默认类名是 active，下面是指定自定义类名

//自定义样式
<NavLink
    to="login"
    className={({ isActive }) => {
        console.log('home', isActive)
        return isActive ? 'base MyClass' : 'base'
    }}
>about</NavLink>

// 默认情况下，当 Home 的子组件匹配成功，Home 的导航也会高亮
// 当 NavLink 上添加了 end 属性后，若 Home 的子组件匹配成功，则 Home 的导航没有高亮效果。
<NavLink to="home" end >home</NavLink>
```

## 路由传参

> 以不使用路由表为例

### 传递 `params`参数

注册路由时声明 `params` 参数，和 React Router 5 一样。

```
export default function App() {
  return (
    <div>
      <Routes>
        <Route path="hello" element={<Hello />}>
          <Route path="message" element={<Message />}>
            <Route path="detail/:id/:name/:age" element={<Detail />} />
          </Route>
        </Route>
      </Routes>
    </div>
  )
}
```

传递参数。

```
<Link to={`detail/${item.id}/${item.name}/${item.age}`}>{item.name}</Link>
```

使用 `useParams()` 接收 `params` 参数。`useParams()` 返回一个参数对象。

```
import React from 'react'
import { useParams, useMatch } from 'react-router-dom'

export default function Detail() {
  // 解构赋值
  const { id, name, age } = useParams()
  return (
    <div>
      <li>id:{id}</li>
      <li>name:{name}</li>
      <li>age:{age}</li>
    </div>
  )
}
```

### 传递 `search` 参数

和 5 版本一样，正常注册路由即可。

```
<Route path="detail" element={<Detail />} />
```

传递参数。

```
<Link to={`detail?id=${item.id}&name=${item.name}&age=${item.age}`}>{item.name}</Link>
```

使用 `useSearchParams()` 接收参数。该方法返回一个包含两个元素的数组：`search` 参数和修改 `search` 参数的方法。

```
import React from 'react'
import { useSearchParams } from 'react-router-dom'

export default function Detail() {
  // 数组的解构赋值
  const [searchParams, setSearchParams] = useSearchParams()
  // 需要调用 get() 方法获取对应的参数值
  const id = searchParams.get('id')
  const name = searchParams.get('name')
  const age = searchParams.get('age')

  function change() {
    setSearchParams('id=666&name=Lily&age=888')
  }

  return (
    <div>
      <li>id:{id}</li>
      <li>name:{name}</li>
      <li>age:{age}</li>
      <button onClick={change}>Change search params</button>
    </div>
  )
}
```

### 传递 `state` 参数

和 5 版本一样，正常注册路由即可。

```
<Route path="detail" element={<Detail />} />
```

传递参数，这里相较于 5 版本有所不同，不必写到一个对象里面。

```
<Link to="detail" state={{ id: item.id, name: item.name, age: item.age }}>
  {item.name}
</Link>
```

使用 `useLocation()` 接收参数。该方法返回路由组件的 `location` 对象，就是 5 版本路由组件的 `location` 属性，其中包含 `state` 参数。

```
import { useLocation } from 'react-router-dom'

export default function Detail() {
  // 连续解构赋值
  const {
    state: { id, name, age },
  } = useLocation()

  return (
    <div>
      <li>id:{id}</li>
      <li>name:{name}</li>
      <li>age:{age}</li>
    </div>
  )
}
```

## `useNavigate()` 编程式路由导航

`useNavigate()` 返回一个函数，调用该函数实现编程式路由导航。函数有两种参数传递方式。

第一种方式传递两个参数：路由和相关参数。参数只能设置 `replace` 和 `state`。想要传递 `params` 和 `search` 参数直接在路由带上。

第二种方式传递数字，代表前进或后退几步。

```
import React, { useState } from 'react'
import { Outlet, useNavigate } from 'react-router-dom'

export default function Message() {
  const [list] = useState([
    { id: 1, name: 'Bruce', age: 33 },
    { id: 2, name: 'You', age: 3 },
    { id: 3, name: 'React', age: 333 },
  ])

  const navigate = useNavigate()

  function showDetail(item) {
    navigate('detail', {
      replace: true,
      state: {
        id: item.id,
        name: item.name,
        age: item.age,
      },
    })
  }

  function back() {
    navigate(1)
  }

  function forward() {
    navigate(-1)
  }

  return (
    <div>
      <ul>
        {list.map((item) => {
          return (
            <li key={item.id}>
              <button onClick={() => showDetail(item)}>查看详情</button>
              <button onClick={back}>后退</button>
              <button onClick={forward}>前进</button>
            </li>
          )
        })}
      </ul>
      <Outlet></Outlet>
    </div>
  )
}
```

## Other Hooks

### `useMatch()`

返回路由组件的 `match` 数据，即 5 版本中的 `match` 属性。

必须传入该组件对应的路由规则才能正确返回，否则返回 `null`。

```
// Detail.jsx
import { useParams, useMatch } from 'react-router-dom'

export default function Detail() {
  const match = useMatch('hello/message/detail/:id/:name/:age')
  console.log(match)
  return (
    <div>
      <li>id</li>
    </div>
  )
}

/*
params: {id: '1', name: 'Bruce', age: '33'}
pathname: "/hello/message/detail/1/Bruce/33"
pathnameBase: "/hello/message/detail/1/Bruce/33"
pattern: {path: 'hello/message/detail/:id/:name/:age', caseSensitive: false, end: true}
*/
```

### `useInRouterContext()`

如果组件在 `<Router>` 的上下文中呈现，则 `useInRouterContext` 钩子返回 `true`，否则返回 `false`。即组件有没有被包裹在 `<BrowserRouter>` 这种东西里面。这个对第三方组件库有用处。

### `useNavigationType()`

返回当前的导航类型（用户是如何来到当前页面的）。

返回值：`POP`、`PUSH`、`REPLACE`。

`POP` 是指在浏览器中直接打开了这个路由组件（刷新页面）。

### `useOutlet()`

用来呈现当前组件中渲染的嵌套路由。

```
const result = useOutlet()
console.log(result)
// 如果嵌套路由没有挂载,则返回 null
// 如果嵌套路由已经挂载,则展示嵌套的路由对象
```

### `useResolvedPath()`

给定一个 URL 值，解析其中的：`path`、`search`、`hash` 值。

```
const res = useResolvedPath('/user?id=001&name=Bruce#React')
console.log(res)

/*
hash: '#React'
pathname: '/user'
search: '?id=001&name=Bruce'
*/
```