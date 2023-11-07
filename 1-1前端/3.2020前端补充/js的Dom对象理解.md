## 总结

### 一、总结：

dom操作有用原生js的dom操作，也可以用对js封装过的jquery等插件来更加方便的进行dom操作

dom是什么？
对于JavaScript，为了能够使JavaScript操作Html，JavaScript就有了一套自己的dom编程接口。
对于Html，dom使得html形成一棵dom树，类似于一颗家族树一样，一层接一层，子子孙孙。

Html的DOM树是什么？
HTML中的每个标签元素，属性，文本都能看做是一个DOM的节点，这些dom节点构成了一个树形结构

原生的dom操作指的是什么？
就是用原生的js进行的操作，相对的就是非原生操作，比如用jquery操作dom

### 二、DOM操作基础介绍

#### 1.理解DOM：

DOM（Document Object Model ，文档对象模型）一种独立于语言，用于操作xml，html文档的应用编程接口。怎么说，我从两个角度理解：
对于JavaScript，为了能够使JavaScript操作Html，JavaScript就有了一套自己的dom编程接口。
对于Html，dom使得html形成一棵dom树，类似于一颗家族树一样，一层接一层，子子孙孙。
所以说，有了DOM，在我看来就是相当于JavaScript拿到了钥匙一样可以去操作Html的每一个节点，触摸Html每寸肌肤。

#### 2.介绍Html的DOM树：

说明：html标签通过浏览器的解析后才会形成dom树，此后HTML中的每个标签元素，属性，文本都能看做是一个DOM的节点，JavaScript都能通过dom的提供的编程接口操作到每个节点，去了解浏览器的渲染机制能够帮助我们了解dom。
Html代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>dom</title>
</head>
<body>
    <div>
        <a href="www.baidu.com">百度</a>
    </div>
</body>
</html>
```

对应的DOM树结构图：

文本节点和属性节点就像是这颗DOM树的果子，而元素节点就是树枝，所以，在操作时，一定要要记顺枝摘果：得先取到元素节点！然后再操作子节点！！

![20210119143221129](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/20210119143221129.png)

#### 3.认识JavaScript中的DOM编程接口：

上面说了html形成的dom树，接着说下通过js的dom编程接口去操作这棵dom树。
JavaScriptDOM操作的常用方法和属性：

```javascript
(常用方法)
获取节点：
document.getElementById(idName) //通过id号来获取元素，返回一个元素对象
document.getElementsByName(name) //通过name属性获取id号，返回元素对象数组
document.getElementsByClassName(className) //通过class来获取元素，返回元素对象数组（ie8以上才有）  
document.getElementsByTagName(tagName) //通过标签名获取元素，返回元素对象数组
document.qurySelectorAll('选择器') // 通过选择器获取一组元素
document.querySelector("选择器") // 通过选择器获取单个元素

获取/设置元素的属性值：
element.getAttribute(attributeName) //括号传入属性名，返回对应属性的属性值
element.setAttribute(attributeName,attributeValue) //传入属性名及设置的值

创建节点Node：
document.createElement("h3") //创建一个html元素，这里以创建h3元素为例  把h3拿来当成一个节点
document.createTextNode(String) //创建一个文本节点
document.createDocumentFragment() //创建一个DOM片段

添加、移除、替换、插入（父元素调用）
element.appendChild() //添加
element.removeChild() //移除
element.replaceChild() //替换
element.insertBefore() //插入

(常用属性)
获取当前元素的父节点 ：
element.parentNode //返回当前元素的父节点对象

获取当前元素的子节点：
element.chlidren //返回当前元素所有子元素节点对象，只返回HTML节点
element.chilidNodes //返回当前元素所有子节点，包括文本，HTML，属性节点。（回车也会当做一个节点）
element.firstChild //返回当前元素的第一个子节点对象
element.lastChild //返回当前元素的最后一个子节点对象

获取当前元素的同级元素：
element.nextElementSibling //返回当前元素的下一个同级元素 没有就返回null
element.previousElementSibling //返回当前元素上一个同级元素 没有就返回null

获取当前元素的文本：
element.innerHTML //返回元素的所有文本，包括html代码
element.innerText //返回当前元素的自身及子代所有文本值，只是文本内容，不包括html代码

获取当前节点的节点类型：
node.nodeType //返回节点的类型,以数字的形式（1-12）   常见几个1：元素节点，2：属性节点，3：文本节点

设置样式：
可以通过dom操作利用JavaScript修改页面CSS样式，让用户有不同的体验感。
element.style.color=“#eea” //设置元素的样式时使用style，这里以设置文字颜色为例

```

#### 4.一些操作案例

##### 1.DOM：Document Object Model（文档对象模型）

网页上的所有内容都是节点，节点分为元素节点、属性节点、文本节点、注释节点、文档节点等

##### 2.元素节点的操作

###### 1.通过元素的id来获取相应的节点

document.getElementById("");

###### 2.通过元素的标签名来获取节点

document.getElementsByTagName("");

###### 3.通过元素的类名来获取节点

document.getElementsByClassName("");

###### 4.通过元素的name属性来获取节点

document.getElementsByName("");

###### 5.获取元素的所有子节点

node.childNodes;

###### 6.创建元素节点

document.createElement("tagName");

###### 7.往父节点最后添加子节点

fatherNode.append(childNode);

###### 8.删除元素节点

fatherNode.removeChild(childNode);

###### 9.替换节点

fatherNode.replaceChidl(newNode,oldNode);



##### 3.属性节点操作

1.添加属性节点
node.setAttribute('attr',"attrValue");
2.删除属性节点
div.removeAttribute("attr");
3.修改属性节点
div.setAttribute("attr","new");
4.获取属性节点
div.getAttribute("style");

##### 4.文本节点

###### 1.创建文本节点

var textNode = document.createTextNode("hello");

###### 2.获取文本节点

var textNode = div.childNodes[0];

###### 3.删除起始位置开始的num个值

textNode.deleteData(starNum,num);

###### 4.尾部添加内容

textNode.appendData("后面哦");

###### 5.中间插入内容

text.insertData(1,"中间哦");

###### 6.获取当前元素的文本：

1.innerHTML属性获取的是元素对象内包含html代码的内容

2.innerText属性只获得元素对象内的文本内容

![image-20210929211125408](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20210929211125408.png)



##### 5.案例

parentNode:返回节点的父节点

childNodes：返回子节点的集合

firstChild：返回节点的第一个子节点，最普遍的方法是访问该元素的本节点

lastChild:返回节点的最后一个子节点

nextSibling:下一个节点

previousSibling:上一个节点

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/2019080910391087.png)

