# Vue2.0学习笔记

## 1.创建一个Vue实例

![image-20210915002719703](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915002719703.png)

 ![image-20210927220050560](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210927220050560.png)

![image-20210927220150786](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210927220150786.png)

![e84a7738c1390614d793a37900e1651](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/e84a7738c1390614d793a37900e1651.png)

![fa2a42dfb32833b258d195a1670460a](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/fa2a42dfb32833b258d195a1670460a.png)

### 1.Vue实例生命周期

#### 1.过程

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做**生命周期钩子**的函数，这给了用户在不同阶段添加自己的代码的机会。

DOM（Document Object Model ，文档对象模型）一种独立于语言，用于操作xml，html文档的应用编程接口。

Vue实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、卸载等一系列过程，我们称这是Vue的生命周期。通俗说就是Vue实例从创建到销毁的过程，就是生命周期。

![image-20210920144236186](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920144236186.png)

​                                                                     ![image-20210920144254235](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920144254235.png)	



## 2.Vue实例选项

  ![image-20210915003534210](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915003534210.png)


## 3.Vue 数据绑定

 ![image-20210915003621163](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915003621163.png)


## 4.案例:

### 页面有一个元素，值为1；有一个按钮，每次点击按钮，数字就增加1

原生写法:

![image-20210915003735944](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915003735944.png)

Vue写法:

![image-20210915003745945](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915003745945.png)

## 5.插值绑定

### 1.{{}}

将元素当成纯文本输出

### 2.v-html

v-html会将元素当成HTML标签解析后输出

### 3.v-text

`将元素当成纯文本输出


## 6.Vue属性绑定

### 1.v-bind

*v-bind的简写是: v-bind用来绑定文本或属性，绑定文本跟v-text差不多，能够绑定的属性有html中的属性、css的样式、对象、数组、number 类型、bool类型。*

*v-bind是单向绑定，它在绑定文本时，当data中的数据发生变化时，页面中的数据也相应改变，但页面中的数据改变不会影响到data。*

### 2.v-model

*v-model实现了数据的双向绑定，页面中的数据与data中的数据是同步变化的，通常用来给表单添加绑定。*

*v-model:value 双向绑定了input的value属性事件*



### 3.v-bind和v-model

![image-20210915005848563](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005848563.png)

### 4.v-model与自定义组件



### 5.类名(实际是数组)和样式(对象的键值)绑定

#### 1.类名绑定

类名可以使用字符串数组对象三种方式为节点动态绑定类名属性

#### 2.样式绑定

样式可以使用字符串对象俩种方式为节点动态绑定类名属性

#### 3.实例图片

![image-20210916025334949](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210916025334949.png)



## 7.事件绑定

### 1.事件绑定指令：v-on,简写@

#### 1.v-on

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005029316.png)

![image-20210915005128208](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005128208.png)

![image-20210915005313667](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005313667.png)

![image-20210915005321081](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005321081.png)

![image-20210915005330091](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005330091.png)

![image-20210915005337312](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005337312.png)

![image-20210915005345322](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005345322.png)

![image-20210915005350031](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005350031.png)

![image-20210915005353606](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915005353606.png)

⭐

*<!-- v-on的简写是@ 它的作用是v-on指令事件绑定机制 addFruit是它在methods中的函数名称 -->*

<button type="button" @click="addFruit">添加</button>

这里要注意onclick事件是绑定事件可以复用，而click只是一次简单的触发

⭐⭐

处理事件时需要用到事件本身的写法:

 ![image-20210916032507558](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210916032507558.png)

#### 2.常见的修饰符

JS原生事件event.preventDefault()阻止元素默认行为,event.stopPropagation()阻止事件冒泡

.stop当事件触发时，阻止事件冒泡

.prevent当事件触发时，阻止元素默认行为

.capture当事件触发时，阻止事件捕获

.self限制事件只作用于节点

.once当事件被触发一次后解除监听

.passive移动端，限制事件永远不调用preventDefault()方法

#### 3.按键修饰符

监听回车键是否被按下的俩种方法

1.<input type="text" @keyup.13="console.log($event)">

2.<input type="text" @keyup.enter="console.log($event)">

#### 4.鼠标修饰符

1.left左键

2.right右键

3.middle中键

#### 5.组合修饰符

有时候我们需要按住多个按键或者鼠标和键盘一起共用来实现某些操作，例如按住ctrl+鼠标可以选取多个文件

常用的系统按钮修饰符:

.ctrl  .alt  .shift  .meta(windows键)

## 8.条件渲染

### 1.v-if

条件性地渲染一块内容。当条件判断为真（true）时，这一内容才会被渲染

### 2.v-show

效果类似

### 3.v-if和v-show的区别

v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
⭐一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。

## 9.列表渲染v-for

#### 1.v-for

##### 我们可以用 v-for 指令基于一个数组来渲染一个列表。v-for 指令需要使用 item in items 形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名。

写法:

![image-20210915003846265](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915003846265.png)

#### 2.在v-for使用对象

例如:

![image-20210915004139751](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915004139751.png)



![image-20210915004332920](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915004332920.png)





#### 3.⭐为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 `key` attribute：

vue中列表循环需加v-bind:key="唯一标识"

key:

![image-20210915004411071](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915004411071.png)

index（数组索引）:

![image-20210915004408232](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915004408232.png)


输出结果0.titele：How to do lists in Vue

利用key或者index帮助vue识别





## 10.组件

#### 1.⭐

#### 组件是Vue中的一个重要概念，是一个可以重复使用的Vue实例。它拥有一个组件名称，以组件名称的方式作为自定义的HTML标签。

因为组件是可复用的Vue实例，所以它们与new Vue（）接收相同的选项，例如data，methods等。仅有的例外是像el这样根实例特有的选项。



#### 2.组件的定义



![image-20210915010118439](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915010118439.png)

这里把button作为了html模板，类似于封装了一个按钮给你



#### 3.组件的使用



![image-20210915014529870](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915014529870.png)



![image-20210915013658203](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915014741932.png)

#### 4.组件的复用

![image-20210915013855890](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915013855890.png)

#### 5.关于data

![image-20210915013916097](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915013916097.png)

#### 6.关于prop

☁prop是你可以在组件上注册的一些自定义属性(attribute)。当一个值传递给一个prop属性的时候，它就变成了那个组件实例的一个property(property：是js获取的DOM对象上的属性值)为了给博文组件传递一个标题，我们可以用一个 `props` 选项将其包含在该组件可接受的 prop 列表中：

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/7%0`W%ZCK9]W}O$~6J9~WFC.png)

一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。在上述模板中，你会发现我们能够在组件实例中访问这个值，就像访问 `data` 中的值一样。

当一个prop被注册后，你就可以像这样把数据作为一个自定义attribute传递进来:

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/3`%SR2~U[0B$FLSLSHI5[N7.png)

然而在一个典型的应用中，你可能在 `data` 里有一个博文的数组：

![img](file:///C:\Users\ttq\Documents\Tencent Files\1253524003\Image\C2C\BD(XC{N0}$17VV1%8N7)3[6.png)



##### 1.prop类型

 ![image-20210920182746627](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920182746627.png)	

![image-20210920105405555](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920105405555.png)

![c21852522fb99be487b5c3f22378775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/c21852522fb99be487b5c3f22378775.png)

![image-20210920105427421](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920105427421.png)

![image-20210920105441348](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920105441348.png)

##### 2.⭐组件实例的作用域是孤立的。这意味着不能 (也不应该) 在子组件的模板内直接引用父组件的数据。父组件的数据需要通过 **prop** 才能下发到子组件中。**props**是子组件访问父组件数据的唯一接口

##### 3.单向数据流： props是单向绑定的

当父组件的属性变化时，将传导给子组件，但是反过来不会。每次父组件更新时，子组件的所有 prop 都会更新为最新值。不要在子组件内部改变 prop。如果你这么做了，Vue 会在控制台给出警告。

在两种情况下，我们很容易忍不住想去修改 prop 中数据：

1. Prop 作为初始值传入后，子组件想把它当作局部数据来用；
2. Prop 作为原始数据传入，由子组件处理成其它数据输出。

对这两种情况，正确的应对方式是：
定义一个局部变量，并用 prop 的值初始化它：

![image-20210917031756605](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210917031756605.png)

定义一个计算属性，处理 prop 的值并返回：

![image-20210917031813065](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210917031813065.png)

⭐JavaScript 中对象和数组是引用类型，指向同一个内存空间，如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。

![image-20210917031841016](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210917031841016.png)

可以为prop指定验证规则，如果传入的数据不符合要求，Vue会发出警告。

##### 4.双向数据流

当对父子组件有双向绑定需求时，通过修饰符.sync配合this.$emit方法实现

![image-20210920110004746](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210920110004746.png)

###### 1.⭐：关于修饰符.sync

![img](file:///C:\Users\ttq\Documents\Tencent Files\1253524003\Image\C2C\]XR9E61T8996]AR2YW`WN9B.png)



##### 4. $parent

⭐Vue 子组件可以通过 $parent属性访问父组件实例的属性和方法，通过 $parent 获取到 父组件 中的 props 、 data或者方法。

而且子组件可以通过$parent 来直接修改父组件的数据，不会报错！

当子组件定制化程度非常高，只为了一个父组件服务，不考虑复用的情况可以使用。

this.$parent.属性方法

可以使用props的时候，尽量使用props显式地传递数据（可以很清楚很快速地看出子组件引用了父组件的哪些数据）。

另外在一方面，直接在子组件中修改父组件的数据是很糟糕的做法，props单向数据流就没有这种顾虑了。

##### 5.$root

⭐Vue 子组件可以通过 $root 属性访问根实例的属性和方法 

#### 7.组件传值

子组件向父组件传值:通过$emit自定义一个事件，将子组件的值抛给父组件；父组件通过触发这个给事件，来获取子组件传来的值。

##### 1.⭐插槽（Slot）是Vue提出来的一个概念，正如名字一样，插槽用于决定将所携带的内容，插入到指定的某个位置，从而使模板分块，具有模块化的特质和更大的重用性。插槽显不显示、怎样显示是由父组件来控制的，而插槽在哪里显示就由子组件来进行控制

![cdd9c7956b49766808119ba74de4318](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/cdd9c7956b49766808119ba74de4318.png)

#### 8.单个根元素

##### 1.每个组件必须只有一个根元素，所以你可以将模板的内容包裹在一个父元素内

![img](file:///C:\Users\ttq\Documents\Tencent Files\1253524003\Image\C2C\7WB{HTDRVU8_1320__39ABF.png)

##### 2.post prop(数组prop)

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/S87XA~J%5B579EVVFH3YOAX4J.png)

![img](file:///C:\Users\ttq\Documents\Tencent Files\1253524003\Image\C2C\`0SNDBTR}1OQE[%(X[$()NQ.png)

#### 9.监听子组件事件



#### 10.组件的组织

##### 1.全局注册

![image-20210915014347907](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915014347907.png)

![image-20210915014815451](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20210915014815451.png

![image-20210915015140513](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015140513.png)

##### 2.局部注册

在Vue实例中使用**components选项**可以局部注册一个组件

![image-20210915014851878](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915014851878.png)

![image-20210915014857630](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20210915014857630.png

![image-20210915015112958](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015112958.png)

![image-20210915015902425](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015902425.png)

注意**局部注册的组件在其子组件中不可用**。

![image-20210915015907865](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015907865.png)

![image-20210915015920635](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015920635.png)

##### 3.示例



##### 4.单个js组件

单个js组件
组件可以放在单个js文件中，以便更好的管理。使用时通过<script>标签引入。

![image-20210915015230101](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210915015230101.png)

