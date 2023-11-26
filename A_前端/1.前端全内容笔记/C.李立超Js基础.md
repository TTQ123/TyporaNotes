# 一、Js基础

## 1.js简介

​       JavaScript（JS）是一种具有函数优先特性的轻量级、解释型或者说即时编译型的编程语言。虽然作为 Web 页面中的脚本语言被人所熟知，但是它也被用到了很多非浏览器环境中，例如 Node.js、Apache CouchDB、Adobe Acrobat 等。进一步说，JavaScript 是一种基于原型、多范式、单线程的动态语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。11

脚本语言：语言不需要经过编译器的编译,而是可以直接交给浏览器**(解释器将语言解释成计算机可以理解的低级语言)**一行行执行

微软公司通过逆向工程破解了JavaScript,于是就开始了浏览器兼容性问题   ( Netscape（网景）>推出了js>被ie打败了>js贡献给了es>后来浏览器卖给了Firefox)

**ECMAScript(Es是标准)是Javascript(Js是实现)的规范。**

**参考地址：[MDN 网页文档 (mozilla.org)](https://developer.mozilla.org/zh-CN/)**

![uTools_1669641660610](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669641660610.png)

**js是由浏览器一边解释一边运行的**

![uTools_1669641852862](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669641852862.png)

**[ECMAScript 6_百度百科 (baidu.com)](https://baike.baidu.com/item/ECMAScript 6/22641264?fromtitle=ES6&fromid=24088827&fr=aladdin#2_2)**

**DOM操作窗口对象,BOM操作浏览器对象**

**什么是ES6**

![uTools_1678278922147](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678278922147.png)

## 2.hello world

![uTools_1669644075313](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669644075313.png)

## 3.编写位置

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>JS的编写位置</title>
        <!-- 
        1.可以将js编写到网页内部的script标签
        -->
        <script>
            alert("哈哈！")
        </script> 

        <!-- 
            2.可以将js编写外部的js文件中，然后通过script标签进行引入
			如果引入了外部的js文件,script标签里就不要写代码了,写一个新的script标签
        -->
        <script src="./script/script.js"></script>
    </head>
    <body>
        <!--
            3.可以将js代码编写到指定属性中
        -->
        <button onclick="alert('你点我干嘛！')">点我一下</button>

        <hr>
		<!--
            点击时超链接时会跳出提示
        -->
        <a href="javascript:alert(123);">超链接</a>
        
        <hr>

        <!--
            点击时超链接时不会跳出提示
        -->
        <a href="javascript:;">超链接</a>
    </body>
</html>

        <!--
            可以直接在地址栏输入javascript:alert(123); 效果也是和超链接一样的
        -->

```

## 4.基本语法

![uTools_1669644859686](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669644859686.png)

## 5.字面量和变量

![uTools_1669645465797](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669645465797.png)

### (1).字面量

​		在计算机科学中，字面量（literal）是用于表达源代码中一个固定值的表示法（notation）。几乎所有计算机编程语言都具有对基本值的字面量表示，诸如：整数、浮点数以及字符串；而有很多也对布尔类型和字符类型的值也支持字面量表示；还有一些甚至对枚举类型的元素以及像数组、记录和对象等复合类型的值也支持字面量表示法。

**例如直接alert.log(a)会报错,a是变量；alert.log(hello)会正常显示**

**vscode多行注释：shift + alt + a**

### (2).变量

![uTools_1669645712798](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669645712798.png)

**Js中的变量是不区分数据类型的**

### (3).常量

![uTools_1669709937247](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669709937247.png)

**常量的值是会被固定不能被修改(内存地址固定了)**

## 6.变量的内存结构

![uTools_1669709903890](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669709903890.png)

![uTools_1669648141698](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669648141698.png)

**就是类似c语言中的指针,通过内存地址找到内存存储的内容**

## 7.标识符的规则

![uTools_1669710562534](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669710562534.png)

**Js区分大小写**

# 二、数据类型(Js中变量没有类型,值才有类型)

![uTools_1669710653036](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669710653036.png)

**七种原始值是构成各种数据的基石**

​          **- 原始值在JS中是不可变类型，一旦创建就不能修改**

![uTools_1669717131553](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669717131553.png)

**第一次b创建的哈哈还会一直存在,只是给b赋值了一个新的值,内存地址指向嘻嘻,哈哈永远存在不会被修改。只有ab变量都不引用时才会被垃圾回收**

## 1.原始值

### 1.数值

```css
/* 
     数值（Number）
          - 在JS中所有的整数和浮点数都是Number类型
          - JS中的数值并不是无限大的，当数值超过一定范围后会显示近似值
		 - JS中的数值并不是无限小的，当数值超过一定范围后会显示近似值
          - Infinity 是一个特殊的数值表示无穷
          - 所以在JS中进行一些精度比较高的运算时要十分注意
          - NaN 也是一个特殊的数值，表示非法的数值
		 - 计算机无法计算十进制的十分之一大小,计算0.1+0.2的时候程序会出问题,得到一个0.30000000000000004的值,所以我们对计算精度有要求时不能直接在js里运算
*/
```

### 2.大整数

```css
/*
 大整数（BigInt）
                    - 大整数用来表示一些比较大的整数
                    - 大整数使用n结尾，它可以表示的数字范围是无限大

 其他进制的数字：
                    二进制 0b
                    八进制 0o
                    十六进制 0x

   		   a = 0b1010>>>10
            a = 0o10>>>>8
            a = 0xff>>>255
*/
```

### 3.类型检查(检查的变量名指向的内存地址的值的类型)

**在引用他人创建的变量时，不知道这个变量的值是什么类型的可以通过typeof检查数据类型**

![uTools_1669711691793](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669711691793.png)

**除了原始值、以及函数不返回object，其余返回值都是object**

### 4.字符串(模板字符串)

```css
/* 
     1.字符串（String）
     	- 在JS中使用单引号或双引号来表示字符串
        - 转义字符 \
               \" --> "
               \' --> '
               \\ --> \\
               \t --> 制表符
               \n --> 换行
       2.模板字符串
           - 使用反单引号` 来表示模板字符串
           - 模板字符串中可以嵌入变量
					例如:
						  let name = "猪八戒"
            			   let str = `你好，${name}`
						  console.log(str)//此时打印出 你好,猪八戒

      3.使用typeof检查一个字符串时会返回 "string"
*/
```

### 5.其它数据类型

#### (1).布尔值

 布尔值（Boolean）

​        \- 布尔值主要用来进行逻辑判断

​        \- **布尔值只有两个true 和 false(在底层其实布尔值本质也是数字，true为1，false为0。所以在控制台显示的颜色和数值的颜色是一样的)**

​        \- 使用typeof检查一个布尔值时会返回 "boolean"

#### (2).空值

空值 （Null）

​	   \- 空值用来表示空对象

​        \- 空值只有一个 null

​        \- 使用typeof检查一个空值时会返回"object"

​        \- 使用typeof无法检查空值

**造成返回object的原因**
不同的对象在底层都表示为二进制，在 JavaScript 中二进制前三位都为 0 的话会被判断为object类型， null 表示null型指针，它的二进制表示是全 0，所以执行 typeof 时会返回“object”。
这个bug是第一版Javascript留下来的。在这个版本，数值是以32字节存储的，由标志位（1~3个字节）和数值组成。标志位存储的是低位的数据。

**vscode可以直接给一行代码给上“”,选中后直接点击shift+“**

#### (3).未定义

未定义（Undefined）

​        \- 当声明一个变量而没有赋值时，它的值就是Undefined

​        \- Undefined类型的值只有一个就是 undefined

​        \- 使用typeof检查一个Undefined类型的值时，会返回 "undefined"

**空值和未定义其实都是为了js早期的思想不报错而设计出来的,正常我们不会自己去用,而是程序会自己在一定的情况下去使用它!**

#### (4).符号(后期才会知道,目前我理解为一把钥匙,拿到这个东西需要这个东西的钥匙)

 符号（Symbol）

​        \- 用来创建一个唯一的标识   

​        \- 使用typeof检查符号时会返回 "symbol"

```css
let c = Symbol()   //调用Symbol()创建了一个符号
console.log(typeof c)
```

运行结果：

![uTools_1669713694703](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669713694703.png)

**symbol()的作用**

```javascript
        //后面的括号可以给symbol做上标记便于识别
        let name = Symbol('name');
        let say = Symbol('say');
        let obj = {
            //如果想 使用变量作为对象属性的名称，必须加上中括号，.运算符后面跟着的都是字符串
            [name]: 'lnj',
            [say]: function () {
                console.log('say')
            }
        }
        obj.name = 'it666';
        obj[Symbol('name')] = 'it666'
        console.log(obj)
```

![uTools_1678280529425](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678280529425.png)

**每一个符号一创建都是独一无二的**

**怎么取值**

![uTools_1678282136296](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678282136296.png)

![uTools_1678282182097](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678282182097.png)



## 2.数据类型转换(显性转换)

**其实我们是没办法转换的(原始值永远是自己),是根据原来的值去创建一个转换后的数据类型**

**什么值都可以转为字符串**

### 1.转换为字符串

#### (1).toString()

```js
let a = 10;
//看起来是a.toString()   实际上是调用值10的toString()方法  10.toString() ==> "10"
a = a.toString();//实际上是根据数值型10去开辟一个新的字符串型的10
```

![uTools_1669733141619](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669733141619.png)

#### (2).String()

```js
let b =  10;
b = String(b);
```

![uTools_1669733564729](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669733564729.png)

**null和undefined还是转成自己 其它等于还是调toString()**

### 2.转化为数值

**不合法的数据转为数值时系统会做一定的处理**

![uTools_1669776519855](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669776519855.png)



### 3.转换为布尔值

![uTools_1669776878598](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669776878598.png)



# 三、运算符

**JS是一门弱类型语言，当进行运算时会通过自动的类型转换来完成运算**

## 1.算术运算符( 转换为字符串(隐式类型转换))

```html
    <title>运算符</title>
    <script>
        /* 
            运算符（操作符）
                - 运算符可以用来对一个或多个操作数（值）进行运算
                - 算术运算符：
                    + 加法运算符
                    - 减法运算符
                    * 乘法运算符
                    / 除法运算符
                    ** 幂运算
                    	-经典运用 求开方
                    		a = 9 ** .5 //得到a=3
                    	-求三次方
                    		let sum = (num3 ** 3);
                    % 模运算，两个数相除取余数

                - 注意：
                    - 算术运算时，除了字符串的加法，
                       运算的其他操作数是非数值时，都会转换为数值然后再运算
        */
        let a = 1 + 1
        a = 10 - 5//5
        a = 2 * 4//8
        a = 10 / 5//2
        a = 10 / 3//得到一个近似值 3.333333335
        a = 10 / 0 // Infinity(相当于是10里面有无数个0)
        a = 10 ** 3//1000
        a = 9 ** .5 // 开方  3
        a = 10 % 2//0
        a = 10 % 3//1
        a = 10 % 4//2

        /* 
            JS是一门弱类型语言，当进行运算时会通过自动的类型转换来完成运算
        
        */
        a = 10 - '5' // 10 - 5
        a = 10 + true // 10 + 1 true被转为了1
        a = 5 + null // 5 + 0 null被转为了0
        a = 6 - undefined // 6 - NaN   得到还是NaN

        /* 
            当任意一个值和字符串做加法运算时，它会先将其他值转换为字符串，
                然后再做拼串的操作
            可以利用这一特点来完成类型转换
                可以通过为任意类型 + 一个空串的形式来将其转换为字符串
                    其原理和String()函数相同，但使用起来更加简洁
            需要注意的事情是转完以后得到的值其实是字符串类型的
        */
        a = 'hello' + 'world' //helloworld
        a = '1' + 2 // "1" + "2"
		
        a = true
	    //用法(隐式类型转换)
        a = a + ''

        console.log(typeof a, a)
      </script>
```

## 2.赋值运算符

```css
扩展   +=    这些写法的效率会更高

a＋＝1计算机可以直接理解为：直接在a的基础上＋1，一步搞定，
但是a＝a＋1计算机要把a＋1的值先算出来，然后再把算出来的值赋值到a的上面，是两步，一步计算一步赋值的运算过程。
```



```js
let  a = 10
10 = a //此时会发生报错,因为10是字面量无法改变
```

```html
    <title>赋值运算符</title>
    <script>
        /* 
            赋值运算符用来将一个值赋值给一个变量
                =
                    - 将符号右侧的值赋值给左侧的变量
                ??=
                    - 空赋值(赋值前进行判断,符合时才赋值)
                    - 只有当变量的值为null或undefined时才会对变量进行赋值
                +=
                    - a += n 等价于 a = a + n
                -=
                    - a -= n 等价于 a = a - n
                *=
                    - a *= n 等价于 a = a * n
                /=
                    - a /= n 等价于 a = a / n
                %=
                    - a %= n 等价于 a = a % n
                **=
                    - a **= n 等价于 a = a ** n
        */
        let a = 10
        a = 5 // 将右边的值 赋值 给左边的变量
        let b = a // 一个变量只有在=号左边时才是变量，在=右边时它是值

        a = 66
        a = a + 11 // 大部分的运算符都不会改变变量的值，赋值运算符除外

        a = 5
        // a = a + 5 // 10
        a += 5 // 在a原来值的基础上增加5
       
        a = null

        a ??= 101

        console.log(a)
        

    </script>
```

## 3.一元的±(元就是未知数,通过这个进行非数值转换为数值(隐式类型转换))

```html
    <script>
       /* 
            一元的±
                + 正号
                    - 不会改变数值的符号
                - 负号
                    - 可以对数值进行符号位取反(正的变负,负的变正)
                
                当我们对非数值类型进行正负运算时，系统会先将其转换为数值然后再运算
       */
       let a = -10
       a = -a

       let b = '123'
       
       
       b = +b //类型转换 等价于b = Number(b)

       console.log(typeof b, b)

    </script>
```

## 4.自增和自减

```html
    <script>
        /* 
            赋值和自增和自减会影响到原来的变量
            ++ 自增运算符
                - ++ 使用后会使得原来的变量立刻增加1
                - 自增分为前自增(++a)和后自增(a++)
                - 无论是++a还是a++都会使原变量立刻增加1
                - 不同的是++a和a++所返回的值不同
                    a++ 是自增前的值 旧值(加完后先用旧值)
                    ++a 是自增后的值 新值(加完后先用新值)

        */
        let a = 10

        // let b = a++
        // console.log("a++ =", b)

        let b = ++a
        // console.log("++a =", b)
        // console.log(a)

        let n = 5
        //           5 + 7 + 7
        let result = n++ + ++n + n

        console.log(result)//result=19

        /* 
            -- 自减运算符
                    - 使用后会使得原来的变量立刻减小1
                    - 自减分为前自减(--a)和后自减(a--)
                    - 无论是--a还是a--都会使原变量立刻减少1
                    - 不同的是--a和a--的值不同
                        a-- 是旧值 (减完了用旧值)
                        --a 是新值 (减完了用新值)
                        
        */
        a = 5
        // console.log('--a', --a)
        console.log('a--', a--)

        console.log(a)
    </script>
```

## 5.逻辑运算符

### (1).逻辑非 !

```css
/*
            ! 逻辑非
                - ! 可以用来对一个值进行非运算
                - 它可以对一个布尔值进行取反操作
                    !!就是还是取到自己本身
                    true --> false
        			false -- > true
            	- 如果对一个非布尔值进行取反，它会先将其转换为布尔值然后再取反
        可以利用这个特点将其他类型转换为布尔值
			- let str = "suwukong"   
*/
```

![uTools_1678281279162](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678281279162.png)



### (2).逻辑与 && 和 逻辑或 ||

**&&俩个为真才为真(找false),||一个为真即为真(找true)；都有短路的功能。**

```html
    <script>
        /* 
            && 逻辑与
                - 可以对两个值进行与运算
                - 当&&左右都为true时，则返回true，否则返回false
                - 与运算是短路的与，如果第一个值为false，则不看第二个值
                - 与运算是找false的，如果找到false则直接返回，没有false才会返回true
                - 对于非布尔值进行与运算，它会转换为布尔值然后运算
                    ❤❤但是最终会返回原值
                    - 如果第一个值为false，则直接返回第一个值;如果第一个值为true，则返回第二个值。
        */
        let result = true && true // true
        result = true && false // false
        result = false && true // false
        result = false && false // false

        true && alert(123) // 第一个值为true，alert会执行
        false && alert(123) // 第一个值为false，alert不会执行

        result = true && true  //true
        result = 1 && 2 // 2 
        //       true && false -> false
        result = 1 && 0 // 0
        //       false && false -> false 
        result = 0 && NaN // 0
        
        /*
            || 逻辑或
                - 可以对两个值进行或运算
                - 当||左右有true时，则返回true，否则返回false
                - 或运算也是短路的或，如果第一个值为true，则不看第二个值
                - 或运算是找true，如果找到true则直接返回，没有true才会返回false
                - 对于非布尔值或运算，它会转换为布尔值然后运算
                    但是最终会返回原值
                    - 如果第一个值为true，则返回第一个;如果第一个值为false，则返回第二个
        */
       
        result = true || false // true
        result = false || true // true
        result = true || true // true
        result = false || false // false

        // false || alert(123) // 第一个值为false，alert会执行
        true || alert(123) // 第一个值为true，alert不会执行

        result = 1 || 2 // 1
        result = "hello" || NaN // "hello"
        result = NaN || 1 // 1
        result = NaN || null // null

        console.log(result)
    </script>
</head>
<body>
    
</body>
</html>
```

## 6.隐式类型转换总结★

```css
                    转换为字符串
                        显式转换
                            String() //a = String(a)
                        隐式转换
                            + "" //a = a+ ""
                    转换为数值
                        显式转换
                            Number() //a = Number(a)
                        隐式转换
                            +  // a = +a
                    转换为布尔值
                        显式转换
                            Boolean() //a = Boolean(a)
                        隐式转换
                            !! // a = !!a
```

## 7.关系运算符

```html
    <title>关系运算符</title>
    <script>
        /* 
            关系运算符
                - 关系运算符用来检查两个值之间的关系是否成立
                    成立返回true，不成立返回false
                >
                    - 用来检查左值是否大于右值
                >=
                    - 用来检查左值是否大于或等于右值
                <
                    - 用来检查左值是否小于右值
                <=
                    - 用来检查左值是否小于或等于右值

            注意：
                当对非数值进行关系运算时，它会先将前转换为数值然后再比较 
                当关系运算符的两端是两个字符串，它不会将字符串转换为数值，
                而是逐位的比较字符的Unicode编码  (a<b 返回true a97 b98)  
                    利用这个特点可以对字符串按照字母排序  

                注意比较两个字符串格式的数字时一定要进行类型转换 
                    例如:
                        let a = "12" <  "2"  //此时返回结果true,因为俩个字符串会直接比Unicode编码
                        我们对齐进行类型转换
                        let a = +"12" <  "2" //此时对第一个数进行了类型转换,就变为了一个数值型,系统会把另一个字符串转为数值型,没必要俩个都转化
        */
        let result = 10 > 5 // true
        result = 5 > 5 // false
        result = 5 >= 5 // true

        result = 5 < "10" // true
        result = "1" > false // true

        result = "a" < "b" // true 比的是Unicode编码
        result = "z" < "f" // false 比的是Unicode编码
        result = "abc" < "b" // true 逐位比Unicode编码

        result = "12" < "2" // true
        result = +"12" < "2" // false 类型转换

        // 检查num是否在5和10之间
        let num = 60
        // result = 5 < num < 10 // 错误的写法 这种写法无论num等于多少永远都返回true
        //它先从左到右进行了 5 < num 这个比较,返回的值再去和10比较,而返回的这个值永远都是true或false
        //因为10永远比0和1大
        result = num > 5 && num < 10
        console.log(result)
        
    </script>
```

## 8.相等运算符

```html
    <title>相等运算符</title>
    <script>
        /* 
            ==
                - 相等运算符，用来比较两个值是否相等
                - 使用相等运算符比较两个不同类型的值时，
                    它会将其转换为相同的类型（通常转换为数值）然后再比较
                    类型转换后值相同也会返回true
                - null和undefined进行相等比较时会返回true
                - NaN不和任何值相等，包括它自身
            ===(完全相等  类型和值都相等)
                - 全等运算符，用来比较两个值是否全等
                - 它不会进行自动的类型转换，如果两个值的类型不同直接返回false
                - null和undefined进行全等比较时会返回false

            !=
                - 不等，用来检查两个值是否不相等
                - 会自动的进行类型转换
            !==
                - 不全等，比较两个值是否不全等
                - 不和自动的类型转换
        */
        let result = 1 == 1 // true
        result = 1 == 2 // false
        result = 1 == '1' // true
        result = true == "1" // true

        result = null == undefined // true
        result = NaN == NaN // false

        result = 1 === "1" // false
        result = null === undefined // false

        result = 1 != 1 // false
        result = 1 != "1" // false
        result = 1 !== "1" // true

        console.log(result)
        
    </script>
```

## 9.条件运算符(三元运算符)

```html
    <title>条件运算符</title>
    <script>
        /* 
            条件运算符
                条件表达式 ? 表达式1 : 表达式2
                - 执行顺序：
                    条件运算符在执行时，会先对条件表达式进行求值判断，
                        如果结果为true，则执行表达式1
                        如果结果为false，则执行表达式2
        */

        // false ? alert(1) : alert(2)

        let a = 100
        let b = 200
        // a > b ? alert('a大！') : alert("b大！")
        let max = a > b ? a : b //返回2者之间的较大值

        alert(max)

    </script>
```

## 10.运算符的优先级

```html
    <title>运算符的优先级</title>
    <script>
        /* 
            和数学一样，JS中的运算符也有优先级，比如先乘除和加减。

            可以通过优先级的表格来查询运算符的优先级
                https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence
                
                - 在表格中位置越靠上的优先级越高，优先级越高越先执行，优先级一样自左向右执行
                    优先级我们不需要记忆，甚至表格都不需要看
                    因为()拥有最高的优先级，使用运算符时，如果遇到拿不准的，可以直接通过()来改变优先级即可
        */
        let a = 1 + 2 * 3 // 7
        a = (1 && 2) || 3
        console.log(a)
    </script>
```

# 四、流程控制

## 1.代码块

**let和var的区别之一**

![image-20221202131232756](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221202131232756.png)

## 2.流程控制语句

![uTools_1669958238315](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669958238315.png)

## 3.条件判断

### (1).if语句

![uTools_1669958596177](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669958596177.png)

## 4.条件分支

### (1).if-else语句|&&if-else if -else语句

```css
        /* 
            if-else语句
            - 语法：
                if(条件表达式){
                    语句...
                }else{
                    语句...
                }

            - 执行流程：
                if-else执行时，先对条件表达式进行求值判断，
                    如果结果为true 则执行if后的语句
                    如果结果为false 则执行else后的语句

            if-else if-else语句：
            - 语法：
                if(条件表达式){
                    语句...
                }else if(条件表达式){
                    语句...
                }else if(条件表达式){
                    语句...
                }else if(条件表达式){
                    语句...
                }else{
                    语句...
                }
            - 执行流程：
                if-else if-else语句，会自上向下依次对if后的条件表达式进行求值判断，
                    如果条件表达式结果为true，则执行当前if后的语句，执行完毕语句结束
                    如果条件表达式结果为false，则继续向下判断，直到找到true为止
                    如果所有的条件表达式都是false，则执行else后的语句

                注意：(短路性质)
                    if-else if-else语句中只会有一个代码块被执行，
                        一旦有执行的代码块，下边的条件都不会在继续判断了
                        所以一定要注意，条件的编写顺序
        */
```

### (2).switch语句

```css
 /* 
                switch语句
                    - 语法：
                        switch(表达式){
                            case 表达式:
                                代码...
                                break
                            case 表达式:
                                代码...
                                break
                            case 表达式:
                                代码...
                                break
                            case 表达式:
                                代码...
                                break
                            default:
                                代码...
                                break
                        }

                    - 执行的流程
                        switch语句在执行时，会依次将switch后的表达式和case后的表达式进行全等比较
                            如果比较结果为true，则自当前case处开始执行代码
                            如果比较结果为false，则继续比较其他case后的表达式，直到找到true为止
                            如果所有的比较都是false，则执行default后的语句

                    - 注意：
                        当比较结果为true时，会从当前case处开始执行代码
                            也就是说case是代码执行的起始位置
                        这就意味着只要是当前case后的代码，都会执行
                        可以使用break来避免执行其他的case

                    - 总结
                        switch语句和if语句的功能是重复，switch能做的事if也能做，反之亦然。
                            它们最大的不同在于，switch在多个全等判断时，结构比较清晰
            
            */
```

## 5.循环语句

### (1).while

```css
/*
                - while语句
                    - 语法：
                        while(条件表达式){
                            语句...
                        }

                    - 执行流程：
                        while语句在执行时，会先对条件表达式进行判断，
                            如果结果为true，则执行循环体，执行完毕，继续判断
                            如果为true，则再次执行循环体，执行完毕，继续判断，如此重复
                            知道条件表达式结果为false时，循环结束

 			通常编写一个循环，要有三个要件
                	1.初始化表达式（初始化变量）
                	2.条件表达式（设置循环运行的条件）
                	3.更新表单式（修改初始化变量）

        初始化表达式
        let a = 0

        条件表达式
        while(a < 3){
        console.log(a)

        更新表达式
         a++
*/
```

**while(1)在java'和JavaScript中的区别**

- **Java里while(1)是非法的，因为java强制要求while()里面的条件表达式必须是boolean型，而不能是int。**

- **在JavaScript中也是可以的，因为1会自动转为布尔值true。C/C++里用while(1)也是可以的，和while(true)等价。**

### (2).do-while

```css
/*
	            do-while循环
                - 语法：
                    do{
                        语句...
                    }while(条件表达式)

                - 执行顺序：
                    do-while语句在执行时，会先执行do后的循环体，
                        执行完毕后，会对while后的条件表达式进行判断
                        如果为false，则循环终止
                        如果为true，则继续执行循环体，以此类推

                    和while的区别：
                        while语句是先判断再执行
                        do-while语句是先执行再判断

                        实质的区别：
                            do-while语句可以确保循环至少执行一次
*/
```

### (3).for语句(js中用的最多的)

#### ①for

```css
/*
	for循环
                - for循环和while没有本质区别，都是用来反复执行代码
                - 不同点就是语法结构，for循环更加清晰
                - 语法：
                    for(①初始化表达式; ②条件表达式; ④更新表达式){
                        ③语句...
                    }

                - 执行流程：
                    ① 执行初始化表达式，初始化变量
                    ② 执行条件表达式，判断循环是否执行（true执行，false终止）
                    ③ 判断结果为true，则执行循环体
                    ④ 执行更新表达式，对初始化变量进行修改
                    ⑤ 重复②，知道判断为false为止

                - 初始化表达式，在循环的整个的生命周期中只会执行1次
                - for循环中的三个表达式都可以省略
                - 使用let在for循环的()中声明的变量是局部变量，只能在for循环内部访问
                    使用var在for循环的()中声明的变量可以在for循环的外部访问


                - 创建死循环的方式：
				-死循环的运用场景:例如游戏场景下,当前人物死了等待下一局才能复活，
                    while(1){}
                    for(;;){}
*/
```

#### ②for练习(还有如何进行代码优化)

```javascript
	   // 求100以内所有3的倍数（求它们个数和总和）
        let count = 0 // 计数器
        let result = 0 // 用来存储计算结果（累加结果）

        for(let i=1; i<=100; i++){
             获取3的倍数
       		if(i % 3 === 0){
                 count++
                 result += i
             }
         }

        //进行代码优化
        for(let i=3; i<=100; i+=3){
            count++
            result += i
        }
        
        console.log(`3的倍数一共有${count}个，总和为${result}`)
```

##### **1.个十百位**

```java
java中求个十百:
    public class Demo1 {
    public static void main(String[] args) {
        int mm = 123;
        System.out.println( mm % 10 +"个位数");//3
        System.out.println( mm / 10 % 10 +"十位数");//2
        System.out.println( mm / 100 % 10 +"百位数");//1
    }
}
js中:
	let num3 = parseInt(i / 100);//百位
            let num2 = parseInt((i - num3 * 100) / 10);//十位   parseInt((i%100)/10);也可以
            let num1 = i % 10;//个位

造成这种差别的原因是js计算出来的数据会带小数,可以用parseInt()进行取整
```

##### **2.1000以内的水仙花树**

```javascript
1.法一(运算)       
    	for (let i = 100; i < 1000; i++) {
            let num3 = parseInt(i / 100);//百位
            // let num2 = parseInt((i - num3 * 100) / 10);//十位   parseInt((i%100)/10);也可以
            let num2 = parseInt((i % 100) / 10);
            let num1 = i % 10;//个位
            let sum = (num3 ** 3 + num2 ** 3 + num1 ** 3);//幂运算的运用
            if (sum === i) {
                console.log(`这个数是水仙花数` + i);
            }
        }
2.法二(通过索引取得每一位数字)
  		for(let i=100; i<1000; i++){
            let strI = i + ""//将数值转化为字符串
            if(strI[0] ** 3 + strI[1] ** 3 + strI[2] ** 3 === i){//通过索引取得每一位数字,java中要单独创建字符串类型
                console.log(i)
            }
        }
```

##### 3.质数

```javascript
        let num = +prompt("请输入一个大于1的整数：")

        // 用来记录num的状态，默认为true，num是质数
        let flag = true

        for (let i = 2; i < num; i++) {
            if (num % i === 0) {
                // 如果num能被i整除，说明num一定不是质数   
                // 当循环执行时，如果从来没有进入过判断（判断代码没有执行），则说明9是质数
                // 如果判断哪怕只执行了一次，也说明 9 不是质数  
                flag = false
            }
        }
        if (flag) {
            alert(`${num}是质数！`)
        } else {
            alert(`${num}不是质数！`)
        }
```

**求100以内的质数**

![uTools_1670162341394](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670162341394.png)

## 6.循环的嵌套

### 1.循环输出的换行问题

- 使用document.write()输出到网页中时要换行使用<br>
- ![uTools_1670159340350](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670159340350.png)
- 使用console.log()打印到控制台时要换行用/n
- ![uTools_1670159431506](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670159431506.png)
- 类似的打印空格网页中&nbsp,控制台\t

### 2.打印图形

```javascript
            /* 
            在循环中也可以嵌套其他的循环

            希望在网页中打印出如下图形
                *****
                *****
                *****
                *****
                *****


                *     j<1    i=0
                **    j<2    i=1
                ***   j<3    i=2
                ****  j<4    i=3
                ***** j<5    i=4


                ***** j<5   i=0
                ****  j<4   i=1
                ***   j<3   i=2
                **
                *

            当循环发生嵌套时，外层循环每执行一次，内层循环就会执行一个完整的周期
            可以理解成外层控制高,内层控制宽
        */
            // 这个for循环，可以用来控制图形的高度
            for (let i = 0; i < 5; i++) {
                // 创建一个内层循环来控制图形的宽度
                for (let j = 0; j < 5; j++) {
                    document.write("*&nbsp;&nbsp;")
                }

                document.write("<br>")
            }

            for (let i = 0; i < 5; i++) {
                for (let j = 0; j < 5 - i; j++) {
                    document.write("*&nbsp;&nbsp;")
                }

                document.write("<br>")
            }

            document.write("<hr>")

            for (let i = 0; i < 5; i++) {
                for (let j = 0; j < i + 1; j++) {
                    document.write("*&nbsp;&nbsp;")
                }

                document.write("<br>")
            }
```

### 3.打印乘法口诀

```javascript
       //通过span控制宽度
		<style>
            span{
                display: inline-block;
                width: 100px;
            }

        </style>
		   // 创建一个外层循环，控制图形高度
            for (let i = 1; i <= 9; i++) {
                // 创建内层循环控制图形的宽度
                for (let j = 1; j < i + 1; j++) {
                    document.write(`<span>${j} × ${i} = ${i*j}</span>`);
                }
                // 打印换行
                document.write("<br>");
            }
```

### 4.等腰三角形

```javascript
        for (let i = 1; i <= 5; i++) {  //i=1
            // 打印空格(倒三角)
            for (let j = 1; j <= 5 - i; j++) { //i=1时 j=4打印4个空格
                document.write("&nbsp;&nbsp;")
            }

            // 打印点
            for (let k = 1; k <= 2 * i - 1; k++) { //i=1时  k=1打印一个1  
                document.write("1")
            }

            // 打印换行
            document.write("<br/>")
        }
```

## 7.break和continue

```html
        <script>
            /* 
            break和continue
                - break
                    - break用来终止switch和循环语句
                    - break执行后，当前的switch或循环会立刻停止
                    - break会终止离他最近的循环

                - continue
                    - continue用来跳过当次循环
                    - continue会终止离他最近的循环
        */
		 //i等于3的那次结束循环
          for (let i = 0; i < 5; i++) {
            	if (i === 3) {
               	 	break
            	}
            	console.log(i)
        	}
            
            //内层循环为1的时候内层循环结束
            for (let i = 0; i < 5; i++) {
                console.log(i)
                for(let j=0; j<5; j++){
                    if(j === 1) break
                    console.log('内层循环--->', j)
                }
            }
           
           //跳过i等于3的那一次
           for (let i = 0; i < 5; i++) {
            if (i === 3) {
                continue
            }
            console.log(i)
        }

            //内层循环为1的时候跳过那一次循环
            for (let i = 0; i < 5; i++) {
                console.log(i)
                for (let j = 0; j < 5; j++) {
                    if (j === 1) continue
                    console.log("内层循环--->", j)
                }
            }

        </script>
```

### 1.对质数进行代码优化

```javascript
     	   //一般性能优化都改动内层循环,外层循环的次数基本是固定的
           //问题：如何修改代码，提升其性能
                    36
                    1 36
                    2 18
                    3 12
                    4 9
                    6 6
            //我们可以发现找到开根号的36时就找不到新的质数了,可以得到-->找到根号n就可以了(<= 根号n)
      
        console.time();//开启定时器
        for (let i = 2; i < 1000000; i++) {
            let flag = true;
            for (let j = 2; j <= i ** .5; j ++) {//进行了开方的处理,效率提升十倍以上,偶数不可能是质数也可以进行优化
                if (i % j === 0) {
                    flag = false;
                    break;
                }
            }
            if (flag = true) {
                console.log(i)
            }
        }
        console.timeEnd();//关闭定时器

//还有一种优化的方法效率较低(去除偶数的方法)
let num = parseInt(prompt("请输入一个整数"))
boolean isPrime = true;
if(num ==1 || num %2 ==0 && num !=2 ){
	isPrime = false;
}else{
	for(int i =3; i<num; i +=2){//2,3都是素数，不进入循环
		if( num % i == 0){
			isPrime = false;
			break;
		}
	}
}
if( isPrime){
	System.out.println(num +"是素数");
}else{
	System.out.println(num + "不是素数");
}

//将这俩个算法结合
        for (let i = 2; i < 1000000; i++) {
            let flag = true;
            if (i == 1 || i % 2 == 0 && i != 2) {
                flag = false;
            } else {
                for (let j = 3; j <= i ** .5; j += 2) {
                    if (i % j === 0) {
                        flag = false;
                        break;
                    }
                }
            }
            if (flag) {
                console.log(i)
            }

        }

```

## 8.js中的字符串输入函数prompt() 

```css
/*
	 prompt() 可以用来获取用户输入的内容
   	 	它会将用户输入的内容以字符串的形式返回，可以通过变量来接收
*/
```

## 9.判断是否为NaN  isNaN()函数

**例子:**

```html
        <script>
            /* 
                - 练习1：
                    编写一个程序，获取一个用户输入的整数。然后通过程序显示这个数是奇数还是偶数。
            */
            // 编写一个程序，获取一个用户输入的整数
            // let num = +prompt("请输入一个整数")
            let num = parseInt(prompt("请输入一个整数"))

            // 验证一下，用户的输入是否合法，只有是有效数字时，我们才检查它是否是偶数
            // 我们不能使用==或===来检查一个值是否是NaN
            // 可以使用isNaN()函数来检查一个值是否是NaN
            if (isNaN(num)) {
                alert("你的输入有问题，请输入整数！")
            } else {
                // 然后通过程序显示这个数是奇数还是偶数。
                if (num % 2 === 0) {
                    alert(`${num} 是偶数！`)
                } else {
                    alert(`${num} 是奇数！`)
                }
            }
        </script>
```

## 9.判断是否输入的是小数

**if(num%1 !== 0)  //对1取余数不等于0**

# 五、对象

## 1.对象

```html
<script>
        /* 
            数据类型：
                原始值
                    1.数值 Number
                    2.大整数 BigInt
                    3.字符串 String
                    4.布尔值 Boolean
                    5.空值 Null
                    6.未定义 Undefined
                    7.符号 Symbol
                对象
                    - 对象是JS中的一种复合数据类型，
                        它相当于一个容器，在对象中可以存储各种不同类型数据
        */

        // 创建对象
        let obj = Object()

        /*
            对象中可以存储多个各种类型的数据
                对象中存储的数据，我们称为属性
            
            向对象中添加属性：
                对象.属性名 = 属性值

            读取对象中的属性
                对象.属性名
                - 如果读取的是一个对象中没有的属性
                    不会报错而是返回undefined
             
            修改属性
        		obj.name = "Tom sun"
        		
        	// 删除属性
        		delete obj.name
        */

        obj.name = "孙悟空"
        obj.age = 18
        obj.gender = "男"
        console.log(obj.name)
        
    </script>
```

## 2.对象的属性

```html
<script>
    /*
            属性名
                - 通常属性名就是一个字符串，所以属性名可以是任何值，没有什么特殊要求
                    但是如果你的属性名太特殊了，不能直接使用，需要使用[]来设置
                    虽然如此，但是我们还是强烈建议属性名也按照标识符的规范命名
     */
    					  let obj = Object();
                            obj.name = "孙悟空"
        				  obj.if = "哈哈" // 不建议
        				  obj.let = "嘻嘻"// 不建议
        				  obj["1231312@#@!#!#!"] = "呵呵"// 不建议
    
    
    
	/*
                - 也可以使用符号（symbol）作为属性名，来添加属性
                    获取这种属性时，也必须使用symbol
                  使用symbol添加的属性，通常是那些不希望被外界访问的属性(相当于一把钥匙)
     */
    						let obj = Object();//对象
					        let mySymbol = Symbol()//符号
                              mySymbol.name="hhh"//这样是添加不进去的
        					// 使用symbol作为属性名
    						//要用对象名[符号名(钥匙名)]="添加的属性"才能添加进去
        					obj[mySymbol] = "通过symbol添加的属性"
        					console.log(obj[mySymbol])//访问时也要用  对象名[符号名(钥匙名)]
    
    
				
       /*  - 使用[]去操作属性时，可以使用变量  */
                	    let obj = Object();
                        obj.age = 18
        			   obj["gender"] = "男"
        			   let str = "address"
       				   obj[str] = "花果山" // 等价于 obj["address"] = "花果山"
                        obj.str = "哈哈" // 使用.的形式添加属性时，不能使用变量,这个代码只会添加一个新的属性
    
    

           /* 
           	属性值
                - 对象的属性值可以是任意的数据类型，也可以是一个对象
    		*/
    			let obj = Object();
    		    obj.a = 123
        		obj.b = 'hello'
        		obj.c = true
        		obj.d = 123n
        		obj.f = Object()//将一个对象赋值给对象里的属性f
        		obj.f.name = "猪八戒"
        		obj.f.age = 28
        		console.log(obj.f.name)//取用的时候就用 大对象.小对象.属性
    
    
		/* 
            使用typeof检查一个对象时，会返回object
         */
            console.log(typeof obj)
        	console.log(typeof obj.f);//这个也会返回object    对象的对象也是对象属性
         /* 
            in 运算符
                - 用来检查对象中是否含有某个属性
                - 语法 属性名 in obj
                - 如果有返回true，没有返回false
        */
            console.log("name" in obj)
    	   console.log("name" in obj.f);//检查对象的对象也是会返回true
</script>
```



## 3.对象的字面量

![uTools_1670241750939](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670241750939.png)



## 4.枚举属性(for-in)

```html
    <script>
        /* 
            枚举属性，指将对象中的所有的属性全部获取

            for-in语句
            - 语法：
                for(let propName(命名) in 对象){
                    语句...
                }

            - for-in的循环体会执行多次，有几个属性就会执行几次，
                每次执行时，都会将一个属性名赋值给我们所定义的变量
            
            - 注意：并不是所有的属性都可以枚举，比如 使用符号添加的属性
        */

        let obj = {
            name:'孙悟空',
            age:18,
            gender:"男",
            address:"花果山",
            [Symbol()]:"测试的属性" // 符号添加的属性是不能枚举的
        }

        for(let propName in obj){
            console.log(propName, obj[propName])
        }

    </script>
```

## 5.可变类型(面试题)

### 1.原始值不可变

![uTools_1670243374121](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670243374121.png)



### 2.对象在内存中的真正模型

![uTools_1670242569319](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670242569319.png)

**对象说的可变类型其实本质上也是不可改变的,原始值还是会存在,它只是改变了属性值指向的内存地址(指向了一个新的内存地址)，也就是我们说的修改属性或者增加删除属性**



### 3.创建俩个对象时

![uTools_1670242990051](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670242990051.png)



### 4.把一个对象赋值给新对象

![uTools_1670243129644](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670243129644.png)



### 5.总结

![uTools_1670244678312](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670244678312.png)

```html
    <script>
        /* 
            - 原始值都属于不可变类型，一旦创建就无法修改
            - 在内存中不会创建重复的原始值

        */
        let a = 10 
        let b = 10
        a = 12 // 当我们为一个变量重新赋值时，绝对不会影响其他变量

        // console.log("a =", a)
        // console.log("b =", b)
        
        /* 
            - 对象属于可变类型
            - 对象创建完成后，可以任意的添加删除修改对象中的属性
            - 注意：
                - 当对两个对象进行相等或全等比较时，比较的是对象的内存地址
                - 如果有两个变量同时指向一个对象，
                    通过一个变量修改对象时，对另外一个变量也会产生影响
        */
       
        // let obj = {name:"孙悟空"}
        let obj = Object()
        obj.name = "孙悟空"
        obj.age = 18

        let obj2 = Object()
        let obj3 = Object()


        // console.log(obj2 == obj3) // false

        let obj4 = obj

        obj4.name = "猪八戒" // 当修改一个对象时，所有指向该对象的变量都会收到影响

        console.log("obj", obj)
        console.log("obj4", obj4)
        console.log(obj === obj4)

    </script>
```

![uTools_1678282588726](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678282588726.png)



## 6.改变量和改对象(const的使用)

![uTools_1670246928666](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670246928666.png)

![uTools_1670247036342](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670247036342.png)

```css
            /* 
                修改对象
                    - 修改对象时，如果有其他变量指向该对象
                        则所有指向该对象的变量都会受到影响

                修改变量
                    - 修改变量时，只会影响当前的变量

                在使用变量存储对象时，很容易因为改变变量指向的对象，提高代码的复杂度
                    所以通常情况下，声明存储对象的变量时会使用const

                注意：
                     const只是禁止变量被重新赋值，对对象的修改没有任何影响
				   换句话说 const声明的变量的那个值(内存地址)只能被赋值一次
            */
```

```html
<script>
   let obj2={}
   obj2.name = "猪八戒" // 这是修改对象(可能影响很多变量,指向该对象的变量都会受到影响)
   obj2 = null // 这是修改修改变量(只影响自己)
    
    
   const obj ={ //用了const就是禁止变量被修改,就是我们不希望对象的指向被复杂化
        name:"猪八戒"
    }
    obj.name="孙悟空"//对象内部的属性是可以被改变的
</script>
```

![uTools_1678282738770](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678282738770.png)

**提示我们不能对常量赋值一个变量**



## 7.方法

```html
 <script>
        /* 
            方法（method）
                - 当一个对象的属性指向一个函数，那么我们就称这个函数是该对象的方法
                  	调用函数就称为调用对象的方法
        */

        let obj = {}

        obj.name = "孙悟空"
        obj.age = 18

        // 函数也可以成为一个对象的属性
        obj.sayHello = function () {
            alert("hello")
        }

        obj.sayHello()//调用obj的sanHello方法

        console.log(obj)//调用console的log方法

        document.write()//调用document的write方法

        String()//调用String函数
     
     	fn()//调用fn函数
        //方法和函数最大的区别其实就是称呼上的区别,.就是调用对象的方法,直接调用就是函数

    </script>
```

## 8.利用对象来存储相反的值

```java
     // 利用对象来存储值
        const reObj = {
            ArrowUp: "ArrowDown",
            ArrowDown: "ArrowUp",
            ArrowLeft: "ArrowRight",
            ArrowRight: "ArrowLeft",
        }

		reObj[ArrowUp] //此时取到的值为ArrowDown,这个用法在键盘事件中很常用
```



# 六、函数

## 1.函数简介

![uTools_1670322353018](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670322353018.png)

## 2.函数的创建方式

```html
    <script>
        /* 
            函数的定义方式：
                1.函数声明
                    function 函数名(){
                        语句...
                    }

                2.函数表达式
                    const 变量 = function(){
                        语句...
                    }

                3.箭头函数
                    () => {
                        语句...
                    }
                    
                   const fn4 = () =>  //当箭头函数后面只有一行代码的时候可以省略大括号
                    
        */

        function fn(){
            console.log("函数声明所定义的函数~")
        }

        const fn2 = function(){
            console.log("函数表达式")
        }

        const fn3 = () => {
            console.log("箭头函数")
        }

        const fn4 = () => console.log("箭头函数")//当函数只有一行代码的时候可以省略大括号
        
        console.log(typeof fn)
        console.log(typeof fn2)
        console.log(typeof fn3)
        console.log(typeof fn4)
        fn4()
       
    </script>
```

## 3.函数的参数

```html
    <script>
        /* 
            形式参数
                - 在定义函数时，可以在函数中指定数量不等的形式参数（形参）
                - 在函数中定义形参，就相当于在函数内部声明了对应的变量但是没有赋值❤

            实际参数
                - 在调用函数时，可以在函数的()传递数量不等的实参
                - 实参会赋值给其对应的形参
                - 参数：
                    1.如果实参和形参数量相同，则对应的实参赋值给对应的形参
                    2.如果实参多余形参，则多余的实参不会使用
                    3.如果形参多余实参，则多余的形参为undefined

                - 参数的类型
                    - JS中不会检查参数的类型，可以传递任何类型的值作为参数
                    - 所以我们在写函数的时候自己要检查传入的参数类型以及做好类型转换(避免js不检查类型带来的错误)
                    - 因为这个所以传入的类型不检查可能导致我们函数的功能不一样
                    
                - 定义参数却不传参
                	- js调用一个带参数的函数，却不给参数
                		- 不给的参数都是undefined

            1.函数声明
                    function 函数名([参数]){
                        语句...
                    }

            2.函数表达式
                const 变量 = function([参数]){
                    语句...
                }

            3.箭头函数
                ([参数]) => {
                    语句...
                }
        */
    </script>
```

**例子:如果你俩个形参写成一样的**

```html
    <script>
        function fn(a, a) {//相当于3覆盖掉了2
            console.log(a);//最后输出3
            console.log(a);//最后输出3
        }

        fn(2, 3)
        //所以我们要避免这种事情 也可以开启严格模式那系统提示报错
    </script>
```

## 4.箭头函数的参数和参数默认值

```html
    <script>
        const fn = (a, b) => {
            console.log("a =", a);
            console.log("b =", b);
        }
        
        // 当箭头函数中只有一个参数时，可以省略()。建议不省略
        const fn2 = a => {
            console.log("a =", a);
        }
        //相当于
        const fn2 = function(a){ console.log("a =", a);}
        
        // fn2(123)

        // 定义参数时，可以为参数指定默认值
        // 默认值，会在没有对应的实参时生效
        const fn3 = (a=10, b=20, c=30) => {
            console.log("a =", a);//1
            console.log("b =", b);//2
            console.log("c =", c);//30
        }

        fn3(1, 2)

    </script>
```

## 5.使用对象作为参数

```html
    <script>
        function fn(a) {
           	// a = {} // 修改变量时，只会影响当前的变量
            //a.name = "猪八戒" // 修改对象时，如果有其他变量指向该对象则所有指向该对象的变量都会受到影响
            console.log(a)
        }

        // 对象可以作为参数传递
        let obj = { name: "孙悟空" }
        
        // 传递实参时，传递并不是变量本身，而是变量中存储的值
        fn(obj)
        console.log(obj)//修改变量不会影响obj,修改对象会影响obj
    </script>
```

![uTools_1678283332486](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678283332486.png)

**Obj的name属性被影响了，对象作为参数传递等于改对象，可能影响多个变量**

![uTools_1678283310208](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678283310208.png)

### (1).以默认值传递和以字面量传递的差别

```javascript
        // 对象以这种形式传递时,函数每次调用，都会重新创建一个对象
        function fn1(a = { name: "黄宇" }) {
            console.log(a);
            a.name = "老鼠"
            console.log(a);
        }
        fn1();//得到的值 黄宇 老鼠
        fn1();//得到的值 黄宇 老鼠


        //对象以字面量的形式传递时,每次调用时不会重新创建对象。
	    //第二次调用函数时不会重新创建一个新的对象 带上黄宇的名字  所以第二次打印的都是老鼠
        let obj2 = { name: "黄宇" };
        function fn2(a = obj2) {
            console.log(a);
            a.name = "老鼠"
            console.log(a);
        }
        fn2()//得到的值 黄宇 老鼠
        fn2()//得到的值 老鼠 老鼠

```



## 6.以函数作为函数的参数

**主要的作用就是把一个函数的内容以参数的形式传递进另一个函数中(动态传递)**

```html
在JS中，函数也是一个对象（一等函数），别的对象能做的事情，函数也可以
	<script>
        function fn(a){
            console.log("a =", a)
            //a()  打印我是fn2 a()其实就是fn2()
        }
       
        //将fn2函数作为fn函数的参数传入
        function fn2(){
            console.log("我是fn2")
        }
        fn(fn2)
		
       	//直接在()中声明一个匿名函数作为参数
        fn(function(){
            console.log("我是匿名函数~")
         })
       
		//直接在()中声明一个箭头函数作为参数
        fn(()=>console.log("我是箭头函数"))

    </script>
```

![uTools_1678283986464](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678283986464.png)

![uTools_1678284053350](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678284053350.png)



## 7.函数的返回值

```html
        <script>
            function fn() {
                /* 
                在函数中，可以通过return关键字来指定函数的返回值
                    返回值就是函数的执行结果，函数调用完毕返回值便会作为结果返回
                
                任何值都可以作为返回值使用（包括对象和函数之类）
                    如果return后不跟任何值，则相当于返回undefined
                    如果不写return，那么函数的返回值依然是undefined

                return一执行函数立即结束
            */
                return {name:"孙悟空"} //对象当做返回值
                return ()=>alert(123)//箭头函数当作返回值
                return//不跟任何值 直接结束函数
            }
            
            console.log("result =", result)
        </script>
```

![uTools_1678284191234](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678284191234.png)

## 8.箭头函数的返回值

```html
    <script>
        /* 
            箭头函数的返回值可以直接写在箭头后
                如果直接在箭头后设置对象字面量为返回值时，对象字面量必须使用()括起来
        */
        
        //箭头函数只有一句语句时
        const sum = (a, b) => a + b  等价于 const sum = function fn(a, b) => { return a + b }

        const fn = () => ({ name: "孙悟空" })//因为箭头后面可以跟着代码块的{}以及对象的{}
    </script>
```

**箭头函数和函数**

![uTools_1676103044183](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676103044183.png)

## 9.作用域

```html
<script>
            /* 
            作用域（scope）
                - 作用域指的是一个变量的可见区域
                - 作用域有两种：
                    全局作用域
                        - 全局作用域在网页运行时创建，在网页关闭时消耗
                        - 所有直接编写到script标签中的代码都位于全局作用域中
                        - 全局作用域中的变量是全局变量，可以在任意位置访问

                    局部作用域
                        - 块作用域
                            - 块作用域是一种局部作用域
                            - 块作用域在代码块执行时创建，代码块执行完毕它就销毁
                            - 在块作用域中声明的变量是局部变量，只能在块内部访问，外部无法访问
        */
  
        {
             {
                let b = "sdasd"
             }
               console.log(b);//这种情况也是访问不到的,小作用域的变量在大作用域无法访问(只有大作用域的变量能在小作用域访问)
        }
</script>
```

## 10.函数作用域

```css
        /* 
            函数作用域
                - 函数作用域也是一种局部作用域
                - 函数作用域在函数调用时产生，调用结束后销毁
                - 函数每次调用都会产生一个全新的函数作用域(每次调用互不影响)
                - 在函数中定义的变量是局部变量，只能在函数内部访问，外部无法访问
        */
```

**js中的函数时可以是可以嵌套的,而java中的方法是不可以嵌套的**

## 11.作用域链(就近原则)

```html
    <script>
        /* 
            作用域链
                - 当我们使用一个变量时，
                    JS解释器会优先在当前作用域中寻找变量，如果找到了则直接使用(就近原则)
                        如果没找到，则去上一层作用域中寻找，找到了则使用
                        如果没找到，则继续去上一层寻找，以此类推
                        如果一直到全局作用域都没找到，则报错 xxx is not defined
        */
        let a = 10

        {
            let a = "第一代码块中的a"
            {
                let a = "第二代码块中的a"
                console.log(a)
            }
        }
        //最后输出 第二代码块中的a

        //函数中的变量也是就近原则
        let b = 33
        function fn(){
            let b = 44

            function f1(){
                let b = 55
                console.log(b)
            }
            f1()
        }
        
        fn()//55

    </script>
```

## 12.window对象

```html
 <script>
        /* 
            Window对象
                - 在浏览器中，浏览器为我们提供了一个window对象，可以直接访问
                - window对象代表的是浏览器窗口，通过该对象可以对浏览器窗口进行各种操作
                    除此之外window对象还负责存储JS中的内置对象和浏览器的宿主对象
                - window对象的属性可以通过window对象访问，也可以直接访问
                - 函数就可以认为是window对象的方法
                - 其实可以理解成全局作用域就是这个window
        */
     
        window.a = 10 // 向window对象中添加的属性会自动成为全局变量 相当于let a = 10
     
        /* 
            var 用来声明变量，作用和let相同，但是var不具有块作用域
                - 在全局中使用var声明的变量，都会作为window对象的属性保存
                - 使用function声明的函数，都会作为window的方法保存(另外俩种声明函数的方式是不会作为window的方法保存的)
                - 使用let声明的变量不会存储在window对象中，而存在一个秘密的小地方(无法访问),发生变量名冲突时优先访问这个地方
                - var虽然没有块作用域，但有函数作用域
        */

        function fn2() {
            var d = 10 // var虽然没有块作用域，但有函数作用域,在函数里声明的var变量全局变量中也访问不到
            d = 10 // 在局部作用域中，如果没有使用var或let声明变量，则变量会自动成为window对象的属性 也就是全局变量
            //就相当于 window.d
        }

    </script>
```

**扩展:window和object的关系**

window 是浏览器内置的全局对象，window 是 Object 创造出来的，通过原型链的方式继承了 Object 的属性和方法

**JavaScript中const、var、不带var和let区别**

- 带var定义的变量只有函数内作用域和全局作用域,作为全局变量时挂载在window对象上,**configurable为false**。**var定义的变量可以修改，如果不初始化会输出undefined，不会报错。**
- 不带var定义的变量,全局作用域**,挂载在window**对象上,**configurable为true**
- let定义的变量具有块级作用域,**不能重复定义**,configurable为false，**函数内部使用let定义后，对函数外部无影响。**
- const拥有let所有性质,但**const不能被直接修改,必须被初始化**,configurable为false
- **用var、let、const命名的变量在加载时会提前准备好内存空间,提升代码性能。而不用就是相当是声明了window对象，运行时轮到这行代码时每一次还要单独分配内存空间。**
- ![uTools_1678284653677](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678284653677.png)

## 13.提升 (js中的提升)  var和let区别(面试题)

```html
    <script>
        /* 
            变量的提升
                - 使用var声明的变量，它会在所有代码执行前被声明(只是声明没有赋值,没用这个)
                    所以我们可以在变量声明前就访问变量(let不行)

            函数的提升
                - 使用函数声明创建的函数，会在其他代码执行前被创建,提前就执行了(function开头,有点用)
                    所以我们可以在函数声明前调用函数

            let声明的变量实际也会提升，但是在赋值之前解释器禁止对该变量的访问
            提升优先级的目的是为了预留内存空间,减少重新分配内存的次数,提升代码性能。

		   变量和函数的提升同样适用于函数作用域。就是在把变量声明提到函数第一行去执行
        */
    </script>
```

## 14.练习(面试题)

```html
<script>
	1. 
      var a = 1
        function fn() {
            a = 2 //函数作用域没有a去外层找到a,重新赋值为2 因为只有一个a 改完了都输出a
            console.log(a) // 2
        }
        fn()
        console.log(a) // 2 
    
	2.
       // 变量和函数的提升同样适用于函数作用域  var a 提到函数第一行执行
       var a = 1
        function fn() {
            console.log(a) //undefined 此时只有var a 没赋值 所以输出undefined
            var a = 2
            console.log(a) // 2
        }
        fn()
        console.log(a) // 1 局部变量不影响外面的
    
    3.
      // 定义形参就相当于在函数中声明了对应的变量，但是没有赋值
      var a = 1
        function fn(a) {
            console.log(a) //undefined(定义了形参就是声明了变量但是没赋值)
            a = 2
            console.log(a) // 2
        }
        fn()
        console.log(a) // 1 
    
    4.
      var a = 1
        function fn(a) {
            console.log(a) //10
            a = 2
            console.log(a) // 2
        }
        fn(10)
        console.log(a) // 1
    
    5.
      var a = 1
        function fn(a) {//这个a是形参
            console.log(a) //1
            a = 2
            console.log(a) // 2
        }
        fn(a)//这个a是实参a=1
        console.log(a) // 1 
    
    6.
       console.log(a)  // 执行alert(2)  var a没用  function a(){}会提升加赋值
        var a = 1
        console.log(a) // 1
        function a() {
            alert(2)
        }
        console.log(a) // 1
        var a = 3
        console.log(a) // 3
        var a = function () {
            alert(4)
        }
        console.log(a) // 执行alert(4)
        var a //没影响 var a早就提升完了
        console.log(a) // 执行alert(4)
    
    
    	//先执行的是提升 赋值是后执行的
    	/*函数会提升加赋值  var只会先提升*/
</script>
```

## 15.debug

- 首先用 debugger在代码中打断点(或者在chrome控制台源代码中左键单击添加断点)
- 添加监视对象(变量或者函数)
- F5刷新页面,此时可以开始执行断点程序
- F9进行单步调试

## 16.立即执行函数

var会覆盖上面的变量,let就稍微好点。var声明的变量要想有块作用域就需要用function函数来创建(这种方式不完美)。

let可以直接加上代码块{}来创建块作用域。var用立即执行函数来解决，为了解决兼容性问题

```html
    <script>
        /* 
            在开发中应该尽量减少直接在全局作用域中编写代码！

            所以我们的代码要尽量编写的局部作用域

            如果使用let声明的变量，可以使用{}来创建块作用域

        */

        {
            let a = 10
        }

        //希望可以创建一个只执行一次的匿名函数

        /* 
            立即执行函数（IIFE）
                - 立即执行一个匿名的函数，并它只会调用一次
                - 可以利用IIFE来创建一个一次性的函数作用域，避免变量冲突的问题
        */
        (function(){
            let a = 10
            console.log(111)
        }());
        
        //也可以写成这样,但是上面那种比较规范
        (function(){
            let a = 20
            console.log(222)
        })()

    </script>
```

## 17.this

```html
        <script>
            /*  
            this
                - 函数在执行时，JS解析器每次都会传递进一个隐含的参数
                - 这个参数就叫做 this
                - this会指向一个对象
                    - this所指向的对象会根据函数调用方式的不同而不同
                        1.以函数形式调用时，this指向的是window(函数其实就是window的方法)
                        2.以方法的形式调用时，this指向的是调用方法的对象
                        ...

                - 通过this可以在方法中引用调用方法的对象
                -一个对象调用了这个方法,this就指代这个对象的地址值(调用者就是对象)
        */

            function fn() {
                console.log(this === window) //true
                console.log("fn打印", this)
            }

            const obj3 = {
                name: "沙和尚",
                sayHello: function () {
                    console.log(this.name)
                },
            }
            const obj4 = { 
                name: "唐僧",
                sayHello: function(){
                    console.log(this.name)
                }
            }
            // 为两个对象添加一个方法，可以打印自己的名字
            obj3.sayHello()
            obj4.sayHello()
        </script>
```

**对象赋值简写**

```html
<script>
      function fn() {
          console.log("fn -->", this)
          }	
    
      //创建一个对象
    const obj = {
        name:"孙悟空",
        fn:fn//这一行的意思就是把fn函数赋值给obj对象的fn属性
    }
   //简写
    const obj = {
        name:"孙悟空",
        fn //当属性名和变量名一样时可以省略
    }
    
    // 12等价
     1.const obj = {
         name:"孙悟空",
           sayHello:function(){
                    console.log(this.name)    
           }
     }
     
    2.const obj = {
         name:"孙悟空",
           sayHello:(){//function在对象中可以省略
                    console.log(this.name)    
           }
     }
</script>
```

## 18.箭头函数的this

```html
<script>
            /* 
            箭头函数：
                ([参数]) => 返回值
            例子：
                无参箭头函数：() => 返回值
                一个参数的：a => 返回值
                多个参数的：(a, b) => 返回值

                只有一个语句的函数：() => 返回值
                只返回一个对象的函数：() => ({...})
                有多行语句的函数：() => {
                    ....    
                    return 返回值
                }

            箭头函数没有自己的this，它的this由外层作用域决定
            箭头函数的this和它的调用方式无关(创建出来是什么就是什么)
            因为箭头函数的this比较稳定,所以在开发时多用箭头函数
        */
        function fn1() {
            console.log("fn>>>", this);
        }
        const fn2 = () => {
            console.log("fn2>>>", this);//this永远执行window,和调用方式无关
        }
        fn1() //window
        fn2() //window

        const obj = {
            name:"suwukong",
            fn1:fn1,
            fn2:fn2
        }

        fn1()//obj
        fn2()//window

        const obj1 = {
            name:"suwukong",
            fn1:fn1,
            fn2:fn2,
            sayHello(){
                console.log(this.name);
                // function t(){
                //    console.log("t>>>",this); 
                // }
                // t()//以方法形式调用 window

                const t2 = ()=>{
                    console.log("t2>>>",this);
                }
                t2()//this就是obj1  因为外层作用域就是obj1
            }
        }

        obj1.sayHello()
</script>
```

## 19.严格模式

```html
    <script>

        /* 
            JS运行代码的模式有两种：
                - 正常模式
                    - 默认情况下代码都运行在正常模式中，
                        在正常模式，语法检查并不严格
                        它的原则是：能不报错的地方尽量不报错
                    - 这种处理方式导致代码的运行性能较差

                - 严格模式
                    - 在严格模式下，语法检查变得严格
                        1.禁止一些语法
                        2.更容易报错
                        3.提升了性能

                - 在开发中，应该尽量使用严格模式(这种才是其它语言的正常模式)，
                    这样可以将一些隐藏的问题消灭在萌芽阶段，
                        同时也能提升代码的运行性能
        */
        "use strict" // 全局的严格模式
        let a = 10
        console.log(a)

        function fn(){
            "use strict" // 函数的严格的模式
        }

    </script>
```

## 20.扩展

**通过js实现网页深色主题，编写代码，通过javascript：代码块保存收藏夹，每次使用时点击该收藏夹即可**

**代码：javascript:var a = document.createElement('style');a.innerHTML=`html{background-color:#fff;filter:invert(1);}img{filter:invert(1)}%60;document.head.appendChild(a)**

![image-20221211110717634](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221211110717634.png)

## 21.函数嵌套

**在js中函数是可以进行嵌套的,而java中是不可以的(只能调用其它函数)**

# 七、面向对象编程OOP

## 1.面向对象简介

- 面向对象的三大要素是封装、继承、多态
- 将对象作为程序的基本单元，将程序和数据封装其中来提高代码的复用性、灵活性以及扩展性
- 以事物为基本单位进行程序开发，只注重自身描述以及事物之间的联系

```html
    <script>
        /* 
            面向对象编程（OOP）
                1. 程序是干嘛的？
                    - 程序就是对现实世界的抽象（照片就是对人的抽象）
                2. 对象是干嘛的？
                    - 一个事物抽象到程序中后就变成了对象
                    - 在程序的世界中，一切皆对象(最重要的)
                3. 面向对象的编程
                    - 面向对象的编程指，程序中的所有操作都是通过对象来完成
                    - 做任何事情之前都需要先找到它的对象，然后通过对象来完成各种操作
                    
                - 一个事物通常由两部分组成：数据和功能
                - 一个对象由两部分组成：属性和方法
                - 事物的数据到了对象中，体现为属性
                - 事物的功能到了对象中，体现为方法

			人
                - 数据：
                    姓名
                    年龄
                    身高
                    体重

                - 功能：
                    睡
                    吃    
        
        */
       const five = {
            // 添加属性
            name:"王老五",
            age:48,
            height:180,
            weight:100,
            // 添加方法
            sleep(){
                console.log(this.name + "睡觉了~")
            },
            eat(){
                console.log(this.name + "吃饭了~")
            }
       }
       
       //知对象(对象是干什么的),拿对象(怎么拿到这个对象),用对象(这个对象有什么属性和方法)
    </script>
```

## 2.类的简介

### (1).简介

**类是对对象的抽象，对象是类的具体实现**

**类是创建对象的模板，对象是类的实例**

```html
       <script>

            /* 
                使用Object创建对象的问题：
                    1. 无法区分出不同类型的对象
                    2. 不方便批量创建对象

                在JS中可以通过类（class）来解决这个问题：
                    1. 类是对象模板，可以将对象中的属性和方法直接定义在类中
                        定义后，就可以直接通过类来创建对象
                    2. 通过同一个类创建的对象，我们称为同类对象
                        可以使用instanceof来检查一个对象是否是由某个类创建
                        如果某个对象是由某个类所创建，则我们称该对象是这个类的实例

                语法：
                    class 类名 {} // 类名要使用大驼峰命名
                    const 类名 = class {}  
                    
                通过类创建对象
                    new 类()
            */

            //const Person = class {} 不常用

            // Person类专门用来创建人的对象
            class Person{

            }

            // Dog类式专门用来创建狗的对象
            class Dog{

            }

            const p1 = new Person()  // 调用构造函数创建对象
            const p2 = new Person()

            const d1 = new Dog()
            const d2 = new Dog()

            console.log(p1 instanceof Person) // true
            console.log(d1 instanceof Person) // false

            
        </script>
```

### (2).类的属性

```html
  <script>
        /* 
            类是创建对象的模板，要创建第一件事就是定义类
        */
        class Person{
            /* 
                类的代码块，默认就是严格模式，
                    类的代码块是用来设置对象的属性的，不是什么代码都能写
            */
           name = "孙悟空" // Person的实例属性name和age p1.name
           age = 18       // 实例属性只能通过实例访问 p1.age

           static test = "test静态属性" // 使用static声明的属性，是静态属性（类属性） Person.test
           static hh = "静态属性"   // 静态属性只能通过类去访问 Person.hh
           //静态属性一般用来定义常量
        }

        const p1 = new Person()
        const p2 = new Person()

        console.log(p1)
        console.log(p2)
    </script>
```

### (3).类的方法

```html
 <script>

        class Person{

            name = "孙悟空"

            // sayHello = function(){
            // } // 添加方法的一种方式  不推荐,打印出来的时候会把方法暴露出来

            sayHello(){//这种写法就是只给外界提供接口,不暴露方法内部是怎么实现的
                console.log('大家好，我是' + this.name)
            } // 添加方法（实例方法） 实例方法中this就是当前实例

            static test(){
                console.log("我是静态方法", this)
            } // 静态方法（类方法） 通过类来调用 静态方法中this指向的是当前类

        }

        const p1 = new Person()

        console.log(p1)

        Person.test()//我是静态方法

        p1.sayHello()

    </script>
```

## 3.构造函数

```javascript
   class Person {
            // 在类中可以添加一个特殊的方法constructor
            // 该方法我们称为构造函数（构造方法）
            // 构造函数会在我们调用类创建对象时执行(new的时候执行)
            constructor(name, age, gender) {
                // 可以在构造函数中，为实例属性进行动态赋值
                // 在构造函数中，this表示当前所创建的对象
                this.name = name //参数赋值给当前对象的name属性
                this.age = age
                this.gender = gender
            }
        }
        const p1 = new Person("孙悟空", 18, "男")
        const p2 = new Person("猪八戒", 28, "男")
        const p3 = new Person("沙和尚", 38, "男")

        	console.log(p1)
	    	console.log(p1)
		    console.log(p1)
```

**java中和js中的区别**

![uTools_1670741202352](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670741202352.png)

![uTools_1670741250914](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670741250914.png)

**js中构造函数必须叫constructor                   而java的构造函数需要和类同名即可**

## 4.面向对象的三大特性

### (1).封装 

```css
/* 
            面向对象的特点：
                封装、继承和多态

            1.封装
                - 对象就是一个用来存储不同属性的容器
                - 对象不仅存储属性，还要负责数据的安全
                - 直接添加到对象中的属性，并不安全，因为它们可以被任意的修改
                - 如何确保数据的安全：
                    1.私有化数据
                        - 将需要保护的数据设置为私有，只能在类内部使用
                        - 私有属性要先声明才能使用
                    2.提供setter和getter方法来开放对数据的操作
                        - 属性设置私有，通过getter setter方法操作属性带来的好处
                            1. 可以控制属性的读写权限
                            2. 可以在方法中对属性的值进行验证

                - 封装主要用来保证数据的安全
                - 实现封装的方式：
                    1.属性私有化 加#
                    2.通过getter和setter方法来操作属性(js提供的简化方法,推荐)
                        get 属性名(){
                            return this.#属性
                        }

                        set 属性名(参数){
                            this.#属性 = 参数
                        }
                    调用的时候可以直接 p1.参数进行操作(但是本质上还是在调用方法修改)
                    3.以前的写法,其它语言的写法,这种一定要调用方法才能修改
                   		例:
                   			getName(){
                   				return this.#name;
                   			}
                   			setName(name){
                   				this.#name=name;
                   			}
                   调用时的语法 p1.setName(新参数)	p1.getName()//获取Name		
        */
```

**其它语言的写法,js中旧的写法**

![uTools_1670743532441](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670743532441.png)

**js推荐的新写法**

![uTools_1670743738194](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670743738194.png)

### (2).多态

```css
 	多态(同一操作作用于不同的对象上面，可以产生不同的解释和不同的执行结果)
                - 在JS中不会检查参数的类型，所以这就意味着任何数据都可以作为参数传递
                - 要调用某个函数，无需指定的类型，只要对象满足某些条件即可
                - 如果一个东西走路像鸭子，叫起来像鸭子，那么它就是鸭子
                - 多态为我们提供了灵活性
			   - js中的多态在所有语言中是最灵活的,但是太灵活也会产生一些问题我们要注意
```

```html
    <script>
        "use strict"
        class Person {
            constructor(name) {
                this.name = name;
            }
        }

        class Dog {
            constructor(name) {
                this.name = name;
            }
        }

        const person = new Person("黄宇")
        const dog = new Dog("死老鼠")

        function say(obj) {
            //js并不限制传入的参数类型,只要含有name这个属性就可以执行
            //这就是js中的多态
            console.log("hello" + obj.name);
        }
        
        say(person)//hello黄宇
        say(dog)//hello死老鼠
    </script>
```

**多态主要依靠方法重载和方法重写,方法重载是同一个函数有不同个参数和参数排列方式效果不同，方法重写是重写父类的方法**

### (3).继承

**通过重写父类同名方法实现扩展性(多态)**

```html
<script>
        /* 
            继承
                - 可以通过extends关键来完成继承
                - 当一个类继承另一个类时，就相当于将另一个类中的代码复制到了当前类中（简单理解）
                - 继承发生时，被继承的类称为 父类（超类），继承的类称为 子类
                - 通过继承可以减少重复的代码，并且可以在不修改一个类的前提对其进行扩展
                
                封装 —— 安全性
                继承 —— 扩展性
                多态 —— 灵活性
            
                - 通过继承可以在不修改一个类的情况下对其进行扩展(这是开发中继承最大的作用,减少代码是其次的作用)
                - OCP 开闭原则
                    - 程序应该对修改关闭，对扩展开放
        */
</script>
```

**继承的例子**

```html
    <script>
        "use strict"
        class Animal {
            str = "父类的字符串"
            constructor(name) {
                this.name = name;
            }
            sayHello() {
                console.log("动物会叫~");
            }
        }
        
        /*
            重写构造函数时，构造函数的第一行代码必须为super()
            因为重写了父类的构造方法相当于父类的构造方法消失了,父类没有被创建
            使用super就是调用了父类的构造方法创建了父类
        */
        class Dog extends Animal {
            constructor(name, age) {//传参
                super(name);//调用父类的构造函数给name赋值(继承的意义)
                //this.name=name; 自己进行赋值(不推荐,这样继承就没什么用了)
                this.age = age;
            }

            sayHello() {
                //子类创建同名方法来重写父类的方法
                console.log("汪汪汪");

                //在方法中可以使用super来引用父类的变量和方法
                super.str;
                super.sayHello();
            }

        }
        const dog = new Dog("黄老狗", 1)

        dog.sayHello();
        console.log(dog);

    </script>
```

***super相当于是子类对象中从父类继承下来部分成员的引用(变量和方法)*。**

![uTools_1670748037074](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670748037074.png)

**执行结果**

![uTools_1670748457840](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670748457840.png)

## 5.对象的内存结构

```css
/*
	抛出问题 在对象中存储函数时,用say(){}时在控制台访问对象时看不见这个函数,但是可以正常调用
	使用say () = function{}或者 sayHello = () => {}在控制台访问对象可以看见这个函数,可以正常调用
	
	经过赋值符号的最终都存储到了对象自身中,并不是存储在原型对象中
*/
```

![uTools_1670750103042](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670750103042.png)

![uTools_1670750045382](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670750045382.png)

![uTools_1670750076582](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670750076582.png)

```html
        <script>

            /* 
                对象中存储属性的区域实际有两个：
                    1. 对象自身
                        - 直接通过对象所添加的属性，位于对象自身中
                        - 在类中通过 x = y 的形式添加的属性，位于对象自身中

                    2. 原型对象（prototype）
                        - 对象中还有一些内容，会存储到其他的对象里（原型对象）
                        - 在对象中会有一个属性用来存储原型对象，这个属性叫做__proto__
                        - 原型对象也负责为对象存储属性，
                            当我们访问对象中的属性时，会优先访问对象自身的属性，
                            对象自身不包含该属性时，才会去原型对象中寻找
                        - 会添加到原型对象中的情况：
                            1. 在类中通过xxx(){}方式添加的方法，位于原型中
                            2. 主动向原型中添加的属性或方法
            */
            class Person {
                name = "孙悟空" //位于对象自身
                age = 18 //位于对象自身
                constructor(){
                     this.gender = "男"//位于对象自身
                 }
                sayHello() {
                    console.log("Hello，我是", this.name)//位于原型对象
                }
            }

            const p = new Person()

            p.address = "花果山" //位于对象自身
            p.sayHello = "hello" //覆盖后优先访问自身

            console.log(p.sayHello)
        </script>
```

**图片示意**

![uTools_1670750845280](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670750845280.png)

## 6.原型对象(prototype)

```html
<script>   
		class Person {
                name = "孙悟空"
                age = 18

                sayHello() {
                    console.log("Hello，我是", this.name)
                }
            }

            const p = new Person() 
            
            const obj = {}

		/* 
                访问一个对象的原型对象
                    对象.__proto__
                    Object.getPrototypeOf(对象)

                原型对象中的数据：
                    1. 对象中的数据（属性、方法等）
                    2. constructor （对象的构造函数）

                注意：
                    原型对象也有原型，这样就构成了一条原型链，根据对象的复杂程度不同，原型链的长度也不同
                        p对象的原型链：p对象 --> 原型 --> 原型 --> null
                        obj对象的原型链：obj对象 --> 原型 --> null

                    原型链：
                        - 读取对象属性时，会优先对象自身属性，
                            如果对象中有，则使用，没有则去对象的原型中寻找
                            如果原型中有，则使用，没有则去原型的原型中寻找
                            直到找到Object对象的原型（Object的原型没有原型（为null））
                                如果依然没有找到，则返回undefined

                        - 作用域链，是找变量的链，找不到会报错
                        - 原型链，是找属性的链，找不到会返回undefined
            */
  </script>    
```

![uTools_1670762335023](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670762335023.png)

## 7.原型的作用

**原型就相当于人类的基因会代代往下传递**

```html
    <script>
        /* 
            所有的同类型对象它们的原型对象都是同一个，
                也就意味着，同类型对象的原型链是一样的

            原型的作用：
                原型就相当于是一个公共的区域，可以被所有该类实例访问，
                    可以将该类实例中，所有的公共属性（方法）统一存储到原型中
                    这样我们只需要创建一个属性，即可被所有实例访问

                JS中继承就是通过原型来实现的,
                    当继承时，子类的原型就是一个父类的实例

            在对象中有些值是对象独有的，像属性（name，age，gender）每个对象都应该有自己的值，
                但是有些值对于每个对象来说都是一样的，像各种方法，对于一样的值没必要重复的创建

            !!如果某个实例突然需要用到和公共不一样的方法或属性,只需要单独重新定义一下这个方法或属性
                读取对象属性时，会优先对象自身属性，
        */
        class Animal {}

        class Cat extends Animal {}

        class TomCat extends Cat {}
        // TomCat --> cat --> Animal实例 --> object --> Object原型 --> null

        // cat --> Animal实例 --> object --> Object原型 --> null(继承时多了Animal原型继承)

        // p对象 --> object --> Object原型 --> null(没有继承的类)

        console.log(cat.__proto__.__proto__.__proto__.__proto__)

    </script>
```

```css
             函数的原型链是什么样子的？
            fn ==> Function原型 ==> Object原型 ==> null;
            
            Object的原型链是什么样子的？
            obj ==> obj原型 ==> null;
```

![uTools_1670764455807](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670764455807.png)

![uTools_1670764490004](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670764490004.png)

![uTools_1670765645393](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670765645393.png)

## 8.修改原型(面试题经常出现)

```html
        <script>
            /* 
                大部分情况下，我们是不需要修改原型对象
                    注意：
                        千万不要通过类的实例去修改原型
                            1. 通过一个对象影响所有同类对象，这么做不合适
                            2. 修改原型先得创建实例，麻烦
                            3. 危险

                处理通过__proto__能访问对象的原型外，
                    还可以通过类的prototype属性，来访问实例的原型
                    修改原型时，最好通过通过类去修改
                    好处：
                        1. 一修改就是修改所有实例的原型
                        2. 无需创建实例即可完成对类的修改

                    原则：
                        1. 原型尽量不要手动改
                        2. 要改也不要通过实例对象去改
                        3. 通过 类.prototype 属性去修改
                        4. 最好不要直接给prototype去赋值(这样覆盖了原来的原型,最好是直接添加新属性)

            */

            class Person {
                name = "孙悟空"
                age = 18

                sayHello() {
                    console.log("Hello，我是", this.name)
                }
            }
           	//修改原型添加fly方法
            Person.prototype.fly = () => {
                console.log("我在飞！")
            }

            class Dog{}

            // 通过实例对象修改原型，向原型中添加方法，修改后所有同类实例都能访问该方法 不要这么做
             p.__proto__.run = () => {
                console.log('我在跑~')
             }
             
            p.__proto__ = new Dog() // 直接为对象赋值了一个新的原型 不要这么做

            console.log(Person.prototype) // 访问Person实例的原型对象

        </script>
```

**Person.prototype===p.__ proto__ //true**

**区别是一个通过类访问,一个通过实例访问**

## 9.instanceof和hasOwn

### (1).instanceof

```css
        /* 
            instanceof 用来检查一个对象是否是一个类的实例
                - instanceof检查的是对象的原型链上是否有该类实例
                    只要原型链上有该类实例，就会返回true
                - 
                    dog -> Animal的实例 -> Object实例 -> Object原型

                - Object是所有对象的原型，所以任何和对象和Object进行instanceof运算都会返回true
        */
```

### (2).hasOwn(in、hasOwnProperty)

```css
            /* 
                in
                    - 使用in运算符检查属性时，无论属性在对象自身还是在原型中，都会返回true

                对象.hasOwnProperty(属性名) (不推荐使用)
                    - 用来检查一个对象的自身是否含有某个属性

                Object.hasOwn(对象, 属性名) (静态推荐使用 可以处理Object.create(null)用hasOwnProperty会报错的问题)
                    - 用来检查一个对象的自身是否含有某个属性
            */
```

很少场景能用到

![uTools_1670767409256](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670767409256.png)

## 10.早期类的创建方式(旧类,兼容老项目)(面试题)

**了解即可,可以使用一些工具将新版本代码转化为老版本代码**

```html
    <script>
        /*
            早期JS中，直接通过函数来定义类
                - 一个函数如果直接调用 xxx() 那么这个函数就是一个普通函数
                - 一个函数如果通过new调用 new xxx() 那么这个函数就是一个构造函数
         */

        /* 
            等价于：
                class Person{

                }
         
         */

        var Person = (function () {
            function Person(name, age) {
                // 在构造函数中，this表示新建的对象
                this.name = name
                this.age = age
            }

            // 向原型中添加属性（方法）
            Person.prototype.sayHello = function () {
                console.log(this.name)
            }

            // 静态属性
            Person.staticProperty = "xxx"
            // 静态方法
            Person.staticMethod = function () { }

            return Person//整个类当作返回值返回
        })()//要将整个类写成一个立即执行函数防止出现错误
        var P1 = new Person()
        console.log(P1); //Person{}
        

        //早期旧类实现继承
        var Animal = (function () {
            function Animal() {
                
            }
            
            return Animal
        })()

        var Cat = (function () {
            function Cat() {

            }

            // 继承Animal
            // 当继承时，子类的原型就是一个父类的实例
            Cat.prototype = new Animal()//继承的原理就是类的prototype属性指向父类的实例

            return Cat
        })()

        var cat = new Cat()

        console.log(cat)
    </script>
```

## 11.new运算符(面试题)

```html
    <script>
        /* 
            new运算符是创建对象时要使用的运算符
                - 使用new时，到底发生了哪些事情：
                https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new

                - 当使用new去调用一个函数时，这个函数将会作为构造函数调用，
                    使用new调用函数时，将会发生这些事：
                    1. 创建一个普通的JS对象（Object对象 {}）, 为了方便，称其为新对象
                    2. 将构造函数的prototype属性设置为新对象的原型
                    3. 使用实参来执行构造函数，并且将新对象设置为函数中的this(所以我们可以通过this访问对象)
                    4. 如果构造函数返回的是一个非原始值，则该值会作为new运算的返回值返回（千万不要这么做）
                        如果构造函数的返回值是一个原始值或者没有指定返回值，则新的对象将会作为返回值返回
                        通常不会为构造函数指定返回值
        */

        function MyClass() {
            // var newInstance = {} 第一步
            // newInstance.__proto__ = MyClass.prototype 第二步
            // 并且将新对象设置为函数中的this
        }
        var newInstance = new MyClass()
        console.log(mc)

        //新类的执行步骤也一样
        class Person {
            //只是他是在构造函数中进行的
            constructor() {

            }
        }

        new Person()
    </script>
```

## 12.对象的总结

**首先,明确一切都是对象**

```html
    <script>
        /*
            面向对象本质就是，编写代码时所有的操作都是通过对象来进行的。
                面向对象的编程的步骤：
                    1. 找对象
                    2. 操作对象
                
                学习对象：
                    1. 明确这个对象代表什么，有什么用    
                    2. 如何获取到这个对象
                    3. 如何使用这个对象（对象中的属性和方法(函数是window的方法)）

                对象的分类：
                    内建对象(语言基石)
                        - 由ES标准所定义的对象
                        - 比如 Object Function String Number ....

                    宿主对象(代码不同的运行环境:浏览器 node....)
                        - 由浏览器提供的对象
                        - BOM(操作浏览器)、DOM(操作网页)

                    自定义对象(vue等框架)
                        - 由开发人员自己创建的对象
        */
    </script>
```

**思考？为什么数值之间能用“-”进行运算，为什么字符型、列表、元组又为什么不行？而字符型可以进行“+”运算？**

![uTools_1670769861447](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670769861447.png)



# 八、数组

## 1.数组简介

```html
      <script>
            /* 
                数组（Array）
                    - 数组也是一种复合数据类型，在数组可以存储多个不同类型的数据
                    - 数组中存储的是有序的数据，数组中的每个数据都有一个唯一的索引
                        可以通过索引来操作获取数据
                    - 数组中存储的数据叫做元素
                    - 索引（index）是一组大于0的整数
                    - 创建数组
                        通过Array()来创建数组，也可以通过[]来创建数组
                        const arr2 = [1, 2, 3, 4, 5] // 数组字面量创建
                        使用数组时，应该避免非连续数组，因为它性能不好

                    - 向数组中添加元素
                        语法：
                            数组[索引] = 元素

                    - 读取数组中的元素
                        语法：
                            数组[索引]
                            - 如果读取了一个不存在的元素，不会报错而是返回undefined

                    - length
                        - 获取数组的长度
                        - 获取的实际值就是数组的最大索引 + 1
                        - 向数组最后添加元素：
                            数组[数组.length] = 元素
                        - length是可以修改的(改长变长,改短会删除元素)
            */
            const arr = new Array()
            const arr2 = [1, 2, 3, 4, 5] // 数组字面量

            arr[0] = 10
            arr[1] = 22
            arr[2] = 44
            arr[3] = 88
            arr[4] = 99

            // 
            // arr[100] = 99

            // console.log(arr[1])

           console.log(typeof arr) // object

            // console.log(arr.length)

            arr[arr.length] = 33
            arr[arr.length] = 55

            arr.length = 5

            console.log(arr)
        </script>
```

## 2.遍历数组

**不像其它语言那样严格性**

![uTools_1671094049634](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094049634.png)

```html
        <script>
            // 任何类型的值都可以成为数组中的元素
            let arr = [1, "hello", true, null, { name: "孙悟空" }, () => {}]

            // 创建数组时尽量要确保数组中存储的数据的类型是相同
            arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧", "白骨精"]

            //正向打印
            for(let i=0; i<arr.length; i++){
                console.log(arr[i])
            }

            //逆向打印
            for (let i = arr.length - 1; i >= 0; i--) {
                console.log(arr[i])
            }

            /* 
                定义一个Person类，类中有两个属性name和age
                    然后创建几个Person对象，将其添加到一个数组中

                遍历数组，并打印未成年人的信息
            
            */
            class Person {
                constructor(name, age) {
                    this.name = name
                    this.age = age
                }
            }

            const personArr = [
                new Person("孙悟空", 18),
                new Person("沙和尚", 38),
                new Person("红孩儿", 8),
            ]

            for(let i=0; i<personArr.length; i++){
                if(personArr[i].age < 18){
                    console.log(personArr[i])
                }
            }
        </script>
```

### (1).for-of(可迭代对象遍历)

```html
        <script>
            /* 
                for-of语句可以用来遍历可迭代对象

                语法：
                    for(变量 of 可迭代的对象){
                        语句...
                    }

                执行流程：
                    for-of的循环体会执行多次，数组中有几个元素就会执行几次，
                        每次执行时都会将一个元素赋值给变量
            */
                    
            const arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]

            for(let value of arr){
                console.log(value)
            }

            for(let value of "hello"){
                console.log(value)
            }
        </script>
```

![uTools_1678322356891](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678322356891.png)

Typed Array 定型数组，Generators被aysnc await取代了

## 3.数组方法(非破坏性)

### (1).isArray

 Array.isArray()

​          \- 用来检查一个对象是否是数组  

```css
            // console.log(Array.isArray({ name: "孙悟空" })) // false
            // console.log(Array.isArray([1, 2, 3])) // true
```

### (2).at

 at()

​          \- 可以根据索引获取数组中的指定元素

​          \- at可以接收负索引作为参数(负数就是从后面倒数)

```css
            // console.log(arr.at(-2))
            // console.log(arr[arr.length - 2])
```

### (3).concart

 concat()

​          \- 用来连接两个或多个数组

​          \- 非破坏性方法，不会影响原数组，而是返回一个新的数组

```javascript
const arr2 = ["白骨精", "蜘蛛精", "玉兔精"]
let result = arr.concat(arr2, ["牛魔王","铁扇公主"])
```

### (4).indexOf和lastIndexOf

indexOf()
                    - 获取元素在数组中第一次出现的索引
                       - 参数：
                        1. 要查询的元素
                        2. 查询的起始位置

lastIndexOf()

​          \- 获取元素在数组中最后一次出现的位置

```css
            let result = arr.indexOf("沙和尚", 3)
            result = arr.lastIndexOf("沙和尚", 3)

               俩个方法的返回值：
                    找到了则返回元素的索引，
                    没有找到返回-1
```

### (5).join

​        join()

​          \- 将一个数组中的元素连接为一个字符串

​          \- ["孙悟空", "猪八戒", "沙和尚", "唐僧", "沙和尚"] --> "孙悟空,猪八戒,沙和尚,唐僧,沙和尚"

​          \- 参数：

​            指定一个字符串作为连接符

```javascript
            result = arr.join() //默认值为英文逗号
            result = arr.join("@-@") //以@-@作为分割符
            result = arr.join("") //不分割   孙悟空猪八戒沙和尚唐僧沙和尚
```

### (6).slice

slice()
                  用来截取数组（非破坏性方法）     

                     - 参数：
                        1. 截取的起始位置（包括该位置）
                        2. 截取的结束位置（不包括该位置）
                            - [)
                            - 第二个参数可以省略不写，如果省略则会一直截取到最后
                            - 索引可以是负值

```css
                    //如果将两个参数全都省略，则可以对数组进行浅拷贝（浅复制）
                                arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
                                result = arr.slice(0, 2)
                                result = arr.slice(1, 3)
                                result = arr.slice(1, -1)
                                result = arr.slice()//浅复制

```

### (7).includes

```css
includes 可以判断一个数组中是否包含某一个元素，并返回true 或者false
```

### (8).find

![uTools_1679475786402](C:\Users\ttq\Downloads\uTools_1679475786402.png)

```javascript
const STU_ARR = [
    { id: "1", name: "孙悟空", age: 18, gender: "男", address: "花果山" },
    { id: "2", name: "猪八戒", age: 28, gender: "男", address: "高老庄" },
    { id: "3", name: "沙和尚", age: 38, gender: "男", address: "流沙河" }
]
const stu = STU_ARR.find(item=>item.id===id)
   // const stu = STU_ARR.find((item)=>{
    //  item其实相当于指代数组  item.id=>>数组.id
    //     return item.id === id
    // })
coslose.log(stu)
```





## 4.对象的复制

**没有产生新对象的不叫复制,下图就不是复制**

![uTools_1671105066995](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671105066995.png)

## 5.浅拷贝和深拷贝

```html
    <script>
        /* 
            浅拷贝（shallow copy）
                - 通常对对象的拷贝都是浅拷贝
                - 浅拷贝顾名思义，只对对象的浅层进行复制（只复制一层）
                - 如果对象中存储的数据是原始值，那么拷贝的深浅是不重要
                - 浅拷贝只会对对象本身进行复制，不会复制对象中的属性（或元素）

            深拷贝（deep copy）
                - 深拷贝指不仅复制对象本身，还复制对象中的属性和元素
                - 因为性能问题，通常情况不太使用深拷贝
        */

        // 创建一个数组
        const arr = [{name:"孙悟空"}, {name:"猪八戒"}]
        const arr2 = arr.slice() // 浅拷贝

        //structuredClone()
        const arr3 = structuredClone(arr) // 专门用来深拷贝的方法

        console.log(arr)
        console.log(arr3)

    </script>
```

###  (1).浅拷贝:只复制第一层

**存储原始值时的内存清空及使用了slice方法**

![uTools_1671105256267](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671105256267.png)

**存储非原始值时的内存情况**

![image-20221215200102015](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221215200102015.png)

**存储非原始值时的内存情况及使用了slice方法，牢记只复制一层**

![uTools_1671105778333](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671105778333.png)

**数组本身不相等,但是里面的元素相等**

![uTools_1671105892836](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671105892836.png)

**此时修改2个数组任一数组的元素都会导致数组变化，引用的原始值还是同一些**

![uTools_1671105940781](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671105940781.png)

![image-20221215200920241](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221215200920241.png)

### (2).深拷贝

**const arr3 = structuredClone(arr) // 专门用来深拷贝的方法**

![uTools_1671106263828](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671106263828.png)

**对比浅拷贝和深拷贝**

**浅拷贝就复制了第一层,而深拷贝会把所有东西都复制了。**         

![uTools_1671106623117](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671106623117.png)

![uTools_1671106658163](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671106658163.png)

## 6.复制的方式(...展开运算符)(对象数组的复制总结)

**数组**

```html
<script>
        const arr2 = arr.slice()//浅复制方法1
  
           /* 
                ... (展开运算符)
                    - 可以将一个数组中的元素展开到另一个数组中或者作为函数的参数传递
                    - 通过它也可以对数组进行浅复制
           */
        
        const arr3 = [arr[0], arr[1], arr[2]]//浅复制方法2
        
        //浅复制方法3
        const arr3 = [...arr]
        const arr3 = ["唐僧", ...arr, "白骨精"]
        
        //...运算符作为函数参数传递
          function sum(a, b, c) {
                return a + b + c
            }
            const arr4 = [10, 20, 30]
            let result = sum(arr4[0], arr4[1], arr4[2])//这写法和下面意思相同
            result = sum(...arr4)
        
</script>
```

**深复制有方法 还有利用json转换**

**对象**

```html
<script>
            /* 
                对象的复制
                    - Object.assign(目标对象, 被复制的对象)
                    - 将被复制对象中的属性复制到目标对象里，并将目标对象返回

                - 也可以使用展开运算符对对象进行复制
            */
    
            const obj = { name: "孙悟空", age: 18 }
            const obj2 = Object.assign({}, obj) //1
            Object.assign(obj2, obj)//2   12相等

            const obj3 = { address: "高老庄", ...obj, age: 48 } // 将obj中的属性在新对象中展开
        </script>
```

## 7.数组方法(破坏性)

### (1).push

- 向数组的末尾添加一个或多个元素，并返回新数组的长度

### (2).pop

- 删除并返回数组的最后一个元素

### (3).unshift

- 向数组的开头添加一个或多个元素，并返回新的长度

### (4).shift

- 删除并返回数组的第一个元素

### (5).splice

  - 可以删除、插入、替换数组中的元素
                - 参数：
                    1. 删除的起始位置
                    2. 删除的数量
                    3. 要插入的元素

### (6).reverse

-  反转数组

## 8.数组去重

方法一

```html
    <script>
        const arr = [1, 2, 1, 3, 2, 4, 5, 5, 6, 7];

        //分别获取数组中的元素
        for (let i = 0; i < arr.length; i++) {
            //获取i后一位的元素
            for (let j = i + 1; j < arr.length; j++) {
                //值进行比较
                if (arr[i] == arr[j]) {
                    arr.splice(j, 1); //2者相等,下标j删除
                    //回退一位在进行比较一次
                    j--;
                }
            }
            console.log(arr[i]);
        }
    </script>
```

方法二

```html
    <script>
        const arr = [1, 2, 1, 3, 2, 4, 5, 5, 6, 7];

        //分别获取数组中的元素
        for (let i = 0; i < arr.length; i++) {
            //检查i后面有没有和arr[i]一样的元素
            const index = arr.indexOf(arr[i], i + 1)//查询是否有arr[i],从i+1开始查询
            //没有找到元素会返回-1,如果不返回-1就是找到了元素
            if (index !== -1) {
                arr.splice(index, 1)
            }
            console.log(arr[i]);
        }
    </script>
```

方法三

```html
    <script>
        const arr = [1, 2, 1, 3, 2, 4, 5, 5, 6, 7];

        const newArr = [];
        //遍历数组
        for (let ele of arr) {
            //如果新数组中出现该元素进行添加
            if (newArr.indexOf(ele) === -1) { //只会查询到第一次出现的元素
                newArr.push(ele)//查询到的元素添加进新数组
            }
        }
        console.log(newArr);
    </script>
```

## 9.排序

### (1).冒泡排序

**思想:**

```html
 <script>
            /* 
                 [9,1,3,2,8,0,5,7,6,4]

                 思路一：
                    9, 1, 3, 2, 8, 0, 5, 7, 6, 4
                    - 比较相邻的两个元素，然后根据大小来决定是否交换它们的位置
                    - 例子：
                        第一次排序：1, 3, 2, 8, 0, 5, 7, 6, 4, 9 //a[0]和整个数组比完一圈
                        第二次排序：1, 2, 3, 0, 5, 7, 6, 4, 8, 9 //a[1]和整个数组比完一圈
                        第三次排序：1, 2, 0, 3, 5, 6, 4, 7, 8, 9
                        ...
                        倒数第二次 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

                    - 这种排序方式，被称为冒泡排序，冒泡排序是最慢的排序方式，
                        数字少还可以凑合用，不适用于数据量较大的排序
            */

            const arr = [9, 1, 3, 2, 8, 0, 5, 7, 6, 4]
            for (let j = 0; j < arr.length - 1; j++) {//最高取到arr.length - 1
                //最大值取到length-1,防止i+1时出现undefined
                for (let i = 0; i < arr.length - 1 - j; i++) {//排完的以后没必要再排序了,i < arr.length - 1 - j;
                    // arr[i] 前边的元素 arr[i+1] 后边元素
                    if (arr[i] < arr[i + 1]) {
                        // 大数在前，小数在后，需要交换两个元素的位置
                        let temp = arr[i] // 临时变量用来存储arr[i]的值
                        arr[i] = arr[i + 1]
                        arr[i + 1] = temp 
                    }
                }
            }

            console.log(arr)
        </script>
```

### (2).选择排序

**思想:不断找出数组中最小的数,然后与当前比较的数进行交换。  时间 :O(n^2)  空间:O(1)**

```html
    <script>
        const arr = [9, 1, 3, 2, 8, 0, 5, 7, 6, 4, 9, 7, 1];

        for (let i = 0; i < arr.length - 1; i++) {//这里减去1的目的是省去第二个for循环当j超出数组长度的时候还要判断(其实加不加都可以)
            for (let j = i + 1; j < arr.length; j++) {
                console.log(arr[j]);
                if (arr[i] > arr[j]) {
                    let t = arr[i];
                    arr[i] = arr[j];
                    arr[j] = t;
                }
            }
        }
        console.log(arr);
    </script>
```

**快速排序思想:以第一个数为基准右往左找比基数小的数，放入i位置，从左往右找比基数大的数，放到j位置，如果i==j。当前数找到了要交换的位置"**

**插入排序思想：不断建立监察哨，排完建立下一个监察哨**

## 10.封装函数

```html
        <script>
            const arr = [9, 1, 3, 2, 8, 0, 5, 7, 6, 4]
            const arr2 = [9, 8, 7, 6, 5, 4, 3, 2, 1]

            //封装选择排序函数
            function sort(array) {
                const arr = [...array]
                for (let i = 0; i < arr.length; i++) {
                    for (let j = i + 1; j < arr.length; j++) {
                        if (arr[i] > arr[j]) {
                            // 交换两个元素的位置
                            let temp = arr[i]
                            arr[i] = arr[j]
                            arr[j] = temp
                        }
                    }
                }
                return arr
            }

            let result = sort(arr2)

            // console.log(arr2)
            // console.log(result)

            class Person {
                constructor(name, age) {
                    this.name = name
                    this.age = age
                }
            }

            const personArr = [
                new Person("孙悟空", 18),
                new Person("沙和尚", 38),
                new Person("红孩儿", 8),
                new Person("白骨精", 16),
            ]


            // 封装filter()函数用来对数组进行过滤
            function filter(arr) {
                const newArr = []
                for (let i = 0; i < arr.length; i++) {
                    if (arr[i].age < 18) {
                        newArr.push(arr[i])
                    }
                }
                return newArr
            }

            result = filter(personArr)
            console.log(result)
        </script>
```

## 11.回调函数

**函数的参数也可以是一个函数(函数可以存储语句,方便我们动态传递参数)**

![uTools_1678590221332](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678590221332.png)

```html
    <script>
        class Person {
            constructor(name, age) {
                this.name = name
                this.age = age
            }
        }

        const personArr = [
            new Person("孙悟空", 18),
            new Person("沙和尚", 38),
            new Person("红孩儿", 8),
            new Person("白骨精", 16),
        ]

        function filter(arr, cb) {//cb参数调用了fn函数
            const newArr = [];
            for (let i = 0; i < arr.length; i++) {
                if (cb(arr[i])) {//cb()就是fn()  参数为arr[i],也就是传上来的personArr数组
                    newArr.push(arr[i])
                }
            }
            return newArr
        }

        function fn(a) {
            return a.age < 18  //函数接受了数组作为参数  相当于--->return arr[i].age < 18 -->return personArr[i].age < 18
        }

        let result = filter(personArr, fn);//将数组和函数作为filter的参数进行传递
        console.log(result);//小于18的会被添加到数组中
    </script>
```

## 12.高阶函数

![uTools_1678351045739](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678351045739.png)

开发写法(不设置新函数,通常回调函数都是匿名函数,参数传递时直接写好)

result = **filter**(personArr, a => a.age < 18)

![uTools_1671462526457](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671462526457.png)

**函数的返回值作为函数**

```html
    <script>
        /*
            希望在someFn()函数执行时，可以记录一条日志
            在不修改原函数的基础上，为其增加记录日志的功能
            可以通过高阶函数，来动态的生成一个新函数
        */

        function someFn() {
            return "hello"
        }

        //在不影响someFn的前提下对其扩展。
        function outer(cb) {
            //返回一个函数
            return () => {
                console.log("记录日记~~~~~~~~~");
                const res = cb()//调用cb()函数赋值给res
                return res //将res作为该新函数的返回值返回
            }
        }

        let result = outer(someFn) //outer函数赋值给了result
        console.log(result);
        result();
        
       // 
       function test(){
           console.log("test~~~~")
           return "test"
        }
        
       let newTest = outer(test)
       newTest()
    </script>
```



## 13.闭包的简介

```html
        <script>
            /* 
                创建一个函数，第一次调用时打印1，第二次调用打印2，以此类推

                可以利用函数，来隐藏不希望被外部访问到的变量

                闭包：
                    闭包就是能访问到外部函数作用域中变量的函数❤(桥梁)
                    在javascript中，只有函数内部的子函数才能读取局部变量，
                    所以闭包可以理解成“定义在一个函数内部的函数“。在本质上，
                    闭包是将函数内部和函数外部连接起来的桥梁。
                什么时候使用：
                    当我们需要隐藏一些不希望被别人访问的内容时就可以使用闭包
                构成闭包的要件：
                    1. 函数的嵌套
                    2. 内部函数要引用外部函数中的变量
                    3. 内部函数要作为返回值返回
            */

            function outer(){
                let num = 0 // 位于函数作用域中
                return () => {
                    num++ //内部函数作用域可以访问到外部函数作用域
                    console.log(num)
                }
            }

            const newFn = outer()

            newFn()
            newFn()
            newFn()
        </script>
```



## 14.闭包的原理

```html
    <script>
        let a = "全局变量a"

        /* 
            函数的作用域，在函数创建时就已经确定了（词法作用域）
                和调用的位置无关
                
            闭包利用的就是词法作用域
        */
        
        function fn() { //fn在全局作用域中定义的 --> 会去全局作用域中找 a 创建及固定
            console.log(a)
        }


        function fn2() {
            let a = "fn2中的a"
            fn()
        }

		fn2()
        
		//闭包
        function fn3() {
            let a = "fn3中的a"

            function fn4() {//fn4的外层作用域就是fn3
                console.log(a)
            }

            return fn4
        }
        
        let fn4 = fn3() //fn3函数的返回值是fn4函数

        fn4() //所以fn4这个变量就是fn4函数  fn4()等于在调用fn4函数 最终还是打印fn3中的a 和怎么调用无关 生成来就确定了

    </script>
```

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671538443673.png)

fn4存储的就是一个函数，也就是fn4函数,加()进行函数的调用



## 15.闭包的注意事项(生命周期)

```html
    <script>
        /* 
               闭包的生命周期：
                   1. 闭包在外部函数调用时产生，外部函数每次调用都会产生一个全新的闭包
                   2. 在内部函数丢失时销毁（内部函数被垃圾回收了，闭包才会消失）

               注意事项：
                   闭包主要用来隐藏一些不希望被外部访问的内容，
                       这就意味着闭包需要占用一定的内存空间

                   相较于类来说，闭包比较浪费内存空间（类可以使用原型(原型就不会重复创建)而闭包不能），
                       需要执行次数较少时，使用闭包(js一般使用习惯是用闭包)
                       需要大量创建实例时，使用类(类也可以藏东西)
           
           */
        function outer2() {
            let num = 0
            return () => {
                num++
                console.log(num)
            }
        }

        let fn1 = outer2() // 独立闭包
        let fn2 = outer2() // 独立闭包

        fn1()

        fn1 = null //此时销毁

    </script>
```

## 16.函数的递归

```html
    <script>
        /* 
            递归
                - 调用自身的函数称为递归函数
                - 递归的作用和循环是基本一致
        */


        // 创建一个函数，可以用来求任意数的阶乘
        /* 
            1! 1
            2! 1 x 2 = 2
            3! 1 x 2 x 3 = 6
            ...
            10! 1 x 2 x 3 x 4 x 5 x 6 x 7 x 8 x 9 x 10 = xxx

            如果用递归来解决阶乘的问题？
                5! = 4! x 5
                4! = 3! x 4
                3! = 2! x 3
                2! = 1! x 2
                1! = 1

            递归的核心思想就是将一个大的问题拆分为一个一个小的问题，小的问题解决了，大的问题也就解决了

            编写递归函数，一定要包含两个要件：
                1.基线条件 ——  递归的终止条件
                2.递归条件 ——  如何对问题进行拆分

            递归的作用和循环是一致的，不同点在于，递归思路的比较清晰简洁，循环的执行性能比较好
                在开发中，一般的问题都可以通过循环解决，也是尽量去使用循环，少用递归
                只在一些使用循环解决比较麻烦的场景下，才使用递归(递归的性能比较差)
        */

        //循坏解决的问题代码会比较多
        function jieCheng(num) {
            // 创建一个变量用了记录结果
            let result = 1

            for (let i = 2; i <= num; i++) {
                result *= i
            }

            return result
        }

        let result = jieCheng(3)

        // console.log(result)
        
		//进行递归
        function jieCheng2(num) {

            // 基线条件
            if (num === 1) {
                return 1
            }

            // 递归条件
            // num! = (num-1)! * num
            return jieCheng2(num - 1) * num

        }

        result = jieCheng2(5)
        /* 
            jieCheng2(5)
                - return jieCheng2(4) * 5
                 - return jieCheng2(3) * 4
                  - return jieCheng2(2) * 3
                    - return jieCheng2(1) * 2
                     - return 1
                     此时计算机就知道了jieCheng2(1)的值为1
        */

        console.log(result)

    </script>
```

**练习**

```html
 <script>
            /* 
                一对兔子出生后的两个月后每个月都能生一对小兔子
                    - 编写一个函数，可以用来计算第n个月的兔子的数量

                1   2   3   4   5   6   7   8   9   10  11  12
                1   1   2   3   5   8   13  21  34 ....
                - 规律，当前数等于前两个数之和（斐波那契数列）
            */

            // 求斐波那契数列中的第n个数
            function fib(n) {
                // 确定基线条件
                if (n <= 1) {
                    return n//返回其它东西就是输入错误
                }

                // 设置递归条件
                // 第n个数 = 第n-1个数 + 第n-2个数
                return fib(n - 1) + fib(n - 2)
            }

            let result = fib(10)

            console.log(result)
        </script>
```

## 17.数组的方法(利用高阶函数)及函数补充

```html
   <script>
        let arr = ["a", "c", "e", "f", "d", "b"]

        arr = [2, 3, 1, 9, 0, 4, 5, 7, 8, 6, 10]

        /* 
            sort()
                - sort用来对数组进行排序（会对改变原数组）
                - 破坏性的方法
                - sort默认会将数组升序排列
                    注意：sort默认会按照Unicode编码进行排序，所以如果直接通过sort对数字进行排序
                        可能会得到一个不正确的结果
                - 参数：
                    - 可以传递一个回调函数作为参数，通过回调函数来指定排序规则
                        (排列数字时使用)
                        (a, b) => a - b 升序排列
                        (a, b) => b - a 降序排列
            forEach()
                - 用来遍历数组
                - 它需要一个回调函数作为参数，这个回调函数会被调用多次
                    数组中有几个元素，回调函数就会调用几次
                    每次调用，都会将数组中的数据作为参数传递
                - 非破坏性方法，不会影响原数组
                - 回调函数中有三个参数：
                    element 当前的元素
                    index 当前元素的索引
                    array 被遍历的数组

            filter()
                - 将数组中符合条件的元素保存到一个新数组中返回
                - 需要一个回调函数作为参数，会为每一个元素去调用回调函数，并根据返回值来决定是否将元素添加到新数组中
                - 非破坏性方法，不会影响原数组
                  - 回调函数中有三个参数：
                    element 当前的元素
                    index 当前元素的索引
                    array 被遍历的数组

            map()
                - 根据当前数组生成一个新数组
                - 需要一个回调函数作为参数，
                    回调函数的返回值会成为新数组中的元素
                - 非破坏性方法不会影响原数组
                  - 回调函数中有三个参数：
                    element 当前的元素
                    index 当前元素的索引
                    array 被遍历的数组

            reduce()
                - 可以用来将一个数组中的所有元素整合为一个值
                - 非破坏性方法不会影响原数组
                - 参数：
                    1. 回调函数，通过回调函数来指定合并的规则
                    2. 可选参数，初始值
        */

        // console.log(arr)

        // arr.sort()
        arr.sort((a, b) => a - b)
        arr.sort((a, b) => b - a)

        // console.log(arr)

        arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]

        arr.forEach((element, index, array) => {
            console.log(array)
        })

        arr.forEach((element, index) => console.log("下标:" + index, "  元素:" + element))//遍历数组元素和下表

        arr = [1, 2, 3, 4, 5, 6, 7, 8]

        let result = arr.filter((ele) => ele > 5)//获取数组中大于5的数

        result = arr.map((ele) => ele * 2) //将数组扩大俩倍

        arr = ["孙悟空", "猪八戒", "沙和尚"]

        result = arr.map((ele) => "<li>" + ele + "</li>")//为元素添加"<li></li>"

        arr = [1, 2, 3, 4, 5, 6, 7, 8]

        result = arr.reduce((a, b) => {
            /* 
                1, 2
                3, 3
                6, 4
                10, 5
            */
            // console.log(a, b)

            return a + b
        })

        result = arr.reduce((a, b) => a + b, 10)//指定了初始值为10,第一个相加的数为10

        console.log(result)
    </script>
```

### 1.Array.from方法

```css
Array.from() 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。
array有的是数组专用(只能Array.方法)   还有一些是创建的对象可以使用(arr.at等)
```



## 18.arguments和可变参数

```html
   <script>
        function fn() {
            /* 
                arguments
                    - arguments是函数中又一个隐含参数(this也是)
                    - arguments是一个类数组对象（伪数组）
                        和数组相似，可以通过索引来读取元素，也可以通过for循环变量，但是它不是一个数组对象，不能调用数组的方法
                    - arguments用来存储函数的实参，
                        无论用户是否定义形参，实参都会存储到arguments对象中
                        可以通过该对象直接访问实参
            */

            console.log(arguments[2])//返回第二个参数
            console.log(Array.isArray(arguments))//false
            for (let i = 0; i < arguments.length; i++) {
                console.log(arguments[i])//遍历
            }

            for(let v of arguments){
                console.log(v)//遍历
            }

            arguments.forEach((ele) => console.log(ele))//无法遍历,无法使用数组的方法
        }

        // fn(1, 10, 33)

        // 定义一个函数，可以求任意个数值的和
        function sum() {
            // 通过arguments，可以不受参数数量的限制更加灵活的创建函数
            let result = 0

            for (let num of arguments) {
                result += num
            }

            return result
        }

        /* 
            可变参数，在定义函数时可以将参数指定为可变参数
                - 可变参数可以接收任意数量实参，并将他们统一存储到一个数组中返回
                - 可变参数的作用和arguments基本是一致，但是也具有一些不同点：
                    1. 可变参数的名字可以自己指定
                    2. 可变参数就是一个数组，可以直接使用数组的方法
                    3. 可变参数可以配合其他参数一起使用
        */

        function fn2(...abc) {
            console.log(abc)
        }

        function sum2(...num) {
            return num.reduce((a, b) => a + b, 0)
        }

        // 当可变参数和普通参数一起使用时，需要将可变参数写到最后
        function fn3(a, b, ...args) {
            // for (let v of arguments) {
            //     console.log(v)
            // }
            // arguments无法配合其它参数一起使用(俩者之间有重叠)

            console.log(args)
        }

        fn3(123, 456, "hello", true, "1111")//从第三个参数开始归args管
    </script>
```

## 19.call和apply方法指定this

```html
        <script>
            /* 
                根据函数调用方式的不同，this的值也不同：
                    1. 以函数形式调用，this是window
                    2. 以方法形式调用，this是调用方法的对象
                    3. 构造函数中，this是新建的对象
                    4. 箭头函数没有自己的this，由外层作用域决定
                    5. 通过call和apply调用的函数，它们的第一个参数就是函数的this
            */
            
            function fn() {
                console.log("函数执行了~", this)
            }

            const obj = { name: "孙悟空", fn }

            /* 
                调用函数除了通过 函数() 这种形式外，还可以通过其他的方式来调用函数
                    比如，我们可以通过调用函数的call()和apply()来个方法来调用函数
                        函数.call()
                        函数.apply()
                        - call 和 apply除了可以调用函数，还可以用来指定函数中的this
                        - call和apply的第一个参数，将会成为函数的this
                        - 通过call方法调用函数，函数的实参直接在第一个参数后一个一个的列出来
                        - 通过apply方法调用函数，函数的实参需要通过一个数组传递
                -- 现在开发都用匿名箭头函数直接固定this了
            */

            // fn.call(obj)
            // fn.apply(console)

            function fn2(a, b) {
                console.log("a =", a, "b =", b, this)
            }

          fn2.call(obj, "hello", true)
            fn2.apply(obj, ["hello", true])

  	</script>
```



## 20.bind 为新函数绑定this

```html
        <script>
            /* 
                根据函数调用方式的不同，this的值也不同：
                    1. 以函数形式调用，this是window
                    2. 以方法形式调用，this是调用方法的对象
                    3. 构造函数中，this是新建的对象
                    4. 箭头函数没有自己的this，由外层作用域决定
                    5. 通过call和apply调用的函数，它们的第一个参数就是函数的this
                    6. 通过bind返回的函数，this由bind第一个参数决定（无法修改）

                bind() 是函数的方法，可以用来创建一个新的函数
                    - bind可以为新函数绑定this
                    - bind可以为新函数绑定参数

                箭头函数没有自身的this，它的this由外层作用域决定，
                    也无法通过call apply 和 bind修改它的this 
                    箭头函数中没有arguments
            */

            function fn(a, b, c) {
                console.log("fn执行了~~~~", this)
                console.log(a, b, c)
            }

            const obj = {name:"孙悟空"}

            const newFn = fn.bind(obj, 10, 20, 30)

            // newFn()


            const arrowFn = () => {
                console.log(this)
            }

            // arrowFn.call(obj)

            const newArrowFn = arrowFn.bind(obj)

            // newArrowFn()

            class MyClass{
                fn = () => {
                    console.log(this)
                }
            }

            const mc = new MyClass()

            // mc.fn.call(window)
        </script>
```

### (1).this的值总结以及箭头函数总结❤❤(面试题)

```css
            根据函数调用方式的不同，this的值也不同：
                1. 以函数形式调用，this是window
                2. 以方法形式调用，this是调用方法的对象
                3. 构造函数中，this是新建的对象
                4. 箭头函数没有自己的this，由外层作用域决定
                5. 通过call和apply调用的函数，它们的第一个参数就是函数的this
                6. 通过bind返回的函数，this由bind第一个参数决定（无法修改）

            箭头函数没有自身的this，它的this由外层作用域决定，
                也无法通过call apply 和 bind修改它的this 
                箭头函数中没有arguments
		   开发中常用箭头函数固定this
```

## 21.在类中普通函数和箭头函数的区别

```javascript
class MyClass{
    fc(){
        //这种方式会直接添加到原型中
        //性能好,但是this不固定
    }
    
    fc = () =>{
        //这种方式会添加到实例中
        //性能较差,this锁死
    }
}
```

# 九、内建对象

##   1.数组解构赋值

```html
    <script>
        /*
            解构赋值
         */
	  1.
        const arr = ["孙悟空", "猪八戒", "沙和尚"]

        let a, b, c;
        // a = arr[0]
        // b = arr[1]
        // c = arr[2]
        [a, b, c] = arr // 解构赋值
        
       2.
        let [d, e, f, g] = ["唐僧", "白骨精", "蜘蛛精", "玉兔精"] // 声明的同时解构

        console.log(d, e, f, g)
            // ;[d, e, f, g] = [1, 2, 3] 未赋值undefined
            // ;[d, e, f = 77, g = 10] = [1, 2, 3] 提前赋初始值
            ;[d, e, f = 77, g = g] = [1, 2, 3] //未赋值的值保留原来的值("玉兔精")
        
	   3.
        let [n1, n2, ...n3] = [4, 5, 6, 7] // 解构数组时，可以使用...来设置获取多余的元素
        console.log(n1, n2, n3) //此时n3成为一个数组接收剩下的元素


        4.//函数的返回值用来解构数组
        function fn() {
            return ["二郎神", "猪八戒"]
        }
        let [name1, name2] = fn()

        5.// 可以通过解构赋值来快速交换两个变量的值
        let a1 = 10
        let a2 = 20
        [a1, a2] = [a2, a1] // [20, 10]

        6.//数组中的值进行交换
        const arr2 = ["孙悟空", "猪八戒"];
        [arr2[0], arr2[1]] = [arr2[1], arr2[0]] // [arr2[0], arr2[1]]就是arr2
        console.log(arr2)

        /* 
            数组中可以存储任意类型的数据，也可以存数组,
                如果一个数组中的元素还是数组，则这个数组我们就称为是二维数组
        */

        const arr3 = [["孙悟空", 18, "男"], ["猪八戒", 28, "男"]]
        //取出二维数组中的值要俩次遍历
        for(let stu of arr3){
             for(let v of stu){
                 console.log(v)
             }
         }

	    1.//解构二维数组
        let [[name, age, gender], obj] = arr3 //孙悟空的数据单独解构 猪八戒的数据解构到obj数组中
        console.log(name, age, gender) //"孙悟空", 18, "男"
        console.log(obj) //输出["猪八戒", 28, "男"]

        
    	2.//如果我们想要一个”默认“值给未赋值的变量，我们可以使用 = 来提供
		let [name = "Guest", surname = "Anonymous"] = ["Julius"];
		alert(name);  //Julius（来自数组的值）
		alert(surname)；  //Anonymous（默认值被使用了）
    
    	3.//还可以用函数
		let [name, surname = prompt('请输入')] = ["Julius"];
		alert(name);  //Julius（来自数组）
		alert(surname);  //你输入的值
    </script>
```

## 2.对象的解构

```html
    <script>
        const obj = { name: "孙悟空", age: 18, gender: "男" }

        1.
        let { name, age, gender } = obj // 声明变量同时解构对象
        let name, age, gender;
        ({ name, age, gender } = obj)//声明完在解构
        let { address } = obj //没有的属性返回undefined
        console.log(name, age, gender，address)
        
	   2.
        let { name: a, age: b, gender: c, address: d = "花果山" } = obj //起别名的赋值

        console.log(a, b, c, d)

        3.//提取对象中的对象的值
        const user = {
            id: 123,
            name: 'hehe',
            education: {
                degree: 'Masters'
            }
        };
        const { education } = user;
        const { degree } = education;
        console.log(degree);//Masters

        4.//简写
        const { education: { degree } } = user;
        console.log(degree);

        5.//提取二维数组的值
        const arr3 = [["孙悟空", 18, "男"], ["猪八戒", 28, "男"]]
        let ddd = arr3[0][1];
        console.log(ddd);


        6.//数据防御 防止数据丢失 加一个缺省值
        const user1 = {
            id: 123,
            name: 'hehe'
        };

        const {
            education: { degree1 } = {}
        } = user1;
        console.log(degree1); //输出 undefined
        console.log(user1); //输出{id: 123, name: 'hehe'}
        
        7.
        let user = {};
	    [user.name, user.surname] = "John Smith".split(" ");//空格分割
	    console.log(user.name);  //John
	    console.log(user.surname);  //Smith
	    console.log(user);//{}
        
        
        8.//如果我们想把一个属性赋值给另一个名字的变量，
        //比如把 options.width 属性赋值给名为 w 的变量，那么我们可以使用冒号来设置变量名称：
        let options = {
            title: "Menu",
            width: 100,
            height: 200
        };
        //{ sourceProperty: targetVariable }
        let { width: w, height: h, title } = options;
        //width -> w
        //height -> h
        //title -> title
        console.log(w);//100
        console.log(h);//200
        console.log(title);//Menu
        
        9.//改进版
        let options = {
            title: "Menu"
        };
        let { width: w = 100, height: h = 200, title } = options;
        alert(title);  //Menu
        alert(w);  //100
        alert(h);  //200
        

       10. //还可以用函数
        let options = {
  		title: "Menu"
	   };
		let {width = prompt("width?"), title = prompt("title?"} = options;
		alert(title);  //Menu
		alert(width);  //(prompt)的返回值
        
       11.//...的使用
        let options = {
            title: "Menu",
            height: 200,
            width: 100
        };
        //title = 名为 title 的属性
        //rest = 存有剩余属性的对象
        let { title, ...rest } = options;
        //现在 title = ”Menu“， rest = {height :200, width: 100}
        alert(rest.height);  //200
        alert(rest.width);  //100
        
        12.//使用立即执行函数
        let title, width, height;
	   ({title, width, height} = {title: "Menu", wifth: 200, height: 100});
	   alert(title);  //Menu
        
    </script>
```

**解构的用途**

![uTools_1678262929323](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678262929323.png)

**嵌套的解构赋值**

![uTools_1678263549946](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678263549946.png)

**.entries()方法**

![uTools_1678263878795](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678263878795.png)

## 3.对象的序列化

```html
    <script>
        /* 
            对象的序列化
                - JS中的对象使用时都是存在于计算机的内存中的
                - 序列化指将对象转换为一个可以存储的格式
                    在JS中对象的序列化通常是将一个对象转换为字符串（JSON字符串）
                - 序列化的用途（对象转换为字符串有什么用）：
                    - 对象转换为字符串后，可以将字符串在不同的语言之间进行传递
                        甚至人可以直接对字符串进行读写操作，使得JS对象可以不同的语言之间传递
                    - 用途：
                        1. 作为数据交换的格式(前后端数据传递等) ❤❤❤
                        2. 用来编写配置文字(项目配置文件,一般是手写) ❤❤❤
                - 如何进行序列化：
                    - 在JS中有一个工具类 JSON （JavaScript Object Notation） JS对象表示法
                    - JS对象序列化后会转换为一个字符串，这个字符串我们称其为JSON字符串(一种格式)  
                    
                - 也可以手动的编写JSON字符串，在很多程序的配置文件就是使用JSON编写的
                - 编写JSON的注意事项：
                    1. JSON字符串有两种类型：
                        JSON对象 {}
                        JSON数组 []
                    2. JSON字符串的属性名必须使用双引号引起来
                    3. JSON中可以使用的属性值（元素）
                        - 数字（Number）
                        - 字符串（String） 必须使用双引号
                        - 布尔值（Boolean）
                        - 空值（Null）
                        - 对象（Object {}）
                        - 数组（Array []）
                    4. JSON的格式和JS对象的格式基本上一致的，
                        注意：JSON字符串如果属性是最后一个，则不要再加,
        */

        const obj = {
            name: "孙悟空",
            age: 18,
        }

        // 将obj转换为JSON字符串
        const str = JSON.stringify(obj) //JSON.stringify() 可以将一个对象转换为JSON字符串(原理就是创建一个新的json字符串)
        const obj2 = JSON.parse(str) // JSON.parse() 可以将一个JSON格式的字符串转换为JS对象

        // console.log(obj)
        // console.log(str) // {"name":"孙悟空","age":18}
        // console.log(obj2) //obj2是深复制 obj===obj2返回false

        const str2 = `{"name":"猪八戒","age":28}`
        const str3 = "{}"
        const str4 = '["hello", true, []]'

        console.log(str2)
    </script>
```

## 4.使用json进行深复制

### (1).深浅复制的区别

**浅复制**

![uTools_1673772622550](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1673772622550.png)

**深复制**

![](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1673772667138.png)

```html
        <script>
            const obj = {
                name: "孙悟空",
                friend: {
                    name: "猪八戒",
                },
            }

            // 对obj进行浅复制
            const obj2 = Object.assign({}, obj)

            // 对obj进行深复制
            const obj3 = structuredClone(obj)

            // 利用JSON来完成深复制
            const str = JSON.stringify(obj) //先转成json
            const obj4 = JSON.parse(str) //在转成对象
		   //简便写法
            const obj5 = JSON.parse(JSON.stringify(obj))
        </script>
```

## 5.Map(键值对结构)

```html
    <script>
        /* 
            Map
                - Map用来存储键值对结构的数据（key-value）
                - Object中存储的数据就可以认为是一种键值对结构
                - Map和Object的主要区别：
                    - Object中的属性名只能是字符串或符号，如果传递了一个其他类型的属性名，
                        JS解释器会自动将其转换为字符串
                    - Map中任何类型的值都可以称为数据的key
        */

        const obj2 = {}

        const obj = {
            "name": "孙悟空",
            'age': 18,
            //对象中不传字符串就要用[]包住
            [Symbol()]: "哈哈",
            //obj2自动转换为字符串 隐式转换为[object object] 通过obj[obj2]或obj[{}]可以取出值
            [obj2]: "嘻嘻"
        }

        // console.log(obj)

        /* 
            创建：
                new Map()

            属性和方法：
                map.size() 获取map中键值对的数量
                map.set(key, value) 向map中添加键值对
                map.get(key) 根据key获取值   
                map.delete(key) 删除指定数据
                map.has(key) 检查map中是否包含指定键
                map.clear() 删除全部的键值对
        */

        // 创建一个Map
        const map = new Map()

        map.set("name", "孙悟空")
        map.set(obj2, "呵呵") //obj2对象成为了钥匙
        map.set(NaN, "哈哈哈")

        map.delete(NaN)
        // map.clear()

        console.log(map)
        console.log(map.get("name"))
        console.log(map.has("name"))
        console.log(map.has(obj2));
    </script>
```

### (1).map转化为数组

```html
    <script>
        const map = new Map()

        map.set("name", "孙悟空")
        map.set("age", 18)
        map.set({}, "呵呵")

        // 将map转换为数组
        const arr = Array.from(map) // [["name","孙悟空"],["age",18]]
        const arr = [...map]

		//传入数组的时候会自动转换
        const map2 = new Map([
            ["name", "猪八戒"],
            ["age", 18],
            [{}, () => { }],
        ])

        console.log(map2)//Map(3) {size: 3, name => 猪八戒, age => 18, {} => () => { }}
        //如果数组有3个数及以上 只取前俩个为键值对

        // 遍历map
        1.for (const entry of map) {
            const [key, value] = entry
            console.log(entry,key,value);
        }
        
        2.for (const [key, value] of map) {
            console.log(key, value)
         }

        3.map.forEach((key, value)=>{
             console.log(key, value)
         })

        /* 
            map.keys() - 获取map的所有的key
            map.values() - 获取map的所有的value
            map.entries() - 获取map的所有键值对
        */

        for (const key of map.keys()) {
            console.log(key)
        }
    </script>
```

## 6.Set集合

```html
    <script>
        /* 
            Set
                - Set用来创建一个集合
                - 它的功能和数组类似，不同点在于Set中不能存储重复的数据

            - 使用方式：
                创建
                    - new Set()
                    - new Set([...])

                方法
                    size 获取数量
                    add() 添加元素
                    has() 检查元素
                    delete() 删除元素
                    
                set要取元素要先转化为数组
                    
        */

        // 创建一个Set
        const set = new Set()

        // 向set中添加数据
        set.add(10)
        set.add("孙悟空")
        set.add(10)

        console.log(set)//Set(2) {size: 2, 10, 孙悟空}

        //遍历
        for(const item of set){
             console.log(item)
         }

        const arr = [...set] //转化为数组
        const arr = Array.from(set) //转化为数组

		//将数组直接传给set
        const arr2 = [1, 2, 3, 2, 1, 3, 4, 5, 4, 6, 7, 7, 8, 9, 10]
        const set2 = new Set(arr2)
        console.log([...set2])//[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    </script>
```

### 1.set和map

**1.都能被转化为数组   2.数组值能整个传给map和set**

## 7.Math数学工具类

```html
        <script>
            /*
                Math
                    - Math一个工具类
                    - Math中为我们提供了数学运算相关的一些常量和方法
                    - 常量：
                        Math.PI 圆周率
                    - 方法：
                        Math.abs() 求一个数的绝对值
                        Math.min() 求多个值中的最小值
                        Math.max() 求多个值中的最大值
                        Math.pow() 求x的y次幂
                        Math.sqrt() 求一个数的平方根

                        Math.floor() 向下取整
                        Math.ceil() 向上取整
                        Math.round() 四舍五入取整
                        Math.trunc() 直接去除小数位

                        Math.random() 生成一个0-1之间的随机数
            */

            // console.log(Math.PI)

            let result = Math.abs(10)
            result = Math.abs(-10)

            result = Math.min(10, 20, 30, 44, 55, -1)
            result = Math.max(10, 20, 30, 44, 55, -1)
            result = Math.pow(4, 2) // 4 ** 2
            result = Math.sqrt(4) // 4 ** .5

            result = Math.floor(1.2)
            result = Math.ceil(1.2)
            result = Math.round(1.4)
            result = Math.trunc(1.5)

            for (let i = 0; i < 50; i++) {
                /* 
                    生成0-5之间的随机数
                        Math.random() --> 0 - 1
                        生成 0-x之间的随机数：
                            Math.round(Math.random() * x)
                            Math.floor(Math.random() * (x + 1))

                        生成 x-y 之间的随机数
                            Math.round(Math.random() * (y-x) + x)
                */
                // result = Math.round(Math.random() * 5)
                // result = Math.floor(Math.random() * 6)

                // 1-6
                // result = Math.round(Math.random() * 5 + 1)

                // 11 - 20
                result = Math.round(Math.random() * 9 + 11)

                console.log(result)
            }
        </script>
```

## 8.Date时间类

```html
        <script>
            /* 
                Date
                    - 在JS中所有的和时间相关的数据都由Date对象来表示
                    - 对象的方法：
                        getFullYear() 获取4位年份
                        getMonth() 返当前日期的月份（0-11）
                        getDate() 返回当前是几日
                        getDay() 返回当前日期是周几（0-6） 0表示周日
                        ......

                        getTime() 返回当前日期对象的时间戳
                            时间戳：自1970年1月1日0时0分0秒到当前时间所经历的毫秒数
                            计算机底层存储时间时，使用都是时间戳
                        Date.now() 获取当前的时间戳

            */

            let d = new Date() // 直接通过new Date()创建时间对象时，它创建的是当前的时间的对象

            // 可以在Date()的构造函数中，传递一个表示时间的字符串
            // 字符串的格式：月/日/年 时:分:秒
            // 年-月-日T时:分:秒
            d = new Date("2019-12-23T23:34:35")


            // new Date(年份, 月, 日, 时, 分, 秒, 毫秒)
            d = new Date(2016, 0, 1, 13, 45, 33)

            d = new Date()


            result = d.getFullYear()
            result = d.getMonth()
            result = d.getDate()
            result = d.getDay()

            result = d.getTime()

            console.log(result) // 1659088108520 毫秒
        </script>
```

## 9.时间的格式化前端显示

```html
    <script>
        const d = new Date()

        let result = d.toLocaleDateString() // 将日期转换为本地的字符串
        result = d.toLocaleTimeString() // 将时间转换为本地的字符串

        /* 
        toLocaleString()
            - 可以将一个日期转换为本地时间格式的字符串
            - 参数：
                1. 描述语言和国家信息的字符串
                    zh-CN 中文中国
                    zh-HK 中文香港
                    en-US 英文美国
                2. 需要一个对象作为参数，在对象中可以通过对象的属性来对日期的格式进行配置
                        dateStyle 日期的风格
                        timeStyle 时间的风格
                            full 正常
                            long 长
                            medium 中
                            short  短

                        hour12 是否采用12小时值
                            true
                            false

                        weekday 星期的显示方式
                            long
                            short
                            narrow

                        year
                            numeric 4位显示
                            2-digit 2位显示                      
    */
        result = d.toLocaleString("zh-CN", {
            year: "numeric",
            month: "long",
            day: "2-digit",
            weekday: "short",
        })

        console.log(result)
    </script>
```

## 10.包装类(正常是js自己用的)(面试题)

```html
    <script>
            /* 
                在JS中，除了直接创建原始值外，也可以创建原始值的对象(通过对象的方式创建原始值)

                    通过 new String() 可以创建String类型的对象
                    通过 new Number() 可以创建Number类型的对象
                    通过 new Boolean() 可以创建Boolean类型的对象
                        - 但是千万不要这么做 //俩个这样创建的对象内容一致也不相等

                包装类：
                    JS中一共有5个包装类
                        String --> 字符串包装为String对象
        			   Number-- > 数值包装为Number对象
       				   Boolean-- > 布尔值包装为Boolean对象
        			   BigInt-- > 大整数包装为BigInt对象(我们不能调用)
        			   Symbol-- > 符号包装为Symbol对象(我们不能调用)
            			- 通过包装类可以将一个原始值包装为一个对象，
        					当我们对一个原始值调用方法或属性时，JS解释器会临时将原始值包装为对应的对象
        						然后调用这个对象的属性或方法

            - 由于原始值会被临时转换为对应的对象，这就意味着对象中的方法都可以直接通过原始值来调用
          */

        let str = new String("hello")
        let num = new Number(11)
        let bool = new Boolean(true)
        let bool2 = new Boolean(true)
        console.log(bool === bool2) //false  对象比较的时候是比较内存地址的,所以不要new String()

        let str = "hello"
        str.name = "哈哈"//给原始值添加属性原本会报错，此时js解释器会临时创建字符串对象暂时存储(添加到一次性对象里)
        console.log(str.name) //返回undefined 此时又会转一次 所以读不到name属性 因为存到上一个一次性对象里了

        let num = 11
        num = num.toString()//原始值调用方法 js会临时转换成Number对象 然后调用toString方法

        // null.toString()
	   //由于原始值会被临时转换为对应的对象，这就意味着对象中的方法都可以直接通过原始值来调用
        //number原始值去调很多方法
        //字符串原始值可以去调用很多方法
        console.log(num)
    </script>
```

## 11.String字符串的方法

```html
        <script>
            /* 
                https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String

                字符串：
                    - 字符串其本质就是一个字符数组
                    - "hello" --> ["h", "e", "l", "l", "o"]
                    - 字符串的很多方法都和数组是非常类似的
                    - 属性和方法(全是非破坏性的，不影响原来数组)：
                        length 获取字符串的长度
                        字符串[索引] 获取指定位置的字符
                        str.at() （实验方法）
                            - 根据索引获取字符，可以接受负索引
                        str.charAt()
                            - 根据索引获取字符
                        str.concat()
                            - 用来连接两个或多个字符串
                        str.includes()
                            - 用来检查字符串中是否包含某个内容
                                有返回true
                                没有返回false
                        str.indexOf()
                            - 有返回索引
                            - 第一次出现
                        str.lastIndexOf()
                            - 有返回索引
                            - 最后一次出现
                            - 查询字符串中是否包含某个内容
                        str.startsWith()
                            - 检查一个字符串是否以指定内容开头
                        str.endsWith()
                            - 检查一个字符串是否以指定内容结尾
                        str.padStart()
                        -   - 往前补内容
                        str.padEnd()
                            - 通过添加指定的内容，使字符串保持某个长度
                        str.replace()
                            - 使用一个新字符串替换一个指定内容(替换第一个,也是返回新的字符串)
                        str.replaceAll()    
                            - 使用一个新字符串替换所有指定内容
                        str.slice()
                            - 对字符串进行切片
                        str.substring() //这个方法会比较智能交换参数1位置
                            - 截取字符串
                        str.substr()
                            - 参数为 起始位置和截取长度
                        str.split()
                            - 用来将一个字符串拆分为一个数组(参数是什么遇见参数就拆分)
                        str.toLowerCase()
                            - 将字符串转换为小写
                        str.toUpperCase()
                            - 将字符串转换为大写
                        str.trim()
                            - 去除前后空格
                        str.trimStart()
                            - 去除开始空格
                        str.trimEnd()
                            - 去除结束空格
            */

            let str = "hello"

            // console.log(str[0])

            // for(let char of str){
            //     console.log(char)
            // }

            // console.log(str.at(0))
            // console.log(str.charAt(0))

            str = "hello hello how are you"

            // console.log(str.includes("how", 13))

            // console.log(str.endsWith("you"))

            str = "100"

            // console.log(str.padStart(7, "0"))


            str = "hello hello how are you"

            let result = str.replace("hello", "abc")
            result = str.replaceAll("hello", "abc")

            result = str.slice(12, 15)
            result = str.substring(12, 15)
            result = str.substring(15, 12)


            str = "abc@bcd@efg@jqk" // ["abc", "bcd", "efg", "jqk"]

            result = str.split("@")

            str = "abcdABCD"

            result = str.toLowerCase()


            str = "    ab  c     "

            console.log(result)
        </script>
```

## 12.正则表达式(规则表达式) 字符串中的正则表达式

```html
    <script>
        /* 
            正则表达式
                - 正则表达式用来定义一个规则
                - 通过这个规则计算机可以检查一个字符串是否符合规则
                    或者将字符串中符合规则的内容提取出来
                - 正则表达式也是JS中的一个对象，
                    所以要使用正则表达式，需要先创建正则表达式的对象
        */


        // new RegExp() 可以接收两个参数（字符串） 1.正则表达式 2.匹配模式
        let reg = new RegExp("a", "i") // 通过构造函数来创建一个正则表达式的对象(动态)

        // 使用字面量来创建正则表达式：/正则/匹配模式
        reg = /a/i

        reg = /\w/

        reg = new RegExp("\\w")

        // console.log(reg)

        reg = new RegExp("a") // /a/ 表示，检查一个字符串中是否有a

        // 通过正则表达式检查一个字符串是否符合规则
        let str = "a"

        let result = reg.test(str) // true

        result = reg.test("b") // false
        result = reg.test("abc") // true
        result = reg.test("bcabc") // true

        console.log(result);

    </script>
```

## 13.正则表达式的语法

```html
        <script>
            /* 
                1.在正则表达式中大部分字符都可以直接写
                2.| 在正则表达式中表示或
                3.[] 表示或（字符集）
                    [a-z] 任意的小写字母
                    [A-Z] 任意的大写字母
                    [a-zA-Z] 任意的字母
                    [0-9]任意数字
                4.[^] 表示除了
                    [^x] 除了x
                5. . 表示除了换行外的任意字符
                6. 在正则表达式中使用\作为转义字符
                7. 其他的字符集
                    \w 任意的单词字符 [A-Za-z0-9_]
                    \W 除了单词字符 [^A-Za-z0-9_]
                    \d 任意数字 [0-9]
                    \D 除了数字 [^0-9]
                    \s 空格
                    \S 除了空格
                    \b 单词边界
                    \B 除了单词边界
                8. 开头和结尾
                    ^ 表示字符串的开头
                    $ 表示字符串的结尾
            */ 

            let re = /abc|bcd/

            re = /[a-z]/

            re = /[A-Z]/

            re = /[A-Za-z]/

            re = /[a-z]/i // 匹配模式i表示忽略大小写

            re = /[^a-z]/ // 匹配包含小写字母以外内容的字符串

            re = /./

            re = /\./

            re = /\w/

            re = /^a/ // 匹配开始位置的a

            re = /a$/ // 匹配结束位置的a

            re = /^a$/ // 只匹配字母a，完全匹配，要求字符串必须和正则完全一致

            re = /^abc$/


            let result = re.test('aa')

            console.log(result)
        </script>
```

## 14.正则表达式的量词

![image-20230921165412292](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230921165412292.png)

```html
        <script>
            /* 
                量词
                    {m} 正好m个
                    {m,} 至少m个
                    {m,n} m-n个(m~n个)
                    + 一个以上，相当于{1,}
                    * 任意数量的a
                    ? 0-1次 {0,1}
            */
           // i表示忽略大小写
           // g表示全局匹配

            let re = /a{3}/

            re = /^a{3}$/  //只有3个a 必须正好
            re = /^ab{3}&/ //此时判断的是字符串是否为abbb 只对b起作用 
            //量词只对前面那个起作用

            re = /^(ab){3}$/

            re = /^[a-z]{3}$/ //任意3个字母

            re = /^[a-z]{1,}$/ //至少1个

            re = /^[a-z]{1,3}$/

            re = /^ba+$/ //b后面至少一个a  

            re = /^ba*$/
            
            re = /^ba?$/

            let result = re.test("baa")

            console.log(result)
        </script>
```



## 15.正则表达式的方法exec和test  也属于字符串方法

```html
        <script>
            /* 
                re.test()
                    - 测试是否符合正则表达式的规则
                     true|false
                re.exec()
                    - 获取字符串中符合正则表达式的内容
                    没有找到返回null
            */
           let str = "abcaecafcacc"

           // 提取出str中符合axc格式的内容
        
           // i表示忽略大小写
           // g表示全局匹配
           let re = /a(([a-z])c)/ig

           //groups表示分组,给需要分组的元素加上()

           let result = re.exec(str)

        //    console.log(result)


            while(result){
                console.log(result[0], result[1], result[2])
                result = re.exec(str)
            }
        </script>
```

## 16.提取手机号练习

```html
    <script>
        /* 
            dajsdh13715678903jasdlakdkjg13457890657djashdjka13811678908sdadadasd

            用自己的语言来把描述出来
                1    3         501789087
                1    3到9之间   任意数字 x 9
        
        */

        let re = /1[3-9]\d{9}/g

        re = /(1[3-9]\d)\d{4}(\d{4})/g

        let str = "dajsdh13715678903jasdlakdkjg13457890657djashdjka13811678908sdadadasd";

        let result = re.exec(str)
        while (result) {
            // console.log(result[0], result[1], result[2])
            console.log(result[1] + "****" + result[2])
            result = re.exec(str)
        }

        re = /^1[3-9]\d{9}$/ //手机号完全匹配

        console.log(re.test("13456789042")) //true
    </script>
```

## 17.字符串的正则表达式方法

```html
    <script>
        /* 
            split()
                - 可以根据正则表达式来对一个字符串进行拆分
            search()
                - 可以去搜索符合正则表达式的内容第一次在字符串中出现的位置
            replace()
                - 根据正则表达式替换字符串中的指定内容
            match()
                - 根据正则表达式去匹配字符串中符合要求的内容(整体取出来,不会取分组的数据)
            matchAll()
                - 根据正则表达式去匹配字符串中符合要求的内容(必须设置g 全局匹配)
                - 它返回的是一个迭代器
        
        */

        let str = "a@b@c@d"

        let result = str.split("@")

        str = "孙悟空abc猪八戒adc沙和尚"
        result = str.split(/a[bd]c/)

        str =
            "dajsdh13715678903jasdlakdkjg13457890657djashdjka13811678908sdadadasd"

        result = str.search("abc")
        result = str.search(/1[3-9]\d{9}/)

        result = str.replace(/1[3-9]\d{9}/g, "哈哈哈")

        result = str.match(/1[3-9]\d{9}/g)

        result = str.matchAll(/1[3-9](\d{9})/g)

        for (let item of result) {
            console.log(item)
        }

    </script>
```





## 18.垃圾回收

![uTools_1675265137516](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675265137516.png)

```html
        <script>
            /* 
                垃圾回收（Garbage collection）
                    - 和生活一样，生活时间长了以后会产生生活垃圾
                        程序运行一段时间后也会产生垃圾
                    - 在程序的世界中，什么是垃圾？
                        - 如果一个对象没有任何的变量对其进行引用，那么这个对象就是一个垃圾
                        - 垃圾对象的存在，会严重的影响程序的性能
                        - 在JS中有自动的垃圾回收机制，这些垃圾对象会被解释器自动回收，我们无需手动处理
                        - 对于垃圾回收来说，我们唯一能做的事情就是将不再使用的变量设置为null
            */


            let obj = {name:"孙悟空"}
            let obj2 = obj

            //只要还有一个对象在引用就不是垃圾对象
            obj = null 
            obj2 = null
        </script>
```

# 十、DOM对象

面向对象：1.知道该对象代表什么有什么用(知对象) 2.拿对象 3.对象的方法和属性怎么用(用对象)

## 1.什么是DOM

**D 文档(整个网页就是一个文档)  O 对象(一切都是对象,可以操作对象)  M  模型(体现对象之间的关系)**

**DOM文档对象模型,BOM浏览器对象模型**

![uTools_1675348807927](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675348807927.png)

**所有对象的原型链上都能找到Node(父类)**

![uTools_1675349793022](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675349793022.png)

## 2.如何使用DOM对象

```html
        <button id="btn">点我一下</button>

        <script>
            /* 
                要使用DOM来操作网页，我们需要浏览器至少得先给我一个对象
                    才能去完成各种操作

                所以浏览器已经为我们提供了一个document对象，它是一个全局变量可以直接使用
                    document代表的是整个的网页
                windows是整个浏览器视口 比document还大  window.document得到的结果是一样的    
            */

            // console.log(document)

            // 获取btn对象
            const btn = document.getElementById("btn")//根据id获取一个元素节点对象

            // console.log(btn)
            // 修改btn中的文字
            btn.innerText = "Click ME"
        </script>
```

![image-20230312102603877](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230312102603877.png)

## 3.doucument对象文档结点

```html
    <a href="#">hhh</a>
    <script>

        /* 
            document对象
                - document对象表示的是整个网页
                - document对象的原型链
                    HTMLDocument(document本身) -> Document -> Node -> EventTarget -> Object.prototype -> null
                - 凡是在原型链上存在的对象的属性和方法都可以通过Document去调用
                - 部分属性：
                    document.documentElement --> html根元素
                    document.head --> head元素
                    document.title --> title元素
                    document.body --> body元素
                    document.links --> 获取页面中所有的超链接
                    ...
        */
        console.log(document.links)
    </script>
```

## 4.元素节点

```html
<body>
    <button id="btn">点我一下</button>
    <span class="s1">我是span</span>
    <span class="s1">我是span</span>
    <span class="s1">我是span</span>
    <span class="s1">我是span</span>
    <span class="s1">我是span</span>

    <div>我是div</div>
    <div>我是div</div>
    <div>我是div</div>
    <div>我是div</div>
    <div>我是div</div>

    <form>
        <input type="text" name="username">
        <input type="radio" name="gender" value="male"> 男
        <input type="radio" name="gender" value="female"> 女
    </form>

    <script>
        /* 
            元素节点对象（element）
                - 在网页中，每一个标签都是一个元素节点
                - 如何获取元素节点对象？
                    1. 通过document对象来获取元素节点
                    2. 通过document对象来创建元素节点
                - 通过document来获取已有的元素节点：
                    document.getElementById()
                        - 根据id获取一个元素节点对象
                    document.getElementsByClassName()
                        - 根据元素的class属性值获取一组元素节点对象
                        - 返回的是一个类数组对象
                        - 该方法返回的结果是一个实时更新的集合
                            当网页中新添加元素时，集合也会实时的刷新
                    document.getElementsByTagName()
                        - 根据标签名获取一组元素节点对象
                        - 返回的结果是可以实时更新的集合
                        - document.getElementsByTagName("*") 获取页面中所有的元素
                    document.getElementsByName()
                        - 根据name属性获取一组元素节点对象
                        - 返回一个实时更新的集合
                        - 主要用于表单项
                    document.querySelectorAll()
                        - 根据选择器去页面中查询元素
                        - 会返回一个类数组（不会实时更新）
                    document.querySelector()
                        - 根据选择器去页面中查询第一个符合条件的元素

                - 创建一个元素节点
                    document.createElement()
                        - 根据标签名创建一个元素节点对象
                */

        const btn = document.getElementById("btn")//根据元素id获取元素节点

        const spans = document.getElementsByClassName("s1")//根据元素的class属性值获取一组元素节点对象 实时更新

        const divs = document.getElementsByTagName("div")//根据标签名获取一组元素节点对象  实时更新

        const genderInput = document.getElementsByName("gender")//根据name属性获取一组元素节点对象   实时更新

        const divs2 = document.querySelectorAll("div")//根据选择器去页面中查询元素 全部返回

        const div = document.querySelector("div")//根据选择器去页面中查询第一个符合条件的元素

        const h2 = document.createElement("h2")//创建节点

    </script>
```

## 5.元素节点的属性和方法

```html
    <body>
        <div id="box1">
            我是box1
            <span class="s1">我是s1</span>
            <span class="s1">我是s1</span>
        </div>

        <span class="s1">我是s1</span>

        <script>
            /* 
                div元素的原型链
                    HTMLDivElement -> HTMLElement -> Element -> Node -> ...

                通过元素节点对象获取其他节点的方法(加♥重点)
                    element.childNodes 获取当前元素的子节点（会包含空白的子节点和文本节点）
                    ♥♥element.children 获取当前元素的子元素(不会包含空白的子节点和文本节点)
                    element.firstElementChild 获取当前元素的第一个子元素(会包含空白的子节点)
                    element.lastElementChild 获取当前元素的最后一个子元素(会包含空白的子节点)
                    element.firstChild 获取第一个节点
                    element.lastChild 获取最后一个节点
                    element.nextSibling 获取当前元素的下一个节点(会包含空白的子节点)
                    ♥♥element.nextElementSibling 获取当前元素的下一个兄弟元素(不会包含空白的子节点)
                    ♥♥element.previousElementSibling 获取当前元素的前一个兄弟元素(不会包含空白的子节点)
                    ♥♥element.parentNode 获取当前元素的父节点
                    element.parentElement 获取当前元素的父元素(文档对象不是元素获取不到 得到null)
                    ♥♥element.tagName 获取当前元素的标签名
            */

            const box1 = document.getElementById("box1")

            const spans = box1.getElementsByTagName("span")

            const spans2 = box1.getElementsByClassName("s1")

            const cns = box1.childNodes

            const children = box1.children

            console.log(children.length)
            
            const a = document.getElementById("box").tagName  //打印出标签名 DIV
        </script>
```

## 6.文本节点

**文本和属性都是位于标签(元素)内部的,所以我们可以直接通过操作标签来修改文本和属性**

![uTools_1675443016969](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675443016969.png)

```html
    <body>
        <div id="box1">
            <span style="text-transform: uppercase;">我是box1</span>
        </div>

        <script>
            /* 
                在DOM中，网页中所有的文本内容都是文本节点对象,
                    可以通过元素来获取其中的文本节点对象，但是我们通常不会这么做

                    我们可以直接通过元素去修改其中的文本
                        修改文本的三个属性
                            element.textContent 获取或修改元素中的文本内容
                                - 获取的是标签中的内容，不会考虑css样式

                            element.innerText 获取或修改元素中的文本内容
                                - innerText获取内容时，会考虑css样式
                                - 通过innerText去读取CSS样式，会触发网页的重排（计算CSS样式,所以性能差一点）
                                - 当字符串中有标签时，会自动对标签进行转义
                                - <li> --> &lt;li&gt;//转义成字符
                                    
                            element.innerHTML 获取或修改元素中的html代码
                                - 可以直接向元素中添加html代码
                                - innerHTML插入内容时，有被xss注入的风险(恶意添加代码)

            */

            const box1 = document.getElementById("box1")

            // const text = box1.firstChild
            // console.log(text)

            // box1.innerText = "xxxx"
            // console.log(box1.textContent)
            
            // box1.textContent = "新的内容"

            /* box1.innerHTML = "<、script src='https://sss/sss.js'><\/script>" *///用户通过这种方式留言时网站有被恶意注入的风险
        </script>
```

## 7.属性节点

**文本和属性都是位于标签(元素)内部的,所以我们可以直接通过操作标签来修改文本和属性**

```html
    <body>
        <input class="a" type="text" name="username" value="admin">
        <script>
           
            /* 
                属性节点（Attr）
                    - 在DOM也是一个对象，通常不需要获取对象而是直接通过元素即可完成对其的各种操作
                    - 如何操作属性节点：
                        方式一：
                            读取：元素.属性名（注意，class属性需要使用className来读取）
                                    读取一个布尔值时，会返回true或false

                            修改：元素.属性名 = 属性值

                        方式二：
                            读取：元素.getAttribute(属性名)

                            修改：元素.setAttribute(属性名, 属性值)

                            删除：元素.removeAttribute(属性名)
            */
            // const input = document.getElementsByName("username")[0]

            //不使用元素节点时需要这样读取
            const input = document.querySelector("[name=username]")
            console.log(input.type)
			
            //直接读取
            console.log(input.getAttribute("type"))

            //修改属性
            input.setAttribute("value", "孙悟空")

            //利用修改来添加属性
            input.setAttribute("disabled", "disabled")
        </script>
```

## 8.事件简介

```html
    <body>
        <!-- <button id="btn" onmouseenter="alert('你点我干嘛~')">点我一下</button> -->
        <!-- onclick单击  ondbclick双击 onmouseenter鼠标移入 -->
        <button id="btn">点我一下</button>

        <script>
            /* 
               事件（event）
                - 事件就是用户和页面之间发生的交互行为
                    比如：点击按钮、鼠标移动、双击按钮、敲击键盘、松开按键...  
                - 可以通过为事件绑定响应函数（回调函数），来完成和用户之间的交互
                - 绑定响应函数的方式：
                    1.可以直接在元素的属性中设置
                    2.可以通过为元素的指定属性设置回调函数的形式来绑定事件（一个事件只能绑定一个响应函数,不能重复绑定）
                    3.可以通过元素addEventListener()方法来绑定事件(添加事件监听器,一个事件可以绑定多个响应函数)
                        - 不用加on on表示当什么什么的时候
                        - 推举使用
            */

            // 获取到按钮对象
            const btn = document.getElementById("btn")
            // 为按钮对象的事件属性设置响应函数
            // btn.onclick = function(){
            //     alert("我又被点了一下~~")
            // }

            // btn.onclick = function(){
            //     alert("1123111")
            // }
            
            // 后面绑定的会覆盖前面的
            btn.addEventListener("click", function(){
                alert("哈哈哈")
            })

            btn.addEventListener("click", function(){
                alert("嘻嘻嘻")
            })

            btn.addEventListener("click", function(){
                alert("呜呜呜")
            })
        </script>
```

## 9.文档的加载

```html
    <script>
        /*
            网页是自上向下加载的，如果将js代码编写到网页的上边,
            js代码在执行时，网页还没有加载完毕，这时会出现无法获取到DOM对象的情况

                window.onload事件会在窗口中的内容加载完毕之后才触发(有内联框架等情况时,所有文档加载完才生效,速度慢)
                document的DOMContentLoaded事件会在当前文档加载完毕之后触发(速度快)

                如何解决这个问题：
                    1. 将script标签编写到body的最后   1
                    2. 将代码编写到window.onload的回调函数中    4
                    3. 将代码编写到document对象的DOMContentLoaded的回调函数中（执行时机更早）  3
                    4. 将代码编写到外部的js文件中，然后以defer的形式进行引入（执行时机更早，早于DOMContentLoaded）  2
        */

            // window.onload = function () {
            //     const btn = document.getElementById("btn")
            //     console.log(btn)
            // }

            // window.addEventListener("load", function () {
            //     const btn = document.getElementById("btn")
            //     alert(btn)
            // })

            // document.addEventListener("DOMContentLoaded", function () {
            //     const btn = document.getElementById("btn")
            //     alert(btn)
            // })
    </script>

    <script defer src="./script/script.js"></script>
</head>

<body>
    <button id="btn">点我一下</button>

    <iframe src="https://www.lilichao.com" frameborder="0"></iframe>

    <script>
            // const btn = document.getElementById("btn")
            // console.log(btn)
    </script>
</body>
```

## 10.切换图片练习

```html
    <title>切换图片</title>
    <style>
        .outer {
            width: 640px;
            margin: 50px auto;
            text-align: center;
        }
    </style>
    <script>
        window.onload = function () {
            // 获取info对象
            const info = document.getElementById("info");

            // 获取img对象
            const img = document.querySelector("img");
            // 获取上一个按钮对象
            const prev = document.getElementById("prev");
            // 获取下一个按钮对象
            const next = document.getElementById("next");

            // 创建一个数组来存储图片的路径
            const imgArr = [
                "./images/1.png",
                "./images/2.png",
                "./images/3.png",
                "./images/4.png",
                "./images/5.png",
            ]

            // 记录索引
            let current = 0;
            // info文本设置
            info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`


            prev.onclick = function () {
                // 改变图片就是改变图片的路径
                current--;
                // 实现循环切换图片的效果
                if (current < 0) {
                    current = imgArr.length - 1;
                }
                img.src = imgArr[current]
                info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`
            }


            next.onclick = function () {
                // 改变图片就是改变图片的路径
                current++;
                // 实现循环切换图片的效果
                if (current > imgArr.length - 1) {
                    current = 0;
                }
                img.src = imgArr[current]
                info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`
            }

        }
    </script>
</head>

<body>
    <div class="outer">

        <p id="info">
            总共n张图片，当前第 m 张
        </p>

        <div class="img-warpper">
            <img src="./images/1.png" alt="">
        </div>

        <div class="btn-warpper">
            <button id="prev">上一张</button>
            <button id="next">下一张</button>
        </div>
    </div>
</body>

```

## 11.文本框勾选练习

```html
    <script>
        /* 
            全选功能
            取消
            反选
            提交
            小checkbox和大checkbox同步
        */

        window.onload = function () {
            /* 
                全选功能
                    - 点击按钮后，使四个多选框都变成选中状态
            */
            // 获取4个多选框
            const hobbies = document.getElementsByName("hobby");
            // 获取全选按钮
            const allBtn = document.getElementById("all");
            // 获取上面那个全选按钮 check-all
            const checkAllBox = document.getElementById("check-all");

            // 为全选按钮绑定响应事件
            allBtn.onclick = function () {
                // 将多选框设置为选中状态
                for (let i = 0; i < hobbies.length; i++) {
                    hobbies[i].checked = true
                }
                // 当4个多选框都选中时  记得同步上面的全选按钮
                checkAllBox.checked = true
            }

            /* 
                取消功能
                    - 点击取消按钮后，取消所有的选中的状态
            */
            // 获取取消按钮
            const noBtn = document.getElementById("no")

            // 为取消按钮绑定响应事件
            noBtn.onclick = function () {
                for (let i = 0; i < hobbies.length; i++) {
                    hobbies[i].checked = false
                }
                // 当有一个多选框不选中时  记得同步上面的全选按钮
                checkAllBox.checked = false
            }

            /* 
                反选功能
                    - 点击按钮后，选中的取消，没选中的选中
            */
            // 获取反选按钮
            const reverseBtn = document.getElementById("reverse")
            // 绑定事件
            reverseBtn.onclick = function () {
                for (let i = 0; i < hobbies.length; i++) {
                    hobbies[i].checked = !hobbies[i].checked //反选功能
                }
                // 获取所有选中的checkbox
                const checkedBox = document.querySelectorAll(
                    "[name=hobby]:checked"
                    // :checked 伪类选择器 表示选中
                )

                // 判断hobbies是否全选
                if (hobbies.length === checkedBox.length) {
                    checkAllBox.checked = true
                } else {
                    checkAllBox.checked = false
                }
            }

            /* 
    提交按钮
        - 点击按钮后，将选中的内容显示出来
*/
            const sendBtn = document.getElementById("send")
            sendBtn.onclick = function () {
                for (let i = 0; i < hobbies.length; i++) {
                    if (hobbies[i].checked) {
                        alert(hobbies[i].value)
                    }
                    // hobbies[i].checked && alert(hobbies[i].value)  也可以使用这种方式 &&是短路运算
                }
            }

            /* 
                check-all
                    - 全选checkbox发生变化后，将小的checkbox和它同步
            */

            checkAllBox.onchange = function () {
                // console.log(this)
                // 在事件的响应函数中，响应函数绑定给谁 this就是谁（箭头函数除外）

                for (let i = 0; i < hobbies.length; i++) {
                    hobbies[i].checked = this.checked //不建议使用这种方式
                }
            }

            /* 
                使全选checkbox和四个checkbox进行同步
                    如果四个全选了，则全选checkbox也选中
                    如果四个没全选，则全选checkbox也不选中
            */

            for (let i = 0; i < hobbies.length; i++) {
                hobbies[i].onchange = function () {
                    // 获取所有选中的checkbox
                    const checkedBox = document.querySelectorAll(
                        "[name=hobby]:checked"
                        // :checked 伪类选择器 表示选中
                    )

                    // 判断hobbies是否全选
                    if (hobbies.length === checkedBox.length) {
                        checkAllBox.checked = true
                    } else {
                        checkAllBox.checked = false
                    }
                }
            }

        }
    </script>
</head>

<body>
    <div>
        <form action="#">
            <div>
                请选择你的爱好:
                <input type="checkbox" id="check-all">全选
            </div>
            <div>
                <input type="checkbox" name="hobby" value="乒乓球" /> 乒乓球
                <input type="checkbox" name="hobby" value="篮球" /> 篮球
                <input type="checkbox" name="hobby" value="羽毛球" /> 羽毛球
                <input type="checkbox" name="hobby" value="足球" /> 足球
            </div>
            <div>
                <button type="button" id="all">全选</button>
                <button type="button" id="no">取消</button>
                <button type="button" id="reverse">反选</button>
                <button type="button" id="send">提交</button>
            </div>
        </form>
    </div>
</body>
```

## 12.DOM对象的修改

```html
<body>
    <button id="btn01">按钮1</button>
    <button id="btn02">按钮2</button>

    <hr />

    <ul id="list">
        <li id="swk">孙悟空</li>
        <li id="zbj">猪八戒</li>
        <li id="shs">沙和尚</li>
    </ul>

    <script>
        /* 
            点击按钮后，向ul中添加一个唐僧
        */

        // 获取ul
        const list = document.getElementById("list")

        // 获取按钮
        const btn01 = document.getElementById("btn01")
        btn01.onclick = function () {
            // <li id="shs">沙和尚</li>

            // 创建一个li
            const li = document.createElement("li")
            // 向li中添加文本
            li.textContent = "唐僧"
            // 给li添加id属性
            li.id = "ts"

            // 1.appendChild() 用于给一个节点添加子节点(添加在最后)
            // list.appendChild(li)

            // 2.insertAdjacentElement()可以向元素的任意位置添加元素
            //两个参数：1.要添加的位置 2.要添加的元素
            // beforeend 标签的最后 afterbegin 标签的开始  
            // beforebegin 在元素的前边插入元素（兄弟元素） afterend 在元素的后边插入元素（兄弟元素）
            // list.insertAdjacentElement("afterend", li)

            // 3.insertAdjacentHTML() 可以直接在任意位置插入代码(用字符串形式"")
            list.insertAdjacentHTML("beforeend", "<li id='bgj'>白骨精</li>")

        }

        const btn02 = document.getElementById("btn02")
        btn02.onclick = function () {
            // 创建一个蜘蛛精替换孙悟空
            const li = document.createElement("li")
            li.textContent = "蜘蛛精"
            li.id = "zzj"

            // 获取swk
            const swk = document.getElementById("swk")

            // 4.replaceWith() 使用一个元素替换当前元素
            // swk.replaceWith(li)

            // 5.remove()方法用来删除当前元素
            swk.remove()

        }
    </script>
</body>
```

## 14.xss攻击

![uTools_1678590568054](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678590568054.png)

## ![uTools_1675618612612](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675618612612.png)

**如果直接使用模板字符串后,网站容易被xss注入攻击**

**如果你的网页中有需要用户输入的内容 不要使用带HTML的方法直接向网页中添加代码的**

## 15.表格添加删除功能练习

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        .outer {
            width: 400px;
            margin: 100px auto;
            text-align: center;
        }

        table {
            width: 400px;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        td,
        th {
            border: 1px black solid;
            padding: 10px 0;
        }

        form div {
            margin: 10px 0;
        }
    </style>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            /* 
                点击删除超链接后，删除当前的员工信息
            */

            // 删除员工的函数单独提取出来 解决了循环会创建多个响应函数的缺陷(它给所有的超链接都一次性创建了响应函数 浪费内存)
            function delEmpHandler() {
                // 本练习中的超链接，我们是不希望发生跳转，但是跳转行为是超链接的默认行为
                // 只要点击超链接就会触发页面的跳转，事件中可以通过取消默认行为来阻止超链接的跳转
                // 使用return false来取消默认行为，只在 xxx.xxx = function(){}这种形式绑定的事件中才适用
                // return false

                // 删除当前员工 删除当前超链接所在的tr
                // this表示当前点击的超链接
                const tr = this.parentNode.parentNode //获取tr才可以删除一整行

                // 获取要删除的员工的姓名
                // const empName = tr.getElementsByTagName("td")[0].textContent
                const empName = tr.firstElementChild.textContent

                // 弹出一个友好的提示
                if (confirm("确认要删除【" + empName + "】吗？")) {
                    // 删除tr
                    tr.remove()
                }
            }

            // 获取所有的超链接
            const links = document.links
            // 为他们绑定单击响应函数
            for (let i = 0; i < links.length; i++) {
                links[i].onclick = delEmpHandler//将函数以对象的形式传给单击事件
                // links[i].addEventListener("click", function(){
                //     alert(123)
                //     return false  addEventListener无法使用这种方法去除默认事件 解决方法是 javascript:;
                // })
            }

            /* 
                点击按钮后，将用户的信息插入到表格中
            */
            // 获取tbody
            const tbody = document.querySelector("tbody")
            const btn = document.getElementById("btn")
            btn.onclick = function () {
                // 获取用户输入的数据
                const name = document.getElementById("name").value //获取值
                const email = document.getElementById("email").value
                const salary = document.getElementById("salary").value

                // 将获取到的数据设置DOM对象
                /* 
                    <tr>
                        <td>孙悟空</td>
                        <td>swk@hgs.com</td>
                        <td>10000</td>
                        <td><a href="javascript:;">删除</a></td>
                    </tr>
                */

                // 创建元素
                const tr = document.createElement("tr")

                // 创建td
                const nameTd = document.createElement("td")
                const emailTd = document.createElement("td")
                const salaryTd = document.createElement("td")

                // 用户直接添加的添加文本不能用innerHTML
                nameTd.innerText = name
                emailTd.textContent = email
                salaryTd.textContent = salary

                // 将三个td添加到tr中
                tr.appendChild(nameTd)
                tr.appendChild(emailTd)
                tr.appendChild(salaryTd)
                tr.insertAdjacentHTML("beforeend", '<td><a href="javascript:;">删除</a></td>')//写死的可以用带HTML的方法

                tbody.appendChild(tr)

                // // 这种写法，容易被xss的攻击
                // tbody.insertAdjacentHTML(
                //     "beforeend",
                //     `
                //         <tr>
                //             <td>${name}</td>
                //             <td>${email}</td>
                //             <td>${salary}</td>
                //             <td><a href="javascript:;">删除</a></td>
                //         </tr>
                //     `
                // )

                // 由于上边的超链接是新添加的，所以它的上边并没有绑定单级响应函数，所以新添加的员工无法删除
                // 解决方式：为新添加的超链接单独绑定响应函数
                // links[links.length - 1] 由于links是实时更新的 这样可以直接获取新添加的超链接
                links[links.length - 1].onclick = delEmpHandler

            }
        })
    </script>
</head>

<body>
    <div class="outer">
        <table>
            <tbody>
                <tr>
                    <th>姓名</th>
                    <th>邮件</th>
                    <th>薪资</th>
                    <th>操作</th>
                </tr>
                <tr>
                    <td>孙悟空</td>
                    <td>swk@hgs.com</td>
                    <td>10000</td>
                    <td><a href="javascript:;">删除</a></td>
                    <!-- href="javascript:;" 这行代码的意思是不进行跳转 转为执行js代码 这一段js代码的效果是什么都不执行-->
                </tr>
                <tr>
                    <td>猪八戒</td>
                    <td>zbj@glz.com</td>
                    <td>8000</td>
                    <td><a href="javascript:;">删除</a></td>
                </tr>
                <tr>
                    <td>沙和尚</td>
                    <td>shs@lsh.com</td>
                    <td>6000</td>
                    <td><a href="javascript:;">删除</a></td>
                </tr>
            </tbody>
        </table>

        <form action="#">
            <div>
                <label for="name">姓名</label>
                <input type="text" id="name" />
            </div>
            <div>
                <label for="email">邮件</label>
                <input type="email" id="email" />
            </div>
            <div>
                <label for="salary">薪资</label>
                <input type="number" id="salary" />
            </div>
            <button id="btn" type="button">添加</button>
            <!-- 按钮默认类型是submit自动提交 可以更改type属性或者设置为return false -->
        </form>
    </div>
</body>

</html>
```

## 16.节点的复制

```html
<body>
    <button id="btn01">点我一下</button>

    <ul id="list1">
        <li id="l1">孙悟空</li>
        <li id="l2">猪八戒</li>
        <li id="l3">沙和尚</li>
    </ul>

    <ul id="list2">
        <li>蜘蛛精</li>
    </ul>

    <script>
        /* 点击按钮后，将id为l1的元素添加list2中 */
        const list2 = document.getElementById("list2")
        const l1 = document.getElementById("l1")
        const btn01 = document.getElementById("btn01")
        btn01.onclick = function () {
            const newL1 = l1.cloneNode(true) // 用来对节点进行复制的

            /* 
                使用 cloneNode() 方法对节点进行复制时，它会复制节点的所有特点包括各种属性
                    这个方法默认只会复制当前节点，而不会复制节点的子节点
                    可以传递一个true作为参数，这样该方法也会将元素的子节点一起复制(包括文本节点)
                    默认为false,只复制当前节点
            */
            newL1.id = "newL1"//更改id
            list2.appendChild(newL1)
        }
    </script>
</body>
```

## 17.修改CSS样式1(js来操控表现,前面16点控制结构)

```html
    <style>
        /* 
            一般我们用js修改样式的时候都是直接修改内联样式
            一般不修改样式表(外部引入)
            样式会直接修改元素的内联样式中(优先级高,一定会实现不会被覆盖)
            */
        /*
        	写css样式的时候不要随便用!important
        	不然使用js修改的时候也要加上!important 太麻烦了
        */
        .box1 {
            width: 200px;
            height: 200px;
            background-color: #bfa;
        }
    </style>
</head>

<body>
    <button id="btn">点我一下</button>

    <hr />

    <div class="box1"></div>

    <script>
        /* 
            点击按钮后，修改box1的宽度
        */

        const btn = document.getElementById("btn")
        const box1 = document.querySelector(".box1")

        btn.onclick = function () {
            // 修改box1的样式
            // 修改样式的方式：元素.style.样式名 = 样式值
            // 如果样式名中含有-，则需要将样式表修改为驼峰命名法
            // background-color --> backgroundColor
            // 因为- 在JS中代表减法
            box1.style.width = "400px"
            box1.style.height = "400px"
            box1.style.backgroundColor = "yellow"
        }
    </script>
```

## 18.读取CSS样式

```html
    <style>
        .box1 {
            height: 200px;
            background-color: #bfa;
        }

        .box1::before {
            content: "hello";
            color: red;
        }
    </style>
</head>

<body>
    <button id="btn">点我一下</button>

    <hr />

    <div class="box1"></div>

    <script>
        /* 
            点击按钮后，读取元素的css样式
            我们要拿到当前生效的样式才有用(内联样式和样式表都不是我们要的)
        */

        const btn = document.getElementById("btn")
        const box1 = document.querySelector(".box1")

        btn.onclick = function () {
            /* 
                getComputedStyle()
                    - 它会返回一个对象，这个对象中包含了当前元素所有的生效的样式
                    - 参数：
                        1. 要获取样式的对象
                        2. 要获取的伪元素
                    - 返回值：
                        返回的一个对象，对象中存储了当前元素的样式

                    - 注意：
                        样式对象中返回的样式值，不一定能拿来直接计算
                            所以使用时，一定要确保值是可以计算的才去计算
                            有的返回值auto变成实际值 有的还是auto
            */
            const styleObj = getComputedStyle(box1)

            console.log(styleObj.width)
            console.log(styleObj.left)

            // console.log(parseInt(styleObj.width) + 100) 计算时要去掉单位
            // box1.style.width = parseInt(styleObj.width) + 100 + "px" 设置数值时要加上单位

            // console.log(styleObj.backgroundColor)

            // 获取伪元素的DOM对象时要使用到第二个参数
            const beforeStyle = getComputedStyle(box1, "::before")
            // console.log(beforeStyle.color)

            console.log(box1.firstElementChild)
        }
    </script>
```

## 19.通过属性读取样式(高宽等)

```html
    <style>
        #box1{
            width: 200px;
            height: 200px;
            padding: 50px;
            margin: 50px;
            border: 10px red solid;
            background-color: #bfa;
            overflow: auto;
        }

        #box2{
            width: 100px;
            height: 500px;
            background-color: orange;
        }

    </style>
</head>
<body>
    <button id="btn">点我一下</button>
    <hr>
    <div>
        <div id="box1">
            <div id="box2"></div>
        </div>
    </div>
    

    <script>
        // 在js中以id命名的标签会被自动创建一个DOM对象,可以被读取到但是不能直接操作
        console.log(btn)

        const btn = document.getElementById("btn")
        const box1 = document.getElementById("box1")

        btn.onclick = function(){
            /* 
                这些方法都是直接拿到没有单位的值 可以直接用
                元素.clientHeight
                元素.clientWidth
                    - 获取元素内部的宽度和高度（包括内容区和内边距）

                元素.offsetHeight
                元素.offsetWidth
                    - 获取元素的可见框的大小（包括内容区、内边距和边框）

                元素.scrollHeight
                元素.scrollWidth
                    - 获取元素滚动区域的大小

                元素.offsetParent
                    - 获取元素的定位父元素
                    - 定位父元素：离当前元素最近的开启了定位的祖先元素，
                        如果所有的元素都没有开启定位则返回body

                元素.offsetTop
                元素.offsetLeft
                    - 获取元素相对于其定位父元素的偏移量

                元素.scrollTop
                元素.scrollLeft
                    - 获取或设置元素滚动条的偏移量(可以直接设置,不止获取)
            */

            // console.log(box1.scrollHeight)
            // console.log(box1.scrollWidth)

            // console.log(box1.offsetParent)

            // console.log(box1.offsetLeft)
            // console.log(box1.offsetTop)

            console.log(box1.scrollTop)
        }
       
    </script>
</body>
</html>
```

![uTools_1678593590076](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1678593590076.png)

## 20.修改CSS样式2

```html
        <style>
            .box1 {
                width: 200px;
                height: 200px;
                background-color: #bfa;
            }


            .box2{
                background-color: yellow;
                width: 300px;
                height: 500px;
                border: 10px greenyellow solid;
            }
        </style>
    </head>
    <body>
        <button id="btn">点我一下</button>

        <hr />

        <div class="box1 box3 box4"></div>

        <script>
            /* 
                点击按钮后，修改box1的宽度
            */

            const btn = document.getElementById("btn")
            const box1 = document.querySelector(".box1")

            btn.onclick = function () {

                // 除了直接修改样式外，也可以通过修改class属性来间接的修改样式
                /* 
                    通过class修改样式的好处(加上一个class类)：
                        1. 可以一次性修改多个样式
                        2. 对JS和CSS进行解耦
                */
                // 直接添加
                // box1.className += " box2" 记得加上空格,不建议这样写 太低端了(容易添加多次同个类)

                // 元素.classList 是一个对象，对象中提供了对当前元素的类的各种操作方法
                /* 
                    元素.classList.add() 向元素中添加一个或多个class(不需要考虑空格)
                    元素.classList.remove() 移除元素中的一个或多个class
                    元素.classList.toggle() 切换元素中的class(有的删除,没有加上,适合做切换的效果)
                    元素.classList.replace() 替换class(后面替换前面的,多个类时不会影响其它类)
                    元素.classList.contains() 检查class
                */
                // box1.classList.add("box2", "box3", "box4")
                // box1.classList.add("box1")//如果要添加的类名已经存在了,不会重复添加

                // box1.classList.remove("box2")
                // box1.classList.toggle("box2")
                // box1.classList.replace("box1", "box2")

                let result = box1.classList.contains("box3")

                console.log(result)
                
            }
        </script>
    </body>
</html>
```

## 21.事件对象简介

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <style>
            #box1{
                width: 300px;
                height: 300px;
                border: 10px greenyellow solid;
            }

        </style>
    </head>
    <body>
        <div id="box1"></div>

        <script>
            /* 
                event 事件
                    - 事件对象
                        - 事件对象是由浏览器在事件触发时所创建的对象，
                            这个对象中封装了事件相关的各种信息
                        - 通过事件对象可以获取到事件的详细信息
                            比如：鼠标的坐标、键盘的按键..
                        - 浏览器在创建事件对象后，会将事件对象作为响应函数的参数传递，
                            所以我们可以在事件的回调函数中定义一个形参来接收事件对象
            */

            const box1 = document.getElementById("box1")

            // box1.onmousemove = event => {  创建参数为event的函数
            //     console.log(event)
            // 	   当箭头函数中只有一个参数时，可以省略()。建议不省略
            // }

            box1.addEventListener("mousemove", event => {
                console.log(event.clientX, event.clientY)

                box1.textContent = event.clientX + "," + event.clientY
            })
        </script>
    </body>
</html>
```

## 22.事件对象event详解

```html
        <style>
            #box1 {
                width: 300px;
                height: 300px;
                background-color: greenyellow;
            }

            #box2 {
                width: 250px;
                height: 250px;
                background-color: #ff0;
            }

            #box3 {
                width: 200px;
                height: 200px;
                background-color: orange;
            }
        </style>
    </head>
    <body>
        <div id="box1">
            <div id="box2">
                <div id="box3"></div>
            </div>
        </div>

        <a id="chao" href="https://lilichao.com">超链接</a>

        <script>
            /* 
            在DOM中存在着多种不同类型的事件对象
                - 多种事件对象有一个共同的祖先 Event
                    - event.target 触发事件的对象
                      this是绑定事件的对象,但是由于冒泡的存在,触发事件的对象是不确定的,2者不一定相等
                    - event.currentTarget 绑定事件的对象（和this一样）
                    - event.stopPropagation() 停止事件的传导
                    - event.preventDefault() 取消默认行为
                - 事件的冒泡（bubble）
                    - 事件的冒泡就是指事件的向上传导
                    - 当元素上的某个事件被触发后，其祖先元素上的相同事件也会同时被触发
                    - 冒泡是默认存在的,和绑定没绑定事件无关
                    - 冒泡的存在大大的简化了代码的编写，但是在一些场景下我们并不希望冒泡存在
                        不希望事件冒泡时，可以通过事件对象来取消冒泡
                         -event.stopPropagation() // 取消事件的传导
        */
            
            const box1 = document.getElementById("box1")
            const box2 = document.getElementById("box2")
            const box3 = document.getElementById("box3")
            const chao = document.getElementById("chao")

            chao.addEventListener("click", (event) => {
                event.preventDefault() // 取消默认行为(代替return false,不考虑使用绑定事件响应函数的方式)
                alert("被点了~~~")

            })

            box1.addEventListener("click", function (event) {
                // alert(event)
                /* 
                在事件的响应函数中：
                    event.target 表示的是触发事件的对象
                    this 绑定事件的对象
            */
                // console.log(event.target)
                // console.log(this)

                console.log(event.currentTarget)

                // alert("Hello 我是box1")
            })

            // box2.addEventListener("click", function(event){
            //     event.stopPropagation()
            //     alert("我是box2")
            // })

            // box3.addEventListener("click", function(event){
            //     event.stopPropagation() // 取消事件的传导
            //     alert("我是box3")
            // })
        </script>
```

## 23.练习冒泡(冒泡的优点)

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        #box1 {
            width: 100px;
            height: 100px;
            background-color: greenyellow;
            border-radius: 50%;
            position: absolute;
        }

        #box2 {
            width: 500px;
            height: 500px;
            background-color: orange;
        }

        #box3 {
            width: 200px;
            height: 200px;
            background-color: tomato;
        }

        #box4 {
            width: 100px;
            height: 100px;
            background-color: skyblue;
            position: absolute;
            bottom: 0;
        }
    </style>
</head>

<body>
    <div id="box1"></div>

    <div id="box2"></div>

    <div id="box3" onclick="alert(3)">
        <div id="box4" onclick="alert(4)"></div>
    </div>

    <script>
        /*
            使小绿球可以跟随鼠标一起移动
            
            事件的冒泡和元素的样式无关，之和结构相关

            鼠标在box2中移动时,按理应该触发box2的事件
            然而box2会一直传导导document层,从而触发document的事件(祖先和子元素一样的事件都会被chu'fa)
        */

        const box1 = document.getElementById("box1")
        const box2 = document.getElementById("box2")

        document.addEventListener("mousemove", (event) => {
            box1.style.left = event.x + "px"
            box1.style.top = event.y + "px"
        })

        box2.addEventListener("mousemove", event => {
            // 如果绑定了这个事件,会执行完box2的然后在执行document的
            console.log(111);
            event.stopPropagation()
        })
    </script>
</body>

</html>
```

## 24.事件的委派

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>

<body>
    <button id="btn">点我一下</button>

    <hr />

    <ul id="list">
        <li><a href="javascript:;">链接一</a></li>
        <li><a href="javascript:;">链接二</a></li>
        <li><a href="javascript:;">链接三</a></li>
        <li><a href="javascript:;">链接四</a></li>
    </ul>

    <script>
        /* 
            我一个希望：
                只绑定一次事件，既可以让所有的超链接，包括当前的和未来新建的超链接都具有这些事件

            思路：
                可以将事件统一绑定给document，这样点击超链接时由于事件的冒泡，
                    会导致document上的点击事件被触发，这样只绑定一次，所有的超链接都会具有这些事件

            由于document的范围太大,点哪都会触发,所以要解决这个问题

            委派就是将本该绑定给多个元素的事件，统一绑定给document，这样可以降低代码复杂度方便维护(可以绑定给其它的,解决一些特殊问题)
        */

        // 获取list
        const list = document.getElementById("list")
        const btn = document.getElementById("btn")

        // 获取list中的所有链接
        const links = list.getElementsByTagName("a")


        document.addEventListener("click", (event) => {
            // 在执行代码前，先来判断一下事件是由谁触发
            // 检查event.target 是否在 links 中存在
            // links是一个类数组对象 我们需要进行转换  array.from 和 展开运算符[...] 进行转换

            // console.log(Array.from(links))

            //在这个数组内的对象才触发
            if ([...links].includes(event.target)) {//includes()检查数组是否含有
                alert(event.target.textContent)
            }
        })

        // 点击按钮后，在ul中添加一个新的li
        btn.addEventListener("click", () => {
            list.insertAdjacentHTML(
                "beforeend","<li><a href='javascript:;'>新超链接</a></li>"
                //老的解决方法就是新添加一个对象就绑定一次事件
                // 用for循环这种 会创建多个响应函数(可以提取出来)和绑定多次响应函数
                // for(let i = 0;i<links.length;i++){
                //     links[i].addEventListener("click",(event)=>{
                //         alert(111)
                //     })
                // }
            )
        })
    </script>
</body>

</html>
```

## 25.事件的捕获

```html
<!DOCTYPE html>
<html lang="zh">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        #box1 {
            width: 300px;
            height: 300px;
            background-color: greenyellow;
        }

        #box2 {
            width: 200px;
            height: 200px;
            background-color: orange;
        }

        #box3 {
            width: 100px;
            height: 100px;
            background-color: tomato;
        }
    </style>
</head>

<body>
    <div id="box1">
        <div id="box2">
            <div id="box3"></div>
        </div>
    </div>

    <script>
        /* 
            事件的传播机制：
                - 在DOM中，事件的传播可以分为三个阶段：
                    1.捕获阶段 （由祖先元素向目标元素进行事件的捕获(捕获到触发对象)）（默认情况下，事件不会在捕获阶段触发）
                    2.目标阶段 （触发事件的对象）
                    3.冒泡阶段 （由目标元素向祖先元素进行事件的冒泡,此时开始执行,从子元素到祖先元素）

                - 事件的捕获，指事件从外向内的传导，
                    当前元素触发事件以后，会先从当前元素最大的祖先元素开始向当前元素进行事件的捕获

                - 如果希望在捕获阶段触发事件，可以将addEventListener的第三个参数设置为true
                    一般情况下我们不希望事件在捕获阶段触发，所以通常都不需要设置第三个参数
                    加了true后顺序就是123,本来是321(点3的情况下)
                    如果设置了true并且加上了event.stopPropagation(),表示捕获事件停止
                    此时给box1设置了event.stopPropagation(),则点3时只弹出1,因为到1这就不会在进行捕获了,2,3的值拿不到
        */

        const box1 = document.getElementById("box1")
        const box2 = document.getElementById("box2")
        const box3 = document.getElementById("box3")

        box1.addEventListener("click", event => {
            alert("1" + event.eventPhase) // eventPhase 表示事件触发的阶段
            //1 捕获阶段 2 目标阶段 3 冒泡阶段

        })

        box2.addEventListener("click", event => {
            alert("2" + event.eventPhase)
        })

        box3.addEventListener("click", event => {
            alert("3" + event.eventPhase)
        })

    </script>
</body>

</html>
```

# 十一、BOM对象

## 1.BOM对象简介

```html
        <script>
            /* 
                BOM
                    - 浏览器对象模型
                    - BOM为我们提供了一组对象，通过这组对象可以完成对浏览器的各种操作
                    - BOM对象：
                        - Window —— 代表浏览器窗口（同时也是全局对象） 俩个作用
                        - Navigator —— 浏览器的对象（可以用来识别浏览器）
                        - Location —— 浏览器的地址栏信息
                        - History —— 浏览器的历史记录（控制浏览器前进后退）
                        - Screen —— 屏幕的信息

                    - BOM对象都是作为window对象的属性保存的，所以可以直接在JS中访问这些对象
                    不用像DOM那样去创建才能访问
            */
            console.log(history)
        </script>
```

## 2.Navigator

```html
    <script>
        /* 
            - Navigator —— 浏览器的对象（可以用来识别浏览器）
                userAgent(用户代理) 返回一个用来描述浏览器信息的字符串
                一般在老的代码才需要我们自己去检测代码在这个浏览器中是否支持
                   
        */

        // console.log(navigator.userAgent)

        let sBrowser
        const sUsrAg = navigator.userAgent

        // The order matters here, and this may report false positives for unlisted browsers.

        if (sUsrAg.indexOf("Firefox") > -1) {//检查
            sBrowser = "Mozilla Firefox"
            // "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:61.0) Gecko/20100101 Firefox/61.0"
        } else if (sUsrAg.indexOf("SamsungBrowser") > -1) {
            sBrowser = "Samsung Internet"
            // "Mozilla/5.0 (Linux; Android 9; SAMSUNG SM-G955F Build/PPR1.180610.011) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/9.4 Chrome/67.0.3396.87 Mobile Safari/537.36
        } else if (
            sUsrAg.indexOf("Opera") > -1 ||
            sUsrAg.indexOf("OPR") > -1
        ) {
            sBrowser = "Opera"
            // "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.102 Safari/537.36 OPR/57.0.3098.106"
        } else if (sUsrAg.indexOf("Trident") > -1) {
            sBrowser = "Microsoft Internet Explorer"
            // "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; Zoom 3.6.0; wbx 1.0.0; rv:11.0) like Gecko"
        } else if (sUsrAg.indexOf("Edge") > -1) {
            sBrowser = "Microsoft Edge (Legacy)"
            // "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299"
        } else if (sUsrAg.indexOf("Edg") > -1) {
            sBrowser = "Microsoft Edge (Chromium)"
            // Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36 Edg/91.0.864.64
        } else if (sUsrAg.indexOf("Chrome") > -1) {
            sBrowser = "Google Chrome or Chromium"
            // "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Ubuntu Chromium/66.0.3359.181 Chrome/66.0.3359.181 Safari/537.36"
        } else if (sUsrAg.indexOf("Safari") > -1) {
            sBrowser = "Apple Safari"
            // "Mozilla/5.0 (iPhone; CPU iPhone OS 11_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/11.0 Mobile/15E148 Safari/604.1 980x1306"
        } else {
            sBrowser = "unknown"
        }

        alert(`You are using: ${sBrowser}`)
    </script>
```

## 3.Location

```html
    <body>
        <button id="btn">点我一下</button>

        <input type="text" name="username" />

        <script>
            const btn = document.getElementById("btn")
            btn.addEventListener("click", () => {
                /* 
                
                    location 表示的是浏览器地址栏的信息(也可以获取到具体的,分为多部分)
                        - 可以直接将location的值修改为一个新的地址，这样会使得网页发生跳转
                        - location.assign() 跳转到一个新的地址 (可以回退)
                        - location.replace() 跳转到一个新的地址（无法通过回退按钮回退）
                        - location.reload() 刷新页面，可以传递一个true来强制清缓存刷新(没有true的时候例如火狐就会保存用户输入,不会清除)
                        - location.href 获取当前地址
                */

                // console.log(location.href)

                // location = "https://www.lilichao.com" //点击按钮后会直接跳转

                // location.assign("https://www.lilichao.com")

                // location.replace("https://www.lilichao.com")

                location.reload(true)
            })
        </script>
```

## 4.History 

```html
        <button id="btn">点我一下</button>

        <script>
            const btn = document.getElementById("btn")
            btn.onclick = () => {

                /* 
                    history.back()
                        - 回退按钮
                    history.forward()
                        - 前进按钮
                    history.go()
                        - 可以向前跳转也可以向后跳转(数字控制一次回退或前进几个页面)
                */

                // console.log(history.length)//历史记录的长度

                // history.back()

                // history.forward()

                history.go(-1)

            }

        </script>
```

## 5.定时器

```html
    <body>
        <h1 id="num"></h1>

        <script>
            /* 
                通过定时器，可以使代码在指定时间后执行
                    - 设置定时器的方式有两种：
                        setTimeout() 常用
                            - 参数：
                                1. 回调函数（要执行的代码）
                                2. 间隔的时间（毫秒）
                            - 关闭定时器
                                clearTimeout()

                        setInterval() (每间隔一段时间代码就会执行一次)
                            - 参数：
                                1. 回调函数（要执行的代码）
                                2. 间隔的时间（毫秒）
                            - 关闭定时器
                                clearInterval()

            */

            const timer = setTimeout(()=>{
                alert("我是定时器中的代码")
            }, 3000)

            // clearTimeout(timer)


            const numH1 = document.getElementById("num")

            // let num = 0

            // const timer = setInterval(() => {
            //     num++
            //     numH1.textContent = num

            //     if(num === 200){
            //         clearInterval(timer)
            //     }
            // }, 30)

        </script>
```

## 6.事件循环(调用堆栈)

```html
        <script>
            // 整个script也是一个整个的执行环境
            /* 
                事件循环（event loop）
                    - 函数在每次执行时，都会产生一个执行环境
                    - 执行环境负责存储函数执行时产生的一切数据
                    - 问题：函数的执行环境要存储到哪里呢？
                        - 函数的执行环境存储到了一个叫做调用栈的地方
                        - 栈，是一种数据结构，特点 后进先出
                    
                    调用栈（call stack）
                        - 调用栈负责存储函数的执行环境
                        - 当一个函数被调用时，它的执行环境会作为一个栈帧
                            插入到调用栈的栈顶，函数执行完毕其栈帧会自动从栈中弹出(执行的时候放到最上面)
                            栈顶是谁此时就是在执行谁
            */

            function fn() {
                let a = 10
                let b = 20

                function fn2() {
                    console.log("fn2")
                }

                fn2()

                console.log("fn~")
            }

            fn()

            console.log(1111)
        </script>
```

![uTools_1675776978229](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675776978229.png)

**调用fn2的时候fn还没执行完毕,还在这个栈中**

![uTools_1675777374122](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675777374122.png)

## 7.事件循环(消息队列)(js代码是单线程的,所以等待执行的代码在消息队列中)

```html
<body>
    <button id="btn">点我一下</button>
    <button id="btn02">点我一下2</button>

    <script>
        /* 
            事件循环（event loop）
                - 函数在每次执行时，都会产生一个执行环境
                - 执行环境负责存储函数执行时产生的一切数据
                - 问题：函数的执行环境要存储到哪里呢？
                    - 函数的执行环境存储到了一个叫做调用栈的地方
                    - 栈，是一种数据结构，特点 后进先出
                    - 队列，是一种数据结构，特点 先进先出
                
                调用栈（call stack）
                    - 调用栈负责存储函数的执行环境
                    - 当一个函数被调用时，它的执行环境会作为一个栈帧
                        插入到调用栈的栈顶，函数执行完毕其栈帧会自动从栈中弹出

                消息队列
                    - 消息队列负责存储将要执行的函数
                    - 当我们触发一个事件时，其响应函数并不是直接就添加到调用栈中的
                        因为调用栈中有可能会存在一些还没有执行完的代码
                    - 事件触发后，JS引擎是将事件响应函数插入到消息队列中排队
                        
                    
        */

        function fn() {
            let a = 10
            let b = 20

            function fn2() {
                console.log("fn2")
            }

            fn2()

            console.log("fn~")
        }

        fn()

        console.log(1111)

        const btn = document.getElementById("btn")
        const btn02 = document.getElementById("btn02")
        btn.onclick = function () {
            alert(1111)

            const begin = Date.now()//获取时间戳

            while (Date.now() - begin < 3000) { }//当前时间-刚才获取的时间 < 3秒(时间过去3秒后就循环借宿)
            //使用while占着调用栈,需要3秒执行完才会执行,此时alert会被延时三秒
        }

        btn02.onclick = function () {
            alert(2222)
        }
    </script>
```

![uTools_1675778184126](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675778184126.png)

## 8.定时器原理(基于事件循环)

```html
    <script>
        /* 
        定时器的本质，就是在指定时间后将函数添加到消息队列中(此时不一定执行,因为栈中不一定是空的)
        */

        // console.time()
        // setTimeout(function(){
        //     console.timeEnd()
        //     console.log("定时器执行了~")
        // }, 3000)

        // 使程序卡6s
        // const begin = Date.now()
        // while (Date.now() - begin < 6000) {}

        /* 
        setInterval() 每间隔一段时间就将函数添加到消息队列中
            但是如果函数执行的速度比较慢，它是无法确保每次执行的间隔都是一样的(间隔不平均)
            	第一次执行函数的时间已经超过了第二次将函数插入到消息队列中的时间了
    	*/
        
        // console.time("间隔")
        // setInterval(function(){
        //     console.timeEnd("间隔")

        //     // console.log("定时器执行了~~")
        //     alert("定时器执行~")

        //     console.time("间隔")
        // }, 3000)

        /* 
        希望可以确保函数每次执行都有相同间隔
            - 用setTimeout模仿setInterval
    	*/

         console.time("间隔")
         setTimeout(function fn() {
             console.timeEnd("间隔")
             alert("哈哈")
             console.time("间隔")
             // 在setTimeout的回调函数的最后，在调用一个setTimeout
             setTimeout(fn, 3000)
             //函数执行完以后再次调用,可以模拟setInterval的功能,同时可以确保无论函数执行时间长短,间隔时间都是3秒
                  //- 不会像setInterval有时候会出现同时执行俩次代码的情况,间隔时间不确定
                  //- 这种方式需要记得在开启下一个定时器之前关闭上一个定时器,避免用户同时打开多次定时器导致多个定时器重复执行
        }, 3000)

        /*
        setTimeout(() => {
            console.log(11111)
        }, 0)

        console.log(222222) //还是这个先执行,此时它已经进栈了,111还得在队列里排一下队
         */
    </script>
```

## 9.定时器切换图片

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>切换图片</title>
    <style>
        .outer {
            width: 640px;
            margin: 50px auto;
            text-align: center;
        }
    </style>
    <script>
        window.onload = function () {
            // 获取info对象
            const info = document.getElementById("info");

            // 获取img对象
            const img = document.querySelector("img");
            // 获取上一个按钮对象
            const prev = document.getElementById("prev");
            // 获取下一个按钮对象
            const next = document.getElementById("next");

            // 创建一个数组来存储图片的路径
            const imgArr = [
                "./images/1.png",
                "./images/2.png",
                "./images/3.png",
                "./images/4.png",
                "./images/5.png",
            ]

            // 记录索引
            let current = 0;
            // info文本设置
            info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`


            prev.onclick = function () {
                clearTimeout(timer)
                // 改变图片就是改变图片的路径
                current--;
                // 实现循环切换图片的效果
                if (current < 0) {
                    current = imgArr.length - 1;
                }
                img.src = imgArr[current]//用这种方式其它图片要等点击按钮时才会加载(在服务器中会产生卡顿,体验不好)
                //解决的方式是五张图片都写到页面中,进行隐藏,一次性加载完毕
                info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`
            }


            next.onclick = function () {
                clearTimeout(timer)
                // 改变图片就是改变图片的路径
                current++;
                // 实现循环切换图片的效果
                if (current > imgArr.length - 1) {
                    current = 0;
                }
                img.src = imgArr[current]
                info.textContent = `总共 ${imgArr.length} 张图片，当前第 ${current + 1} 张`
            }

            /*
                图片的自动切换的功能
            */

            const autoBtn = document.getElementById("autoBtn");
            //创建一个变量来存储定时器的id
            let timer;

            autoBtn.onclick = () => {
                // 关闭定时器(开启下一个定时器之前关闭上一个定时器,避免用户同时打开多次定时器)
                clearTimeout(timer)
                timer = setTimeout(function auto() {//timer赋值
                    next.onclick()
                    timer = setTimeout(auto, 3000)//执行结束后再次调佣,避免间隔时间不确定的情况
                }, 3000)
            }


        }
    </script>
</head>

<body>
    <div class="outer">

        <p id="info">
            总共n张图片，当前第 m 张
        </p>

        <div class="img-warpper">
            <img src="./images/1.png" alt="">
        </div>

        <div class="btn-warpper">
            <button id="prev">上一张</button>
            <button id="autoBtn">自动</button>
            <button id="next">下一张</button>
        </div>
    </div>
</body>

</html>
```

## 10.定时器切换图片练习(完善版)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            list-style: none;
        }

        img {
            vertical-align: top;
        }

        .outer {
            width: 640px;
            height: 390px;
            margin: 100px auto;
            position: relative;
        }

        .img-list {
            /* 防止高度塌陷 */
            height: 390px;
        }

        .img-list li {
            position: absolute;
            opacity: 0;
            transition: opacity 1s;
        }

        li.current {
            z-index: 1;
            opacity: 1;
        }

        /* 设置切换按钮的样式 */
        .prev-next a {
            font-size: 60px;
            color: #fff;
            font-weight: bold;
            text-decoration: none;
            position: absolute;
            height: 80px;
            top: 0;
            bottom: 0;
            margin: auto;
            z-index: 2;
            opacity: 0.5;
        }

        #next {
            right: 0;
        }

        .prev-next a:hover {
            opacity: 1;
        }

        /* 设置导航点的样式 */
        .dots {
            position: absolute;
            display: flex;
            justify-content: center;
            z-index: 3;
            left: 0;
            right: 0;
            bottom: 5px;
            margin: auto;
        }

        .dots a {
            width: 20px;
            height: 20px;
            margin: 5px;
            border-radius: 50%;
            background-color: #fff;
            opacity: 0.5;
        }

        .dots a:hover,
        .dots .active {
            opacity: 1;
        }
    </style>
</head>

<body>
    <div class="outer">
        <ul class="img-list">
            <li class="current">
                <a href="#"><img src="./images/1.png" alt=""></a>
            </li>
            <li>
                <a href="#"><img src="./images/2.png" alt=""></a>
            </li>
            <li>
                <a href="#"><img src="./images/3.png" alt=""></a>
            </li>
            <li>
                <a href="#"><img src="./images/4.png" alt=""></a>
            </li>
            <li>
                <a href="#"><img src="./images/5.png" alt=""></a>
            </li>
        </ul>
        <!-- 添加切换按钮 -->
        <div class="prev-next">
            <a id="prev" href="javascript:;">
                < </a>
                    <a id="next" href="javascript:;">></a>
        </div>

        <div class="dots">
            <a class="active" href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
            <a href="javascript:;"></a>
        </div>
    </div>

    <script>
        // 获取5个小点
        const dots = Array.from(document.querySelectorAll(".dots a"));//获取所有的点并且转化为数组
        // 获取5张图片
        const imgArr = [...document.querySelectorAll(".img-list li")];//获取所有的图片并且转化为数组

        //绑定小点的单击事件,直接绑定给document方便全局管理
        document.addEventListener("click", (event) => {
            const index = dots.indexOf(event.target);//获取当前触发事件图片的索引
            if (index !== -1) {//index不等于-1表示找到了对应图片
                changeImg(index)//调用函数(index作为参数)
            }
        })

        //绑定切换上一张图片按钮的单击事件
        const prev = document.getElementById("prev");
        prev.onclick = () => {
            changeImg("prev")
        }

        //绑定切换下一张图片按钮的单击事件
        const next = document.getElementById("next");
        next.onclick = () => {
            changeImg("next")
        }

        // 创建定时器,完成自动切换的功能(同时解决用户切换和自动切换的Bug)
        const toggleChange = (function () {
            //创建变量接收定时器的id
            let timer = null;
            //使用了闭包,这样别的函数就无法访问到timer进行修改,导致一些奇怪的bug
            return () => {
                // 判断timer是否是null
                if (timer === null) {
                    timer = setTimeout(function auto() {//函数第一次调用时打开定时器
                        //自动切换功能
                        changeImg("next")
                        timer = setTimeout(auto, 3000)//2次调用模拟setInterval的功能
                    }, 3000)
                } else {
                    clearTimeout(timer)//函数第二次调用时关闭定时器
                    timer = null
                }
            }
        })()

        toggleChange()//第一次调用函数开启定时器

        // 使用定时器解决用户切换和自动切换的Bug
        // 获取outer
        const outer = document.getElementsByClassName("outer")[0]

        // 当鼠标移入时表示用户对图片有兴趣,此时自动切换停止
        outer.onmouseenter = () => {
            toggleChange()//鼠标移入时关闭定时器
        }

        // 当鼠标移出时,重新开启自动切换
        outer.onmouseleave = () => {
            toggleChange()//鼠标移出时打开定时器
        }

        // 创建函数(功能为控制下一张切换的图片)
        /* 
            changeImg 用来切换图片
                参数：
                    dir 切换图片的方向
                        next
                        prev
                        index 传入index时表示此时点击的是小点(函数高度封装)    
 
        */
        function changeImg(dir) {
            // 获取当前显示的图片
            const current = document.querySelector(".img-list .current")

            // 获取下一张要显示的图片
            let next;
            if (dir === "next") {
                //点击下一张按钮时切换,最后一张图片跳转到第一张
                next = current.nextElementSibling || imgArr[0]
            } else if (dir === "prev") {
                //点击上一张按钮时切换,第一张图片时跳转到最后一张
                next = current.previousElementSibling || imgArr.at(-1)
            } else if (typeof dir === "number") {
                //传入index时表示此时正在点击小点
                next = imgArr[dir]//index传入赋值给dir
            }

            // 获取要显示的图片的索引
            const index = imgArr.indexOf(next)//传入的是next才可以

            // 切换显示状态
            current.classList.remove("current")
            next.classList.add("current")

            // 切换active
            const currentActive = document.querySelector(".active")
            currentActive.classList.remove("active")

            // 获取到当前要显示的小点(添加active类)
            dots[index].classList.add("active")
        }

    </script>
</body>

</html>
```



## 11.贪吃蛇(DOM+BOM)

**禁止掉头原始写法**

![uTools_1676018954232](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676018954232.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: content-box;
        }

        #main {
            height: 420px;
            width: 360px;
            border: 10px #000 solid;
            background-color: #b7d4a8;
            border-radius: 20px;
            margin: 50px auto;
        }

        #stage {
            width: 304px;
            height: 304px;
            border: 2px solid #000;
            margin: 20px auto;
            position: relative;
        }

        #snake>div {
            width: 10px;
            height: 10px;
            background-color: #000;
            /* 开启定位才能计算偏移量 */
            position: absolute;
            border: 1px solid #b7d4a8;
        }

        #food {
            width: 10px;
            height: 10px;
            position: absolute;
            top: 100px;
            left: 120px;
            /* 排列方式 */
            display: flex;
            flex-flow: wrap;
        }

        #food>div {
            width: 5px;
            height: 5px;
            background-color: #000;
            transform: rotate(45deg);
        }

        #info {
            width: 304px;
            margin: 0px auto;
            display: flex;
            justify-content: space-between;
            font: bold 20px courier;
        }
    </style>
</head>

<body>
    <div id="main">
        <div id="stage">

            <div id="snake">
                <div></div>
            </div>

            <div id="food">
                <div></div>
                <div></div>
                <div></div>
                <div></div>
            </div>
        </div>

        <div id="info">
            <div>SCORE:<span id="score">0</span></div>
            <div>LEVEL:<span id="level">1</span></div>
        </div>
    </div>

    <script>
        // 获取存放蛇的div
        const snake = document.getElementById("snake")
        // 根据div获取整条蛇
        const snakes = snake.getElementsByTagName("div")

        // 获取食物
        const food = document.getElementById("food")


        // 获取分数和level的span
        const scoreSpan = document.getElementById("score")
        const levelSpan = document.getElementById("level")

        // 创建变量存储分数和等级
        let score = 0
        let level = 0

        // 食物的坐标应该在0-290之间
        function changeFood() {
            // 生成0-29之间的随机数
            const x = Math.floor(Math.random() * 30) * 10//向下取整,所以要乘30
            const y = Math.floor(Math.random() * 30) * 10//向下取整,所以要乘30

            // 设置食物的坐标
            food.style.left = x + "px"
            food.style.top = y + "px"
        }


        // 设置一个变量存放方向,键盘事件只控制方向
        let dir;

        // 创建一个变量来记录按键的状态(确保不能同时按2次按键卡计时器的bug)
        let keyActive = true;//表示激活

        const keyArr = ["ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight"]

        // 利用对象来存储值
        const reObj = {
            ArrowUp: "ArrowDown",
            ArrowDown: "ArrowUp",
            ArrowLeft: "ArrowRight",
            ArrowRight: "ArrowLeft",
        }
        
        /*
            游戏禁止掉头：
                构成的要件：
                    1. 身体超过2
                    2. 不能是相反的方向
                处理：
                    保持原来的方向不变（不修改dir的值）       
        */
        
        // // 绑定按键事件(在这里修改可以同时拿到现在和等下的方向)
        document.addEventListener("keydown", (event) => {
            // 如果按了别的按键就不改变方向
            // 只能按一次键盘,解决了在定时器触发前按多次键盘可以掉头的情况
            // keyActive为true才能触发掉头
            if (keyActive && keyArr.includes(event.key)) {
                // 判断蛇是否掉i头
                /*
                    第一次执行时长度小于2,可正常调整方向
                    当长度大于2时,利用reObj[dir]取到相反的值(上取下)
                    这样确保了往右走的时候不可以直接往左掉头
                    设往右走(不可以往左走了) dir此时为ArrowRight
                    此时按ArrowLeft(event.key)
                    reObj[dir]==>reObj[ArrowRight]取到的值为ArrowLeft
                    reObj[dir]==event.key 不给dir进行赋值,不可掉头
                    俩者不相等的时候才可以赋值转弯
                */
                if (snakes.length < 2 || reObj[dir] !== event.key) {
                    dir = event.key//触发事件的键位
                    keyActive = false;//按过一次按键以后设置为false不可再次触发
                }
            }
        })


        // 要使得身体可以和头一起移动,只需要在蛇移动时,变化蛇尾的位置

        setTimeout(function move() {
            // 定时器来控制蛇的速度,不会出现卡顿的现象,同时可以操控关卡难度


            //获取蛇头
            const head = snakes[0]
            // 获取蛇头坐标
            let x = head.offsetLeft;
            let y = head.offsetTop;

            switch (dir) {
                case "ArrowUp":
                    // 向上移动蛇
                    y -= 10;
                    break
                case "ArrowDown":
                    // 向下移动蛇
                    y += 10;
                    break
                case "ArrowLeft":
                    // 向左移动蛇
                    x -= 10;
                    break
                case "ArrowRight":
                    // 向右移动蛇
                    x += 10;
                    break
            }

            // 检查蛇是否吃到食物
            if (
                head.offsetTop === food.offsetTop &&
                head.offsetLeft === food.offsetLeft
            ) {
                //1.改变食物的位置
                changeFood()
                //2.增加蛇的身体
                snake.insertAdjacentHTML("beforeend", "<div/>")
                score++;
                scoreSpan.textContent = score; //吃完加分

                // 等级
                if (score % 10 === 0 && level < 14) {//15级最高
                    level++;
                    levelSpan.textContent = level + 1;
                }
            }

            // 判断游戏是否结束 撞墙和撞自己
            // 撞墙
            if (x < 0 || x > 290 || y < 0 || y > 290) {
                alert("撞到墙了!游戏结束!")
                return
            }
            /*
                撞自己 判断条件要取到倒数第二个 因为我们的逻辑是尾巴变成头
                循坏转的时候头尾是不应该撞到的 (snakes.length就会撞到)
            */
            for (let i = 0; i < snakes.length - 1; i++) {
                if (snakes[i].offsetLeft === x && snakes[i].offsetTop == y) {
                    alert("撞到自己了!游戏结束!")
                    return
                }
            }

            // 获取尾巴
            const tail = snakes[snakes.length - 1]
            // 移动蛇的位置 css样式设置
            tail.style.left = x + "px"
            tail.style.top = y + "px"
            // 将尾巴移动到蛇头的位置,结构上要重新调整
            snake.insertAdjacentElement("afterbegin", tail)//将tail插入到蛇头的位置

            //定时器执行的时候在把他设置为true
            keyActive = true;

            setTimeout(move, 300 - level * 20) //level升一级加快20毫秒
        }, 300)
        
    </script>
</body>

</html>
```

# 十二、jQuery(JavaScript库)

![uTools_1676033209719](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676033209719.png)

1.引入

```css
 1.直接引入
<!-- <script src="./scripts/jquery-3.6.1.js"></script> -->
 2.cdn(公共服务器)引入
<script src="https://lf9-cdn-tos.bytecdntp.com/cdn/expire-1-M/jquery/3.6.0/jquery.js"></script>
```

## 1.核心函数

```html
<body>

    <div></div>

    <button id="btn01">点我一下</button>
    
    <script>

        /* 
            引入jQuery库，其实就是向网页中添加了一个新的函数$(也可以用jQuery访问)
                - $ 是jQuery中的核心函数，jQuery的所有功能都是通过该函数来进行的
                - 核心函数的功能
                    - 两种作用
                        1. 将它作为工具类使用
                            - 在核心函数中jQuery为我们提供了多个工具方法

                        2. 将它作为函数使用
                            - 将一个函数作为$的参数
                                - 这个函数会在文档加载完毕之后执行
                                - 相当于：
                                    document.addEventListener("DOMContentLoaded", function(){})//可以访问到所有DOM

                            - 将选择器字符串作为参数
                                - jQuery自动去网页中查找元素
                                - 作用类似于 document.querySelectorAll("...")
                                - 注意：
                                    通过jQuery核心函数查询到的结果并不是原生的DOM对象，
                                        而是一个经过jQuery包装过的新的对象，这个对象我们称其为jQuery对象
                                        jQuery对象中为我们提供了很多新的方法，方便我们做各种DOM操作
                                            但是jQuery对象不能直接调用原生DOM对象的方法
                                            一般我们为jQuery对象命名时，会使用$开头，和元素DOM对象加以区分

                            - 将DOM对象作为参数
                                - 可以将DOM对象转换为jQuery对象，从而使用jQuery对象的方法
                            
                            - 将html代码作为参数
                                - 会根据html代码来创建元素（jQuery对象）
        */

        // console.log(jQuery)

        // var num = 10
        // function fn(){}

        // console.log($.isFunction(num)) false

        // console.log($.isFunction(fn)) // true

        // console.log(typeof fn === "function")

        // console.log($)

        $(function(){

            $("#btn01").click(function(){
                // alert("你点我干嘛~~")

                var btn = document.getElementById("btn01") // [object HTMLButtonElement]

                var $btn = $("#btn01") // [object Object]

                // alert($(btn))

                var $h1 = $("<h1>我是一个标题</h1>") // 会根据html代码创建元素
                //返回的还是jQuery对象

                $("div").append($h1)

            })
        })
    </script>
```

## 2.对象

```html
<body>
    <button id="btn01">点我一下</button>
    <ul>
        <li id="swk">孙悟空</li>
        <li id="zbj">猪八戒</li>
        <li>沙和尚</li>
        <li>唐僧</li>
        <li>白骨精</li>
    </ul>

    <script>
        /* 
        jQuery对象
            - 通过jQuery核心函数获取到的对象就是jQuery对象
            - jQuery对象是jQuery中定义的对象
                可以将其理解为是DOM对象的升级版，在jQuery对象中为我们提供了很多简单易用的方法
                    来帮助我们简化DOM操作
            - jQuery对象本质上是一个DOM对象的数组（类数组）
                可以通过索引获取jQuery对象中的DOM对象(取出来的就是原生的DOM对象,可以用原生的方法)
            - 当我们修改jQuery对象时，它会自动修改jQuery中的所有元素
                这一特点称为jQuery的隐式迭代
            - 通常情况下，jQuery对象方法的返回值依然是一个jQuery对象
                所以我们可以在调用一个方法后继续调用其他的jQuery对象的方法
                这一特性，称为jQuery对象的 链式调用               
    */
        $("#btn01").click(function () {
            var $li = $("li")
            // alert($li[0].textContent)

            // $li.text("哈哈哈")//每个li都被修改了

            var text = $li.text() // 读取文本，返回所有标签中的文本
            var id = $li.attr("id") // 读取属性时，只返回第一个标签的属性

            // alert(id)

            // var result = $li.text("新的文本内容")
            // alert(result === $li) true 返回的还是jQuery对象

            $li.text("新的文本内容").css("color", "red")//链式调用 
        })
    </script>
```

## 3.方法

```html
        <script src="./scripts/jquery-3.6.1.js"></script>
        <style>
            .box1 {
                width: 200px;
                height: 200px;
                background-color: #bfa;
            }

            .box2 {
                border: 10px red solid;
            }

            .box3 {
                background-color: orange;
            }
        </style>
        <script>
            // https://api.jquery.com/category/manipulation/class-attribute/
            $(function () {
                // 为按钮绑定响应函数
                $("#btn").click(function () {
                    // 为box1添加class
                    // addClass() 可以为元素添加一个或多个class
                    // $(".box1").addClass(["box2", "box3"])

                    // addClass可以接收一个回调函数作为参数
                    // $(".box1").addClass(function (index, className) {
                    //     // 在回调函数中，this表示的是当前的元素

                    //     // if (index % 2 === 0) {
                    //     //     // 添加box2
                    //     //     this.classList.add("box2")
                    //     // } else {
                    //     //     // 添加box3
                    //     //     this.classList.add("box3")
                    //     // }

                    //     if (index % 2 === 0) {
                    //         // 添加box2
                    //         // 把this转为jquery对象
                    //         $(this).addClass("box2")
                    //     } else {
                    //         // 添加box3
                    //         $(this).addClass("box3")
                    //     }
                    // })

                    $(".box1").addClass(function(index){

                        // 回调函数的返回值会成为当前元素的class(最方便用)
                        // return ["box2", "box3"]

                        if(index % 2 === 0){
                            return "box2"
                        }else{
                            return "box3"
                        }

                    })
                })
            })
        </script>
    </head>
    <body>
        <button id="btn">点我</button>

        <hr />

        <div class="box1"></div>
        <div class="box1"></div>
        <div class="box1"></div>
    </body>
```

## 4.复制对象的方法

```html
    <script src="./scripts/jquery-3.6.1.js"></script>
    <script>
        $(function () {

            $("#list li:nth-child(1)").click(function () {
                alert("孙悟空")
            })

            /* 
                clone() 用来复制jQuery对象
            */
            var $swk = $("#list li:nth-child(1)").clone(true) //传true事件也会一起复制
            var $list2 = $("#list2")

            $("#btn").click(function () {
                $list2.append($swk)
            })
        })

    </script>
</head>

<body>

    <button id="btn">点我</button>

    <hr>

    <ul id="list">
        <li>孙悟空</li>
        <li>猪八戒</li>
    </ul>

    <ul id="list2">
        <li>沙和尚</li>
        <li>唐僧</li>
    </ul>
</body>
```

## 5.添加容器的方法

```html
    <script src="./scripts/jquery-3.6.1.js"></script>
    <script>
        $(function () {
            /* 
                unwrap() 删除外层父元素 参数可以限定外层容器是什么才删除 
                wrap() 为当前元素添加一个容器(分别添加) 参数
                wrapAll() 为当前的所有元素统一添加容器  参数
                wrapInner() 为当前元素添加一个内部容器  参数
                这些也可以通过传函数动态的控制
            */
            $("#btn").click(function () {
                // $("#list li").unwrap()
                // $("#list li").wrap("<div/>")
                // $("#list li").wrapAll("<div/>")
                $("#list li").wrapInner("<div/>")

            })
        })
    </script>
</head>

<body>
    <button id="btn">点我</button>

    <hr />

    <ul id="list">
        <li>孙悟空</li>
        <li>猪八戒</li>
    </ul>

    <ul id="list2">
        <li>沙和尚</li>
        <li>唐僧</li>
    </ul>
</body>
```

## 6.添加子元素的方法

```html
        <style>
            #box1 {
                width: 200px;
                height: 200px;
                background-color: #bfa;
            }

            #box2 {
                width: 100px;
                height: 100px;
                background-color: orange;
            }

            #box3 {
                width: 100px;
                height: 100px;
                background-color: yellow;
            }
        </style>
        <script src="./scripts/jquery-3.6.1.js"></script>
        <script>
            $(function () {
                /* 
                    append()
                        - 向父元素后边添加一个子元素
                    appendTo()
                        - 将子元素添加到父元素后边
                    prepend()
                    prependTo()
                        - 向父元素的前边添加子元素
                    text()
                        - 获取/设置元素的文本内容
                    html()
                        - 获取/设置元素的html代码
                        
                */
                $("#btn").click(function () {

                    // $("#box1").append("<div id='box2'/>")

                    // $("<div id='box2'/>").appendTo("#box1")

                    // $("#box1").prepend("<div id='box2'/>")
                    $("<div id='box2'/>").prependTo("#box1")
                })
            })
        </script>
    </head>
    <body>
        <button id="btn">点我</button>
        <hr />

        <div id="box1">
            <div id="box3"></div>
        </div>
    </body>
```

## 7.各种方法

**根据兄弟元素添加元素的方法**

![uTools_1676036987762](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1676036987762.png)

```html
        <style>
            #box1 {
                width: 200px;
                height: 200px;
                background-color: #bfa;
            }

            #box2 {
                width: 100px;
                height: 100px;
                background-color: orange;
            }

            #box3 {
                width: 100px;
                height: 100px;
                background-color: yellow;
            }
        </style>
        <script src="./scripts/jquery-3.6.1.js"></script>
        <script>
            $(function () {
                /* 
                    empty() 删除所有的子元素
                    remove() 移除元素（同时移除事件）
                    detach() 移除元素
                */

                var $li = $("li:nth-child(1)")

                $li.click(function () {
                    alert("哈哈哈")
                })

                $("#btn").click(function () {
                    // $("ul").empty()

                    // $("li:nth-child(1)").remove()
                    $("li:nth-child(1)").detach()
                })

                $("#btn2").click(function () {
                    $("ul").append($li)
                })

                $("#btn3").click(function () {
                    /* 
                        操作属性的方法
                        attr() 读取布尔值返回实际值
                        prop() 读取布尔值返回 true/false
                            - 用来读取或设置元素的属性
                            - 读取布尔值属性时两者不会返回不同的值
                    */

                    var type = $("input[type=text]").attr("type")
                    var name = $("input[type=text]").prop("name")

                    var checked = $("input[type=radio]").prop("checked")//true  attr返回checked

                    // alert(checked)

                    // $("input[type=text]").prop("value","哈哈")  //把值修改为哈哈
                    // $("input[type=radio]").prop("checked", true)

                    $("input[type=text]").val("xxx")//不写值是读取,写值就赋值

                })
            })
        </script>
    </head>
    <body>
        <button id="btn">点我</button>
        <button id="btn2">点我2</button>
        <hr />

        <ul>
            <li>孙悟空</li>
            <li>猪八戒</li>
            <li>沙和尚</li>
            <li>唐僧</li>
        </ul>

        <input type="radio" name="gender" value="male" /> 男
        <input type="radio" name="gender" value="female"  /> 女

        <hr />

        <input type="text" name="username" />

        <hr />

        <button id="btn3">点我3</button>
    </body>
```

## 8.操作css样式

```html
        <style>
            #box1 {
                width: 200px;
                height: 200px;
                padding: 100px;
                border: 10px red solid;
                background-color: #bfa;
            }

            #box2 {
                width: 100px;
                height: 100px;
                background-color: orange;
            }

            #box3 {
                width: 100px;
                height: 100px;
                background-color: yellow;
            }
        </style>
        <script src="./scripts/jquery-3.6.1.js"></script>
        <script>
            $(function () {
                $("#btn").click(function () {
                    /* 
                        css 可以用来读取或设置元素的样式(驼峰和非驼峰都可以用)
                    */

                    var $width = $("#box1").css("width")

                    // alert($("#box1").css("background-color"))
                    // alert($("#box1").css("left"))

                    // $("#box1").css("width", 300)//默认单位为px

                    // $("#box1").css({width:300, height:500, backgroundColor:"yellow"})//此时需要驼峰命名

                    // alert($("#box1").innerHeight())//内容区加内边距

                    // $("#box1").innerHeight(500)

                    // alert($("#box1").offset().top + '--' + $("#box1").offset().left)

                    $("#box1").offset({ top: 500, left: 300 })//会自动开启定位调整位置
                })

                $("#btn2").click(function () {})

                $("#btn3").click(function () {})
            })
        </script>
    </head>
    <body>
        <button id="btn">点我</button>
        <button id="btn2">点我2</button>
        <hr />

        <div id="box1"></div>

        <hr />

        <hr />

        <button id="btn3">点我3</button>
    </body>
```

## 9.筛选对象的方法

```html
        <script src="./scripts/jquery-3.6.1.js"></script>
        <style>
            .box1 {
                float: left;
                width: 100px;
                height: 100px;
                border: 1px red solid;
                margin: 10px;
            }
        </style>

        <script>
            $(function () {
                $("#btn01").click(function () {
                    //     $(".box1").css("background-color", "#bfa")

                    // eq()用来获取jQuery对象中指定索引的元素
                    // first() 获取第一个元素
                    // last() 获取最后一个元素
                    // even() 获取索引为偶数的元素
                    // odd() 获取索引为奇数的元素
                    // slice() 切片
                    // $(".box1").eq(-1).css("background-color", "#bfa")
                    // $(".box1").even().css("background-color", "#bfa")

                    // $(".box1").slice(1, 3).css("background-color", "#bfa")

                    $(".box1").filter(".a").css("background-color", "#bfa")

                    // $(".box1")[0]
                    // $(".box1").get(0)
                })
            })
        </script>
    </head>
    <body>
        <button id="btn01">点我</button>

        <hr />

        <div class="box1"></div>
        <div class="box1"></div>
        <div class="box1"></div>
        <div class="box1 a"></div>
        <div class="box1 a"></div>
        <div class="box1 a"></div>
        <div class="box1"></div>
        <div class="box1 a"></div>
        <div class="box1"></div>
        <div class="box1"></div>
    </body>
```

```html
        <script src="./scripts/jquery-3.6.1.js"></script>
        <style>
            .box1 {
                float: left;
                width: 100px;
                height: 100px;
                border: 1px red solid;
                margin: 10px;
            }

            .box2{
                float: left;
                width: 200px;
                height: 200px;
                border: 1px orange solid;
            }
        </style>

        <script>
            $(function () {
                $("#btn01").click(function () {
                    // end() 将jQuery对象恢复到筛选前的状态
                    // add() 向jQuery对象中添加元素
                    // contents() 获取当前jQuery对象中所有元素的内容(所有子元素)
                    // addBack() 筛选前的和筛选到的添加到一起

                    // $(".box1")
                    //     .filter(".a")
                    //     .css("background-color", "#bfa")
                    //     .end()
                    //     .css("border-color", "blue")
                    // $(".box1")
                    //     .css("border-color", "blue")
                    //     .filter(".a")
                    //     .css("background-color", "#bfa")


                    // $(".box1").add(".box2").css("background-color", "#bfa")

                    $(".box1").contents().addBack().css("background-color", "#bfa")
                })
            })
        </script>
    </head>
    <body>
        <button id="btn01">点我</button>

        <hr />

        <div class="box1"><span>我是span</span></div>
        <div class="box1"><span>我是span</span></div>
        <div class="box1"><span>我是span</span></div>
        <div class="box1 a"><span>我是span</span></div>
        <div class="box1 a"><span>我是span</span></div>
        <div class="box1 a"></div>
        <div class="box1"></div>
        <div class="box1 a"></div>
        <div class="box1"></div>
        <div class="box1"></div>

        <div class="box2"></div>
    </body>
```

## 10.事件的处理

```html
    <script src="./scripts/jquery-3.6.1.js"></script>
    <style>
        .box1{
            float: left;
            width: 100px;
            height: 100px;
            margin: 10px;
            border: 2px red solid;
        }

    </style>
</head>
<body>
<body>
    <button id="btn01">点我</button>
    <button id="btn02">点我2</button>
    <button id="btn03">点我3</button>

    <a href="#">超链接</a>

    <hr>

    <div class="box1"></div>
    <div class="box1"></div>
    <div class="box1"></div>
    <div class="box1"></div>
    <div class="box1"></div>

    <script>
        $(function(){

            // 可以通过指定方法来为jQuery对象绑定事件(底层是addEventListener那个方法)
            $("a").click(function(event){
                // 在jQuery的事件响应函数中，同样有事件对象，但是这个对象是经过jQuery包装过的新的对象
                // 包装该对象主要是为了解决兼容性的问题

                event.stopPropagation()//取消冒泡
                event.preventDefault()//取消默认行为

                alert(123)

                // 在jQuery的事件回调函数中，可以通过return false来取消默认行为和冒泡
                // return false
            })

            // $(document.body).click(function(){
            //     alert("body")
            // })

            

            // 也可以通过on()方法来绑定事件(底层是addEventListener那个方法)
            $("#btn01").on("click.a", function(){//指定命名空间,可以指定删除
                alert("通过on绑定的事件！")
            })

            $("#btn01").on("click.b", function(){
                alert("通过on绑定的事件！2")
            })

            $("#btn01").on("click.c", function(){
                alert("通过on绑定的事件！3")
            })

            $("#btn02").on("click", function(){
                // off()可以用来取消事件的绑定
                $("#btn01").off("click.a")
            })

            $("#btn03").on("click", function(){
                $(document.body).append("<div class='box1'/>")
            })

            // $(".box1").on("click", function(){
            //     alert("哈哈")
            // })
            
            // 事件的委托
            // $(document).on("click",".box1", function(event){//第二个参数表示document委托给谁
            //     alert("哈哈")
            // })

            // one()用来绑定一个一次性的事件
            $(".box1").one("click", function(){
                alert('嘻嘻')
            })

        })

    </script>
</body>
```



# ⭐⭐扩展⭐⭐

# 1.Js类型判断的几种方式

## 1.typeof

![uTools_1671094415098](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094415098.png)

## 2.instancof

![uTools_1671094408841](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094408841.png)

## 3.constructor

![uTools_1671094380995](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094380995.png)

![uTools_1671094485832](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094485832.png)

## 4.Object.prototype.toString.call

![uTools_1671094391789](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671094391789.png)

# 2.各种遍历的方法

```css
    <script>
        /* 
            枚举属性，指将对象中的所有的属性全部获取

            for-in语句
            - 语法：
                for(let propName(命名) in 对象){
                    语句...
                }

            - for-in的循环体会执行多次，有几个属性就会执行几次，
                每次执行时，都会将一个属性名赋值给我们所定义的变量
            
            - 注意：并不是所有的属性都可以枚举，比如 使用符号添加的属性
        */

        let obj = {
            name:'孙悟空',
            age:18,
            gender:"男",
            address:"花果山",
            [Symbol()]:"测试的属性" // 符号添加的属性是不能枚举的
        }

        for(let propName in obj){
            console.log(propName, obj[propName])
        }

    </script>


     <script>
            /* 
                for-of语句可以用来遍历可迭代对象

                语法：
                    for(变量 of 可迭代的对象){
                        语句...
                    }

                执行流程：
                    for-of的循环体会执行多次，数组中有几个元素就会执行几次，
                        每次执行时都会将一个元素赋值给变量
            */
                    
            const arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]

            for(let value of arr){
                console.log(value)
            }

            for(let value of "hello"){
                console.log(value)
            }
       </script>


          forEach()
                - 用来遍历数组
                - 它需要一个回调函数作为参数，这个回调函数会被调用多次
                    数组中有几个元素，回调函数就会调用几次
                    每次调用，都会将数组中的数据作为参数传递
                - 非破坏性方法，不会影响原数组
                - 回调函数中有三个参数：
                    element 当前的元素
                    index 当前元素的索引
                    array 被遍历的数组
```



# 3.静态方法和实例方法的区别

![uTools_1675358177310](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675358177310.png)

# 4.Window和window的区别

## 1.概念上看

**1）Window和window都是由浏览器实现的【native code】，应该可以增加属性，但肯定没法修改其原始代码；2）window是由构造函数Window实例化的对象，各自有自己独立的内存空间。**

## 2.继承关系上看

**window的继承关系为：window—>Window.prototype—>Windowproperties.prototype—>EventTarget.prototype—>Object.prototype;而Window的继承关系为：Window—>EventTarget—>Function.prototype—>Object.prototype。两者的顶层都是Object.prototype，不可能单独为Window和window增加新的属性，Window的根下一层Function.prototype也不可能增加新的属性，因为所有自定义函数和对象都会用到这两个玩意；要想一样（指属性一样），只能从Window的EventTarget这一层和window的Windowproperties.prototype这一层以下做文章。对于对象属性可以互相引用，做到一样，对于原始类型的属性，只能通过代码来同步**

**Window是类，window是实例，而且通常是单例模式。**

**类只能使用静态方法,实例可以使用静态和动态的方法**

window===Window //false
Window.window===window //true
在上面定义的变量也不能相互访问，如下：
window.name="zhangsan"
Window.name //undefine

## 3.document

**HTMLDocument继承自Document。 在浏览器中，document对象是HTMLDocument的一个实例，表示整个HTML页面。document对象是window对象的一个属性，因此可以直接调用**

**window表示窗口(浏览器的内建对象)  document表示整个页面**

# 5.js中的this问题

**js中的this问题指的是在函数中的问题，在函数外的this就是对应的环境，浏览器中对应window，node中对应一个空对象**

```
this的指向是在执行上下文创建的时候确定了这一次的函数的this指向谁(执行上下文什么时候创建，就是执行的时候创建，也就是调用，this的指向就是在调用的时候确定的)
```

![image-20230818170234095](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818170234095.png)

**使用bind的时候容易造成混淆**

![image-20230818170827032](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230818170827032.png)

**if的时候就会指向新对象，else就是第一个参数**

```css
       /*
			什么是this?
                - 函数在执行时，JS解析器每次都会传递进一个隐含的参数
                - 这个参数就叫做 this
                - this会指向一个对象
                    - this所指向的对象会根据函数调用方式的不同而不同
                        1.以函数形式调用时，this指向的是window(函数其实就是window的方法)
                        2.以方法的形式调用时，this指向的是调用方法的对象
                        ...

                - 通过this可以在方法中引用调用方法的对象
                -一个对象调用了这个方法,this就指代这个对象的地址值(调用者就是对象)
        */

		/* 
            箭头函数的this：
                ([参数]) => 返回值
            例子：
                无参箭头函数：() => 返回值
                一个参数的：a => 返回值
                多个参数的：(a, b) => 返回值

                只有一个语句的函数：() => 返回值
                只返回一个对象的函数：() => ({...})
                有多行语句的函数：() => {
                    ....    
                    return 返回值
                }

            箭头函数没有自己的this，它的this由外层作用域决定
            箭头函数的this和它的调用方式无关(创建出来是什么就是什么)
            因为箭头函数的this比较稳定,所以在开发时多用箭头函数
        */

            根据函数调用方式的不同，this的值也不同：
                1. 以函数形式调用，this是window
                2. 以方法形式调用，this是调用方法的对象
                3. 构造函数中，this是新创建的对象
                4. 箭头函数没有自己的this，由外层作用域决定
                5. 通过call和apply调用的函数，它们的第一个参数就是函数的this
                6. 通过bind返回的函数，this由bind第一个参数决定（无法修改）

            箭头函数没有自身的this，它的this由外层作用域决定(箭头函数的this一出生就确定了)
                也无法通过call apply 和 bind修改它的this 
                箭头函数中没有arguments

            在事件的响应函数中：
                    event.target 表示的是触发事件的对象
                    this 绑定事件的对象
```



# 6.JS调用函数加不加括号的区别

```javascript
function run(){
	alert("doing...");
	return "str";
}
 
alert("run:"+run); //不带()，获取方法内容
run();//带()，调用方法执行
alert("run():"+run());//带括号，获取方法返回值
```

![uTools_1675617972480](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1675617972480.png)

# 7.Promise异步

**Node.js中介绍了,前端默认都是全栈开发工程师**

# 8.Vue和React

**次要掌握的先学,先学React再来学Vue(react是大公司用的多)**

