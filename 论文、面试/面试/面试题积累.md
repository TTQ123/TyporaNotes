# 1.vue

1.vue中setup和data、methods可以共存吗？

答案：可以共存，但不建议，如果定义了同名变量或方法以setup的为显示

**原因是因为setup比vue2的beforeCreate的执行顺序还早，这样会出现一个很恶心的事情就是在data或methods里面可以用this访问到setup的数据,但是setup里的不能访问methods和data。**

![image-20240102211857089](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240102211857089.png)

![image-20240102212551597](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240102212551597.png)



2.vue的钩子函数有哪些?

这个就不仅仅要回答vue的生命周期钩子函数,例如还有nextTick()，路由守卫的钩子函数,它们也会在一些特定的阶段自动的执行这些函数完成相应的功能。



3

**除了我们自己定义在外部的ref在脚本中需要.value, 系统返回的或者其它不是我们主动定义的不用.value**

例如pinia 返回的实例对象有ref定义的变量也不用 .value

补充: 调用仓库返回的是一个reactive的实例对象

```ts
import {ref, reactive} from 'vue'
let sum = ref(0)
let arr = reactive({
  a:1,
  b:ref(2)
})
console.log(sum.value);
console.log(arr.a, arr.b);
```

