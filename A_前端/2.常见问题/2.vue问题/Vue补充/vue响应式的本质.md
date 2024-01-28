通过面试题来理解

子组件

```vue
<template>
  <p>{{ count }}</p>
  <p>{{ doubleCount }}</p>
</template>

<script setup>
// 父页面增加count时doubleCount会不会跟着变化
import { computed, ref, watchEffect } from 'vue'

const props = defineProps({
  count: Number
})

// 重点: vue响应式的本质的是函数 和 数据之间的关联
/*
   函数指的是被vue监控起来的函数,vue2中是watcher,vue3中是effect
   vue3中会被监控的函数:
     1.render
     2.computed
     3.watchEffect
     4.watch
   数据
     1.必须是响应式的数据
     2.必须在上述的函数中使用
*/
// 例如数据变化会触发模板更新
// 其实本质是模板是render渲染函数 数据变化后render函数重新执行

// 场景1
// 不会变化 因为此处涉及的是数据和数据的变化 并没有形成函数和数据关联
// js并没有通过数据改变另一个数据的能力
const doubleCount = ref(props.count * 2)

// 场景2
// 会变化 props.count变化时会触发watchEffect重新运行，导致doubleCount.value
// 重新计算值，计算值后又会触发模板render函数更新
const doubleCount = ref(0)
watchEffect(() => {
  console.log('watchEffect执行了')
  doubleCount.value = props.count * 2
})

// 场景3 不会变化
// 在调用函数时我们传入了props.count,这其实是传递了一个原始值,使其失去了响应性
// 因此count * 2 和我们传入的props.count就没有关系了,所以watchEffect不会重新运行,只运行一次
// 所以doubleCount.value一直不会更新
function useDouble(count) {
  const doubleCount = ref(count * 2)
  watchEffect(() => {
    console.log('watchEffect执行了')
    doubleCount.value = count * 2
  })
  return doubleCount
}
const doubleCount = useDouble(props.count)

// 场景4 会变化
// 响应式数据变化触发computed重新计算值->doubleCount.value重新计算值->触发模板render函数更新
const doubleCount = computed(() => props.count * 2)

// 场景5 不会变化
// 还是一样，因为传递了一个原始值给这个函数，所以computed里面没有用到响应式数据
function useDouble(count) {
  const doubleCount = computed(() => count * 2)
  return doubleCount
}
const doubleCount = useDouble(props.count)

// 场景6 如何使得场景5有效  常见的vueUse也是这个原理
// 就是把整个响应式对象传给函数
function useDouble(props) {
  const doubleCount = computed(() => props.count * 2)
  return doubleCount
}
const doubleCount = useDouble(props)

// 常见的vueUse也是这个原理避免丢失响应性
function useDouble(props, propName) {
  const doubleCount = computed(() => props[propName] * 2)
  return doubleCount
}
// 传递一个响应对象 然后还要指定要修改的属性名
const doubleCount = useDouble(props, 'count')
</script>
```



父组件

```vue
<script setup>
import { ref } from 'vue'
import AppIndex from './AppIndex.vue'

const count = ref(0)
</script>

<template>
  <AppIndex :count="count"></AppIndex>
  <button @click="count + 5">点击</button>
</template>
```