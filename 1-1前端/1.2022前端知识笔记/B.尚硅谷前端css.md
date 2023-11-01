# 1.CSS的三大特性是继承、层叠、优先级

## 1.css的三种引入方式

### 1.行内样式

在标签内部通过style属性来设置元素样式



### 2.内部样式表

通过在head中添加style标签

```html
<head>
    <style>
        p{
            color:blue
        }
    </style>
</head>
```

优点是复用性相对高，缺点就是只能对单页面生效，不能跨页面生效。



### 3.外部样式表

通过link标签引入外部css文件，这种方法可以让一个css文件多网页使用

```html
<link rel=“stykesheet” href=“./1.css”> //rel=“styslesheet”表示样式表 html还有很多新的rel引用方式
//href指定路径
a标签也通过href属性来指定路径的，img这些使用src属性来指定路径的
```

**将样式编写到外部的css文件中，可以使用到浏览器的缓存机制，从而加快网页的加载速度**

```css
页面在加载时会进行分析，优先加载重要的资源内容。比如浏览器一般会先加载CSS，再去加载JavaScript脚本和图像文件。当然，浏览器的判断并不一定都是准确的，下面就来看看如何影响浏览器对资源加载的优先级。
```

**多个网页引用同一个css文件时，只需要第一次加载时缓存一次(这也是大部分网页第一次打开较慢的原因)，后面的网页就不用在加载一次，从而提高了网页的加载速度**

css中注释使用ctrl+/



### 4.css基本语法 选择器 声明块

```css
/*
	通过选择器选择指定元素
	声明快来为指定元素设置样式，声明块是由一个个声明组成  名值对结构
	样式名：样式值;
*/ 
p{
	color:blue;
}
```



### 5.常用选择器

#### 1.元素选择器 语法：  标签名{}

根据元素选择一组元素标签

例如p{}

#### 2.id选择器  语法：#id值{}

**作用：根据id值选择❤一个元素**

例如 #shcool1{}

#### 3.类选择器  语法：.class{}

**根据元素的class属性值选中❤一组元素**

#### 4.通配选择器 语法：*{}

全选选择器



### 6.复合选择器

#### 1.交集选择器  作用：希望元素满足多个条件❤

**语法：选择器1选择器2{}**

**交集选择器中如果有元素选择器，必须使用元素选择器开头**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /*
            将class为red的div字体大小设置为30px
        */
        div.red {
            font-size: 30px;
        }
        /*
        	选中div2
        */
        .a.b.c{
            font-size:30px;
        }
        /*
        	class值是可以有多个的❤
        */
    </style>
</head>

<body>
    <div class="red">我是div</div>
    <p class="red">我是p</p>
    <div class="red2 a b c">
      我是div2
    </div>
</body>

</html>
```



#### 2.并集选择器  作用：同时选择多个选择器对应的元素

**语法：选择器1，选择器2{}**

**满足的选择器全部选中❤**

```css
/*
	选择id值为id1，class值为class1，span标签
	#id1,.class1,span{}
*/
同时选中！
```



### 7.关系选择器(父子兄弟祖先后代选择器)

```css
/*
	1.父元素 直接包含子元素的元素叫做父元素
	2.子元素 直接被父元素包含的元素叫做子元素
	3.祖先元素 直接或间接包含后代元素的元素叫做祖先元素
		-一个元素的父元素也是他的祖先元素
	4.后代元素 直接或间接被祖先元素包含的元素叫做后代元素
		-子元素也是后代元素
	5.兄弟元素 拥有相同父元素的元素的是兄弟元素
*/
```

#### 1.子元素选择器

**语法:父元素>子元素{}**

```html
<style>
    /*
    	此时如果要只选第一个div中的span
    	我们利用复合选择器加子元素选择器  记得元素选择器要写在开头
    	语法:  div.class1 > span{}
    	
    div>p>span{}  选择div的子元素p的子元素span
    */
</style>

<div class="calss1">
    <span>我是div中的span</span>
</div>

<div>
    <span>我也是div中的span</span>
    <p>
        <span></span>
    </p>
</div>

```



#### 2.后代元素选择器

**语法：祖先 后代{}**   **开发中最常用的之一**

**例子：选中ul中的最后一个li的a标签    ul li：last-child a{ }**



#### 3.兄弟选择器

**语法：前一个+下一0个{}**  **作用：选择前一个紧挨着的下一个的兄弟元素**

**选择下边所有的兄弟元素  语法：div~span{}   选择div下面的所有兄弟元素span**



### 8.属性选择器 语法：[属性值]{}

**作用:通过元素的属性名来选择**    例如：[class] 选择有设置class属性的元素

```css
/*
	1.[属性名}选择含有指定属性的元素
	2.[属性名=属性值] 选择含有指定属性和属性值的元素
	
	
	3.[属性名^=属性值] 选择属性值以指定值开头的元素
	4.[属性名$=属性值] 选择属性值以指定值结尾的元素
	5.[属性名*=属性值] 选择属性值含有某值的元素
*/
```

**此时2个div都会被选中**

![uTools_1678068378494](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678068378494.png)



### 9.伪类选择器和伪元素选择器  作用：用来描述一个元素的特殊状态❤

**语法：:伪类{}   ::伪元素{}**

```html
<style>
	/*
    	要求将ul的第一个li设置为红色
    		方法1 ul>li.first{color:red;}  这种方法的缺点是有时候结构不固定的时候，样式就不能够适用条件了
    		方法2 利用伪类选择器
    		ul>li:first-child{color:red;}
    */
    /*
    注意点:以下这些伪类都是根据所有的子元素进行排序
    	1.:first-child 第一个子元素
    	2.:last-child 最后一个子元素
    	3.:nth-child() 选择第n个元素
    		特殊值
    			n 第n个  n的范围0到正无穷
    			2n 或 even 表示选中偶数位的元素
    			2n+1 或 odd 表示选中奇数位的元素
    	
    */
    
    /*
    	以下这些伪类是在同类型元素中进行排序
        4.:first-of-type 第一个
        5.:last-of-type  最后一个
        6.:nth-of-type()  第n个
        
    	7.:not() 否定伪类   除了这个元素,作用是单独把一个标签单独拿出来设置
    		-将符合条件的元素从选择器中去除
    	例子:将除了第三个子元素的其它元素背景颜色设为red
    		ul>li:not(:nth-child(3)){background-color:red}
  		
    	8.当元素获得焦点时 :foucs  例如input:foucs,表示当鼠标移入文本框时
    */
</style>

<ul>
	<li class="first">1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>

```



### 10.超链接的伪类

```html
<style>
    /*
    1.没有访问过的链接  a:link{}用来表示没访问过的链接(正常的链接，所有的链接都算正常的链接)
    2.访问过的链接  a:visited{}用来表示访问过的链接  由于隐私的原因我们都正常都不去设置  如果真的要改最多改个颜色
    3.鼠标移入的状态 a:hover{}用来表示鼠标移入时的状态
    4.鼠标点击时的状态，正在点击时的状态 a:active{}
    注意:1和2只能用在a标签，3和4是所有元素都可以进行设置的
	*/
    
    当你需要四个伪类同时设置时需要注意顺序要满足lvha 即link visited hover active(或者vlha都可以)
    原因是因为浏览器的就近原则link是未点击时的样式，距离更近
    
    
    1.如果一个链接没有被访问过，那么它有可能同时拥有 link , hover 两个属性，不能让 link 写在后面，
    否则不管 hover 是否，都会显示link的样式；同样的道理，如果一个链接已经被访问过了，
    那么它有可能同时拥有visited , hover 两个属性，hover 要在 visited 的后面；
    
    2.如果把hover放在active后面，那么实际你在激活（active）链接的时候就触发了hover伪类，
    hover在后面覆盖了active的颜色，所以始终无法看到active的颜色 。
    
    3.
    当 <a> 标签的 href 属性为空的时候，:link样式不会生效，所以正常的 color : yellow 会生效；
    当 <a> 标签的 href 属性不为空的时候，:link 样式才会生效，这时候，如果 <a> 标签正常样式 和 a：link 冲突了的话，以写在后面的那个为准；
</style>

```

**此时字体为红色**

![uTools_1678069082968](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678069082968.png)



### 11.伪元素选择器  作用：表示特殊并不真实存在的元素(特殊的位置)❤

**语法 ：：**

```css
<style>
    /*
    	1.::first-letter 表示第一个字母
    	2.::first-line 表示第一行
    	3.::selection 表示鼠标选中的内容
    	4.::before 元素的开始
    	5.::after 元素的最后
    		-before和after必须结合content属性来适用，这俩个也是开发中用的最多的
    		注意:通过伪元素产生的内容在网页中是无法选中的(通过css向html中添加内容)，例如百度文库就会采用这种让你无法进行复制，以此保护版权
    */
</style>

```



### 12.关于CSS样式继承的问题

```html
<style>
	/*
    	继承是发生在祖先和后代之间的，我们为一个元素设置样式的同时也会应用到它的后代元素
    	继承是为了方便我们的开发，利用继承我们可以将一些通用的样式设置到共同的祖先元素上，这样设置一次所有元素都有该样式
    	因为在默认情况下一个标签的内容的样式都是一样的
    
    	注意:并不是所有的样式都会被继承
    		--比如背景和布局相关的样式都不会被继承
    	css属性的继承性可以在zeal的css文档查询或者w3shcool查询
    */
    
    /*
    	此时给p元素设置一个背景颜色  span是不会继承的
    	在视觉效果看来是继承了，其实没有继承，只是默认的背景颜色是透明的，p元素的red背景色透过了透明
    */
    p{
        background-color:red;
    }
</style>

<div>
    <p>
        我是一个p元素
        <span>我是p里的span</span>
    </p>
</div>

/**/
```



### 13.选择器权重(简单来说范围越大权重越低)

**当你发现设置的css样式不起作用时首先就要考虑是不是权重有问题**

```html
<style>
	/*
    	样式的冲突发生在当我们选中不同的选择器，选中相同的元素，并且为相同的样式设置不同的值时，就会发生冲突
    	
    	发生冲突时，由选择器优先级决定具体表现的样式
    
    	⭐选择器的权重
    		!important 10000  开发时不要用，js改不了
    		内联样式 1000   权重过高也是我们不使用内联样式的原因之一
    		id选择器 100
    		类选择器和伪类选择器 10
    		元素选择器 1
    		
    	比较优先级时，需要将所有的选择器的优先级进行相加计算，优先级越高越优先显示
    */
</style>
```

**此时显示为color:aqua的效果**

![uTools_1678069417475](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678069417475.png)



### 14.单位

#### 1.长度

##### 1.像素（显示器实际上是由一个个的像素构成的）

不同屏幕的像素大小是不同的，像素越小的屏幕显示的效果越清晰

同样的px在不同的设备下显示效果不一样

##### 2.百分比(设置属性相对于其父元素属性的百分比)

百分比的好处在于子元素可以跟随父元素的改变而改变



#### 2.em和rem

##### 1.em

em是相对于元素的字体大小来计算的，浏览器默认字体大小是16px

1 em = 1 font-size(正常是16px)

em会随字体大小的改变而改变

##### 2.rem

rem是相对于根元素(html标签)的字体大小来计算的，用在移动端适配最多

rem会随字体大小的改变而改变



#### 3.颜色单位

##### 1.RGB值（根据光的三原色）

​	--RGB实际上是通过三种颜色的不同浓度来调配出不同的颜色r red,g green,b blue

​		 每一种颜色的范围在0-255（0%-100%）之间

**--语法：RGB(红色，绿色，蓝色)**

黑色  RGB(0,0,0)  白色(255,255,255)

##### 2.RGBA值(透明效果的RGB值)

**语法：(红，绿，蓝，不透明度)    1表示完全不透明  0表示完全透明**

##### 3.十六进制的RGB值

**语法：#红色绿色蓝色   浓度通过00-ff表示**

如果颜色俩位重复可以进行缩写（三个值都要俩俩重复）  例如#aabbcc可简写成#abc

#### 4.HSL和HSLA值(透明)，在工业设计中用的最多

H 色相(0-360)

S  饱和度,颜色的浓度(0%-100%)

L 亮度，颜色的亮度(0%-100%)  0%表示0亮度就是黑色

A  透明度(0-1)



## 2.layout布局

### 1.文档流(normal flow)

```html
<!--
	文档流
		1.网页是一个多层的结构，一层摞着一层的结构
		2.通过css可以为每一层设置不同的样式
		3.用户只能看到最顶上的一层
		4.在这些所有层中，❤最低下的一层称为文档流，文档流是网页的基础(位置要记住最下面一层)
		5.我们所创建的元素默认都是在文档流中进行排列，就像人默认出生在地球
		
	元素主要有俩个状态
		1.在文档流中
		2.脱离文档流(不在文档流中)

	元素在文档流中的特点:
		块元素
			1.块元素会在页面中独占一行，无论宽度如何(自上而下的排列),table是唯一的例外，他不会把宽度占满
			2.宽度是父元素的全部(会把父元素撑满)
			3.默认高度是被内容撑开(子元素占的多大，一行就是一行的高度，多行就是多行的高度)

		行内元素
			1.行内元素不会独占页面的一行，只占自身的大小
			2.行内元素在页面中自左向右水平排列，如果一行中不够放下所有元素，则会第二行继续自左向右排列(就像书写的习惯)
			3.默认宽度和高度都是被自身的内容撑开

	元素脱离文档流的特点：
		块元素：
			1.块元素不再独占页面的一行(未脱离时独占一行)
			2.宽度和高度变为默认被内容撑开 除非特殊设置
		行内元素：
			行内元素脱离文档流以后会变成块元素，特点和块元素一样
			❤也就是说脱离文档流以后，不需要在区分块和行内元素了

			元素设置浮动后，将会从文档流中脱离，从文档流中脱离后，元素的特点也会发生改变
			相对定位和粘滞定位(粘滞定位就是一种特殊的相对定位)不会脱离文档流,绝对定位和固定定位会脱离文档流。
-->
```



### 2.盒模型 box-model

**开发时最忌讳的事情造成多个浏览器之间效果不一样的情况**

![src=http___img-blog.csdnimg.cn_20201021101010574.png&refer=http___img-blog.csdnimg](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/src=http___img-blog.csdnimg.cn_20201021101010574.png&refer=http___img-blog.csdnimg.webp)

```html
<!--
	-css将页面中所有的元素都设置为了一个矩形的盒子,页面的布局就变成了把不同的盒子放到不同的位置。
	-每一个盒子由以下几个部分组成:
		-内容区(content)
			元素中所有的子元素和文本内容都在内容区中排列
				❤❤内容区的大小由width和height来设置

		-内边距(padding)
			-内容区和边框之间的距离是内边距，默认是和内容贴紧
			-内边距的设置会影响盒子的大小，背景颜色会延申到内边距上
				！！一个盒子❤可见框的大小，由内容区 内边距 和 边框共同决定
				计算盒子大小时，需要将这三个区域加到一起计算	
				-padding-top 上内边距
				-padding-right	右内边距
				-padding-bottom 下内边距
				-padding-left 左内边距
				简写方式 padding 同时指定四个方向的内边距  上右下左  和border-width一样的值

		-外边距(margin)
			-外边框不会影响盒子可见框的大小
			-但是外边距会影响盒子的位置 有关布局
				-margin-top
					-上外边距，设置一个正值，元素会向下移动
				-margin-right
					-右外边距 默认情况下设置它不会产生任何效果
				-margin-bottom
					-❤下外边距，设置一个正值，其下边的元素会向下移动
				-margin-left
					-左外边距，设置一个正值，元素会向右移动

				设置负数值时元素会像相反方向移动
						-元素在页面中是按照自左向右的顺序排列的(国外可能不是):
						-默认情况之下我们设置上和左元素会移动自身，而设置下和右则会移动其它元素。	
			margin也可以简写 设置四个方向  margin的设置会影响到盒子的实际占用空间大小

		-边框(border)
			1.边框属于盒子边缘，里边属于盒子内部，外边都不属于
				❤❤边框的大小会影响整个盒子的大小
				要设置边框，至少要设置下面三个属性(三个必须同时写)
				边框的宽度:border-width 设置以后上下左右都会增加
					-默认值一般是3个像素，不写也可以显示，但是一定要自己设置，防止浏览器不一样的解析
					-用来指定4个方向的边框的宽度 
					-值的情况
						4个值:上 右 下 左
						3个值:上 左右 下
						2个值:上下 左右
						1个值:上下左右
				除了border-width，还有一组border-xxx-width (top bottom left right) 用来单独设置一个方向的宽度

				2.边框的颜色:border-color
					-border-color不写的时候，默认使用color(前景色)的颜色
					-同样可以四个边框的颜色，和border-width规则一样
						border-color(blue,red,black,white)

				3.边框的样式:border-style
					-solid 表示实线
					-dotted 点状虚线
					-dashed 虚线
					-double 双线
					-默认值是none 表示没有边框
					-也是可以给四个方向同时设置的
						border-style(solid dotted dashed double)

				❤❤最重要的！！！
					border简写属性(开发最常用的)   例如border(solid 10px blue)
				4.border也由border-xxx 用来单独设置一边
					-例如右边不想设置，我们可以这样操作
						-border：10px red solid   border-right:none;

-->
```

例子：内边距

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            background-color: blue;
            width: 200px;
            height: 200px;
            border: 10px solid red;
            /*设置内边距*/
            padding: 100px;
        }

        .box2 {
            /*子元素内容撑满*/
            width: 100%;
            height: 100%;
            background-color: yellow;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2">
            我是div2我是div2我是div2我是div2我是div2
        </div>
    </div>
</body>

</html>
<!--
	此时这个盒子的整体大小为 边框+内边距+内容区=20+200+200=420px   420px*420px的一个盒子
-->
```

例子:外边距

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 100px;
            height: 100px;
            background-color: blue;
            margin-bottom: 100px;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: red;
        }
    </style>
</head>

<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>

</html>
```



### 3.！！水平布局(这里也解释了margin-right为什么没用)

```html
<!--
	元素在水平方向的布局:
		元素在其父元素中水平方向的位置由以下几个属性共同决定
		margin-left border-left padding-left width margin-right border-right padding-right
			-❤一个元素在其父元素中必须满足以下等式
				即 margin-left+border-left+padding-left+width+margin-right+border-right+padding-right=其父元素内容区的宽度(一定要满足)
			这个等式必须要满足，如果相加结果使得等式不成立，成为过度约束❤❤，则等式会自动调整
				-如果这七个值中没有auto的情况，则浏览器会自动调整margin-right以实现等式成立(所以我们设置右外边距不会生效)
					-七个值中有三个值可以设置为auto(自动调整)，如果有auto，则会自动调整auto让等式成立
						-width margin-left margin-right  可以看下面的例子
		需要记的是:width的默认值其实就是auto,不设置的时候就是auto

	特殊情况:
		1.如果将一个宽度和外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0
				 div {
           			width: auto;
				   /*这里margin-left效果也是一样的*/
           			margin-right: auto;  /* margin-right:auto;会自动调为0 */
				  }
		！！此时width宽度调整为最大，margin-left和margin-right均为0

		
		2.如果三个值都设置为auto，则外边距为0，宽度最大
				 div {
           			width: auto;
         		    /* margin:auto;会自动调为0 */
           			margin: auto;
				  }
		综上所诉:宽度和外边距一起设置auto的时候都是默认宽度最大的。


		3.如果将俩个外边距设置为auto，宽度固定值，则会将外边距设置为相同的值
			-所以利用这个特点来让一个元素在其父元素中水平居中
				代码:
						width:xxxpx; margin:0 auto;//上下边距0 左右auto


		！！4.如果遇到子元素的内容超出了父元素的宽度，则浏览器会把margin-right设置为负数来满足等式，要记得不管任何情况等式都满足
-->
```

例子：没有auto

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 800px;
            height: 200px;
            border: 10px red solid;
        }

        .box2 {
            width: 200px;
            height: 200px;
            background-color: blue;
        }
     /*
    	等式为
    	margin-left+border-left+padding-left+width+margin-right+border-right+padding-right=父元素内容宽度
    	0+0+0+200+0+0+0=800
    	这时候浏览器自动调整margin-right=600px
    */
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
</body>

</html>
```



例子：有auto

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 800px;
            height: 200px;
            border: 10px red solid;
        }

        .box2 {
            width: auto;
            height: 200px;
            background-color: blue;
        }
     /*
    	此时设置了auto等式为
    	margin-left+border-left+padding-left+width+margin-right+border-right+padding-right=父元素内容宽度
    	0+0+0+auto+0+0+0=800
    	设置了width:autp   也就是意味着width变成了800px
    */
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>

</body>

</html>
```



### 4.垂直布局

```html
<!--
	1.默认情况下父元素的高度被内容撑开
	2.子元素是在父元素内容区中排列的
		-如果子元素的大小超过了父元素，则它会从父元素中溢出
		-使用overflow属性来设置父元素如何处理溢出的子元素内容
			-可选值
				-visible 默认值  溢出内容在父元素外部位置显示
				-hidden 溢出内容将会被裁剪
				-scroll 生成俩个滚动条
				-auto 根据需要生成滚动条
			-overflow-x和overflow-y可以分别为水平和垂直方向设置

	扩展知识 1.visibility:hidden;隐藏自己但是占据空间  2.dispaly:none;隐藏自己且不占据空间
	clip 裁剪
		
-->
```



### 5.垂直外边距的重叠

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1,
        .box2 {
            width: 200px;
            height: 200px;
        }

        /* 
        外边距的重叠只产生在普通文档流的上下外边距之间， 只有 块元素 会发生外边距重叠，行内元素 和 行内块元素 都不会发生外边距重叠问题
        原因：根据规范，一个盒子如果没有添加 BFC，那么它的上边距应该和其文档流中的第一个子元素的上边距重叠。
        
            垂直外边距的重叠
              -相邻的垂直方向外边距会发生重叠现象
              -兄弟元素
                -都为正值:兄弟元素之间的相邻垂直外边距会取俩者之间的较大值(保证双方都满足，类似俩个人吵架分开的距离)
                -一正一负：取两者的和
                -都为负值:取两者中绝对值较大的
                兄弟元素之间外边距的重叠，对于开发中是有利的，我们不用处理

              -父子元素(第一个和最后一个会发生重叠)
                -父子元素垂直相邻外边距，子元素的会传递给父元素(上外边距)
                -父子外边距的折叠会影响页面的布局，必须进行处理  下面给俩个例子处理方式    
        */

        .box1 {
            background-color: aqua;
            margin-bottom: 100px;
        }

        .box2 {
            background-color: blueviolet;
            margin-top: 100px;
        }

        /* 例子1   避免使用外边距*/
        .box3 {
            width: 200px;
            /* 这里要记得调整父元素的高度，因为设置了padding-top会把父元素撑大 */
            height: 100px;
            background-color: aqua;
            padding-top: 100px;
        }

        .box4 {
            width: 100px;
            height: 100px;
            background-color: red;
            /* margin-top: 100px;  避免使用外边距,不使用外边距就不会造成外边距重叠*/
        }

        
        /* 例子2  */
        .box5 {
            width: 200px;
            /* 这里要记得调整父元素的高度，因为设置了border会把父元素撑大 */
            height: 199px;
            background-color: aqua;
            //利用border隔开父子元素的外边距,padding也可
            border: 1px aqua solid;
        }

        .box6 {
            width: 100px;
            /* 子元素也要调小1px */
            height: 99px;
            background-color: red;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <!-- 兄弟元素 -->
    <div class="box1"></div>
    <div class="box2"></div>


    <!-- 假设要让子元素在父元素中下移100px -->
    <!-- 解决方法一:别用外边距-->
    <div class="box3">
        <div class="box4"></div>
    </div>
    <!-- 解决方法二:让它们不相邻即可 -->
    <div class="box5">
        <div class="box6"></div>
    </div>

</body>

</html>
```



### 6.行内盒子模型

```html
<!--
	1.行内元素的盒子模型
		-行内元素不支持设置宽度和高度
		-可以设置padding，但是垂直方向的padding不会影响页面的布局(最多是占据了相邻元素的空间，不会改变布局)
		-可以设置border，但是垂直方向的border不会影响页面的布局(最多是占据了相邻元素的空间，不会改变布局)
		-可以设置margin，但是垂直方向的margin不会影响页面的布局(最多是占据了相邻元素的空间，不会改变布局)
			-总结:可以为其设置这些样式，但是垂直方向的设置不会影响布局
	
	2.display 用来设置元素显示的类型
		可选值：
			-inline 将元素设置为行内元素
			-block 将元素设置为块元素
			-inline-block 将元素设置为行内块元素
				-行内块，既可以设置宽度和高度又不会独占一行(类似替换元素，水平相邻的时候类似写字，俩俩之间会留有空隙，
				  解决方案是将代码不打空格连起来写，较为麻烦，开发一般不选用)
			-table 将元素设置为一个表格
			-❤none 元素不在页面中显示(适合设置输入移入前的多级导航条)  完全隐藏也不用占据页面位置
			-table-cell 将元素设置为一个tr
	
	3.visibility 用来设置元素的显示状态
		可选值:
			visible 默认值，在页面中正常显示
			❤hidden 元素在页面中隐藏 不显示，但是移入占据页面的位置


	关于3种隐藏的方式
          display:none: 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击； visibility: hidden:不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击； opacity: 0: 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击。
--->
```

#### 1.display和visibility 和opacity的区别

```css
display: none
DOM 结构：浏览器不会渲染 display 属性为 none 的元素，会让元素完全从渲染树中消失，渲染的时候不占据任何空间；
事件监听：无法进行 DOM 事件监听，不能点击；
性能：修改元素会造成文档回流（reflow 与 repaint）,读屏器不会读取display: none元素内容，性能消耗较大；
继承：是非继承属性，由于元素从渲染树消失，造成子孙节点消失，即使修改子孙节点属性子孙节点也无法显示，毕竟子类也不会被渲染；
场景：显示出原来这里不存在的结构；
transition：transition 不支持 display。

2.visibility: hidden
DOM 结构：不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见；
事件监听：无法进行 DOM 事件监听，不能点击；
性能：修改元素只会造成本元素的重绘（repaint），是重回操作，比回流操作性能高一些，性能消耗较少；读屏器读取visibility: hidden元素内容；
继承：是继承属性，子孙节点消失是由于继承了visibility: hidden，子元素可以通过设置 visibility: visible 来取消隐藏；
场景：显示不会导致页面结构发生变动，不会撑开；
transition：transition 支持 visibility，visibility 会立即显示，隐藏时会延时。

3.opacity: 0
DOM 结构：透明度为 100%，不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见；
事件监听：可以进行 DOM 事件监听，可以点击；
性能：提升为合成层，是重建图层，不和动画属性一起则不会产生repaint（不脱离文档流，不会触发重绘），性能消耗较少；
继承：会被子元素继承，且子元素并不能通过 opacity: 1 来取消隐藏；
场景：可以跟transition搭配；
transition：transition 支持 opacity，opacity 可以延时显示和隐藏。

打个比方：
display: none： 从这个世界消失了, 不存在了；
opacity: 0： 视觉上隐身了, 看不见, 可以触摸得到；
visibility: hidden： 视觉和物理上都隐身了, 看不见也摸不到, 但是存在的；
```



**附加题：CSS 隐藏页面上的一个元素有哪几种方法？**

1. display:none，visibility:hiden，opacity:0 这三种；
2. 设置 fixed 并设置足够大负距离的 left top 使其“隐藏”(固定定位定到看不见的地方去)；
3. 用层叠关系 z-index 把元素叠在最底下使其“隐藏”；
4. 用 text-indent:-9999px 使其文字隐藏。



### 7.浏览器的默认样式

```html
<!--
	浏览器会自带一些样式，来确保网页没有设置样式时候可以自动设置
	一般通过引入一些css文件来去除这些样式
	这种情况在PCd端出现的最多
-->
```



### 8.盒子的大小

默认情况下，盒子可见框的大小由内容区，内边距和边框共同决定。

box-sizing用来设置盒子尺寸的计算方式(设置width和height的作用)

​		可选值：

​						content-box 默认值 宽度和高度用来设置内容区的大小

​						border-box  宽度和高度用来设置整个盒子可见框的大小（不包括margin）

​								width和height 指定的是内容区 内边距 和 边框的总大小



### 9.轮廓阴影和圆角

```css
/*
	1.outline 用来设置轮廓，用法和border一模一样
		轮廓和边框不一样的是轮廓不会影响到可见框的大小  一般设置鼠标移入时显示盒子的整体轮廓

	2.box-shadow 用来设置阴影 (box-shadow:1px 1px 1px red)
		水平偏移量(可以设置负值，设置阴影的水平位置 正值向右边移动)
		垂直偏移量(可以设置负值，设置阴影的垂直位置 正值向下边移动)
		阴影的模糊半径(值越大模糊半径越大)
		阴影的颜色(一般用rgba来设置阴影)

	3.border-radius 用来设置圆角，圆角设置圆的半径大小
		有四个值 顺序是顺时针左上，右上，右下，左下
		三个值 顺序是 左上，右上/左下，右下
		俩个值 顺序是 左上/右下 右上/左下
		一个值 设置四个方向的
		⭐⭐⭐
		圆角可以设置对一个方向的圆角设置时可以设置俩个值来实现椭圆的效果
			俩个值分别是设置水平和垂直方向的圆角半径
			一个值的时候就是画圆
		⭐⭐⭐
		将元素设置为圆形，固定写法
			border-radius:50%;
*/
```



## 3.一些练习总结

```html
<!--
	1.要记住虽然marginn-left和padding-left能实现同一个效果，但是他们之间是有区别的
		-margin设置以后那一部分就不属于盒子了，而padding设置以后还是属于盒子里

	2.要让一个文字在父元素中垂直居中，固定设置 ❤❤
		-让父元素的line-height和父元素的height相等

	3.如果子元素设置了width宽度，意味着这时候宽度不是auto了，这时候设置padding以后，盒子就会溢出父元素

	4.设置a标签去除下划线:text-decoration:none
	5.子元素设置的样式和父元素样式冲突以后，会去除继承性，使用子元素设置的样式
	6.盒子的嵌套法:div套div nav套div ul套li
	7.转化为行内块 inline-block 为了边框和文字宽度一致
-->
```



## 4.浮动❥

### 1.浮动的简介

```css
/*
	通过float来设置浮动 通过浮动可以使得一个元素向其父元素的左侧或者右侧移动(只在父元素内)
		none为默认值 不浮动
		left 元素向左浮动
		right 元素向右浮动
	⭐⭐⭐注意:设置完浮动以后，水平布局的等式便不需要强制成立
		⭐⭐元素设置浮动以后，会完全从文档流中脱离，不再占用文档流的位置
		  	⭐所以元素下边的还在文档流中的元素会自动向上移动

	浮动的特点❤:
		1.浮动元素会完全脱离文档流，不在占据文档流中的位置
		2.设置浮动以后元素会向父元素的左侧或者右侧移动
		3.浮动元素默认情况下不会从父元素中溢出
		4.浮动元素向左和右移动时，不会超过它前边的浮动元素(水平考虑)
		5.如果浮动元素的上边是一个没有浮动的块元素，则浮动元素无法上移
		6.浮动元素不会超过它上边的浮动兄弟元素，最多就是和它一样高度(垂直考虑)
		7.可以通过调整html的结构配合浮动来实现不同的布局需求
	
	元素设置浮动后，将会从文档流中脱离，从文档流中脱离后，元素的特点也会发生改变
	脱离文档流的特点：
		块元素：
			1.块元素不在独占页面的一行(未脱离时独占一行)
			2.宽度和高度变为默认被内容撑开 除非特殊设置
		行内元素：
			行内元素脱离文档流以后会变成块元素，特点和块元素一样
			❤也就是说脱离文档流以后，不需要在区分块和行内元素了

	浮动原本的作用，浮动元素不会盖住文字，文字会自动环绕在元素的周围，利用这一点实现文字环绕效果
*/
```



### 2.简单布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        header,
        main,
        footer {
            width: 1000px;
            margin: 0 auto;
        }

        header {
            background-color: blue;
            height: 100px;
        }

        main {
            background-color: #bfa;
            height: 400px;
        }

        footer {
            background-color: palevioletred;
            height: 100px;
        }

        /* 设置main里面的nav */
        nav {
            float: left;
            width: 200px;
            height: 100%;
            background-color: antiquewhite;
        }

        article {
            float: left;
            width: 580px;
            height: 100%;
            margin: 0 10px;
            background-color: aqua;
        }

        aside {
            float: left;
            width: 200px;
            height: 100%;
            background-color: rgb(13, 230, 114);
        }

        .box1 {
            float: left;
            width: 180px;
            height: 100%;
            background-color: blueviolet;
        }

        .box2 {
            float: right;
            width: 180px;
            height: 50%;
            background-color: cornflowerblue;
        }
    </style>
</head>

<body>
    <!-- 头部 -->

    <header></header>

    <main>
        <!-- 左侧边栏 -->
        <nav></nav>
        <!-- 设置中间内容 -->
        <article>
            <div class="box1"></div>
            <div class="box2"></div>
        </article>
        <!-- 设置右边的内容 -->
        <aside></aside>
    </main>

    <!-- 尾部 -->
    <footer></footer>
</body>

</html>
```



### 3.高度坍塌和BFC

```HTML
<!--
	高度塌陷的问题:
		在浮动布局中，我们一般都要设置父元素的高度默认是被子元素撑开的
			当子元素浮动以后，其会完全脱离文档流，子元素会从文档流中脱离
			这就使得他无法撑起父元素的高度，导致父元素的高度丢失了，这时父元素下面的元素会自动上移，影响页面布局

	利用BFC来解决这个问题
	BFC是块级格式化环境(可以理解为是一个独立于整个页面的布局环境)
		BFC是CSS中一个隐含的属性，不能直接开启,开启BFC后该元素会变成一个独立的布局环境

	开启BFC后的特点:
		1.开启BFC的元素不会被浮动元素所覆盖
		2.开启BFC的元素子元素和父元素外边距不会重叠(默认情况下父元素是会跟着子元素的外边距移动的)
		3.开启BFC的元素可以包含住浮动的元素(元素不会脱离这块区域，只是脱离了文档流)
	
	开启BFC的方法(开启BFC的方法都会有一些副作用):
		1.设置元素的浮动(不推荐在布局时使用浮动开启BFC)
		2.将元素设置为行内块元素(不推荐在布局时使用设置行内块元素开启BFC)
		3.将元素的overflow设置为一个非visible的值
			-一般情况下我们直接设置为hidden的副作用最小
-->
```



### 4.BFC解决演示

```html
三个例子
<!-- 1.开启BFC的元素不会被浮动元素覆盖 -->
    <style>
        .box1 {
            width: 100px;
            height: 100px;
            background-color: #bfa;
            float: left;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: red;
            /*开启以后浮动以后box1脱离文档流,所以box2往前移动,开启BFC后 box2不会被浮动的box1覆盖*/
            overflow: hidden;
        }
	</style>
    <div class="box1"></div>
    <div class="box2"></div>

<!-- 2.开启BFC的元素子元素和父元素外边距不会重叠 -->
 	<style>
        .box3 {
            width: 200px;
            height: 200px;
            background-color: #bfa;
            /* 开启BFC后 box3不会和子元素box4外边距重叠 */
            overflow: hidden;
        }

        .box4 {
            margin: 100px 0 0 0;
            width: 100px;
            height: 100px;
            background-color: red;
        }
    </style>
    <div class="box3">
        <div class="box4"></div>
    </div>

<!--3.开启BFC的元素可以包含住浮动的元素 解决高度塌陷-->
    <style>
        .box1 {
            border: 10px red solid;
            overflow: hidden;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: aqua;
            float: left;
        }
    </style>
    <div class="box1">
        <div class="box2"></div>
    </div>
```



### 5.解决高度塌陷的较好方法clear

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            font-size: 50px;
        }

        .box1 {
            width: 200px;
            height: 200px;
            background-color: #bfa;
            float: left;
        }

        .box2 {
            width: 400px;
            height: 400px;
            background-color: #baf;
            float: right;
        }

        .box3 {
            width: 200px;
            height: 200px;
            background-color: burlywood;
            /* 通过clear元素可以清除浮动元素对当前元素的影响 是当前元素
                    clear可选值：
                        left 清除左侧浮动元素对当前元素的影响
                        right 清除右侧浮动元素对当前元素的影响
                        both 清除俩侧浮动元素重对当前元素影响最大的
                clear的原理是为设置了clear属性的元素添加一个上外边距，以此来消除浮动元素的影响
                    需要注意的是 这个上外边距在浏览器开发者工具中是见不到的
            */
            clear: right;
        }
    </style>
</head>

<body>
    <div class="box1">1</div>
    <div class="box2">2</div>
    <div class="box3">3</div>
</body>

</html>
```



### 6.单独解决高度塌陷的终极方案  clear加伪元素选择器

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            border: 10px red solid;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: aqua;
            /* .box2设置了浮动，父元素高度会发生塌陷 */
            float: left;
        }

        /*
            2.解决高度塌陷的思路是在box1和box之间2(after的位置)加上一个空内容,这样空内容就可以撑起父元素的高度,box2浮动以后父元素高度就不会塌陷
        */
        .box1::after {
            /* 添加一个空内容 */
            content: "";
            /*
            	因为伪元素是行内元素，所以设置了clear也不会产生影响将其转化为table以后设置才会生效
            	clear对块元素生效
            */
            display: table;
            /* 通过clear清除影响box2浮动对伪元素的影响 */
            clear: both;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
</body>

</html>
```

### 7.解决外边距重叠的终极方案

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /*  
            解决外边距重叠的思路是在box1和box之间2(before的位置)加上一个空内容隔开二者,这样对box2设置外边距就不会影响父元素box1
        */
        .box1 {
            width: 200px;
            height: 200px;
            background-color: aqua;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: blue;
            margin-top: 100px;
        }

        .box1::before {
            content: '';
            /* 伪元素是行内元素,所以要转化为table才可以独占一行起到隔离的效果 */
            display: table;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
</body>

</html>
```



### 8.clearfix方法：这个样式可以同时解决高度塌陷和外边距重叠的问题(终极版)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            border: 10px red solid;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: #bfa;
            margin-top: 200px;
            float: left;
        }

        /* 
            1.解决外边距重叠的思路是在box1和box2之间(before的位置)加上一个空内容隔开二者,这样对box2设置外边距就不会影响父元素box1
            2.解决高度塌陷的思路是在box1和box2之间(after的位置)加上一个空内容,这样空内容就可以撑起父元素的高度,box2浮动以后父元素高度就不会塌陷
         */
        /* .clearfix类 这个样式可以同时解决高度塌陷和外边距重叠的问题 记住这个样式 */
        .clearfix::before,
        .clearfix::after {
            /* 
                1:12行设置before的效果(解决外边距重叠)
                2:123行设置after的效果(解决高度塌陷)
            */
            content: "";
            /* (类似<table>)此元素会作为块级表格来显示，表格前后带有换行符。效果比display：block好 作用是转化为块元素 */
            display: table;
            /* 通过clear清除浮动的影响 */
            clear: both;
        }
    </style>
</head>

<body>
    <div class="box1 clearfix">
        <div class="box2"></div>
    </div>
</body>

</html>
```



## 5.定位❥

### 1.关于定位

```html
<!--
	通过定位可以将元素摆放到页面的任意位置，使用position属性来设置定位
		可选值:
			static 默认值，元素是静止的没有开启定位
			relative 开启元素相对定位
			absolute 开启元素的绝对定位
			fixed 开启元素的固定定位
			sticky 开启元素的粘滞定位

	!!定位我们要明确这种定位的参照物是什么！！！♥

	偏移量(offset):当元素开启了定位以后，通过偏移量来设置元素的位置，只要position值不为默认就可以设置偏移量
		可选值:
			top:定位元素和定位位置上边的距离
			bottom:定位元素和定位位置下边的距离
			left:定位元素和定位位置左边的距离
			right:定位元素和定位位置右边的距离

		元素垂直方向由top和bottom俩个属性控制，水平方向由left和right俩个属性控制
		(这里要记得想到了设置margin时，设置上左是动自己的，设置下右是动别人的)
		top值越大元素越向下移动
		bottom值越大元素越向上移动 超过了他的容器就会跑到另外一边
		left值越大元素越向右移动
		right值越大元素越向左移动
-->
```



### 2.相对定位 relative

```html
相对定位是参照于元素在文档流中的位置进行定位的
<!--
	特点:
		1.开启相对定位后，不设置偏移量元素不会发生任何变化♥
		2.!!相对定位是参照于元素在文档流中的位置进行定位的
		3.相对定位会提升元素的层级,但是不会使其脱离文档流
		4.相对定位不会改变元素的性质，因为没有脱离文档流,块还是块,行内还是行内
-->
```



### 3.绝对定位 absolute

```html
⭐⭐⭐⭐绝对定位元素是相对于其包含块进行定位的(参照物)
<!--
	特点:
		1.开启绝对定位后，不设置偏移量元素位置不会发生任何变化♥
		2.开启绝对定位后，元素会从文档流中脱离
		3.绝对定位会改变元素的性质，因为脱离了文档流，行内变成块，块的宽高被内容撑开
		4.绝对定位会使元素提升一个层级
		5.绝对定位元素是相对于其包含块进行定位的(参照物)
	
	包含块的概念:
		1.正常情况下:
			--包含块就是离当前元素最近的祖先块元素
		2.绝对定位的包含块:
			--包含块就是离它最近的开启了定位的祖先元素
				-如果所有的祖先元素都没有开启定位则根元素(html)就是它的包含块(一般我们给祖先定位开启相对定位来设置包含块，这样影响最小)

		-html(根元素、初始包含块)
-->
⭐ 绝对定位元素的布局❥:
<!--
	当我们开启了绝对定位后
		水平方向布局的等式就需要添加left和right俩个值，规则和之前的一样
left+margin-left+border-left+padding-left+width+margin-right+border-right+padding-right+right=其父元素内容区的宽度(一定要满足)
		  当发生了过度约束之后:
		     ❤如果9个值中没有auto，则自动调整right值以此来使等式满足
			 如果有auto，则自动调整auto值来使等式成立
			  可设置auto的值:❤❤margin-left,margin-right,left,right  (在没开启绝对定位时,可以设置auto的值为margin-left,margin-right和widih)
		又因为left和right的值默认是auto，所以如果不设置left和right,等式不满足时，会自动调整这俩个值
		
		垂直方向的布局也必须要满足等式
		top + margin-top/bottom + padding-top/bottom + border-top/bottom + height + bottom = 包含块的高度
			如果有auto，则自动调整auto值来使等式成立
			可设置auto的值:❤❤margin-top,margin-bottom,top,bottom			
-->
```



### 4.固定定位 fixed

```html
⭐⭐⭐⭐固定定位永远参照于浏览器的视口的左上角顶点进行定位！！
<!--
	特点:
		1.固定定位也是一种绝对定位，大部分特点和绝对定位一样
		2.开启绝对定位后，不设置偏移量元素位置不会发生任何变化♥
		3.开启绝对定位后，元素会从文档流中脱离
		4.绝对定位会改变元素的性质，因为脱离了文档流，行内变成块，块的宽高被内容撑开
		5.绝对定位会使元素提升一个层级
		6.！！唯一不同的固定定位永远参照于浏览器的视口的左上角顶点进行定位！！(视口就是可视区域)
			-固定定位的元素不会随网页的滚动条滚动
-->
```



### 5.粘滞定位 sticky  兼容性不够好

```html
<!--
	特点:
		1.粘滞定位和相对定位的特点基本一致
			-不同的是粘滞定位可以在元素到达某个位置时将其固定
		2.粘滞定位参考于包含块进行定位(绝对定位也是参考于包含块,不同的是开启绝对定位以后的性质)
-->
```



**总结:相对定位和粘滞定位不会使元素脱离文档流，只提升了层级。绝对定位和固定定位会使得文档脱离文档流。**



### 6.元素的层级

```html
<!--
        /* 	元素层级很多情况下用在导航条移入显示的效果中
            对于开启了定位的元素，可以通过z-index来指定元素的层级
                -z-index需要一个整数作为参数，值越大元素的层级越高
                    1.元素的层级越高越优先显示
                    2.如果元素的层级一样，则优先显示靠下面的元素(结构靠下)
                    3.祖先的元素的层级在高也不会盖住子元素，只会盖住它同级(只会盖住它的兄弟)
        */
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>123</title>
    <style>

        body {
            font-size: 60px;
            background-color: #bfa;
        }

        .box1 {
            width: 200px;
            height: 200px;
            background-color: blueviolet;
            position: relative;
            z-index: -1;
        }

        .box2 {
            width: 200px;
            height: 200px;
            background-color: blue;
            position: absolute;
            top: 50px;
            left: 50px;
            z-index: 1;
        }

        .box3 {
            width: 200px;
            height: 200px;
            background-color: red;
            position: absolute;
            top: 100px;
            left: 100px;
            z-index: 3;
        }

        .box4 {
            width: 100px;
            height: 100px;
            background-color: pink;
            position: absolute;
            z-index: 2;
        }
    </style>
</head>

<body>
    <div class="box1">1</div>
    <div class="box2">2</div>
    <div class="box3">3
        <div class="box4"></div>
    </div>
</body>

</html>
```



### 7.例子：设置水平和垂直双居中

```html
因为水平和垂直都可以通过margin自动调整，所以以下代码可以实现水平垂直双居中
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 500px;
            height: 500px;
            background-color: #bfa;
            /* 为box2的父元素开启相对定位 */
            position: relative;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: pink;
            /* 开启绝对定位 */
            position: absolute;
            /* margin设置auto 使得水平和垂直方向自动调整等式成立 */
            margin: auto;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
</body>

</html>
```

### 8.浮动和定位的用法

```html
<!--
	宏观上我们用浮动布局、微小的细节我们通过定位来移动到想要的位置
-->
```



## 6.CSS样式补充

### 1.字体

```css
<!--
	1.color 用来设置字体颜色

	2.font-size 字体的大小

	3.font-family 字体的格式 字体族
		可选值:
			-serif 衬线字体 -san-serif非衬线字体 monospace等宽字体
			指定字体的大类别，浏览器会自动使用该类别下的字体
		可设置多个字体，多个字体间逗号隔开，优先显示第一个字体，如果浏览器不支持就使用下一个，最后一个就是兜底

	4.font-face可以将服务器中的字体之间提供给用户去使用(字脸)
		-但是这种方式会占服务器网速，加载更慢;也会出现版权的问题;字体格式的问题也会出问题.
		-微软雅黑也是商用要钱的
		@font-face{
  			font-family:'字体名称';
   			src:url(字体路径) format("字体格式");
		}
-->
```



### 2.图标字体

```css
我们在使用图标时,我们可以将图标直接设置为字体，然后通过font-face来对字体进行引入
fontawesome的使用(免费可商用的)
	1.将css和webfonts移动到项目中
	2.将all.css引入网页
	3.使用的三种方式
	通过类名来使用图标字体,一般只有fas和fab这俩种格式,记住下面这俩个
		(1)通过类名来引用的 fas指定的是哪一个类，也是通过font-face来写的，fas后面那个就是类里的那一个图标，fab同理
		-class="fas fa-bell"
		-class="fab fa-accessible-icon"
		但是这种引入方式很麻烦，要用一次就要指定一次类名

		(2)通过伪元素来设置图标字体
		1.找到要设置图标的元素通过before或after选择
		2.在content中设置字体的编码,文档中查询(记得加\)
		3.设置字体的样式
			fab
				-font-family
			fas
				-font-family
				-font-weight
		
		(3)通过实体来使用图标字体(实体就是在网页中书写一些特殊符号)
			&#x图标的编码
```

#### 实例：

(1)：

![uTools_1667228534955](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667228534955.png)

(2)：

![uTools_1667228390152](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667228390152.png)

(3):

![uTools_1667228474523](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667228474523.png)

#### iconfont：阿里的图标库  但是版权问题不清晰

![uTools_1667229051055](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667229051055.png)



### 3.行高 line-height    也是可以被继承的

**行高指的是行之间基线的距离**

![uTools_1668851000692](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668851000692.png)

**行间距**

![uTools_1668851117187](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668851117187.png)

![uTools_1668852177838](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668852177838.png)

**所以height=line-height的时候相当于line-height就是整个盒子的高度**

**原理：我们也可以把行高记为，行高就是一行的高度，这一行的高度中包含了上下两个间距和文本内容本身。而文本内容在每一行中都是居中的**

**关于line-height的继承性**

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <style>
        body {
            font-size: 20px;
            /* 父元素设置了line-height */
            line-height: 4;
            /* 
            	百分比也是一样的
            	line-height: 400%;
            */
        }

        /* 此时div的行高为父元素的字体大小*4=80px */

        p {
            /* 此时p元素的行高为自身的字体大小*4=40px */
            font-size: 10px;
        }
    </style>
</head>

<body>
    <div>1232323</div>
    <p>asdasdas</p>
    <p>asdasdas</p>

</body>

</html>
```

**行高和高度的区别**

![uTools_1668852529966](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668852529966.png)

```html
<!--
	行高指的是文字占有的实际高度,可以通过line-height来设置行高(px em 如果是一个整数的话行高会是字体的指定的倍数)
		行高会在字体框的上下平均分配
		行高有俩个用处，一个是设置单行文字在元素种垂直居中(多行时元素会自动变大撑开然后垂直居中)
			height=100px;line-height=100px;
			原理是:
				行高，也就line-height的组成部分有三部分组成，文字大小，上间隙，下间隙
	♥我们也可以把行高记为，行高就是一行的高度，这一行的高度中包含了上下两个间距和文本内容本身。而文本内容在每一行中都是居中的
				
		二是设置文字的行间距 行间距=行高-字体大小
			font-size:50px;line-height:100px; 此时行间距为50px 

	字体框就是字体存在的格子，设置font-size实际上就是在设置字体框的高度
-->

```



### 4.字体简写属性(同时设置字体所有属性)

```css
font 可以设置字体的相关的所有属性
	-font:字体风格 字体加粗 字体大小/行高 字体族
		字体大小和字体族必须写，且顺序不变
		字体风格字体加粗行高可以省略不写，不写的时候系统会自动使用默认值normal

div{
    font:50px/2 '微软雅黑';//设置了50px的字体，2倍的行高，字体族为微软雅黑
}
```



### 5.字体的水平和垂直对齐

![uTools_1667291728655](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667291728655.png)



### 6.图片对齐方式

图片是替换元素，默认情况下就是和文字的对齐方式一样，就是基线对齐，涉及到图片对齐时给图片设置一个vertical-align非默认值即可

基线对齐有时候图片和文字中间会有一点点留白的效果，为了解决这个问题，我们只需要给图片设置

vertical-align：bottom/top;



### 7.字体的其他样式

![uTools_1667292011510](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667292011510.png)

**例子:网页未显示部分省略号显示**

```css
    <style>
        .box1 {
            /* 解决网页留白处省略号显示 */
            /* 以下四个属性都必须写上才能实现效果 */

            /* 必须给盒子指定一个宽度 */
            width: 100px;
            /* 
                网页留白处处理
                white-space:
                    -normal 正常显示
                    -nowrap 不换行
                    -pre 保留空白
            */
            white-space: nowrap;
            /* 父元素溢出裁剪 */
            overflow: hidden;
            /* 文本溢出时以省略号显示 */
            text-overflow: ellipsis;
        }
    </style>
```



### 8.text-indent 首行缩进

**这个属性常用来隐藏首行文字,例如logo的div中一般需要放置文字来让搜索引擎更快找到自己，而我们又不希望他显示在网页中**

```css
<div class="header w clearfix">
        	<h1 class="logo" title="小米商城">
                小米官网
              <a class="home" href="/"></a>
            </h1>
    </div>

样式设置:
	    /* 隐藏logo中的文字，设置一个负值,网页中最常用的隐藏文字的做法 */
    	text-indent: -9999px;
```



### 9.css项目补充

**1.给标签取类名的时候要注意噢，尽量不要以ad开头，会被广告拦截器拦截。**

2.用link引入网站收藏和展示的logo

![uTools_1668695085999](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668695085999.png)

3.我们写好的代码都是需要压缩的，加快网站的访问速度。在Vscode里可以安装JS & CSS Minifier (Minify)插件，在需要压缩的css和js文件中点击F1，输入mini，点击minify:Doucment，这样就可以进行压缩了，后期webpack会更好用。



## 6.背景

```html
<!--
	1.background-color  背景颜色

	2.background-image:url(路径)  背景图片
		-同时设置了背景图片和颜色，背景颜色会成为图片的背景色
		-背景图片小于元素，则会自动在元素种平铺铺满元素，图片过大，有一部分会无法显示

	3.background-repeat 设置背景的重复方式
		默认值 repeat 沿着x和y轴重复
		repeat-x 沿着x轴
		repeat-y 沿着y轴
		no-repeat 不重复

	4.background-position 设置图片的位置
		法一:
			top,left,right,bottom,center 使用时必须用俩个值，只写一个值另一个值默认为center
		法二:
			通过偏移量设置，偏移量为水平和垂直俩个方向
-->
```

背景2：

![uTools_1667627923285](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667627923285.png)

![uTools_1667628318888](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667628318888.png)

![uTools_1667628328506](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667628328506.png)

![uTools_1667628563501](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667628563501.png)

**例子：通过切图达到导航条渐变颜色的效果**

```html
1.截图获取图片
2.在ps种截取水平方向1px高度和父元素一样的图片
	-1.矩形框选中，选择功能中的裁剪
	 2.导出保存为web所用格式
3.用background-repeat水平铺满
```

![image-20221105143303406](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221105143303406.png)

**例子：按钮效果练习**

![uTools_1667630841666](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667630841666.png)

![uTools_1678077431058](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678077431058.png)

**为了解决这个问题引出了雪碧图**

![uTools_1667632607073](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667632607073.png)

**雪碧图的使用：适用于小图标的场景**

![uTools_1667632937308](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667632937308.png)

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678077561071.png)

![uTools_1678077721552](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678077721552.png)

灵活使用

**雪碧图制作   腾讯的GoPng在线制作**



## 7.渐变

### 1.线性渐变

```html
<!--
	!!渐变是图片，需要通过background-image来设置
		线性渐变:颜色沿着一条直线发生变化
			-background-image:linear-gradient()
				-background-image:linear-gradient(red,yellow)表示红色开头，黄色结尾，中间过渡。
				-可以在开头指定渐变的方向>>background-image:linear-gradient(to top,red,yellow)
					-可选值有很多:
						-to top 等
						-to top left 等
						-xxdeg 表示度数
						-1turn 表示转一圈
				-渐变可以同时指定多个颜色，多个颜色默认情况下平均分布
				-可以手动指定渐变的分布情况 background-image:linear-gradient(red 50px,yellow) 指定了红色从50px开始渐变
					-红色在50px这个地方到达最高值开始渐变，如果它前面没元素时默认红色先铺满
				-repeating-linear-gradient 可以平铺的线性渐变
-->
```



### 2.径向渐变

![uTools_1667745631462](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667745631462.png)



## 8.浏览器调试

1.ctrl+F5可以强制刷新缓存，有时候要测试第一次进入网站的效果就要用到

2.F12 NETWORK-ALL  可以监视网页加载资源的情况

3.style中显示的是设置了的样式,computed才是成功计算并且生效了的样式。



## 9.PS的使用

### 1.切图

方法一：

​		1.选中矩形框按钮，裁切所要的图片

​		2.点击图像按钮，选择裁剪

​		3.点击文件按钮，选择保存为web所用格式

方法二(针对psd文件)：

​		1.选择鼠标十字型按钮，上方选中自动选择，图层

​		2.点击图片里所要的部分

​		3.按住alt并点击右侧小眼睛图标

​		4.点击图像按钮，选择裁切

​		5.点击文件按钮，选择保存为web所用格式

### 2.文字格式(psd文件)

点击T按钮可用查看文字的字体大小和格式以及字体颜色等

### 3.取色器

最下方的俩个黑白色方块的按钮

# 2.HTML补充

## 1.表格table

### 1.表格简介

![uTools_1667745937267](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667745937267.png)



### 2.长表格

![uTools_1667746191974](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667746191974.png)



### 3.表格的一些样式

table的宽度并不是和普通块元素一样占满屏幕的

![uTools_1667746932778](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667746932778.png)



利用table-cell实现盒子居中效果

![uTools_1667747010221](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1667747010221.png)

**text-align**属性设置元素在水平方向（x轴）的位置

**vertical-align**属性设置元素的垂直方向（Y轴）对齐方式(只对行内元素和行内块元素起作用)

**vertical-align** 它只影响行内元素和行内块元素，不影响块级元素等，所以它最主要的是拿来使文字和图片对齐，不让文字超过图片，影响其美观



### 4.表单元素

```html
<!--
	在网页中，表单用来将本地的数据提交给远程的服务器(Node.js等网页服务器或者脚本)
	使用form来创建一个表单
		form的属性
			action:表单要提交的服务器地址,这个必须指定
-->

例子:
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表单</title>
</head>

<body>
    <form action="电影卡片.html">
        <!-- 
            文本框
                数据要想提交到服务器中，必须为元素指定一个name属性
                value可以设置默认显示值
                autocomplete="off"可以关闭表单自动补全
                readonly 将表单项设置为只读,数据可以提交
                disabled 将表单项设置为禁用,数据不可以提交
                autofocus 设置表单项自动获取焦点,不设置的时候默认第一个文本框
         -->
        <input type="text" name="text1">
        <!-- 
            密码框
                数据要想提交到服务器中，必须为元素指定一个name属性
         -->
        <input type="password" name="password">

        <!-- 
            单选按钮
                单选按钮必须有一个共同的name属性才内单选，name就是分组的作用
                像这种选择框必须要指定一个value属性，value属性决定提交的结果
                checked 可以将单选按钮设置为默认选中
         -->
        <input type="radio" name="danxuan" value="a">
        <input type="radio" name="danxuan" value="b">

        <!-- 
            多选框
                也需要指定name属性，也可以设置checked
         -->
        <input type="checkbox" name="box1" value="1">
        <input type="checkbox" name="box1" value="2">
        <input type="checkbox" name="box1" value="3">

        <!-- 
            下拉列表
                也需要指定name属性和value属性
                selected可以设置默认选中，没设置默认选择第一个
         -->
        <select name="haha">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
        </select>

        <!-- 提交按钮,value值设置按钮显示效果 -->
        <input type="submit" value="注册">
        <!-- 重置按钮 -->
        <input type="reset">
        <!-- 普通按钮,单击无效果配合js用,value值设置按钮显示效果 -->
        <input type="button" value="123">
        
        <br>
        
        <!-- button按钮,成对出现,可以设置复杂的效果 -->
        <button type="submit">提交</button>
        <button type="reset">重置</button>
        <button type="button">按钮</button>
    </form>
</body>

</html>
```



### 5.♥♥♥前端的几种水平垂直居中方式

```html
总结:浮动的居中都要用到定位,弹性盒子就不用
<!--
1.文本垂直居中时使用
	-只对文本有效果，对定宽高的div是没有用的。所以在文本水平垂直居中时使用。注意：只对单行文本有用
方法:line-height
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 100px;
            height: 100px;
            background-color: aqua;
            line-height: 100px;
        }
    </style>
</head>

<body>
    <div class="box1">
        <p>12132</p>
    </div>
</body>

</html>

<!--
2.通过绝对定位的方式  absolute + 负margin
方法:首先知道子元素的宽高，给子元素设置top：50%；left：50%，但绝对定位是基于子元素的左上角，我们所希望的效果是子元素的中心居中显示，借助外边距的负值，负的外边距可以让元素向相反方向定位。缺点是需要知道子元素的宽高
/*
	移动到包含块的百分50,然后移动自己自身宽高的一半就是居中的位置了
*/
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1 {
            width: 500px;
            height: 500px;
            background-color: aqua;
            position: relative;
        }

        .box2 {
            width: 100px;
            height: 100px;
            background-color: yellow;
            /*通过百分比将图片移动到容器中心，再对齐中心点就行了。*/
            /*移动到包含块的百分50,然后移动自己自身宽高的一半就是居中的位置了*/
            position: absolute;
            /* 这俩行代码是移动到父元素的top和left50% */
            top: 50%;
            left: 50%;
            /* 移动自己自身的一半外边距定位到中心点 */
            margin-top: -50px;
            margin-left: -50px;
        }
  </style>
</head>

<body>
    <div class="box1">
        <div class="box2"></div>
    </div>

</body>

</html>

<!--
3.通过绝对定位的方式 absolute + margin auto+top/bottom/left/right为0,缺点也是需要知道子元素的宽高
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box3 {
            margin-top: 200px;
            width: 500px;
            height: 500px;
            background-color: aqua;
            position: relative;
        }

        .box4 {
            width: 100px;
            height: 100px;
            background-color: blue;
            position: absolute;
            margin: auto;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            /*
            如果只需要设置水平居中的话就margin:0 auto;
            如果只需要设置垂直居中的话就margin:auto 0;
            */
            
        }
    </style>
</head>

<body>
    <div class="box3">
        <div class="box4"></div>
    </div>
</body>

</html>

<!--
4.display:table-cell实现水平垂直居中
♥这种方式用在不确定子元素的宽高和数量的时候最好用
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Demo001_displayTable</title>
    <style>
        /*** table-cell middle center组合使用 ***/
        .cell {
            /* 使div成为一个块级表格元素 */
            display: table-cell;
            /* 垂直居中  把此元素放置在父元素的中部*/
            vertical-align: middle;
            /* 水平居中 */
            text-align: center;
            width: 240px;
            height: 180px;
            border: 1px solid #666;
        }
        /*vertical-align这个是设置元素的垂直排列的.  还有一种用法是图片有留白时*/
        /*如果不加display: table-cell;的时候 vertical-align: middle;是不起作用的 因为他和text-align的原理是不一样的 text-align是设置文本的
        当table-cell在元素中设置时 就是自身的内容把当成一个整体，在整个单元格内的垂直对齐方式。*/
    </style>
</head>

<body>
    <div class="cell">
        <p>我爱你</p>
        <p>亲爱的中国</p>
        <div style="width:100px;height:50px;border:1px solid #ccc;display:inline-block">div(inline-block)</div>
    </div>
</body>

</html>

<!--
5.absolute + calc（计算）
-->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<style>
    .box1 {
        position: relative;
        height: 300px;
        width: 300px;
        background-color: pink;
    }

    .box2 {
        height: 100px;
        width: 100px;
        background-color: skyblue;
        position: absolute;
        /* 往右偏移父元素的50%-自身的一半 */
        left: calc(50%-50px);
        /* 往下偏移父元素的50%-自身的一半 */
        top: calc(50% - 50px);
        /*缺点是也要知道子元素的自身大小*/
    }
</style>

<body>

    <div class="box1">
        <div class="box2"></div>

    </div>
</body>

</html>


<!--
6.transform: translateX(-50%)translateY(-50%);
变形的平移函数 这个方法通过绝对定位的方式 absolute + 负margin思想是一样的
优点是不需要知道子元素的宽高,因为是浏览器自动计算的
-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <style>
        .box1 {
            background-color: aqua;
            position: absolute;
            /* 首先移动到包含块中间 */
            left: 50%;
            top: 50%;
            /* 在平移自身的一半距离 */
            transform: translateX(-50%)translateY(-50%);
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2">一些文本...</div>
        <div class="box2">一些文本...</div>
        <div class="box2">一些文本...</div>
        <div class="box2">一些文本...</div>
    </div>

</body>

</html>

<!--
7.display:flex布局
缺点是兼容性太差了
-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <style>
        .box1 {
            width: 600px;
            height: 600px;
            /*设置为弹性盒子*/
            display: flex;
            /* 垂直居中 */
            /*
            align-items中的items指的是flex 中的子项，
            因此align-items指的就是flex子项们相对于flex
            容器在垂直方向上的对齐方式
            */
            align-items: center;
            /* justify-content是水平布局 */
            justify-content: center;
            border: 1px solid #000000;
        }
    </style>
</head>

<body>
    <div class="box1">
        <div class="box2">一些文本...</div>
    </div>

</body>

</html>
```

# 3.Animation 动画

## 1.过渡

```css
/* 
   过渡（transition）
         - 通过过渡可以指定一个属性发生变化时的切换方式
         - 通过过渡可以创建一些非常好的效果，提升用户的体验

             1.transition-property: 指定要执行过渡的属性  
                多个属性间使用,隔开 
                如果所有属性都需要过渡，则使用all关键字
                大部分属性都支持过渡效果，注意过渡时必须是从一个有效数值向另外一个有效数值进行过渡
           			- transition-property: height , width; 
          		 	- transition-property: all; 


              2.transition-duration: 指定过渡效果的持续时间
                时间单位：s 和 ms  1s = 1000ms
 					- transition-duration: 100ms, 2s;
 					- transition-duration: 2s; 


             3.transition-timing-function: 过渡的时序函数
               -指定过渡的执行的方式  
                可选值：
                    ease 默认值，慢速开始，先加速，再减速
                    linear 匀速运动
                    ease-in 加速运动
                    ease-out 减速运动
                    ease-in-out 先加速 后减速
                    cubic-bezier() 来指定时序函数
                        https://cubic-bezier.com这个网址可以生成时序函数
                    steps() 分步执行过渡效果
                        可以设置一个第二个值：
                            end ,在时间结束时执行过渡(默认值)
                            start ,在时间开始时执行过渡
 							- transition-timing-function: cubic-bezier(.24,.95,.82,-0.88); 
 							- transition-timing-function: steps(2, start); 

             4.transition-delay: 过渡效果延迟，等待一段时间后在执行过渡(鼠标移入执行完毕后,鼠标移出的时候等待时间恢复原样)
              		- transition-delay: 2s; 
             
            /* 5.transition 可以同时设置过渡相关的所有属性，只有一个要求，
			如果要写延迟，则两个时间中第一个是持续时间，第二个是延迟 */

             transition:2s margin-left 1s cubic-bezier(.24,.95,.82,-0.88);
```

**例子:米兔练习，鼠标移入使得兔子动起来**

![uTools_1668733506955](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668733506955.png)

![uTools_1668733523968](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668733523968.png)

## 2.动画

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>

    <style>
        *{
            margin: 0;
            padding: 0;
        }

        .box1{
            width: 800px;
            height: 800px;
            background-color: silver;
            overflow: hidden;
        }

        .box1 div{
            width: 100px;
            height: 100px;
            margin-bottom: 100px;
            margin-left: 10px;
            
        }

        .box2{
            background-color: #bfa;
            

            /* 设置box2的动画 */
            /* 1.animation-name: 要对当前元素生效的关键帧的名字 */
            /* animation-name: test; */

            /* 2.animation-duration: 动画的执行时间 */
            /* animation-duration: 4s; */  

            /* 3.动画的延时时间 */
            /* animation-delay: 2s; */

            /* 
               4.animation-iteration-count 动画执行的次数 
                可选值：
                    次数
                    infinite 无限执行
            */
            /* animation-iteration-count: 1; */

            /*
               5.animation-direction
                指定动画运行的方向
                    可选值：
                    normal 默认值  从 from 向 to运行 每次都是这样 
                    reverse 从 to 向 from 运行 每次都是这样 
                    alternate 从 from 向 to运行 重复执行动画时反向执行(回来的时候反方向)
                    alternate-reverse 从 to 向 from运行 重复执行动画时反向执行

            /* 
                6.animation-play-state: 设置动画的执行状态 
                  可选值：
                    running 默认值 动画执行
                    paused 动画暂停

            /* 
            	7.animation-fill-mode: 动画的填充模式
                  可选值：
                    none 默认值 动画执行完毕元素回到原来位置
                    forwards 动画执行完毕元素会停止在动画结束的位置
                    backwards 动画延时等待时，元素就会处于开始位置
                    both 结合了forwards 和 backwards
            */
 
            /*
            	8.animation: test 2s 2 1s alternate;
            	简写属性,唯一的要求也是俩个时间的顺序
            	如果要写延迟，则两个时间中第一个是持续时间，第二个是延迟
            */

            
        }

        .box1:hover div{
            animation-play-state: paused;
        }

        /* 
        动画
            动画和过渡类似，都是可以实现一些动态的效果，
                不同的是过渡需要在某个属性发生变化时才会触发
                动画可以自动触发动态效果
                
            设置动画效果，必须先要设置一个关键帧，关键帧设置了动画执行每一个步骤
        */
        
        /*关键帧(@keyframes) 关键字名称{
            from{}
            to{}
        }*/
        
        @keyframes test {
            /* from表示动画的开始位置 也可以使用 0% */
            from{
                margin-left: 0;
                background-color: orange;
            } 

            /* to动画的结束位置 也可以使用100%*/
            to{
                background-color: red;
                margin-left: 700px;
            }
        }
    </style>

</head>
<body>

    <div class="box1">
        <div class="box2"></div>
        <!-- <div class="box3"></div> -->
    </div>
    
</body>
</html>
```

**例子:奔跑的少年**

![uTools_1668735084762](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668735084762.png)



## 3.关键帧:小球下落动画

```html
<style>
	    
    	.outer{
            height: 500px;
            border-bottom: 10px black solid;
            margin: 50px auto;
            overflow: hidden;
        }
     	.outer div{
            float: left;
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background-color: #bfa;
            animation: ball .5s forwards linear infinite alternate;
        }
    
      @keyframes ball {
            from{
                margin-top: 0;
            }

            to{
                margin-top: 400px;
            }

             20%,to{
                margin-top: 400px;
                animation-timing-function: ease-in;
            }

            40%{
                margin-top: 100px;
            }

            80%{
                margin-top: 200px;
            } 
        }
</style>

<div class="outer">
    <div></div>
</div>

```



## 4.变形

```css
            /* 
                变形就是指通过CSS来改变元素的形状或位置
                  -变形不会影响到页面的布局(这个是他和margin的最大区别)
                - transform 用来设置元素的变形效果
                    - 平移：
                        translateX() 沿着x轴方向平移
                        translateY() 沿着y轴方向平移
                        translateZ() 沿着z轴方向平移
                            - 平移元素，百分比是相对于自身计算的(利用这点可以完成水平垂直居中的效果)
			x,y,z轴发生旋转以后的效果就不一样了，要让z轴生效首先要设置视距 persepective(正常是600-1200)
			旋转的效果要生效(3D效果)首先要设置视距
			XYZ轴就是物理上的左手法制
		*/
```

**z轴**

![uTools_1668912854252](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668912854252.png)

**例子：鼠标移入凸显的效果 小米官网的补充**

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <style>
        body {
            background-color: aquamarine;
        }

        .box4,
        .box5 {
            width: 220px;
            height: 300px;
            background-color: #fff;
            float: left;
            margin: 0 10px;
            transition: all .3s;
        }

        .box4:hover,
        .box5:hover {
            transform: translateY(-4px);
            box-shadow: 0 0 10px rgba(0, 0, 0, .3)
        }
    </style>
</head>

<body>
    <div class="box4"></div>
    <div class="box5"></div>

</body>

</html>
```

## 5.旋转

![uTools_1668914106378](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668914106378.png)

**例子：钟表**

```html
 <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        /* 设置表的样式 */
        .clock {
            width: 500px;
            height: 500px;
            margin: 0 auto;
            margin-top: 100px;
            border-radius: 50%;
            position: relative;
            background-image: url(./img/13/bg3.jpg);
            /*背景铺满盒子*/
            background-size: cover;
        }
		/*居中的公共样式*/
        .clock>div {
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            margin: auto;
        }

        /* 设置时针 我们都是让他的父元素动*/
        .hour-wrapper {
            height: 70%;
            width: 70%;
            animation: run 7200s linear infinite;
        }

        .hour {
            height: 50%;
            width: 6px;
            background-color: #000;
            margin: 0 auto;

        }

        /* 设置分针 */
        .min-wrapper {
            height: 80%;
            width: 80%;
            animation: run 600s steps(60) infinite;
        }

        .min {
            height: 50%;
            width: 4px;
            background-color: #000;
            margin: 0 auto
        }

         /* 设置秒针 */
         .sec-wrapper {
            height: 90%;
            width: 90%;
            animation: run 10s steps(60) infinite;
        }

        .sec {
            height: 50%;
            width: 2px;
            background-color: #f00;
            margin: 0 auto
        }


/* 
        旋转的关键帧
*/
        @keyframes run {
            from {
                transform: rotateZ(0);
            }

            to {
                transform: rotateZ(360deg);
            }
        }
    </style>
</head>

<body>

    <!-- 创建表的容器 -->
    <div class="clock">
        <!-- 创建时针 -->
        <div class="hour-wrapper">
            <div class="hour"></div>
        </div>

        <!-- 创建分针 -->
        <div class="min-wrapper">
            <div class="min"></div>
        </div>

        <!-- 创建秒针 -->
        <div class="sec-wrapper">
            <div class="sec"></div>
        </div>

    </div>

</body>

</html>
```

**例子：复仇者联盟立方体**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>

    <style>
        html {
            perspective: 800px
        }

        .cube {
            width: 200px;
            height: 200px;
            /* background-color: #bfa; */
            margin: 100px auto;
            /* 设置3d变形效果 */
            transform-style: preserve-3d;
            /* transform: rotateX(45deg) rotateZ(45deg); */
            animation: rotate 20s infinite linear;
            /* transform:rotateY(45deg) scaleZ(2); */
        }

        .cube>div {
            width: 200px;
            height: 200px;
            /* 为元素设置透明效果 */
            opacity: 0.7;
            position: absolute;
        }

        img {
            vertical-align: top;
        }

        .box1 {
            transform: rotateY(90deg) translateZ(100px);
        }

        .box2 {
            transform: rotateY(-90deg) translateZ(100px);
        }

        .box3 {
            transform: rotateX(90deg) translateZ(100px);
        }

        .box4 {
            transform: rotateX(-90deg) translateZ(100px);
        }

        .box5 {
            transform:rotateY(180deg) translateZ(100px);
        }

        .box6 {
            transform: rotateY(0deg) translateZ(100px);
        }

        @keyframes rotate {
            form{
                transform:rotateX(0) rotateZ(0)
            }

            to{
                transform:rotateX(1turn) rotateZ(1turn)
            }
        }
    </style>
</head>

<body>

    <!-- 创建一个外部的容器 -->
    <div class="cube">
        <!-- 引入图片 -->
        <div class="box1">
            <img src="./img/14/1.jpg">
        </div>

        <div class="box2">
            <img src="./img/14/2.jpg">
        </div>

        <div class="box3">
            <img src="./img/14/3.jpg">
        </div>

        <div class="box4">
            <img src="./img/14/4.jpg">
        </div>

        <div class="box5">
            <img src="./img/14/5.jpg">
        </div>

        <div class="box6">
            <img src="./img/14/6.jpg">
        </div>
    </div>
</body>

</html>
```



**透明效果：opacity**

**3D效果 transform-style: preserve-3d;**



## 6.缩放

![uTools_1669001220180](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669001220180.png)

**z轴的要在3d效果才能看见,z轴是拉长z轴整条轴**

## 7.三种隐藏元素的方法

```css
/*
1.display: none(渲染元素不继续占据空间)
DOM 结构：浏览器不会渲染 display 属性为 none 的元素，会让元素完全从渲染树中消失，渲染的时候不占据任何空间；
事件监听：无法进行 DOM 事件监听，不能点击；
性能：修改元素会造成文档回流（reflow 与 repaint）,读屏器不会读取display: none元素内容，性能消耗较大；
继承：是非继承属性，由于元素从渲染树消失，造成子孙节点消失，即使修改子孙节点属性子孙节点也无法显示，毕竟子类也不会被渲染；
场景：显示出原来这里不存在的结构；
transition：transition 不支持 display。

2.visibility: hidden(渲染元素继续占据空间)
DOM 结构：不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见；
事件监听：无法进行 DOM 事件监听，不能点击；
性能：修改元素只会造成本元素的重绘（repaint），是重回操作，比回流操作性能高一些，性能消耗较少；读屏器读取visibility: hidden元素内容；
继承：是继承属性，子孙节点消失是由于继承了visibility: hidden，子元素可以通过设置 visibility: visible 来取消隐藏；
场景：显示不会导致页面结构发生变动，不会撑开；
transition：transition 支持 visibility，visibility 会立即显示，隐藏时会延时。

3.opacity: 0(渲染元素继续占据空间)
DOM 结构：透明度为 100%，不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见；
事件监听：可以进行 DOM 事件监听，可以点击；
性能：提升为合成层，是重建图层，不和动画属性一起则不会产生repaint（不脱离文档流，不会触发重绘），性能消耗较少；
继承：会被子元素继承，且子元素并不能通过 opacity: 1 来取消隐藏；
场景：可以跟transition搭配；
transition：transition 支持 opacity，opacity 可以延时显示和隐藏。

打个比方：
display: none： 从这个世界消失了, 不存在了；
opacity: 0： 视觉上隐身了, 看不见, 可以触摸得到；
visibility: hidden： 视觉和物理上都隐身了, 看不见也摸不到, 但是存在的；
*/
```

### 扩展：CSS 隐藏页面上的一个元素有哪几种方法？

```
display:none，visibility:hiden，opacity:0 这三种；
设置 fixed 并设置足够大负距离的 left top 使其“隐藏”；
用层叠关系 z-index 把元素叠在最底下使其“隐藏”；
用 text-indent:-9999px 使其文字隐藏。
```

# 4.Less(css预处理语言)

**less是一个css增强版,通过less可以编写更少的代码实现更强大的样式**

## 1.css函数兼容性的问题

目前原生css也可以直接变量设置这些东西了

### 1.--*  设置变量

```html
<style>
    html{
        /*设置一次整个网页都可以用 维护方便*/
        --color:yellow;
    }
    .box1{
        color:var(--color);
    }
</style>
```

### 2.calc() 计算函数

![uTools_1678078938736](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678078938736.png)

**可以计算任何数值,但是兼容性也不好**



## 2.less在vscode中的使用

![uTools_1669002215237](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669002215237.png)

**如何转换less代码**

**1.安装easy.less插件   2.文件格式命名为*.less   3.保存后系统会自动生成相应的css代码**



## 3.less语法

```less
// less中的单行注释，注释中的内容不会被解析到css中

/*
    css中的注释，内容会被解析到css文件中
*/

//关系嵌套,逻辑清晰维护方便
.box1{
    background-color: #bfa;

    .box2{
        background-color: #ff0;

        .box4{
            color: red;
        }
    }

    .box3{
        background-color: orange;
    }
}

//变量，在变量中可以存储一个任意的值
// 并且我们可以在需要时，任意的修改变量中的值
// 变量的语法： @变量名
@a:200px;
@b:#bfa;
@c:box6;

.box5{
    //使用变量时，如果是直接使用则以 @变量名 的形式使用即可
    width: @a;
    color:@b;
}

//作为类名，或者一部分值使用时必须以 @{变量名} 的形式使用  url("@{c}/1.png")
.@{c}{
    width: @a;
    background-image: url("@{c}/1.png");
}

//作为属性名来用,也是以  @{变量名}
@p:color;
div{
    @{p}:#ff0;
}

 // 变量发生重名时，会优先使用比较近的变量
@d:200px;
@d:300px;
div{
    @d:115px;//会使用这个值
    width: @d;
    height: @e;
}

//可以在变量声明前就使用变量
@e:335px;

//height直接引用width的值,用  $属性 的形式引用
div{
    width: 300px;
    height: $width;
}
```

## 4.less 父元素和扩展

### 1.父元素选择

**编译前：**

![uTools_1669110006291](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110006291.png)

**编译后：**

![uTools_1669110020204](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110020204.png)

```less
//&表示外层的父元素 (最近的那个大括号)
编译前:
.box1{
    &:hover{
        color:red;
    }
}

编译后:
.box1:hover{
    color:red;
}
```

### 2.extend 扩展函数 用选择器分组，性能好

**extend 对当前选择器扩展指定选择器的样式 (选择器分组)    使用了这个以后会继承引用的样式,然后自己写自己的样式**   

**编译前**

![uTools_1669110308180](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110308180.png)

**编译后**

![uTools_1669110525698](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110525698.png)

### 3.minxin 混合函数(通过直接复制,性能差)

**编译前**

![uTools_1669110902359](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110902359.png)

**编译后**

![uTools_1669110940350](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669110940350.png)



### 4.上述第三点不是混合函数的真正用法,应该用extend,这里讲述混合函数的真正用处

```less
//在混合函数中直接设置变量
.test(@w:100px,@h:200px){
    //不给函数赋值就取默认值width:100px,height:200px
    width:@w;
    height:@h;
}

//调用
div{
    //1.按顺序传参
    .test(200px,300px)
    //2.不传参取默认值
    .test()
    //3.传一个参，第一个数接收参数，第二个取默认值
    .test(300px)
    //4.不按顺序传参数
    .test(height:300px;width:200px)
}

//less自己封装的函数
span{
    color：average(yellow,blue);//这个函数会计算出中间的颜色(平均值)
    background-color:darken(yellow,10%);//背景颜色加深10%
}
```

## 5.less的补充

### 1.less模块化处理(每个模块负责不同功能)

**@import 将其它less文件引入到当前的less中(相当于复制了一份过来)**

### 2.less中的运算

![uTools_1669128018213](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669128018213.png)

**注意:在vscode使用less进行除法的时候需要加()**

![uTools_1669471550915](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669471550915.png)



### 3.如何进行css和less的关联(我们在网页中能看到的是css的错误位置,但我们需要改变的是less文件)

1.复制less.cimpie中的内容

2.点击vscode设置,选中扩展,选中easy less configfuration

3.点击在settings.json中编辑

4.将内容复制到大括号内  第一个是设置压缩css文件,第二个文件是打开css-less关联，第三个是否生成css文件

# 5.Flex弹性盒(兼容性差  css3新特性,新项目使用)

## 1.弹性盒子简介

```html
 <!-- 
        flex(弹性盒、伸缩盒)  目前在移动端直接使用,PC端需要考虑兼容性
            - 是CSS中的又一种布局手段，它主要用来代替浮动来完成页面的布局
            - flex可以使元素具有弹性，让元素可以跟随页面的大小的改变而改变
            - 弹性容器
                - 要使用弹性盒，必须先将一个元素设置为弹性容器
                - 我们通过 display 来设置弹性容器
                    display:flex  设置为块级弹性容器(独占一行)
                    display:inline-flex 设置为行内的弹性容器(不独占一行)

            - 弹性元素
                - 弹性容器的直接子元素是弹性元素（弹性项）
                - 弹性元素可以同时是弹性容器
 -->
```



## 2.弹性盒子样式

```html
1.<!-- [设置在父元素里]
	justify-content
    - 如何分配主轴上的空白空间（主轴上的元素如何排列）
    - 可选值：
        flex-start 元素沿着主轴起边排列
        flex-end 元素沿着主轴终边排列
        center 元素居中排列
        space-around 空白分布到元素两侧
        space-between 空白均匀分布到元素间
        space-evenly 空白分布到元素的单侧 
-->

2.<!--  [设置在父元素里]
	align-items(元素间的关系): 
    - 元素在辅轴上如何对齐
        - 可选值：
            stretch 默认值，将元素的长度设置为相同的值
            flex-start 元素不会拉伸，沿着辅轴起边对齐
            flex-end 沿着辅轴的终边对齐
            center 居中对齐
            baseline 基线对齐
-->

3.<!--  [设置在父元素里]
	align-content: 辅轴空白空间的分布(多行)
		可选值和justify-content一样
-->

4.<!--弹性盒子元素水平垂直居中(默认情况下主轴左到右,如果主轴发生变化后要改变)
justify-content:centet;
align-items:center;-->

5.<!--  [设置在父元素里]
	 align-self: 用来覆盖当前弹性元素上的align-items(为元素单独设置align-items的意思)
		可选值和align-items一样
-->
```



## 3.弹性元素样式

```html
<!-- 
       弹性元素的属性：[设置在子元素里]
           	 1.(弹簧伸长)flex-grow 指定弹性元素的伸展的系数(默认值为0,不伸展,系数越大伸展的越长)
             - 当父元素有多余空间的时，子元素如何伸展,父元素的剩余空间，会按照比例进行分配
             2.(弹簧收缩)flex-shrink 指定弹性元素的收缩系数(默认值为1,不收缩,系数越大收缩的越小,如果值为0，表示不减小。)
			 - 当父元素中的空间不足以容纳所有的子元素时，如果对子元素进行收缩
			flex-shrink设置为1时，表示所有子元素大家同时缩小来适应总宽度。当flex-shrink设置为0时，表示大家都不缩小适应。会直接超出父元素
            3.(弹簧静止)flex-basis 指定的是元素在主轴上的基础长度
                 如果主轴是 横向的 则 该值指定的就是元素的宽度
                 如果主轴是 纵向的 则 该值指定的是就是元素的高度
                  - 默认值是 auto，表示参考元素自身的高度或宽度
                    - 如果传递了一个具体的数值，则以该值为准

		简写属性
			flex 可以设置弹性元素所有的三个样式
               顺序为:flex 增长 缩减 基础;
				可选值：
                      initial "flex: 0 1 auto".
                      auto  "flex: 1 1 auto"
                      none "flex: 0 0 auto" 弹性元素没有弹性
-->

<!-- 
	flex-direction 指定容器中弹性元素的排列方式[设置在父元素]
     可选值：
         row 默认值，弹性元素在容器中水平排列（左向右）
             - 主轴 自左向右
         row-reverse 弹性元素在容器中反向水平排列（右向左）
             - 主轴 自右向左
         column 弹性元素纵向排列（自上向下）
			-主轴 自上向下
         column-reverse 弹性元素方向纵向排列（自下向上）
			-主轴 自下向上
     主轴：
         弹性元素的排列方向称为主轴
     侧轴：
         与主轴垂直方向的称为侧轴 
-->

<!-- (弹性元素样式)[设置在父元素]
  flex-wrap(和flex-direction结合使用): 
    设置弹性元素是否在弹性容器中自动换行
    可选值：
        nowrap 默认值，元素不会自动换行
        wrap 元素沿着辅轴方向自动换行
        wrap-reverse 元素沿着辅轴反方向换行
-->

<!--
	flex-flow wrap和direction的简写属性  [设置在父元素]
		例如 flex-flow:row wrap;
-->

<!--[设置在子元素里]
	order决定弹性元素的排列顺序,order值为1排第一个以此类推,可以轻松的设置每个子元素的位置
-->
```

# 6.移动端

## 移动端基础

```css
1.物理像素

在移动设备上的最小物理显示单元。如，iphone6的物理像素为750*1334。

2.逻辑像素

css中逻辑像素px，可以认为是一个“参考像素”。大小不固定，可以放大和缩小。如PC端上的网页放到手机端浏览时，每个px占的空间缩小，从而整个网页缩小。

2.设备独立像素（dip)

也叫密度无关像素，跟设备的硬件像素无关的，是设备上的一个逻辑单位像素，在iphone6中，一个dip等于4个物理像素。

3.设备像素比(dpr)

是指物理像素与设备独立像素比。如iphone6的物理像素为750*1334，设备独立像素为375*667，设备像素比为2， 相当于一个dip占四个物理像素。

4.像素密度(ppi)

每英寸拥有的物理像素的个数，ppi越高，画面越精密。

5.布局视口与视觉视口

手机上为了容纳为桌面浏览器设计的网站，默认布局视口宽度远大于屏幕宽度，然后缩小布局视口的网页，在视觉视口上显示网站的全貌，视觉视口是物理屏幕上的可视区域。

6.viewport

<meta name="viewport" content="width=device-width,initial-scale=1,maxinum-scale=1,user-scalable=no">

device-width表示设备独立像素的宽度。

通过width设置布局视口的宽度，布局视口的宽度＝屏幕的设备独立像素的宽度＝视觉视口的宽度，此时一个css像素对应一个设备逻辑像素。intial-scale=1,表示初始不缩放网页，缩放为1，maxinum-scale表示最大缩放为1，即页面不能放大，user-scalable=no不允许用户手动缩放页面。

通过上面代码的设置，一个css像素对应一个设备逻辑像素，且布局视口与视觉视口的宽度相同。如iphone6，在375px宽的布局视口上布局网页，在相同宽度的视觉视口显示网页，没有缩放。
```



## 1.像素

![uTools_1669178370130](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669178370130.png)

## ![uTools_1669178890181](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669178890181.png)



## 2.完美视口

css像素=逻辑像素

物理像素=设备像素

设备独立像素：与设备无关的逻辑像素，代表可以通过程序控制使用的虚拟像素，是一个总体概念，包括了CSS像素

**例如ipone6的最佳视口比是1：2(1个css像素对应2个物理像素) ，它的物理像素是750px,所以我们要将视口大小(设备独立像素设置为375px)**

![image-20221123130314158](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221123130314158.png)

**width指的是浏览器视口的大小,device-width指的是显示器的尺寸，width=device-width表示宽度等于设备的屏幕宽度(设备独立像素) ，让网页的宽度自动适应手机屏幕的宽度，initial-scale=1.0表示初始缩放1倍，无任何缩放**

**其实它的含义就是将视口设置为：CSS像素=物理像素，即我们在页面中设置的1个CSS像素大小就等价于1个物理像素大小(物理像素会自己取换算)**

**就直接理解成他设置的那个宽度是浏览器F12打开的分辨率**

设置了这一句他的css像素就会等于手机的物理像素，保证先把网页完美的显示出来，如下图

![uTools_1669182981113](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669182981113.png)

没设置的时候就会取默认值anroid的默认浏览器视口980px

![uTools_1669183046965](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669183046965.png)

![uTools_1669179985939](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669179985939.png)



## 3.vw  总是参照于视口宽度进行计算

![uTools_1669195709015](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669195709015.png)



## 4.vw适配方案(没有js的时候最好的手段 )

![uTools_1669196331017](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669196331017.png)

**正常情况下都是乘于40倍来处理,好换算**

```less
//把html的font-size设置以下,假设是750px的设计图
html{
	font-size:(100vw/750)*40;//1rem=1font-size,此时font-size等于40px(对rem扩大了40倍,以后像素直接除以40倍个rem)
}
//需要用到的时候,假设这个盒子宽170px
.box1{
    // 170/40个rem就是我们要的值
	width:(170/40rem);
}
这样适配以后,只要将设计图里的大小除于40得出结果
```



### 1.最终解决方案

**设置font-size**

![image-20231101133003310](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101133003310.png)

这样你在设计图上量到多少px就写多少rem就可以



**如果是项目开发可以用px转换vw的插件**

![image-20231101132854494](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101132854494.png)

# 7.媒体查询

![image-20231101141202634](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101141202634.png)

打印的时候可以加上水印。



## 1.width

一般在响应式页面只设置宽度

```bash
1.min-width 表示最小视口，样式要大于等于指定宽度生效
2.max-width 表示最大视口，样式要小于等于指定宽度生效
```

## 2.连接符

![image-20231101142152391](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101142152391.png)

图中生效的宽度在500-800之间



## 3.响应式布局

**响应式适合用在页面内容较少且简单的页面，如果内容很多就适合移动端一套页面，PC端一套页面**

![image-20231101193818645](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101193818645.png)





# 8.补充

## 1.where和is及has伪类选择器

![image-20231005014158327](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005014158327.png)

![image-20231005014220229](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005014220229.png)

**选中了4个id选择器中的h1**



**is和weher的区别在于where的优先级为0 is会找条件中优先级最高的选择器，在这个例子中和前面正常写法的优先级一样，但是后面书写所以会生效为蓝色**

`is和where就是相当于判别小括号中的条件`



```css
/*这样写会报错，因为它认为这是一条规则，如果出错了就俩个选择器都不加样式*/
#d1 h1,#d1 h1:hovre{ color:red } 

/*这样不会报错，第一个选择器还是会执行*/
:is(#d1 h1,#d1 h1:hovre){ color:red }
```



**has选择器(相当于一个条件)**

1.通过子元素可以选择父元素  包含span的div样式会被设置

![image-20231010193102162](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231010193102162.png)

2.通过下一个兄弟元素选择上一个兄弟元素

![image-20231010192853704](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231010192853704.png)





3.dock栏demo

![image-20231010193022466](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231010193022466.png)



## 2.定位动画演示

1. static为默认值 不需要定位(没有开启定位的意思)

2. fixed固定定位

   ![image-20231005015706361](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005015706361.png)

3. sticky粘滞定位，到达指定位置时显示效果，受父容器影响，固定时原有位置为空白效果，不脱离文档流

   ![image-20231005015916463](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005015916463.png)

   4.relative相对元素本身进行定位，不脱离文档流，元素任然处于原来空间，不影响其它元素位置

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005020113099.png)

5. absolute绝对定位，寻找开启了定位的父元素(除了static以外都算开启定位)进行定位，寻找的是最近的父元素，如果最近没有会一直向上寻找到html根元素，如果根元素也没定位，则会根据窗口左上角进行定位；脱离文档流，可能影响其它元素，如果绝对定位元素没有设置宽度，移动后会根据内容设置一个宽度。

![image-20231005020541661](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005020541661.png)

6. z-index可以设置层级



## 3.flex布局

简介：

一个元素既可以是弹性容器也可以是弹性子元素，不会冲突。

![image-20231101134753227](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231101134753227.png)



![image-20231005023154083](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005023154083.png)



`容器属性`

1.设置主轴方向

![image-20231005023309521](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005023309521.png)



2.定义弹性子元素在主轴方向的对齐

![image-20231005023334482](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005023334482.png)



3.定义弹性子元素在纵轴的对齐方式（单行）

![image-20231005023513745](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005023513745.png)



4.定义多行项目在纵轴方向上的对齐

![image-20231005024057713](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005024057713.png)



5.超出主轴长度是否换行

![image-20231005023627462](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005023627462.png)



6.flex-flow是flex-direction和flex-warp的简写



`项目属性`

1.order 自定义项目(子元素)的排列顺序

![image-20231005024643258](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005024643258.png)



2.align-self  允许子元素设置自己的纵轴对齐方式(设置自己的align-item)

![image-20231005024810355](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005024810355.png)



3.设置元素的放大伸缩默认值

![image-20231005025052744](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005025052744.png)

```bash
1.flex-grow：定义元素在主轴方向上的弹性大小，即默认情况下，元素会根据剩余空间的大小自动增长。例如，如果一个元素的 flex-grow 值为 2，则它会在水平方向上占据两个剩余空间。
2.flex-shrink：定义元素在主轴方向上的弹性大小，即默认情况下，元素会根据剩余空间的大小自动收缩。例如，如果一个元素的 flex-shrink 值为 1，则当空间不足时，它会自动缩小,如果设置为0,则他不会缩小
3.flex-basis：定义元素在主轴方向上的初始大小(项目占据的主轴空间)。例如，如果一个元素的 flex-basis 值为 100px，则它在水平方向上占据 100 像素的初始空间
4.flex:1 不管内容多少，一般都是平分空间，空间大小都一致
5.flex:1 1 auto;有剩余空间就放大，空间不够就缩小，项目长度为原本的长度
6.felx:auto 的效果和 flex： 1 1 auto 相同  
```











## 4.grid二维布局

页面场景为一个大盒子套了六个小盒子

![image-20231005031838537](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005031838537.png)

1.改成三列的固定宽度

![image-20231005025742788](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005025742788.png)

2.改成三列的fr自适应宽度

![image-20231005025725932](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005025725932.png)

![image-20231005025828458](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005025828458.png)

3.column行间距 row列间距 gap统一设置

![image-20231005025901952](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005025901952.png)

![image-20231005030003036](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005030003036.png)



4.特殊布局方式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .layout{
            width: 500px;
            height: 600px;
            background-color: aqua;
            display: grid;
            /*这里可以设置*/
            grid-template-areas:
            "header header header"
            "sidebar content content"
            "footer footer footer";
        }
        header{
            grid-area: header;
            background-color: blue;
            border:1px solid red;
        }
        aside{
            grid-area: sidebar;
            background-color: pink;
            border:1px solid red;
        }
        main{
            grid-area: content;
            background-color: yellow;
            border:1px solid red;
        }
        footer{
            grid-area: footer;
            background-color: red;
            border:1px solid red;
        }
        
    </style>
</head>
<body>
    <div class="layout">
        <header>头部</header>
        <aside>侧边</aside>
        <main>内容</main>
        <footer>底部</footer>
    </div>
</body>
</html>
```

效果

![image-20231005031111056](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005031111056.png)

5.水平垂直对齐和flex类似

![image-20231005031413475](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005031413475.png)

6.如果行轨道和列轨道的长度小于轴(子元素内容没有达到撑开整个grid布局)可以对轨道进行对齐

![image-20231005031731659](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005031731659.png)

## 5.伪类和伪元素

`依附于已经存在的元素而生成`

![image-20231005032847345](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005032847345.png)

伪类选择器可以链式拼接

![image-20231005032948904](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005032948904.png)

![image-20231005033018369](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033018369.png)

伪元素不支持链式

![image-20231005033039577](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033039577.png)

常用的伪类

![image-20231005033107378](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033107378.png)

常用的伪元素

![image-20231005033140776](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033140776.png)



## 6.阴影的高级用法

阴影可以叠加 所以有无限的可能做成不一样的效果

boxshadow:水平偏移 垂直偏移 模糊 扩散 颜色

![image-20231005033251460](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033251460.png)

内部阴影

![image-20231005033349304](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033349304.png)

光从左上方打入(阴影可以嵌套着写完成各种效果)

![image-20231005033513412](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033513412.png)

元素内凹效果

![image-20231005033636468](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033636468.png)

鼠标悬浮空间效果

![image-20231005033820167](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231005033820167.png)

月亮

```css
        div{
            width: 150px;
            height: 150px;
            border-radius: 50%;
            box-shadow: 50px 0px 0px 0px rgba(255,255,0,0.7);
        }
```



## 7.0.5px的问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .box1{
            width: 100px;
            height: 1px;
            background-color: #000;
            transform: scaleY(0.1);
        }
        .box2{
            width: 100px;
            height: 1px;
            background-color: #000;
        }
    </style>
</head>
<body>
    <div class="box1"></div>
    <br>
    <div class="box2"></div>
</body>
</html>
```



移动端

## 8.自适应响应式

```bash
1.对于图片视频等文件可以设置其为100%以达到响应式(100%参考的是父元素宽度)
2.对于其它想响应式宽度的，可以使用vw或rem 这俩个是不考虑父元素的，一个根据视口，一个根据body的font-size
```



## 9.css  :root和var

```css
:root
是一个伪类，表示文档根元素，所有主流浏览器均支持 :root 选择器，除了 IE8 及更早的版本。
在:root中声明相当于全局属性，只要当前页面引用了:root segment所在文件，都可以使用var()来引用。
用 -- 这样写法加上样式名称 例如：–-background 引用：var(–-background)

:root{
  --color:#000
}

body{
  background-color:var(--color)
}

var()
var()函数可以代替元素中任何属性中的值的任何部分。var()函数不能作为属性名、选择器或者其他除了属性值之外的值。（这样做通常会产生无效的语法或者一个没有关联到变量的值。）
```



## 10.图片作为背景

![image-20231020122355143](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231020122355143.png)

