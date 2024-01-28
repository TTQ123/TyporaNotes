## 1.vue2的多层响应性处理

**vue2的多层对象不具有响应性,要特殊处理**

**Vue3已经升级了，多层对象也有响应性**

```vue
<template>  
  <div>  
    <input v-model="message" />  
    <p>{{ message }}</p>  
    <input v-model="nestedData.nestedProp" />  
    <p>{{ nestedData.nestedProp }}</p>  
  </div>  
</template>

<script>  
export default {  
  data() {  
    return {  
      message: "",  
      nestedData: {  
        nestedProp: "",  
      },  
    };  
  },  
  computed: {  
    messageJSON() {  
      return JSON.stringify(this.message);  
    },  
    nestedDataJSON() {  
      return JSON.stringify(this.nestedData);  
    },  
  },  
  watch: {  
    messageJSON(newVal, oldVal) {  
      this.message = JSON.parse(newVal);  
    },  
    nestedDataJSON(newVal, oldVal) {  
      this.nestedData = JSON.parse(newVal);  
    },  
  },  
};  
//在这个例子中，我们使用了 computed 属性来计算 messageJSON 和 nestedDataJSON，并使用 watch 选项来监听它们的变化。当 message 或 nestedData 发生变化时，我们会自动更新 messageJSON 和 nestedDataJSON，从而实现多层对象的响应式。
</script>  
```



**也可以通过引入第三库来帮我们完成vue2的多层响应**

```js
//在 Vue 2 中，实现多层对象的响应式主要有两种方法。除了我之前提到的递归方式外，还有一种方法是使用第三方库，如 vue-observe-js 或 vue-deep-watch。这些库可以自动追踪多层对象的变化，使得响应式更加方便。
```

![image-20230919123932836](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919123932836.png)

![image-20230919123943259](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919123943259.png)



## 2.props的多层响应性

![image-20230919124038969](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230919124038969.png)

### 1.通过递归的方式

```js
export default {  
  props: {  
    nestedData: {  
      type: Object,  
      required: true,  
    },  
  },  
  created() {
    //调用方法
    this.makeResponsive(this.nestedData);  
  },  
  methods: {  
    makeResponsive(obj) {  
      for (const key in obj) {
        //检查当前遍历到的属性值是否是一个对象。如果是对象，则递归调用 makeResponsive 方法；如果不是对象，则执行条件语句之后的代码。
        if (typeof obj[key] === 'object') {
            //递归调用 makeResponsive 方法，将当前属性的值（即嵌套的对象）作为参数传递。
          this.makeResponsive(obj[key]);
        } else {
            //如果当前属性值不是对象
            //使用 Vue.js 的 $set 方法将当前属性的值设置为响应式。这样，当父组件的 nestedData 发生变化时，子组件的 nestedProp 也会自动更新。
          this.$set(obj, key, obj[key]);  
        }  
      }  
    },  
  },  
};  
```



### 2.通过解构的方式来拿到想要的数据(并保持响应性)

```vue
<template>  
  <div>  
    <p>{{ nestedProp }}</p>  
  </div>  
</template>

<script>  
export default {  
  data() {  
    return {  
      nestedProp: null,  
    };  
  },  
  props: {  
    nestedData: {  
      type: Object,  
      required: true,  
    },  
  },  
  created() {  
    this.nestedProp = this.nestedData.nestedProp;  
  },  
}; 
//在这个示例中，我们在 data 中定义了 nestedProp 属性，并在 created 生命周期钩子中通过解构的方式从 nestedData 对象中获取 nestedProp 属性。当父组件的 nestedData 发生变化时，子组件的 nestedProp 也会自动更新。这就实现了通过解构方式获取多层对象并将其中的属性设置为响应式的功能。
</script>  
```

