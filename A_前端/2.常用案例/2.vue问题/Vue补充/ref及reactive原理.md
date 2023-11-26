## 1.reactive为什么不能传字符串

因为reactive是基于proxy对象，它的第一个参数必须是对象。

![image-20231009202653325](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231009202653325.png)



## 2.为什么ref需要ref.value

因为ref的源码实际上模拟proxy对象，但是不是真的，用来处理字符串等原始值类型

get value这个函数返回的是this,_value  所以我们需要ref.value才能获取值

ref实现的源码

![image-20231009202924551](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231009202924551.png)



## 3.ref的收集依赖和触发依赖

![image-20231009203633387](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231009203633387.png)



原理图

![image-20231009203812719](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231009203812719.png)

当我们执行获取值的函数以后，执行的函数fn1会作为依赖存于obj.name这个属性下(这样去理解),这样相当于name属性记住了这个函数，当我们需要再次修改name值时就会通过set value(newValue)再去调用这个函数,此时就是触发了依赖(这样的好处是性能好)



## 4.关于ref中传入对象属性时

在vue3中，ref其实是可以处理原始值也可以处理引用类型的,因为传入的如果是引用类型的，vue内部会直接用reactive来处理这个值，如果是原始值就用ref处理。

但是ref的性能会更好，因为ref进行了重构，性能提升很多，开发尽量用ref。
