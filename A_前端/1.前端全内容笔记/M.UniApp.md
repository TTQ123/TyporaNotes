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



### 2.页面生命周期

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

#### 1.注意事项 nvue中不支持一些vue中支持的文件

![image-20231125153346526](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125153346526.png)

#### 2.补充：nvue是什么

在一些场景下，使用vue文件开发APP页面性能会不满足我们的需求，这时候可以为APP端专门写一个nvue文件。

![image-20231125154109645](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154109645.png)

nvue走的就是weex的原生渲染

![image-20231125154226841](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154226841.png)

![image-20231125154238705](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125154238705.png)

常用的情况就是APP的首页或者登录页使用nvue文件，其它页面就是vue



## 4.pages.json和mainfest.json

### 1.pages.json

![image-20231125223227307](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125223227307.png)

![image-20231125223256948](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125223256948.png)



#### 1.globalStyle和pages的style

![image-20231125224518805](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125224518805.png)

![image-20231125224537658](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125224537658.png)

####  2.在pages添加新页面

要配置一下微信小程序的设置

![image-20231125230055840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230055840.png)

新页面

![image-20231125230116992](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230116992.png)

微信小程序配置一下可以访问新页面，选择添加编译模式

![image-20231125230200407](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230200407.png)



### 2.原生导航栏

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
</style>
```

禁用原生导航栏

![image-20231125231416568](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125231416568.png)

注意事项：没有设置status_bar 那些手机的wifi图标会遮住项目头部的一些地方

![image-20231125230702110](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125230702110.png)

![image-20231125231902712](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231125231902712.png)