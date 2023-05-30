# HTML5

## 1.什么是HTML5

**HTML5** 是 HTML标准的最新演进版本,它是一个新的 HTML *语言*版本包含了新的元素，属性和行为，同时包含了一系列可以被用来让 Web 站点和应用更加多样化，功能更强大的技术。 这套技术往往被称作 *HTML5 和它的朋友们，*通常简称为 *HTML5*。

* h5指的是一系列技术做的移动端**ppt**,它的页面很酷炫，可以提高公司的逼格，亮瞎访问者的双眼，让小白顿生膜拜之感，即使ppt毫无实质，使用大量的插件或库，主要技术有：

   1.页面素材加载技术，使用使用createJS之中的preloadJS（现成的库）

   2.音乐加载播放技术，createJS中同样有soundJS可以实现（又是它）

   3.可以滑动的页面，这不就是ppt吗？用了swiper.js这个Jquery插件（又是库）

   4.可以随意涂抹修改，使用canvas叠加层，canvas是HTML5标准里面的标签。这不是ppt吗？

   5.有动态的文字和图片，常见的是使用了css3或者直接使用js动画,这不是ppt吗?

   6.可以填表报名，使用最基本的表单

   7.可以支持分享自定义的文案和图片

**html5 和h5的区别**

1. html5 是公认的web开发的html规范，是一系列关于html的标准，它就好比是国家的法律，比如未成年不准进网吧，网吧要是允许未成年人进入，国家就要对网吧和未成年人进行处罚和教育。同样的，你写的html网页不遵守html5规范，可能导致你的网页在浏览器上出现一系列问题，后果自负。

- h5是一系列技术的集合，它是应用一系列的web技术出现的产物。

## 2.HTML5新特性

新特性
 1.语意特性,添加`<header><header/><nav><nav>`等标签

 2.多媒体， 用于媒介回放的 video 和 audio 元素

 3.图像效果，用于绘画的 canvas 元素，svg元素等

 4.离线 & 存储,对本地离线存储的更好的支持,local Store,Cookies等

 5.设备兼容特性 ，HTML5提供了前所未有的数据与应用接入开放接口。使外部应用可以直接与浏览器内部的数据直接相连，

 6.连接特性，更有效的连接工作效率，使得基于页面的实时聊天，更快速的网页游戏体验，更优化的在线交流得到了实现。HTML5拥有更有效的服务器推送技术，Server-Sent Event和WebSockets就是其中的两个特性，这两个特性能够帮助我们实现服务器将数据“推送”到客户端的功能

 7.性能与集成特性，HTML5会通过XMLHttpRequest2等技术，帮助您的Web应用和网站在多样化的环境中更快速的工作

## 3.HTML5新增标签

1.多媒体：

```html
<audio></audio>音频内容
<video><video>视频内容
<source></source>   //<source> 标签为媒介元素（比如 <video> 和 <audio>）定义媒介资源。
<embed></embed>  //<embed> 标签定义了一个容器，用来嵌入外部应用或者互动程序（插件）。
<track></track>  //HTML <track> 元素 被当作媒体元素—<audio> 和 <video>的子元素来使用。它允许指定时序文本字幕（或者基于时间的数据），例如自动处理字幕。
```

 2.新表单元素：

```html
<datalist> 标签规定了 <input> 元素可能的选项列表。
<datalist> 标签被用来在为 <input> 元素提供"自动完成"的特性。用户能看到一个下拉列表，里边的选项是预先定义好的，将作为用户的输入数据。请使用 <input> 元素的 list 属性来绑定 <datalist> 元素。
    
<output> 标签作为计算结果输出显示(比如执行脚本的输出)。
    
<keygen> 标签规定用于表单的密钥对生成器字段。
```

 3.新文档节段和纲要:

```html
<header>页面头部、<section>章节、<aside>边栏、<article>文档内容、<footer>页面底部、<section>章节等
```



使用html5shiv可以解决ie低版本不兼容的问题，只需要在head中加上,当版本低于IE9时，浏览器会加载html5.js脚本，使得支持html5的新功能，也可以将脚本文件下载到本地

```html
<head>
  <!--[if lt IE 9]>
  <script src='http://apps.bdimg.com/libs/html5shiv/3.7/html5shiv.min.js'>
  </script>
  <![endif]-->
</head>
```

## 4.input的新增类型

- color,选择颜色
- date 选择日期
- email 用于检测输入的是否为email格式的地址
- month 选择月份
- number  用于应该包含数值的输入域，可以设定对输入值的限定
- range 用于定义一个滑动条，表示范围
- search 用于搜索，比如站点搜索或 Google 搜索
- tel 输入电话号码
- time 选择时间
- url 输入网址
- week 选择周和年

## 5.浏览器本地存储中 cookie 和 localStorage 有什么区别？ localStorage 如何存储删除数据。

- **共同点：sessionStorage、localStorage和cookie都由浏览器存储在本地的数据。**

- *区别*
   1.cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递，localStorage不会自动把数据发给服务器，仅在本地保存

-  2.cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下，存储大小限制也不同，cookie数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。localStorage不会自动把数据发给服务器

-  3.cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。**localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据**

-  4.localStorage支持事件通知机制，可以将数据更新的通知发送给监听者。 api 接口使用更方便。而cookie的原生接口不友好，需要程序员自己封装

  

- HTML5中提供了localStorage对象可以将数据长期保存在客户端，除非人为清除，localStorage提供了几个方法:
   1.存储:`localStorage.setItem(key,value)`如果key存在时，更新value
   2.获取 `localStorage.getItem(key)`如果key不存在返回null
   3.删除 `localStorage.removeItem(key)`一旦删除，key对应的数据将会全部删除
   4.全部清除 `localStorage.clear()` 使用removeItem逐个删除太麻烦，可以使用clear,执行的后果是会清除所有localStorage对象保存的数据

- **注意：localStorage存数的数据是不能跨浏览器共用的，一个浏览器只能读取各自浏览器的数据,储存空间5M。**