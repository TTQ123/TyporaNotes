# 1.uniapp官网介绍

## **1.uniapp框架中封装的内容**

![image-20231114214307921](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231114214307921.png)



1.uniapp自己封装的组件和UI

2.![image-20231114214344669](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231114214344669.png)

3.微信小程序原生的组件等

4.Html5Plus引擎解决了安卓和IOS跨平台开发   小程序没有很多原生的API,但是Html5Plus提供了这一部分API

5.![image-20231114214041212](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231114214041212.png)

6.uni ios android sdk(对性能要求高时不想用js可以导入这个混合开发)

7.其它一些程序的专属API也被包括进来了



## **2.尺寸单位**

![image-20231114220234171](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231114220234171.png)



# 2.uniapp笔记

## 1.基础使用

创建项目直接创建，后期可以使用它里面自带的很多写好的模板。

刚创建出来基础默认项目只有pages和static俩个文件夹。

### 1.如何运行项目

配置模拟器我使用的是mumu浏览器，百度一下如何配置 参考: https://blog.csdn.net/lisyao/article/details/132869033

![image-20231121173311458](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121173311458.png)

**运行到微信小程序模拟器有时候会出现没有设置端口，去微信小程序的设置->安全设置->开启服务端口**

后期发布在服务器的包是build文件夹。



### 2.如何发行uniapp

#### 1.发行为app

发行以后是在build文件夹，运行以后是在dev文件夹(开发版本)

在mainfest.json里面可以设置App图标，版本号，应用描述等等

学习阶段时打包公共证书就行，后面可以直接去认证自有证书

点击发行->原生App云打包

![image-20231121225704005](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121225704005.png)

打包后控制台会显示APK或IPA包位置

![image-20231121225758310](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121225758310.png)



#### 2.发行为web

![image-20231121225957050](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121225957050.png)

打包成功后可以在build文件夹找到直接发布

![image-20231121225942196](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121225942196.png)



#### 3.发行为微信小程序

![image-20231121230120943](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121230120943.png)

![image-20231121230426219](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121230426219.png)

我目前的appid    wx303da12a38734d48

![image-20231121231000694](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121231000694.png)



如果你从微信开发者工具中直接去上传(发布)，测试小程序账号是不可以上传的，要正式认证的小程序账号才可以

![image-20231121231401778](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121231401778.png)

如果你是正式账号(个人/公司)，你其实也可以直接用微信开发者工具上传，但是最好还是都一起用hbuilderx操作运行和发行



#### 4.uniapp工程目录

![image-20231121231710580](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231121231710580.png)

**App.vue中不能写模板template**



## 2.uniapp生命周期

在uniapp中生命周期分为多种

![image-20231123083536806](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123083536806.png)

### 1.应用生命周期

![image-20231123082458991](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123082458991.png)

标注蓝色的三个生命周期是最常用的，默认创建的项目会带这三个。

![image-20231123082615402](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123082615402.png)

![image-20231123082841748](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123082841748.png)



#### 1.小程序场景值

![image-20231123084544879](C:\Users\ttq\AppData\Roaming\Typora\typora-user-images\image-20231123084544879.png)



### 2.页面生命周期❤

页面生命周期是写在pages文件夹下的文件中。其属性如下：

不同的平台对这些页面生命周期的支持是不一样的，使用的时候要去看官网的文档

| ***\*函数名\****                    | ***\说明\***                                                 |
| ----------------------------------- | ------------------------------------------------------------ |
| onInit                              | 监听页面初始化，其参数同 onLoad 参数，为上个页面传递的数据，参数类型为 Object（用于页面传参），触发时机早于 onLoad |
| onLoad                              | [监听页面加载，该钩子被调用时，响应式数据、计算属性、方法、侦听器、props、slots 已设置完成，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参），参考示例](#navigateto) |
| onShow                              | 监听页面显示，页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面 |
| onReady                             | 监听页面初次渲染完成，此时组件已挂载完成，DOM 树($el)已可用，注意如果渲染速度快，会在页面进入动画完成前触发 |
| onHide                              | 监听页面隐藏                                                 |
| onUnload                            | 监听页面卸载                                                 |
| onResize                            | 监听窗口尺寸变化                                             |
| onPullDownRefresh                   | [监听用户下拉动作，一般用于下拉刷新，参考示例](https://uniapp.dcloud.net.cn/api/ui/pulldown) |
| onReachBottom                       | 页面滚动到底部的事件（不是scroll-view滚到底），常用于下拉下一页数据。具体见下方注意事项 |
| onTabItemTap                        | 点击 tab 时触发，参数为Object，具体见下方注意事项            |
| onShareAppMessage                   | 用户点击右上角分享                                           |
| onPageScroll                        | 监听页面滚动，参数为Object                                   |
| onNavigationBarButtonTap            | 监听原生标题栏按钮点击事件，参数为Object                     |
| onBackPress                         | [监听页面返回，返回 event = {from:backbutton、 navigateBack} ，backbutton 表示来源是左上角返回按钮或 android 返回键；navigateBack表示来源是 uni.navigateBack；详见](#onbackpress) |
| onNavigationBarSearchInputChanged   | 监听原生标题栏搜索输入框输入内容变化事件                     |
| onNavigationBarSearchInputConfirmed | 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。 |
| onNavigationBarSearchInputClicked   | 监听原生标题栏搜索输入框点击事件（pages.json 中的 searchInput 配置 disabled 为 true 时才会触发） |
| onShareTimeline                     | 监听用户点击右上角转发到朋友圈                               |
| onAddToFavorites                    | 监听用户点击右上角收藏                                       |

参考地址：

https://uniapp.dcloud.net.cn/tutorial/page.html#lifecycle

 

注意：

1、**页面和组件的区别**

组件放在“components”文件夹下，

页面文件是在"pages/index/"中，页面的配置在pages.json中

**2、页面生命周期中，带有“原生”属性的钩子函数表示与“pages.json”有关，即:无需自定义函数，直接在“pages.json”中进行配置即可使用。**

**我们可以在pages.json的style中配置一些封装的原生组件例如搜索框，然后在下面这些生命周期函数中监听数据等**

**在这里可以找到要用的style样式**

![image-20231123094411562](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123094411562.png)

![image-20231123092851141](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123092851141.png)

参考文档：https://uniapp.dcloud.net.cn/collocation/pages.html#style

演示：“app-plus”->“titleNview”->“searchInput”->“placeholder”

注意：

1.此时在微信小程序内无法正常显示，原因是在官方文档中提示：只支持App和H5。所以，在编写时，需要充分阅读和参考官方文档。

**2.虽然只配置了app-plus，但是h5也能实现页面效果。原因是：配置编译到 App 平台时的特定样式，部分常用配置 H5 平台也支持。**

**3.页面数据绑定与vue一样，使用{{}}，但是需要注意：view、text等是参考小程序的写法，与html里面的span、div书写方式不一样，只能写组件里面的标签，参考如下：**

https://uniapp.dcloud.net.cn/component/view.html#



示例用法 这俩写法都可以

![image-20231123085531886](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231123085531886.png)



### 3.组件生命周期

说实话你创建vue3的uniapp项目很多语法还是vue2的，这个生命周期就是。

![image-20231125152759259](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125152759259.png)



## 3.尺寸转换及view及页面

### 1.view

在uniapp中，view就相当于h5中的div，以后的大部分布局都使用的是view这个布局元素，然后在uniapp中所有的布局建议全部使用flex布局

text就相当于以前的p标签



### 2.pages和components的区别

**pages就相当于vue中的view文件夹，实现页面跳转的，但是在uniapp中页面的跳转不是在路由设置，而是在pages.json文件和路由一起进行设置**

components就是一样的组件文件夹



### 3.RPX

![image-20231125152959811](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125152959811.png)

![image-20231125153111562](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125153111562.png)

![image-20231125152933137](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125152933137.png)

换算就是 750*100/设计稿宽度

#### 1.注意事项 nvue中不支持一些vue中支持的单位

![image-20231125153346526](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125153346526.png)

#### 2.补充：nvue是什么

在一些场景下，使用vue文件开发APP页面性能会不满足我们的需求，这时候可以为APP端专门写一个nvue文件。

![image-20231125154109645](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154109645.png)

nvue走的就是weex的原生渲染

![image-20231125154226841](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154226841.png)

![image-20231125154238705](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154238705.png)

常用的情况就是APP的首页或者登录页使用nvue文件，其它页面就是vue



## 4.pages.json配置

### 1.pages.json

![image-20231125223227307](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125223227307.png)

![image-20231125223256948](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125223256948.png)



#### 1.globalStyle和pages的style

![image-20231125224518805](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125224518805.png)

![image-20231125224537658](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125224537658.png)

**默认启动的页面就是pages数组的第一个页面**

####  2.在pages添加新页面

要配置一下微信小程序的设置

![image-20231125230055840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230055840.png)

新页面

![image-20231125230116992](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230116992.png)

微信小程序配置一下可以访问新页面，选择添加编译模式

![image-20231125230200407](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230200407.png)



### 2.自定义导航栏的使用

原生导航栏的颜色只支持white和black，所以有时候我们可以禁用原生导航栏。

![image-20231125230744308](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230744308.png)

如果要自定义导航栏实现这种效果

![image-20231125230958462](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230958462.png)

index.vue

```vue
<template>
	<!-- 自己设置导航栏，不使用原生的 -->
	<view class="status_bar">
		<!-- 这里是状态栏 -->
	</view>
	<view class="top">
		我的导航栏
	</view>
	<view class="content">
		这是我的主页面
	</view>
</template>

<script>
	export default {}
</script>

<style>
    .status_bar {
        /* 这个是uniapp封装好的一个变量，根据不同手机决定占位元素的高度 */
		height: var(--status-bar-height);
		width: 100%;
		background-color: orange;
	}
	.top {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		background-color: orange;
		font-size: 30rpx;
	}


</style>
```

禁用原生导航栏

![image-20231125231416568](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125231416568.png)

注意事项：没有设置status_bar 那些手机的wifi图标会遮住项目头部的一些地方

![image-20231125230702110](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230702110.png)

![image-20231125231902712](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125231902712.png)



### 3.easycom超级组件

![image-20231126204715425](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126204715425.png)

![image-20231126204744721](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126204744721.png)

如果需要自定义easycom就要自定义设置，看官网

**easycom在pages.json也是一样**

#### 1.给组件设置样式

在vue中，可以直接给引入的组件设置不一样的样式

![image-20231126210045365](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126210045365.png)

但是uniapp中无法进行属性的传递，只能用props传值

uniapp中内置组件是无法直接修改样式的，可以通过传props的方式来修改，或者用穿透选择器

例子：

父组件

```vue
<template>
	<!-- 自己设置导航栏，不使用原生的 -->
	<view class="status_bar">
		<!-- 这里是状态栏 -->
	</view>
	<view class="top">
		我的导航栏
	</view>
	<view class="content">
		这是我的主页面
	</view>
	<view class="button">
		<!-- 这样设置是没有用的，会关键词冲突，要用classxx或者abcd -->
		<uni-button class="btn"></uni-button>
		<uni-button classValue="btn"></uni-button>
	</view>
</template>

<script>
	export default {}
</script>

<style>
	.top {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		text-align: center;
		background-color: orange;
		font-size: 30rpx;
	}

	.status_bar {
		/* 这个是uniapp封装好的一个变量，根据不同手机决定占位元素的高度 */
		height: var(--status-bar-height);
		width: 100%;
		background-color: orange;
	}

	/* 因为在uni-app不能像vue一样进行属性的传递 */
	/* 在uniapp里没办法直接给内置组件定义样式 只能通过props传值 */
	/* 定制按钮组件的样式 */
	.btn {
		margin-top: 20rpx;
		background-color: aqua;
	}
</style>
```

子组件

```vue
<template>
	<view class="active">
		<button :class='classValue'>使用easycom方式定义的按钮</button>
	</view>
</template>

<script>
	export default {
		props: {
			classValue: {
				type: String,
				default: ''
			}
		}
	}
</script>

<style>
</style>
```



### 4.tabBar 页面底部导航栏

tabBar里面要用到的页面，要在pages中先进行引入，因为它是跳转的页面

![image-20231126212640706](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126212640706.png)

例子

![image-20231126212752530](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126212752530.png)

### 5.subPackages

查看项目代码大小:微信开发者工具->详情->基本配置->本地代码

![image-20231126213612476](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126213612476.png)

![image-20231126213738495](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126213738495.png)

![image-20231126213759780](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126213759780.png)

则需要在 pages.json 中填写

```json
{
	"pages": [{
        // 主包,一打开就会加载
		"path": "pages/index/index",
		"style": { ...}
	}, {
		"path": "pages/login/login",
		"style": { ...}
	}],
	"subPackages": [{
        // root表示分包1的根路径
		"root": "pagesA",
		"pages": [{
			"path": "list/list",
			"style": { ...}
		}]
	}, {
        // root表示分包2的根路径
		"root": "pagesB",
		"pages": [{
			"path": "detail/detail",
			"style": { ...}
		}]
	}],
     // 分包预载配置。
	"preloadRule": {
		"pagesA/list/list": {
			"network": "all",
			"packages": ["__APP__"]
		},
		"pagesB/detail/detail": {
			"network": "all",
			"packages": ["pagesA"]
		}
	}
}
```

![image-20231126214602880](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126214602880.png)

解释

![image-20231126214702697](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126214702697.png)



## 5.mianfest.json配置

常见的就是配置APP图标什么的

![image-20231126214927788](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126214927788.png)



## 6.uniapp路由

![image-20231126215154049](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126215154049.png)



### 1.组件方式实现页面跳转

![image-20231126220552076](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126220552076.png)

![image-20231126220658898](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126220658898.png)

![image-20231126220815653](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126220815653.png)

url支持绝对路径和相对路径

#### 1.打开新页面

打开新页面的方式，跳转到那个页面后会有一个自动显示的返回按钮

![image-20231126221818669](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126221818669.png)

#### 2.重定向

重定向的方式没有返回按钮，有回到主页的home按钮

![image-20231126222023245](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126222023245.png)

#### 3.回退

回退要注意，不能是重定向过来的页面跳转的，不然你设置是无效的

![image-20231126222604131](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126222604131.png)

#### 4.跳转至底部tabBar

如果是tabBar的页面，必须用switchTab方式来跳转，用其它方式无法跳转。

这种跳转方式没有返回键和home键。

![image-20231126222936188](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126222936188.png)



#### 5.relaunch

适合用在本页面中跳转，不希望有回退。跳完以后不会出现回退按钮，只有回主页的按钮。

本页跳转就算你用了redirect，也还是有回退按钮，这样页面栈就会爆满了，建议用relauch。

![image-20231126223432316](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126223432316.png)



### 2.API方式实现页面跳转

js编程方式....

#### 1.uni.navigateTo

![image-20231127105509822](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127105509822.png)





#### 2.uni.redirectTo



#### 3.uni.reLaunch



#### 4.uni.switchTab



#### 5.uni.navigateBack



### 3.参数传递

![image-20231203192731514](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203192731514.png)

页面携带参数

![image-20231127111053785](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111053785.png)

![image-20231127111308279](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111308279.png)

**跳转后的页面接收参数(必须在onLoad生命周期内)**

![image-20231127110939355](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127110939355.png)

参数传递时有特殊字符需要编码  **encodeURIComponent**

![image-20231127111215016](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111215016.png)

接收到了编码时

![image-20231127111401367](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111401367.png)

需要进行解码

![image-20231127111419166](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111419166.png)



#### 1.如果要用变量

![image-20231127111746757](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111746757.png)

![image-20231127111802864](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111802864.png)

##### 1.传递多个参数

![image-20231127111827804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111827804.png)



##### 2.传递数组或对象

方法1

![image-20231127111951853](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127111951853.png)

方法2

![image-20231127112050918](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127112050918.png)

方法3

![image-20231127112125470](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127112125470.png)



### 4.获取页面栈

微信小程序页面栈为5层

![image-20231127120305218](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127120305218.png)

![image-20231127120637362](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127120637362.png)

注意：我们只能去展示页面栈，不能直接去修改这个页面栈



### 5.微信小程序跳转层级限制

![image-20231127120744935](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127120744935.png)

解决方案

![image-20231127121520507](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127121520507.png)

![image-20231127121459548](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127121459548.png)



### 6.tabBar传参的方式

#### tabBar的页面特征

![image-20231127122829396](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127122829396.png)



![image-20231127121812862](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127121812862.png)



#### 1.利用本地缓存

![image-20231127170723237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127170723237.png)

发送页面

![image-20231127170640237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127170640237.png)

接收页面 利用onshow生命周期函数来接收

onShow监听页面显示，页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面

![image-20231127170951160](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127170951160.png)



#### 2.利用全局**globalData**

![image-20231127122254169](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127122254169.png)

![image-20231127122303109](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127122303109.png)



#### 3.利用状态库pinia或者vuex

定义一个store，然后在跳转页set，被跳转页get



#### 4.利用minxs混入的解决方案

这种方式没必要，太麻烦了，杀鸡用牛刀。

https://juejin.cn/post/7251501955373072445



#### 5.注意

![image-20231127122433432](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127122433432.png)



### 7.自定义封装tabBar

如果不是底部选项卡的页面，跳转后，底部选项卡就会消失，有时候我们不希望它下面的底部选项卡会消失，这时候我们要自己封装tabBar，这样所有的页面都可以访问到选项卡。

![image-20231127171701671](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231127171701671.png)

tabBar能看到的页面只有本身就是tabBar的那几个。但是大部分应用用原生tabBar就可以满足了，很多应用就那几个页面需要使用tabBar



封装的组件

我们的思路就是通过在父页面的时候使用onLoad生命周期获取页目路由，传给子组件，然后在组件生命周期mounted中接收，这样就可以控制跳转时候的样式，也可以进行页面的传参，不受原生tabBar的限制。

```vue
<template>
	<!-- 测试创建easycom组件 -->
	<!-- <view>这是一个uni-tab-bar组件</view> -->
	<!-- 占位符 防止有内容被导航栏挡住了 -->
	<view class="tab-bar-wrap"></view>
	<!-- 导航栏区域 -->
	<view class="tab-bar">
		<!-- 首页 -->
		<view :class="{item:true, home:true, active:homeActive}" @click="redirectPage('/pages/index/index')">
			<view class="icon"></view>
			<view class="text">首页</view>
		</view>
		<!-- 我的 -->
		<view :class="{item:true, my:true, active:myActive}" @click="redirectPage('/pages/my/my')">
			<view class="icon"></view>
			<view class="text">我的</view>
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				// 设置默认的属性，用来切换导航栏样式
				homeActive: true,
				myActive: false
			}
		},
		// 父组件需要把页面路由传给我
		// 然后通过这个去控制样式切换
		props: {
			curRoute: {
				type: String,
				default: ''
			}
		},
		methods: {
			redirectPage(url) {
				uni.redirectTo({
					url
				})
			}
		},
		// 当组件被创建时，执行switch函数
		// 这是vue的生命周期,初始化结束
		// 生命周期就是在某一阶段会自动的去执行一些函数
		mounted() {
			// 在哪个页面让它自己选中
			// this.curRoute 和 case的选项匹配
			switch (this.curRoute) {
				case "pages/index/index":
					this.homeActive = true;
					this.myActive = false;
					break;
				case "pages/my/my":
					this.homeActive = false;
					this.myActive = true;
					break;
				default:
					this.homeActive = true;
					this.myActive = false;
			}
		}
	}
</script>

<style>
	/* 设置组件的样式 */
	/* 设置与上方的间距 */
	.tab-bar-wrap {
		width: 100%;
		height: 130rpx;
	}

	/* 设置导航栏的区间 */
	.tab-bar {
		width: 100%;
		height: 100rpx;
		background-color: white;
		border-top: 1px solid gray;
		position: fixed;
		left: 0;
		bottom: 0;
		z-index: 99;
		display: flex;
		justify-content: space-around;
		align-items: center;
	}

	/* 设置每一个选项卡的宽度和高度 */
	.tab-bar .item {
		width: 80rpx;
		height: auto;
	}

	/* 设置选项卡的标题 */
	.tab-bar .item .text {
		font-size: 24rpx;
		text-align: center;
	}

	/* 选中后，标题文字颜色改变 */
	.tab-bar .item.active .text {
		color: #ff0000;
	}

	/* 选项卡里面的图标 */
	.tab-bar .item .icon {
		width: 60rpx;
		height: 60rpx;
		margin: 0 auto;
	}

	/* 设置首页的图标 */
	/* 没有选中时的图标 */
	.tab-bar .item.home .icon {
		background-image: url("~@/static/image/home1.png");
		background-size: 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	/* 图标选中后，改变成红色 */
	/* 模拟以前的active */
	.tab-bar .item.home.active .icon {
		background-image: url("~@/static/image/home2.png");
		background-size: 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	/* 设置我的图标 */
	.tab-bar .item.my .icon {
		background-image: url("~@/static/image/my1.png");
		background-size: 100%;
		background-position: center;
		background-repeat: no-repeat;
	}

	/* 图标选中后，改变成红色 */
	.tab-bar .item.my.active .icon {
		background-image: url("~@/static/image/my2.png");
		background-size: 100%;
		background-position: center;
		background-repeat: no-repeat;
	}
</style>
```



页面使用(每个页面要使用都可以，但是父组件要提供页面栈给封装的子组件)

```vue
<template>
	<navigator url="/pages/my/my" open-type="navigate">
		<button>去我的</button>
	</navigator>
	<view class="active">
		123
	</view>
	<!-- 使用自定义的tabBar组件 -->
	<uni-tab-bar :curRoute="curRoute"></uni-tab-bar>
</template>

<script>
	export default {
		data() {
			return {
				curRoute: ''
			}
		},
		// 页面生命周期
		// 页面加载
		onLoad(args) {
			// 获取页面栈
			let pages = getCurrentPages()
			// 获取当前页面
			let curPage = pages[pages.length - 1]
			// 赋值给curRoute传给子组件
			this.curRoute = curPage.route;
		}
	}
</script>

<style>
</style>
```



#### 1.这样封装也突破了tabBar的传参限制

index组件

```vue
<template>
	<view class="active">
		<button @click="gotoMy">去我的</button>
	</view>
	<view class="active">
		123
	</view>
	<!-- 使用自定义的tabBar组件 -->
	<uni-tab-bar :curRoute="curRoute"></uni-tab-bar>
</template>

<script>
	export default {
		data() {
			return {
				curRoute: ''
			}
		},
		methods: {
			gotoMy() {
				uni.navigateTo({
					url: '/pages/my/my?id=1&name=zs'
				})
			}
		},
		// 页面生命周期
		// 页面加载
		onLoad(args) {
			// 获取页面栈
			let pages = getCurrentPages()
			// 获取当前页面
			let curPage = pages[pages.length - 1]
			// 赋值给curRoute传给子组件
			this.curRoute = curPage.route;
			console.log(args.id, args.name);
		}
	}
</script>

<style>
</style>
```

my组件

```vue
<template>
	<view class="active">
		<button @click="gotoIndex">去首页</button>
	</view>
	<view class="active">
		123
	</view>
	<!-- 使用自定义的tabBar组件 -->
	<uni-tab-bar :curRoute="curRoute"></uni-tab-bar>
</template>

<script>
	export default {
		data() {
			return {
				curRoute: ''
			}
		},
		methods: {
			gotoIndex() {
				uni.navigateTo({
					url: '/pages/index/index?id=2&name=ls'
				})
			}
		},
		// 页面生命周期
		// 页面加载
		onLoad(args) {
			// 获取页面栈
			let pages = getCurrentPages()
			// 获取当前页面
			let curPage = pages[pages.length - 1]
			// 赋值给curRoute传给子组件
			this.curRoute = curPage.route;
			console.log(args.id, args.name);
		}
	}
</script>

<style>
</style>
```



## 7.运行环境及平台配置

![image-20231128165439847](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128165439847.png)

![image-20231128165741600](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128165741600.png)



### 1.判断环境

开发环境生产环境测试环境....

![image-20231128172147179](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172147179.png)

![image-20231128172247455](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172247455.png)

```js
// 三元运算符可以这样写
// 如果为dev 返回dev.com 如果为pro 返回xxx.com 其它情况返回空
let baseApi = process.env.NODE_ENV === 'development' ? 'http://dev.xxx.com' : process.env.NODE_ENV === 'production' ? 'http://www.xxx.com':'';

export default{
	baseApi
}
```

挂载到vue全局变量里

![image-20231128172708547](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172708547.png)



vue文件中使用全局变量来判断目前处于什么环境

![image-20231128172619737](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172619737.png)



### 2.自定义环境

![image-20231128172851536](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172851536.png)

![image-20231128172920877](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128172920877.png)



### 3.判断平台

#### 1.编译期间判断

使用条件编译可以为不同平台配置不同代码

![image-20231128174608118](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231128174608118.png)

![image-20231129214611873](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129214611873.png)

**js、css、html都是可以用条件编译的**

![image-20231129215219135](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215219135.png)

![image-20231129215236710](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215236710.png)

![image-20231129215248616](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215248616.png)

只有|| 或这种连接符号 表示在俩个平台都行

ifndef就是除了这个平台



#### 2.运行时判断

尽量不用，在开发时都解决好

![image-20231129215602195](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215602195.png)



## 8.内置组件

### 1.view组件

![image-20231129215711469](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215711469.png)

![image-20231129215947684](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129215947684.png)

设置hover-class

![image-20231129220549944](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129220549944.png)



### 2.button组件

它的open-type的开放能力，其实就是 uni.xxxx()  就是和前面那个路由跳转组件一样的，只是封装到了这个组件里面去，让它功能更强大。

#### 1.type值

button如果设置了type值，就会有一些默认样式，有时候给它设置类样式无法解决，这是因为选择器优先级问题，uniapp的优先级可能设置了更高，例如 父>button{},这种情况我们可以用行内样式解决。

#### 2.去除边框

要去除默认样式的边框第一种是border-radius设置为0 第二种是

![image-20231129223937786](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231129223937786.png)

open-type有很多的开放功能

![image-20231130085912242](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130085912242.png)

![image-20231130090059617](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130090059617.png)



#### 3.分享小程序

![image-20231130211044181](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130211044181.png)

**注意小程序的分享方法和生命周期是同级的**

![image-20231130211142893](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130211142893.png)

![image-20231130211159305](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130211159305.png)

点右上角也可以分享给好友

![image-20231130211308711](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130211308711.png)

### 3.checkBox组件

```react
<template>
	<view>
		<!-- checkbox组件 -->
		<checkbox-group @change="checkboxChange">
			<label class="uni-list-cell" v-for="item in items" :key="item.value">
				<view>
					<checkbox :value="item.value" :checked="item.checked" />
				</view>
				<view>{{item.name}}</view>
			</label>
		</checkbox-group>
		<button @click="submit()">提交</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'checkbox组件',
				items: [{
						value: 'USA',
						name: '美国'
					},
					{
						value: 'CHN',
						name: '中国',
						checked: 'true' // 默认选中中国
					},
					{
						value: 'BRA',
						name: '巴西'
					},
					{
						value: 'JPN',
						name: '日本'
					},
					{
						value: 'ENG',
						name: '英国'
					},
					{
						value: 'FRA',
						name: '法国'
					}
				]
			}
		},
		methods: {
			checkboxChange(e) {
				// 获取detail.value值
				console.log(e)
				var items = this.items,
                     // 事件对象的detail里面存放着值
					values = e.detail.value;
				for (var i = 0, lenI = items.length; i < lenI; ++i) {
					const item = items[i]
					// 如果是有被选中的
					if (values.includes(item.value)) {
						this.$set(item, 'checked', true)
					} else {
						this.$set(item, 'checked', false)
					}
				}
			},
			// 提交时，将选中的数据存入数组，然后输出。最终目的是在数据库里进行处理
			submit() {
				let arr = [];
				for (var i = 0; i < this.items.length; i++) {
					// 如果items里面被选中的
					if (this.items[i].checked) {
						// 就添加到数组中
						arr.push(this.items[i])
					}
				}
				// 字符串转成数组
				console.log(JSON.stringify(arr))
			}
		}
	}
</script>

<style>
	.uni-list-cell {
		display: flex;
	}
</style>
```



### 4.radio单选框组件

```vue
<template>
	<view>
		<!-- radio组件 -->
		<radio-group @change="radioChange">
			<label class="uni-list-cell" v-for="item in items" :key="item.value">
				<view>
					<radio :value="item.value" :checked="item.checked" />
				</view>
				<view>{{item.name}}</view>
			</label>
		</radio-group>
		<button @click="submit()">提交</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'radio组件',
				items: [{
						value: 'USA',
						name: '美国'
					},
					{
						value: 'CHN',
						name: '中国',
						checked: 'true' // 默认选中中国
					},
					{
						value: 'BRA',
						name: '巴西'
					},
					{
						value: 'JPN',
						name: '日本'
					},
					{
						value: 'ENG',
						name: '英国'
					},
					{
						value: 'FRA',
						name: '法国'
					}
				]
			}
		},
		onLoad() {
			this.newItem = {} // 全局变量
		},
		methods: {
			radioChange(e) {
				var val = e.detail.value;
				// console.log(val)   // 输出选中的value
				for (var i = 0; i < this.items.length; i++) {
					if (this.items[i].value == val) {
						this.newItem = this.items[i];
						break;
					}
				}
			},
			// 提交时，将选中的数据存入数组，然后输出。最终目的是在数据库里进行处理
			submit() {
				console.log(JSON.stringify(this.newItem))
			}
		}
	}
</script>

<style>
	.uni-list-cell {
		display: flex;
	}
</style>
```



### 5.scroll-view

滚动组件 可以上下左右滚动

![image-20231130214158187](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231130214158187.png)

```vue
<style>
	.scroll-y {
		width: 100%;
		height: 300rpx;
		background: gray;
	}

	.red {
		background-color: red;
	}

	.yellow {
		background-color: yellow;
	}

	.bluie {
		background-color: blue;
	}

	/* uniapp中的scroll组件没办法直接用felx：1让子元素水平分bu */
	.scroll-x {
		width: auto;
		height: 300rpx;
		display: flex;
		/* white-space 属性设置如何处理元素内的空白。 */
		/* 空白不换行 */
		white-space: nowrap;
	}

	.red1 {
		display: inline-block;
		height: 300rpx;
		width: 100%;
		background-color: red;
	}

	.yellow1 {
		display: inline-block;
		height: 300rpx;
		width: 100%;
		background-color: yellow;
	}

	.bluie1 {
		display: inline-block;
		height: 300rpx;
		width: 100%;
		background-color: blue;
	}
</style>
<template>
	<view>
		<!-- 开启上下滚动 -->
		<scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-y" @scrolltoupper="top" @scrolltolower="bottom"
			@scroll="scroll" :scroll-with-animation="true">
			<view class="red">第一个A</view>
			<view class="yellow">B</view>
			<view class="bluie">C</view>
			<view class="red">A</view>
			<view class="yellow">B</view>
			<view class="bluie">C</view>
			<view class="red">A</view>
			<view class="yellow">B</view>
			<view class="bluie">C</view>
			<view class="red">A</view>
			<view class="yellow">B</view>
			<view class="bluie">C</view>
			<view class="red">A</view>
			<view class="yellow">B</view>
			<view class="bluie">C</view>
			<view class="red">A</view>
			<view class="yellow">B</view>
			<view class="bluie">最后一个C</view>
		</scroll-view>
		<button @click="toTop">回到顶部</button>
		<!-- 横向滚动 -->
		<scroll-view scroll-x="true" class="scroll-x" :scroll-with-animation="true">
			<view class="red1">A</view>
			<view class="yellow1">B</view>
			<view class="bluie1">C</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 默认状态下和元素内容页面顶部的距离
				scrollTop: 0,
				// 滚动条临时的距离
				tmpScrollTop: 0
			}
		},
		methods: {
			// 滚动到顶部
			top(e) {},
			// 滚动到底部
			bottom(e) {},
			// 发生滚动
			scroll(e) {
				// 发生滚动时给临时滚动条设置距离(不能直接给scrollTop设置，不然会一直回滚)
				this.tmpScrollTop = e.detail.scrollTop
				// console.log(this.scrollTop)
			},
			// 使用按钮回到顶部的方法 需要用到组件异步更新(也可以用定时器)
			toTop() {
				// 临时滚动条的目的是赋值给这里用
				this.scrollTop = this.tmpScrollTop
				this.$nextTick(() => {
					// 回到顶部
					this.scrollTop = 0
				})
				uni.showToast({
					icon: "none",
					title: "纵向滚动 scrollTop 值已被修改为 0"
				})
			}
		}
	}
</script>
```

### 6.swiper

**滑块组件，类似轮播图**

![image-20231203143300698](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203143300698.png)

![image-20231203143645356](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203143645356.png)



### 7.text组件

![image-20231203144049512](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203144049512.png)

![image-20231203144456618](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203144456618.png)

例子

![image-20231203144513529](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203144513529.png)

![image-20231203144639774](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203144639774.png)

**不开decode解码的话，文本有特殊字符就不会解析，只能解析纯文本**



### 8.rich-text

这个东西是用来设置一些超级文本，比如超链接或者是不同的字体颜色，其实没必要这样，直接用class什么的去控制了

![image-20231203145634789](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203145634789.png)

![image-20231203150147589](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203150147589.png)



html字符串节点支持style和class的设置

![image-20231203150807362](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203150807362.png)



用数组的方式性能好但是很难书写，可以用这个插件来吧html字符串转为数组

![image-20231203151601009](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203151601009.png)

![image-20231203151635424](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203151635424.png)

![image-20231203151741158](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203151741158.png)



















## 9.内置API

### 1.请求微信授权

开始授权前，需要配置appid以及开启微信登录模块，同时微信开发者工具基础库应该调至2.25.2

```vue
<template>
	<view class="btn-box">
		<button @click="toIndex">前往首页</button>
		<button @click="getUserProfile">获取授权</button>
	</view>
	<view class="userinfo-box" v-if="isAutorized">
		<image class="img-avar" :src="userinfo.avatarUrl"></image>
		<text class="text-name">{{ userinfo.nickName }}</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isAutorized: false,
				userinfo: {
					avatarUrl: '',
					nickName: '',
					openid: ''
				},
				// 请求微信接口需要的参数
				weixin: {
					jscode2sessionUrl: 'jscode2session',
					appid: 'wx303da12a38734d48',
					secret: ''
				}
			}
		},

		methods: {
			toIndex() {
				uni.switchTab({
					url: '/pages/index/index'
				})
			},
			getUserProfile() {
				// 固定this
				const that = this;
				uni.showLoading({
					title: '正在授权进行中...'
				})
				// 获取用户信息的接口
				uni.getUserProfile({
					lang: 'zh_CN',
					desc: '授权获得更多服务',
					success(userRes) {
						// 给了一个默认的头像和姓名
						const {
							avatarUrl,
							nickName
						} = userRes.userInfo;
						uni.login({
							provider: 'weixin',
							success(res) {
								// 拼接请求微信后台的url
								let url =
									`https://api.weixin.qq.com/sns/${that.weixin.jscode2sessionUrl}?appid=${that.weixin.appid}&secret=${that.weixin.secret}&js_code=${res.code}&grant_type=authorization_code `;
								console.log("登录成功！" + url)
								// 发起网络请求
								uni.request({
									// 请求地址
									url,
									success(res2) {
										console.log("授权成功成功！")
										console.log("获取头像，昵称成功！")
										that.userinfo.avatarUrl = avatarUrl;
										that.userinfo.nickName = nickName;
										that.userinfo.openid = res2.data.openid;

										//保存授权状态
										// that.userStore.saveWxUserinfo(that.userinfo);

										// 显示用户头像和nickName
										that.isAutorized = true
									}
								})
							}
						})
					},
					fail() {
						title: '授权失败'
					},
					// 请求结束了以后隐藏 loading 提示框。
					complete() {
						uni.hideLoading();
					},
				})
			}
		}
	};
</script>
```



### 2.现在的方法是这样的

需要授权就用授权按钮，需要头像就用头像

```vue
<style scoped>
	.avatar {
		width: 100rpx;
		height: 100rpx;
	}

	.weui-input {
		width: 100%;
		height: 30rpx;
	}
</style>

<template>
	<view class="serach-bar">
		<!-- <button open-type="openSetting">跳出授权页</button> -->
		<button class="avatar-wrapper" open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
			设置头像
		</button>
		<view>
			<input type="nickname" class="weui-input" placeholder="请输入昵称" v-model="nickname" @focus="onInput($event)" />
		</view>
		<view>
			用户头像:
			<image class="avatar" :src="avatarUrl"></image>
		</view>

		<view class="text">
			用户名称:
			{{ nickname }}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				avatarUrl: '',
				nickname: ''
			}
		},
		methods: {
			onInput(e) {
				// 如果用户直接选择了微信昵称 这里需要我们手动绑定一下
				if (e.detail.value) {
					this.nickname = e.detail.value
				}
			},
			onChooseAvatar(e) {
				const {
					avatarUrl
				} = e.detail
				this.avatarUrl = avatarUrl
			}
		}
	}
</script>
```

![image-20231201002005532](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231201002005532.png)

### 3.交互反馈

#### 1.uni.showToast

![image-20231203193417599](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203193417599.png)

mask用的比较多，因为弹出提示的时候，我们不希望用户还能操作页面。

![image-20231203193503721](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203193503721.png)

![image-20231203193756923](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203193756923.png)

#### 2.uni.showLoading()

![image-20231203193925960](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203193925960.png)

#### 3.uni.showModal()

这东西可以在里面内嵌一个输入框

![image-20231203194449082](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203194449082.png)

![image-20231203194508873](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203194508873.png)

例子:

```vue
<template>
	<button @click="showModal">验证手机号</button>
	<view class="active">
		手机号 --- {{ data }}
	</view>
</template>

<script setup>
	import {
		ref
	} from 'vue'
	const data = ref()

	const showModal = () => {
		uni.showModal({
			title: '输入框',
			placeholderText: '请输入手机号',
			// 显示输入框
			editable: true,
			success(res) {
				// 用户点了确定
				if (res.confirm) {
					data.value = res.content
					console.log(res.content);
				} else if (res.cancel) {
					console.log('用户取消输入');
				}
			}
		})
	}
</script>

<style>
</style>
```



#### 4.uni.showActionSheet()

显示上拉选项卡，和表单里面的一个组件很像

![image-20231203200658228](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203200658228.png)



#### 5.uni.setNavigationBarTitle(OBJECT)

动态设置标题栏

动态设置标题栏颜色

![image-20231204103427522](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204103427522.png)

#### 6.uni.showNavigationBarLoading(OBJECT)

loading显示在导航栏上面



### 4.tabbar补充

给tabbar加上iconfont图标，官方文档里面有iconfont的相关配置，可以弄成更好的图片

**首先把iconfont下载下来，引入static文件夹，记得是.ttf的格式**

**不过这个不支持小程序端，小程序还是用原来的iconpath**



![image-20231204212144214](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204212144214.png)

![image-20231204213158689](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204213158689.png)



#### 1.动态设置tabBar  -- uni.setTabBarItem

#### 2.在APP.vue中动态设置tabBar样式

![image-20231204220317490](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204220317490.png)



#### 3.隐藏和显示tabBar

在tabBar页面，有时候我们想暂时隐藏tabBar或显示就可以用这个

![image-20231204220429158](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204220429158.png)



#### 4.为tabBar右上角添加文本

![image-20231204220618868](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204220618868.png)



#### 5.右上角添加小红点

![image-20231204220815385](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231204220815385.png)



### 5.网络请求API

例子 演示了俩种传参

```vue
<template>
	<view v-for="item in url" :key="item.id">
		<button @click="createMsg(1)">获取消息</button>
		<image :src="item.url" mode="aspectFill"></image>
	</view>
	<br />
	<!-- 用/的传参方式 -->
	<button @click="createMsg1(1)">获取消息1</button>
	<view v-for="item in newUrl" :key="item.id">
		{{ item.title }}
	</view>
</template>

<script setup>
	import {
		ref
	} from 'vue'
	const url = ref([''])
	const newUrl = ref([])
	const createMsg = (limit) => {
		uni.request({
			url: 'https://api.thecatapi.com/v1/images/search',
			method: 'get',
			data: {
				// 一次获取三张图片
				limit: limit
			},
			success: (res) => {
				console.log(res.data)
				url.value = res.data
			}
		})
	}
	const createMsg1 = (row) => {
		uni.request({
			url: `https://jsonplaceholder.typicode.com/photos/${row}`,
			// 这种方式就不用data传值了
			method: 'get',
			success: (res) => {
				console.log(res.data)
				newUrl.value.push(res.data)
				console.log(newUrl.value);
			}
		})
	}
</script>
```



## 10.vue补充

### 1.修饰符

#### 1.native

在组件上定义的方法vue都认为我们是自定义的事件，有时候我们需要在组件上用原生事件例如click，此时要加上native修饰符

![image-20231203153853804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203153853804.png)

#### 2.sync

这是父组件

![image-20231203154454193](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203154454193.png)

写上这个相当于是

![image-20231203154524745](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203154524745.png)

**sync相当于替你绑定了事件，事件名为update:xxx , 相当于v-model**

vue3里面已经没有了这个修饰符



## 11.命令行创建uni-app项目

![image-20231203182908183](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231203182908183.png)



## 12.补充

### 1.uniapp拦截器

经典案例:路由拦截

```js
//白名单
const whiteList = [
	'/',
	'/pages/index/index',
	'/pages/my/my',
	'/pages/index/login',
	'/pages/index/register',
	'/pages/index/wiki',
	'/pages/index/crop',
	'/pages/serach/search',
	'/pages/listview/listIndex'
]

function hasPermission(url) {
	let islogin = uni.getStorageSync('isLogin');
	islogin = Boolean(Number(islogin)); //返回布尔值
	// 在白名单中或有登录判断条件可以直接跳转
	if (whiteList.indexOf(url) !== -1 || islogin) {
		return true
	}
	return false
}

export default async function() {
	const list = ['navigateTo', 'redirectTo', 'reLaunch', 'switchTab'];
	list.forEach(item => {
		uni.addInterceptor(item, {
			invoke(e) {
				// 获取要跳转的页面路径（url去掉"?"和"?"后的参数）
                 // 拆分以后取第一部分就是url地址
				const url = e.url.split('?')[0]
				if (whiteList.includes(url)) {
					console.log('url', url, e)
					// 判断当前窗口是白名单，如果是则不重定向路由
					return true;
				} else {
					uni.showToast({
						title: '用户没有权限...',
						duration: 2000,
						icon: 'none',
					})
					return false
				}
			},
			fail() {
				return false
			}
		})
	})
}
```

参考地址:[uniapp如何实现路由守卫、路由拦截，权限引导_uniapp路由导航守卫-CSDN博客](https://blog.csdn.net/m0_57033755/article/details/132871892)

官网地址:[uni.addInterceptor(STRING, OBJECT) | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/api/interceptor.html#拦截器的适用场景非常多-比如路由拦截-权限引导等。)
