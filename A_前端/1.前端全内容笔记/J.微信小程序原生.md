**1.开发推荐选择iPhone6/7/8，因为他是375px，也就是750rpx，更好做页面适配。**

**2.小程序的宿主环境是指程序运行需要的依赖环境，安卓的在苹果跑不了(手机微信就是它的环境)**

**3.小程序所有API带Sync的都是同步的，其余的都是异步的函数**

**4.小程序是基于node.js的，所以它支持的模块规范是CJS**



**5.小程序的语言组成**

![image-20231211200830852](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211200830852.png)



**WebView 技术**

![image-20231211104012613](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211104012613.png)

![image-20231211104037562](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211104037562.png)



**6.wxss和css的关系**

![image-20231211200923885](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211200923885.png)

![image-20231211200947838](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211200947838.png)



**7.小程序的宿主环境**

![image-20231211201050410](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201050410.png)

![image-20231211201128836](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201128836.png)

![image-20231211201140820](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201140820.png)

![image-20231211201109219](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201109219.png)

![image-20231211201203965](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201203965.png)

**8.补充:三元运算符**

![image-20231212105505249](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212105505249.png)



# 1.官方文档

## 1.页面配置

分为全局配置和页面配置

全局配置在app.json中，每个页面有自己单独的json配置文件，局部的json配置文件优先级更高。

**全局配置**

![image-20231213083725493](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231213083725493.png)

**如果配置了navigatStyle: 'custom' 表示导航栏需要我们自己自定义，所以此时所有window的配置都无效**

![image-20231213084135439](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231213084135439.png)



**页面配置**

不用加window

![image-20231213083753808](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231213083753808.png)



### 1.sitemap.json

**通过配置 `sitemap.json`，可以优化小程序的搜索引擎优化（SEO）效果，提高页面在搜索结果中的展示和排名。**

![image-20231211160954779](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211160954779.png)

![image-20231211161012945](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211161012945.png)

![image-20231211200737168](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211200737168.png)



## 2.视图层

数据绑定在 3-小程序框架 -3.1

### 1.条件渲染

![image-20231212103735680](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212103735680.png)

### 2.wxss

![image-20231212104008489](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212104008489.png)

![image-20231212104043919](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212104043919.png)

![image-20231212110621663](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212110621663.png)

### 3.wxs

![image-20231212111051375](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212111051375.png)



### 4.事件绑定

![image-20231212113054081](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212113054081.png)

在target.dataset.xx就可以接收到参数







## 3.小程序框架

### 1.数据绑定

框架的核心是一个响应的数据绑定系统,其实是融合了vue和react

![image-20231211160028143](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211160028143.png)

**如果是要修改标签内的，和vue不一样**

![image-20231211160116942](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211160116942.png)

![image-20231211201444966](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201444966.png)



#### 1.列表渲染 wx:for

![image-20231211163533858](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211163533858.png)

默认为index和item,可以进行修改

![image-20231211164034628](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211164034628.png)

item也是同理

不指定key的时候默认key为index,可以主动指定一个wx:key

![image-20231211165046757](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211165046757.png)



#### 2.数据更新

```js
        // 数据更新
        this.setData({
            name: name,
            friend: {
                name: '我是宇宇hello'
            }
        })
```



#### 3.事件传参

![image-20231211201559704](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201559704.png)

![image-20231211201616869](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201616869.png)

![image-20231211201706644](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201706644.png)

![image-20231211201726117](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211201726117.png)

```html
    <!-- 要传常数要套双花括号 -->
	<!-- 不能直接在方法后面加()传参 要用data- 来传参数 -->
    <button bind:tap="onClick" data-number="{{123}}">修改死狗name</button>
```

```js
    // 单击修改名称
    onClick(e) {
        // 接收参数的地方
        console.log(e.target.dataset.number);
    },
```



### 2.小程序场景值

![image-20231211161234477](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211161234477.png)

场景值列表: https://developers.weixin.qq.com/miniprogram/dev/reference/scene-list.html



**什么时候来使用场景值**

**小程序的场景值（scene）是指用户打开小程序时传递给小程序的一个参数，用于标识用户打开小程序的场景。通过场景值，开发者可以根据不同的场景做出相应的逻辑处理，提供更加个性化和定制化的用户体验。**

场景值的具体取值是由微信客户端定义的，不同的场景值代表不同的场景。以下是一些常见的场景值及其含义：

- 1011: 扫描小程序码打开
- 1012: 长按图片识别小程序码打开
- 1013: 手机相册选取小程序码打开
- 1014: 扫描手机相册中的条码打开
- 1017: 透传小程序模板消息打开
- 1019: 地理位置消息打开
- 1020: 卡券详情页打开
- 1022: 前往小程序体验版的入口页
- 1023: 微信连Wi-Fi状态栏打开小程序
- 1024: 公众号 profile 页相关小程序列表打开
- 1025: 扫描一维码打开
- 1026: 扫描二维码打开
- 1027: 扫描小程序码打开
- 1031: 长按图片识别一维码打开
- 1032: 长按图片识别二维码打开
- 1034: 手机相册选取一维码打开
- 1035: 手机相册选取二维码打开

**开发者可以通过获取场景值，根据不同的场景进行业务处理。例如，可以根据场景值判断用户是通过扫描小程序码打开的，然后展示相应的欢迎页面；或者根据场景值判断用户是通过地理位置消息打开的，然后提供与地理位置相关的功能。**

在小程序中，可以通过 `App.onLaunch` 和 `App.onShow` 方法的回调参数中获取场景值。具体的代码示例如下：

```js
App({
  onLaunch: function (options) {
    console.log('场景值:', options.scene);
  },
  onShow: function (options) {
    console.log('场景值:', options.scene);
  }
});
```

**通过打印上述代码中的 `options.scene`，开发者可以在控制台查看到当前小程序的场景值。**



### 3.在app.js中注册小程序

![image-20231211161644355](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211161644355.png)

```bash
1.onLoaunch 表示小程序第一次加载 初始化
2.onShow 表示监听小程序启动或切前台
3.onHide 表示小程序进入后台
4.onError 表示处理程序抛出的异常问题
```

参考网址:https://developers.weixin.qq.com/miniprogram/dev/reference/api/App.html



### 4.Page注册页面

![image-20231211161958866](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211161958866.png)

示例

```js
//index.js
Page({
    // 页面初始化数据
  data: {
    text: "This is page data."
  },
    
    // 以下表示页面的生命周期函数
  onLoad: function(options) {
    // 页面创建时执行
  },
  onShow: function() {
    // 页面出现在前台时执行
  },
  onReady: function() {
    // 页面首次渲染完毕时执行
  },
  onHide: function() {
    // 页面从前台变为后台时执行
  },
  onUnload: function() {
    // 页面销毁时执行
  },
  onPullDownRefresh: function() {
    // 触发下拉刷新时执行
  },
  onReachBottom: function() {
    // 页面触底时执行
  },
  onShareAppMessage: function () {
    // 页面被用户分享时执行
  },
  onPageScroll: function() {
    // 页面滚动时执行
  },
  onResize: function() {
    // 页面尺寸变化时执行
  },
  onTabItemTap(item) {
    // tab 点击时执行
    console.log(item.index)
    console.log(item.pagePath)
    console.log(item.text)
  },
  // 事件响应函数
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    }, function() {
      // this is setData callback
    })
  },
  // 自由数据
  customData: {
    hi: 'MINA'
  }
})
```



### 5.使用类似vue2中的混入

![image-20231211162232136](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211162232136.png)

**就是定义了一个公共的js文件来存储数据和方法， 在页面里可以直接使用**



### 6.使用Compoent注册页面

![image-20231211163119048](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211163119048.png)



### 7.页面生命周期

![page-lifecycle.2e646c86](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/page-lifecycle.2e646c86.png)



### 8.页面路由

微信有这个页面栈的概念。

![image-20231211172446165](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211172446165.png)

![image-20231211172723471](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211172723471.png)

![image-20231211172741355](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211172741355.png)



### 9.模块化和设置全局变量

![image-20231211174820915](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211174820915.png)



**可以加APP({}) 里面挂载全局变量,在每个js文件都可以访问到这个全局变量**

**getApp()用来获取小程序实例**

![image-20231211174912386](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211174912386.png)



### 10.小程序的API接口

小程序开发框架提供丰富的微信原生 API，可以方便的调起微信提供的能力，如获取用户信息，本地存储，支付功能等。详细介绍请参考 [API 文档](https://developers.weixin.qq.com/miniprogram/dev/api/index.html)。

通常，在小程序 API 有以下几种类型：

1. ![image-20231212102917271](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212102917271.png)

2. ![image-20231212102954511](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212102954511.png)

3. ![image-20231212103112898](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212103112898.png)

4. ![image-20231212103231667](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212103231667.png)

5. ![image-20231212103248858](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231212103248858.png)



## 4.猜数字小游戏

```js
Page({
    data: {

    },
    // 初始化数据方法
    initGameNum() {
        this.setData({
            number: Math.floor(Math.random() * 100) + 1, // 随机数
            // 每一次输入的内容
            info: '',
            // 输入框的内容 默认值为-1
            inpNum: '',
            // 计数
            count: 0,
            // 游戏标识符
            isRun: true,
            // 是否合法数据
            flag: false
        })
        console.log('答案是' + this.data.number);
    },

    // 获取用户输入 判断输入的数字区间是否在1-100
    checkNum(e) {
        //isNaN:判断其是不是一个number数字
        if (isNaN(e.detail.value)) {
            wx.showToast({
                title: '非法字符',
                icon: 'error'
            })
            // 输入不合法 flag为false
            this.setData({
                flag: false,
                inpNum: ''
            })
            return;
        }

        // 数据越界
        if (e.detail.value < 0 || e.detail.value > 100) {
            wx.showToast({
                title: '数据越界',
                icon: 'error'
            });
            // 游戏停止
            this.setData({
                flag: false,
                inpNum: ''
            })
            return
        }

        //  数据合法就赋值更新
        this.setData({
            inpNum: e.detail.value,
            // 合法的时候flag为true
            flag: true
        })
    },

    // 提交的方法
    onSubmit() {
        // 如果是flag直接return
        if (this.data.flag === flag) {
            return
        }
        // 输入的信息
        let mation = this.data.info
        // 游戏的次数
        let num = this.data.count + 1

        if (this.data.inpNum == this.data.number) {
            mation = mation + "\n恭喜你唐腾强,猜中了,答案是" + (this.data.number)
            this.setData({
                info: mation,
                isRun: false
            });
            // 猜中直接结束了
            return
        }

        // 猜大猜小
        if (this.data.inpNum < this.data.number) {
            mation = mation + "\n唐腾强,第" + (num) + "个回合:" + (this.data.inpNum) + "猜小了"
        } else if (this.data.inpNum > this.data.number) {
            mation = mation + "\n唐腾强,第" + (num) + "个回合:" + (this.data.inpNum) + "猜大了"
        }

        if (num === 4) {
            mation = mation + "\n回合结束"
            this.setData({
                info: mation,
                isRun: false
            })
            return
        }

        this.setData({
            info: mation,
            count: num,
            // 清空输入框
            inpNum: '',
            // 提交按钮以后重置flag
            flag: false
        })
    },

    // 重新开始
    restart() {
        this.initGameNum()
    },
    onLoad(options) {
        this.initGameNum()
    }
})
```

```html
<view class="container">
    <view class="title">欢迎来到猜数字游戏</view>
    <view class="content" style="margin: 30rpx 0;">
        <view wx:if="{{isRun}}">
            <input class="input" style="margin-bottom: 30rpx;" placeholder="请输入1-100的数字" bindblur="checkNum" value="{{inpNum}}" />
            <!-- 如果不在js里判断 就在这里判断,不为true的时候不能点击 -->
            <!-- <button  class="button" bind:tap="{{flag === true ? 'onSubmit': ''}}" style="margin-bottom: 30rpx;" type="primary">猜一下</button> -->
            <button class="button" bind:tap="onSubmit" style="margin-bottom: 30rpx;" type="primary">猜一下</button>
        </view>

        <view wx:else>
            <view class="text"><text>游戏结束,点击按钮重新开始</text></view>
            <button type="primary" bind:tap="restart">重新开始</button>
        </view>

        <view>
            <text class="result">{{ info }}</text>
        </view>

    </view>
</view>
```

```css
/* pages/game/game.wxss */
input{
    border: gray 1px solid;
    border-radius: 10px;
    font-size: 28rpx;
    height: 70rpx;
}

.text{
    display: flex;
    justify-content: center;
    margin-bottom: 50rpx;
}
```

