# CSS3

## ![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710011930755.png)

## CSS3现状

- 在CSS2的基础上新增（扩展）样式
- 移动端支持优于PC端
- 不断改进中
- 应用相对广泛

## 1.CSS3属性(结构)选择器

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200516094132623.png)

input[style="color:red"]

## 2. CSS3结构伪类选择器

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200516094234422.png)

nth-child 详解:

- 注意：本质上就是选中第几个子元素

- n 可以是数字、关键字、公式

- n 如果是数字，就是选中第几个

- 常见的关键字有 even 偶数、odd 奇数

- 常见的公式如下(如果 n 是公式，则从 0 开始计算)

- 但是第 0 个元素或者超出了元素的个数会被忽略
  ![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200516094400941.png)

- **`nth-child` 和 `nt-of-type` 的区别**
- `nth-child` 选择父元素里面的第几个子元素，不管是第几个类型
- `nth-of-type` 选择指定类型的元素

## 3.CSS3伪元素选择器

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200516094531788.png)

注意事项：

- before 和 after 必须有 content 属性

- before 在内容前面，after 在内容后面

- **before 和 after 创建的是一个元素，但是属于行内元素**

- **创建出来的元素在 Dom 中查找不到，所以称为伪元素**

- **伪元素和标签选择器一样，权重为 1**

  典型应用：
  添加字体图标

  ```css
  <p>Hello World!</p>
  
  <style>
  p {
     width: 220px;
     height: 22px;
     border: 1px solid lightseagreen;
     margin: 60px;
     position: relative;
  }
  p::after {
      /*引入字体图标*/
    content: '\ea50';
    font-family: 'icomoon';
    position: absolute;
    top: -1px;
    right: 10px;
  }
  </style
  ```

## 4. CSS3过渡(非常重要)

过渡动画：是从一个状态渐渐的过渡到另外一个状态，IE9以下不支持，经常和:hover一起搭配使用
语法格式：

```css
transition:要过渡的属性 花费时间 运动曲线 何时开始
```

![image-20211005212227862](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20211005212227862.png)

运动曲线示意图:

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200321183443774.png)

示例:

```css
div {
		width: 200px;
		height: 100px;
		background-color: pink;
		/* transition: 要过渡的属性  花费时间  运动曲线  何时开始; */
		/* transtion 过渡的意思  这句话写到div里面而不是 hover里面 
		过渡写到本身上，谁做动画，给谁加*/
		transition: width 0.6s ease 0s, height 0.3s ease-in 1s;			
}
/*hover 在内容后面*/
div:hover {  /* 鼠标经过盒子，我们的宽度变为400 */

			width: 600px;
			height: 300px
}

transition: all 0.6s;  /* 所有属性都变化用all 就可以了  后面俩个属性可以省略 */
```

常见效果：
按钮变换底色 图片移动 小米效果 （阴影效果） 传智导航栏效果 等等

![image-20211005212601313](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20211005212601313.png)

## 5.CSS3 2D转换

**转换**（transform）是CSS3中具有颠覆性的特征之一，**可以实现元素的位移、旋转、缩放等效果。**
转换（transform）可以简单理解为变形

- 移动：translate
- 旋转：rotate
- 缩放：scale

### 1) 二维坐标系

2D转换是改变标签在二维平面上的位置和形状的一种技术

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200622124055317.png)

### 2) 2D转换之移动(translate)

2D移动是2D转换里的一种功能，可以改变元素在页面中的位置，类似**定位**

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200622124334882.png)

1.语法:

```css
transform: translate(x, y);
            /* 或者分开写 */
	transform: translateX(x);
	transform: translateY(y);
```

2.重点

- 定义2D转换中的移动，沿着X和Y轴移动元素
- translate最大的优点：不会影响到其他元素的位置
- translate中的百分比单位是相对于自身元素的translate:(50%, 50%);
- **对行内标签没有效果**，就是用在块级元素的

### 3) 2D转换之旋转rotate

2D旋转指的是让元素在2维平面内顺时针旋转或者逆时针旋转。

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200622215304178.png)

1.语法：

```css
transform:rotate(度数);
```

2.重点

- rotate里面的度数的单位是deg比如rotate(45deg)
- 角度为正时为顺时针，负时为逆时针
- **默认旋转的中心点是元素的中心点**

##### 案例：三角形

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200622215500312.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>三角形</title>
    <style>
        div {
            position: relative;
            width: 249px;
            height: 35px;
            border: 1px solid #000;
        }
        
        div::after {
            content: "";
            position: absolute;
            top: 8px;
            right: 15px;
            width: 10px;
            height: 10px;
            border-bottom: 1px solid #000;
            border-right: 1px solid #000;
            transform: rotate(45deg);
            transition: all 0.2s;
        }
        /* 鼠标经过div 里面的三角旋转 */
        div:hover::after {
            transform: rotate(225deg);
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

最终效果，当鼠标放置在三角图标上时三角图标旋转。

### 4) 2D转换中心点transform-origin

1.语法

```css
transform-origin:x y;
```

**2.重点**

- 注意后面的参数x和y用空格隔开
- x y默认的中心点是元素的中心点（50% 50%）
- **还可以给x y设置像素或者方位名词（top bottom left right center）**

##### 案例：旋转案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>旋转案例</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            border: 1px solid pink;
            margin: 100px auto;
            overflow: hidden;
        }
        
        div::before {
            content: "黑马";
            display: block;
            width: 200px;
            height: 200px;
            background-color: lightgreen;
            transform: rotate(180deg);
            /*设置了方向*/
            transform-origin: left bottom;
            transition: all 0.2s;
        }
        /* 鼠标经过div 里面的before复原 */
        
        div:hover::before {
            transform: rotate(0deg);
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

### 5）2D转换之缩放scale

可以放大和缩小，只要给元素添加上了这个属性就能控制它放大还是缩小

1.语法:

```css
transform:scale(x,y);
```

2.注意
注意其中的x和y用逗号分隔，里面的数字不跟单位就是倍数
transform: scale(1, 1)：宽和高都放大一倍，相当于没有放大
transform: scale(2, 2)：宽和高都放大了2倍
transform: scale(2)：只写一个参数，第二个参数则和第一个参数一样
transform: scale(0.5, 0.5)：缩小1倍
**scale缩放最大的优势：可以设置转换中心点缩放，默认以中心点缩放的，而且不影响其他盒子**

##### 案例：图片放大

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>图片放大</title>
    <style>
        div {
            overflow: hidden;
            float: left;
            margin: 10px;
        }
        
        div img {
            transition: all .4s;
        }
        
        div img:hover {
            transform: scale(1.1);
        }
    </style>
</head>

<body>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
</body>

</html>
```

##### 案例：分页按钮

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>分页按钮案例</title>
    <style>
        li {
            float: left;
            width: 30px;
            height: 30px;
            line-height: 30px;
            text-align: center;
            margin-left: 10px;
            margin-top: 20px;
            border-radius: 50%;
            list-style: none;
            border: 1px solid green;
            cursor: pointer;
            transition: all .4s;
        }
        
        li:hover {
            /*放大1.2倍*/
            transform: scale(1.2);
        }
    </style>
</head>

<body>
    <div>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
        </ul>
    </div>
</body>

</html>
```

结果如图:

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200622225307902.png)

### 6)  2D转换综合写法

注意：

1. **同时使用多个转换，其格式为：transform: translate() rotate() scale()……等**
2. **其顺序会影响转换的效果（先旋转会改变坐标轴的方向）**
3. **当我们同时有位移(移动)和其他属性的时候，记得要将位移放到最前面**



## 6.CSS3动画

动画（animation）是CSS3中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。
相比较过渡，动画可以实现更多的变化，更多的控制，连续自动播放等效果。

#### 1)动画的基本使用

制作动画分为两步：

1. **先用keyframes定义动画(类似定义类选择器)**
   
   动画序列

- 0%是动画的开始，100%是动画的完成，这样的规则就是动画序列
- 在**@keyframes**中规定某项CSS样式，就能创建由当前样式逐渐改为新样式的动画效果
- 动画是使元素从一种样式逐渐便化为另一种样式的效果，你可以改变任意多的样式任意多的次数。
- 请用百分比来规定变化发生的时间，或用关键词 " form " 和 ‘’ to " ，等同于0%和100%

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200623151300486.png)

```CSS
	@keyframes 动画名称 {
		0%{
			width: 100px;
		}
		100%{
			width: 200px;
		}   
	}
```

**2.再使用（调用）动画**

```css
  div{
       width: 200px;
       height: 200px;
       background-color: green;
       margin: 100px auto;
       /* 调用动画 */
       animation-name: 动画名称;
       /* 持续时间 */
       animation-duration: 持续时间;
   }
```

#### 2)动画常用属性

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200624092633324.png)

具体每个属性的具体值需要用到的时候在百度

#### 3)动画简写属性

**animation：1.动画名称(name) 2.持续时间(duration) 3.运动曲线(timing-function) 4.何时开始(delay) 5.播放次数(iteration-count) 6.是否反方向(direction) 7.动画起始或者结束的状态(fill-mode）；**

**写法：animation: name duration timing-function delay iteration-count direction fill-mode;**

- **简写属性里面不包含animation-play-state，如需使用，单独写**
- 暂停动画：animation-play-state：puased;经常和鼠标经过等其他配合使用
- 想要动画走回来，而不是直接就回来(逆向在播放回来)：animation-direction: alternate
- 盒子动画结束后，停在结束位置：animation-fill-mode: forwards
  

##### 案例：7热点图

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>热点图</title>
    <style>
        body{
            background-color: #333;
        }
        .map{
            position: relative;
            width: 747px;
            height: 616px;
            margin: 0 auto;
            background: url('media/map.png') no-repeat;
        }
        .city{
            position: absolute;
            top: 227px;
            right: 191px;
        }
        .tb{
            top: 499px;
            right: 80px;
        }
        .dotted{
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #09f;
        }
        /*选中有class属性且值以pulse开头的*/
        div[class^='pulse']{
            position: absolute;
            top: 50%;
            left: 50%;
            width: 10px;
            height: 10px;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            box-shadow: 0 0 12px #009dfd;
            /*动画名称pulse 持续1.2s  匀速播放 无限循环播放动画*/
            animation: pulse 1.2s linear infinite;
        }
        .city .pulse2{
            animation-delay: 0.4s;
        }
        .city .pulse3{
            animation-delay: 0.8s;
        }
        @keyframes pulse {
            0%{}
            70%{
                /* 用scale会导致阴影也放大 */
                /* transform: scale(2); */
                width: 40px;
                height: 40px;
                /*不透明度*/
                opacity: 1;
            } 
            100%{
                width: 70px;
                height: 70px;
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="map">
        <div class="city">
            <div class="dotted">
                <div class="pulse1"></div>
                <div class="pulse2"></div>
                <div class="pulse3"></div>
            </div>
        </div>
        <div class="city tb">
            <div class="dotted">
                <div class="pulse1"></div>
                <div class="pulse2"></div>
                <div class="pulse3"></div>
            </div>
        </div>
    </div>
</body>
</html>
```

效果图:

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200630174729618.png)

如果用scale结果如图(修改元素大小)：

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200701140619729.png)

#### 4)速度曲线细节

animation-timing-function：规定动画的速度曲线，默认是ease

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200701151013732.png)

##### 案例：速度曲线

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>速度曲线案例</title>
    <style>
        div{
            width: 0;
            height: 20px;
            background-color: lightgreen;
            font-size: 12px;
            /* 让文字强制一行显示 */
            white-space: nowrap;
            /* steps就是分几步来完成动画
               保持最后一帧的状态
            */
            animation: move 5s steps(8) forwards;
            
        }
        @keyframes move {
            0%{
                width: 0;
            }
            100%{
                width: 100px;
            }
        }
    </style>
</head>
<body>
    <div>
        前端欢迎您！
    </div>
</body>
</html>
```

##### 案例：奔跑的熊

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>奔跑的熊</title>
    <style>
        body {
            /*背景图片*/
            background: url('../Img/loginBg.png') no-repeat;
            /*绑定bgback
              6s完成一次
              无线循环播放
              */
            animation: bgback 6s steps(8) infinite;
        }

        div {
            /*相对定位*/
            position: absolute;
            width: 200px;
            height: 100px;
            background: url('../Img/wx.png') no-repeat;
            /*动画名称
              0.4s完成动画
              steps(8)把动画分为8部分运行
              infinite无限播放
              forwards当动画完成后，保持最后一帧的状态
            */
            animation: bear 0.4s steps(8) infinite, move 2s steps(8) forwards;
        }

        @keyframes bear {
            0% {
                background-position: 0 0;
            }

            100% {
                background-position: -1600px 0;
            }
        }

        @keyframes move {
            0% {
                left: 0;
                top: 200px;
            }

            100% {
                left: 50%;
                top: 200px;
                transform: translateX(-50%);
            }
        }

        @keyframes bgback {
            0% {
                background-position: 0 0;
            }

            100% {
                background-position: -1600px 0;
            }
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

结果如图：

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/2020070118002799.png)

### 7.3D转换

特点：

- 近大远小
- 物体后面遮挡不可见

#### 1.三维坐标系

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200702144156475.png)

三维坐标系其实就是指立体空间，立体空间是由3个轴共同组成的。

- **x轴：水平向右 注意：x右边是正值**
- **y轴：垂直向下 注意：y下面是正值**
- **z轴：垂直屏幕 注意：往外面是正值**

#### 2.3D移动 translate3D

3D移动在2D移动的基础上多加了一个可以移动的方向，就是z轴方向

- transform: translateX(100px)：仅仅是在X轴上移动

- transform: translateY(100px)：仅仅是在Y轴上移动

- transform: translateZ(100px)：仅仅是在Z轴上移动（注意：translateZ一般用px单位）

- transform: translate3d(x,y,z)：其中x、y、z分别要移动的轴的方向的距离（x、y、z没有不可省略，写0）


#### 3.透视perspective（一般给父盒子添加）

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200702163340776.png)

在2D平面产生近大远小视觉立体，但是只是效果是二维的

- 如果想要在网页产生3D效果需要透视（可理解成3D物体投影在2D平面内）
- 模拟人类的视觉位置，可认为安排一只眼睛去看
- 透视也称为视距：视距就是人的眼睛到屏幕的距离
- 距离视觉点越近的在电脑平面成像就越大，越远成像就越小
- 透视的单位是像素
  **透视写在被观察元素的父盒子上面的**
  d：就是视距，视距就是一个距离人的眼睛到屏幕的距离
  z：就是z轴，物体距离屏幕的距离，z轴越大（正值）我们看到的物体就越大。

#### 4.translateZ（一般给里面的盒子添加）

**transform: translateZ(100px)：仅仅是在Z轴上移动，有了透视，就能看到translateZ引起的变化了。**

#### 5.3D旋转rotate3d

3D旋转指可以让元素在三维平面内沿着x轴，y轴，z轴或者自定义轴进行旋转。
语法

- transform: rotateX(45deg)：沿着x轴正方向旋转45度

- transform: rotateY(45deg)：沿着y轴正方向旋转45度

- transform: rorateZ(45deg)：沿着z轴正方向旋转45deg

- transform: rotate3d(x, y, z, deg)：沿着自定义轴旋转，deg为角度（了解）
  沿x轴旋转：单杠

  

  **对于元素旋转的方向的判断，需要用到左手准则**
  **左手准则**

- 左手的手拇指指向x轴的正方向

- 其余手指的弯曲方向就是该元素沿着x轴旋转的方向

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200707233233365.png)

沿y轴旋转：钢管舞

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200707233826371.png)

- 对于元素旋转的方向的判断，需要用到左手准则

左手准则

- 左手的手拇指指向y轴的正方向
- 其余手指的弯曲方向就是该元素沿着y轴旋转的方向(正值)

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200707233632938.png)

沿z轴(向屏幕内为正)旋转：抽奖转盘

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/2020070723383855.png)

transform: rotate3d(x, y, z, deg)：沿着自定义轴旋转deg为角度（了解即可）
xyz是表示旋转轴的矢量，是标识你是否希望沿着该轴旋转，最后一个标示旋转的角度。

#### 6.3D呈现transform-style(使被转换的子元素保留其 3D 转换)

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200709220545438.png)

- 控制子元素是否开启三维立体环境
- transform-style: flat子元素不开启3d立体空间，默认的
- transform-style: preserve-3d;子元素开启立体空间
- **代码写给父级，但是影响的是子盒子**
- **这个属性很重要**



##### 案例：两面翻转的盒子

**实现步骤**

1.搭建HTML结构

- box父盒子里面包含两个子盒子
- box是翻转的盒子，front是前面盒子，back是后面盒子

2.CSS样式

- box指定大小，切记要添加3d呈现
- back盒子要沿着Y轴翻转180度
- 最后鼠标经过box沿着Y旋转180deg

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D导航栏</title>
    <style>
        body {
            perspective: 400px;
        }
        
        .box {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 200px auto;
            transition: all .5s;
            /* 让背面的盒子保留立体空间，给父级添加 */
            transform-style: preserve-3d;
        }
        
        .front,
        .back {
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            font-size: 24px;
            text-align: center;
            line-height: 300px;
        }
        
        .front {
            background-color: lightcoral;
            z-index: 1;
        }
        
        .back {
            background-color: lightgreen;
            /* 像手机一样背靠背旋转 */
            transform: rotateY(180deg);
        }
        
        .box:hover {
            transform: rotateY(180deg);
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="front">是日前端</div>
        <div class="back">在这里等你</div>
    </div>
</body>

</html>
```

##### 案例：3D导航栏

###### 实现步骤：

1. 搭建HTML结构

- li做导航栏

- .box是翻转的盒子，front是前面的盒子，bottom是底下的盒子
  思路：

  ![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710005820504.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D导航栏</title>
    <style>
        li {
            list-style: none;
            perspective: 500px;
        }
        
        ul {
            margin: 100px;
        }
        
        ul li {
            /*左浮动排列*/
            float: left;
            width: 100px;
            height: 50px;
            margin-left: 10px;
        }
        
        .box {
            position: relative;
            width: 100%;
            height: 100%;
            transition: all .5s;
            /* 让背面的盒子保留立体空间，给父级添加 */
            transform-style: preserve-3d;
        }
        
        .front,
        .bottom {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            line-height: 50px;
            text-align: center;
        }
        
        .front {
            background-color: lightgreen;
            transform: translateZ(25px);
        }
        
        .bottom {
            background-color: yellowgreen;
            /* 这里的x轴一定是负值 */
            /* 如果有移动或者其他样式，必须先写移动 */
            transform: translateY(25px) rotateX(-90deg);
        }
        
        .box:hover {
            transform: rotateX(90deg);
        }
    </style>
</head>

<body>
    <ul>
        <li>
            <div class="box">
                <div class="front">是日前端</div>
                <div class="bottom">在这里等你</div>
            </div>
        </li>
        <li>
            <div class="box">
                <div class="front">是日前端</div>
                <div class="bottom">日拱一卒</div>
            </div>
        </li>
        <li>
            <div class="box">
                <div class="front">是日前端</div>
                <div class="bottom">在这里等你</div>
            </div>
        </li>
    </ul>
</body>

</html>
```

结果如图：

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710003124571.png)

##### H5C3综合案例：旋转木马

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>旋转木马</title>
    <style>
        body{
            perspective: 800px;
        }
        section{
            position: relative;
            width: 300px;
            height: 200px;
            margin: 100px auto;
            transform-style: preserve-3d;
            animation: rotate 8s linear infinite;
            background: url(images/pig.jpg) no-repeat;
        }
        section div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url(images/dog.jpg) no-repeat;
        }
        section div:first-child{
            transform: rotateY(0deg) translateZ(300px);
        }
        section div:nth-child(2){
            transform: rotateY(60deg) translateZ(300px);
        }
        section div:nth-child(3){
            transform: rotateY(120deg) translateZ(300px);
        }
        section div:nth-child(4){
            transform: rotateY(180deg) translateZ(300px);
        }
        section div:nth-child(5){
            transform: rotateY(240deg) translateZ(300px);
        }
        section div:last-child{
            transform: rotateY(320deg) translateZ(300px);
        }
        section:hover{
            animation-play-state: paused;
        }
        @keyframes rotate {
            0%{
                transform: rotateY(0);
            }
            100%{
                transform: rotateY(360deg);
            }
        }
    </style>
</head>
<body>
    <section>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </section>
</body>
</html>
```

结果如图:

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710125013517.png)

### 7.练习1

#### ![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710125604324.png)

HTML结构：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>01.《阴阳师》二维码</title>
    <link rel="stylesheet" href="css/index.css">
</head>
<body>
    <div class="scan">
        <img class="qrcode" src="images/57b280b496dee47507111c56NRN73rVj.png" alt="">
        <img class="line" src="images/line_dd0b705.png" alt="">
    </div>
</body>
</html>
```

CSS样式：

```css
*{
    margin: 0;
    padding: 0;
}
body{
    padding: 50px;
}
.scan{
    position: relative;
    /* margin: 50px; */
    width: 145px;
    height: 297px;
    background: url(../images/index_z_71df05e.png) 0 0 no-repeat;
}
.qrcode{
    position: absolute;
    display: block;
    left: 19px;
    top: 45px;
    width: 107px;
}
.line{
    position: absolute;
    left: 9px;
    top: -3px;
    width: 120px;
    height: 15px;
    -webkit-animation: sao 4s linear infinite;
    -moz-animation: sao 4s linear infinite;
    -ms-animation: sao 4s linear infinite;
    animation: sao 4s linear infinite;
}
@keyframes sao{
    0%{
        top: 42px;
    }
    50%{
        top: 145px;
    }
    100%{
        top: 42px;
    }
}
```

结果：

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710125644658.png)

### 8.练习2

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710125904699.png)







## 7.浏览器私有前缀

浏览器私有前缀是为了兼容老版本的写法，比较新版本的浏览器无需添加。

### 7.1私有前缀

- -moz-：代表firefox浏览器私有属性
- -ms-：代表ie浏览器私有属性
- -webkit-：代表safari、chrome私有属性
- -o-：代表Opera私有属性

### 7.2提倡的写法

![在这里插入图片描述](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20200710005706315.png)



> 本文为CSDN博主「是日前端」的原创文章。
> 原文链接：https://blog.csdn.net/focusmickey/article/details/104722797
