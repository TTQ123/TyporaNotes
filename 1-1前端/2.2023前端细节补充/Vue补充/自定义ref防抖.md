# 1.自己来实现防抖

```vue
<template>
    <!-- Vue中利用自定义ref实现防抖 -->
    <div>
        <input type="text" :value="text" @input="handleUpdate">
        <p>{{ text }}</p>
    </div>
</template>

<script setup>
import { ref } from 'vue';
const text = ref('')
let timer
const handleUpdate = (e) => {
    clearTimeout(timer)
    setTimeout(() => {
        text.value = e.target.value
    }, 500)
}
</script>
```



# 2.抽离成一个防抖函数

vue

```vue
<template>
    <!-- Vue中利用自定义ref实现防抖 -->
    <div>
        <input type="text" :value="text" @input="handleUpdate">
        <p>{{ text }}</p>
    </div>
</template>

<script setup>
import { debounce } from '@/uitls/debounce.js'
import { ref } from 'vue';
const text = ref('')

// 更新的函数
const update = (e) => text.value = e.target.value
// 调用debounce 传入更新函数和防抖时间
const handleUpdate = debounce(update, 500)
</script>
```

js

```js
// 抽离的防抖函数 传入函数和防抖时间 默认防抖500
export function debounce(fn, delay = 500){
    let timer;
    // debounce函数返回一个可以接收任意参数的函数
    return function(...args){
        clearTimeout(timer)
        timer = setTimeout(() => {
            // call的第一个参数为函数指定this
            // 指定this是在调用 debounce 函数时确定的
            fn.call(this, ...args)
        }, delay)
    }
}
```



# 3.基于Object.defineProperty的自定义ref

vue

```vue
<template>
    <!-- Vue中利用自定义ref实现防抖 -->
    <div>
        <input type="text" v-model="text">
        <p>{{ text }}</p>
    </div>
</template>

<script setup>
import { debounceRef } from '@/uitls/debounceRef.js';
const text = debounceRef('')
</script>
```

js

```js
// vue提供的自定义ref的入口函数 提供track, trigger函数
import { customRef } from 'vue'

// value表示传入的值 delay表示延迟时间
export function debounceRef(value, delay = 1000){
    return customRef((track, trigger) => {
        let timer
        return {
            get(){
                // 收集依赖(记录谁使用了我的value)
                // 这个函数是vue提供的 可以收集依赖
                track()
                return value
            },
            set(setValue){
                // 派发更新(所有使用到的都进行更新)
                // 可以进行派发更新
                clearTimeout(timer)
                timer = setTimeout(() => {
                    trigger()
                    value = setValue
                }, delay)
            }
        }
    })
}
```

