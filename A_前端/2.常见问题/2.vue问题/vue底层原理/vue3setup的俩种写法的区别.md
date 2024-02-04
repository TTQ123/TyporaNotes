1.通过语法糖写法 获取组件实例打印

![image-20240106204158767](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106204158767.png)

2.不通过语法糖写法 获取组件实例打印

![image-20240106204222897](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106204222897.png)



`通过对比我们可以发现,不通过语法糖的方式打印出来的组件实例,向外部暴露了很多东西,就像vue2打印组件实例一样`

接下来我们通过插件查看这俩个组件的编译结果(vue文件最终会形成一个编译结果)

![image-20240106210742324](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106210742324.png)

对比

没有语法糖的

![image-20240106210804369](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106210804369.png)

使用语法糖的

![image-20240106210830958](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106210830958.png)



**expose的配置有俩种方式**

**配置以后就只会暴露你想暴露的东西**

1. 

![image-20240106210926143](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106210926143.png)

2. 

![image-20240106210949490](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240106210949490.png)



**1.如果只是调用expose，没有指定暴露的东西，那就什么都不暴露**



**2.而加上了语法糖的写法会自动调用expose**



**3.如果我们想要在语法糖中向外界暴露就需要使用defineExpose宏函数**

**这里引出了另一个知识点：宏函数只参与编译,不参与代码运行,所以他们不需要导入可以直接使用,因为他们只在编译时生效,运行环境里压根没有这个函数**



**4.为什么要这样设计？因为这样减少了在组件外部修改组件内部数据方法的可能，更加规范,语法糖的写法会自动调用expose函数，所以我们更推荐使用**





**模板的数据来源是来自组件的实例，但是这个组件实例上面没有这些数据**

![image-20240129223611757](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240129223611757.png)

这个数据是在$setup里面拿到的，不是在组件实例上的

setup编译的时候会把数据传到$setup这个参数上