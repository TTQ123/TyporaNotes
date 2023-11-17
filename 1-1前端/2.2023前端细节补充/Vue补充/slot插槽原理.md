# 1.vue3中使用setup来定义组件

```vue
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'Vue3Setup',
  setup() {
    // 声明响应式数据
    const message = ref('Hello, Vue 3!');

    // 定义方法
    const increment = () => {
      message.value += '!';
    };

    // 返回需要暴露给模板的数据和方法
    return {
      message,
      increment
    };
  }
};
</script>
```



# 2.插槽的使用

## 1.默认插槽

默认插槽是最简单的一种插槽，也是最常用的一种。它允许父组件将任意内容插入子组件中。默认插槽在子组件中使用 `slot` 元素来定义，不需要指定名称。

在父组件中，可以使用子组件的标签包裹任意内容来插入到默认插槽中。例如：

```vue
<template>
  <div>
    <h1>这是父组件</h1>
    <ChildComponent>
      <p>这是插入到默认插槽的内容</p>
    </ChildComponent>
  </div>
</template>
```

在子组件中，可以使用 `slot` 元素来引用默认插槽的内容。例如：

```vue
<template>
  <div>
    <h2>这是子组件</h2>
    <slot></slot>
  </div>
</template>
```





## 2.具名插槽

具名插槽允许父组件将内容插入到子组件中的指定插槽中。具名插槽在子组件中使用 `slot` 元素来定义，需要指定一个名称。

在父组件中，可以使用 `v-slot` 指令来将内容插入到指定名称的插槽中。例如：

```vue
<template>
  <div>
    <h1>这是父组件</h1>
    <ChildComponent>
      <template v-slot:header>
        <h2>这是插入到具名插槽中的内容</h2>
      </template>
    </ChildComponent>
  </div>
</template>
```

在子组件中，可以使用 `slot` 元素的 `name` 属性来引用具名插槽的内容。例如：

```vue
<template>
  <div>
    <slot name="header"></slot>
    <p>这是子组件的内容</p>
  </div>
</template>
```



## 3.作用域插槽

作用域插槽允许子组件将数据传递给父组件，以便父组件可以在插槽中使用。作用域插槽在子组件中使用 `slot` 元素来定义，需要指定一个名称和一个参数。

在父组件中，可以使用 `v-slot` 指令来将内容插入到指定名称的插槽中，并使用 `slot-scope` 属性来接收子组件传递的数据。例如：

```vue
<template>
  <div>
    <h1>这是父组件</h1>
    <ChildComponent>
      <template v-slot:default="slotProps">
        <p>{{ slotProps.message }}</p>
      </template>
    </ChildComponent>
  </div>
</template>
```

在子组件中，可以在 `slot` 元素中传递一个对象，该对象包含需要传递给父组件的数据。例如：

```vue
<template>
  <div>
    <slot :message="message"></slot>
  </div>
</template>

<script>
export default {
  name: 'ChildComponent',
  data() {
    return {
      message: '这是子组件传递的数据'
    };
  }
};
</script>
```



# 3.理解插槽的原理

**插槽的本质是父组件传给子组件一个对象，子组件在配置函数里决定每个插槽渲染的位置。**

子组件

```js
// 这是子组件 我们没有通过单文件组件的写法 而是通过定义配置对象来实现插槽预留

// createElementVNode 函数，用于创建虚拟节点
import { createElementVNode } from 'vue'

/*
    原本在子组件我们是这样写的 这每一行其实都是调用了他对应的函数 default() slot1()....
    <slot></slot>
    <slot name="slot1"></slot>
    <slot name="slot2" msg="Hello"></slot>
*/

// 导出Vue 3 组件的配置对象
export default {
    // setup用于配置组件的行为和响应式数据
    // props 是一个响应式对象，包含了组件接收到的属性值。可以通过解构赋值的方式直接在 setup 函数中使用属性值，而不需要额外导入。
    // context 是一个包含了一些有用的上下文信息的对象。它包含了 attrs、slots、emit 等属性，用于访问组件的属性、插槽和事件。
    setup(props, { slots }){
        const defaultVNodes = slots.default() // 返回的都是一个数组
        const slot1VNodes = slots.slot1()
        const slot2VNodes = slots.slot2({msg: 'Hello,我是插槽2'})
        return () => {
            // 第一个参数是元素的标签名，第二个参数是元素的属性，第三个参数是元素的子节点
            return createElementVNode('div', null, [
                ...defaultVNodes,
                ...slot1VNodes,
                ...slot2VNodes
            ])
        }
    }
}
```



父组件

```vue
<template>
    <!-- 在父组件中引用 -->
    <Comp>
        <!-- 默认插槽 -->
        <p>default slot</p>
        <!-- 具名插槽 -->
        <template #slot1>
            我是插槽1
        </template>
        <!-- 作用域插槽 -->
        <template #slot2="msg">
            <p>{{ msg }}</p>
        </template>
    </Comp>

</template>

<script setup>
import Comp from '@/uitls/Comp.js'
</script>
```

