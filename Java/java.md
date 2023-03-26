# 1.java

1.staick是java静态方法，staick命名的方法(函数)，可以直接类名.方法()调用
没有加staick的方法要创建一个对象类才能进行调用

2.java中构造函数之间的相互调用是用this

3.函数等价

![uTools_1668334789360](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668334789360.png)

4.java在删除空间的时候可以用逻辑清除的方法

例如：调用clear方法清除整个数组的元素,没必要重新创数组，直接另size=0；这样别人就访问不到数组元素了。这样也不会浪费内存空间，因为之前数组元素占据的空间最后还是要用的，而且清除数组和重新申请数组空间也会浪费时间和内存。

开发者的角度和框架设计者的角度是不一样的，只需要程序逻辑合理就可以。

5.java垃圾回收的原理可以简单理解为没有变量引用数组空间的时候，程序会自动销毁。

6.java的位运算

​				a>>1 的意思就是a * 0.5   	a <<1 的意思就是a * 2

7.java中的泛型只能存放对象,如果要放基本数据类型就要使用基本数据类型的包装类
例如int对应的包装类是integer  
​			ArrayList <Integer> list = new ArrayList<>();

8.在java中,所有的类都继承java.lang.Object   用这个类可以实现泛型动态数组

9.在eclipse中使用alt+shift+s可以快速生成一些构造函数

10.java中提醒虚拟机JVM进行垃圾回收  System.gc();

11.在java中equals比较的是俩个数据的内存地址，内存地址相等才判断相等，这种一般是针对对象类的，像integer这种类内部的equals方法都是重写过的，比较的是数值，所以不影响使用。

12.java中空值调用方法会报空指针异常错误

13.for用在不确定次数的情况下跳出循环
for(int i =1; i>=99999;i++){
   if(xxxx)
   i=100000；
}

14.while跳出循环
boolean a = true;
while(a){
  if(xxxx)
  a=false;
}

**15.y/n输入错误的时候(不确定输错几次用while)**

```java
 String s = in.next().toLowerCase();
//不为y/n就是输入错误
while (!s.equals("y") && !s.equals("n")) {
    System.out.println("输入错误!请重新输入y或者n:");
    s = in.next().toLowerCase();
}
```

![uTools_1669353966545](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1669353966545.png)
16.&&和||是短路运算符，&和|是非短路运算符。&&和||具有短路的功能，而&和|不具备短路功能。

17.“Break”语句只能在封闭迭代或Switch语句中使用。 在条件分支语句是不能直接用的

18.java里while(1)应该是非法的，因为java强制要求while()里面的条件表达式必须是boolean型，而不能是int。
C/C++里用while(1)是可以的，和while(true)等价。在JavaScript中也是可以的，因为1会自动转为布尔值true。

19.java的内部类可以解决什么问题

- 内部类方法可以访问该类定义所在作用域中的数据，包括被 private 修饰的私有数据
- 内部类可以对同一包中的其他类隐藏起来
- 内部类可以解决java 单继承的缺陷
- 当我们想要定义一个回调函数却不想写大量代码的时候我们可以选择使用匿名内部类来实现 举例说明如下：

20.java中this的作用

- this指代当前对象，当方法里面的局部变量和成员变量同名的时候，但是程序又需要在该方法里去覆盖这个成员变量，那么就必须使用this,以区分类的属性和方法中的参数。
- ![uTools_1670561534315](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670561534315.png)
- 让类中的一个方法去访问类中的另一个方法。
- ![uTools_1670561573009](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670561573009.png)
- this(参数)这种语法可以完成对构造方法的调用，只能在一个构造方法中使用this语句来调用类的其他构造方法，而不能在实例方法中用this语句来调用类的其他构造方法，也不能通过方法名来直接调用构造方法。且this()只可以放在所有语句的第一行。
- ![uTools_1670561694580](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670561694580.png)
- ![uTools_1670561721618](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670561721618.png)

21.java方法中不加void，那么这个地方一定是被一个其它的数据类型所替代。如20小点中的构造方法和普通方法。

22.this关键字

![uTools_1670680260544](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670680260544.png)

**把传过来的参数中的数据赋值给成员位置的name**

![uTools_1670680324378](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670680324378.png)

**一个对象调用了这个方法,this就指代这个对象的地址值(调用者就是对象)**

![uTools_1670683975479](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670683975479.png)

23.![uTools_1671699507571](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1671699507571.png)
