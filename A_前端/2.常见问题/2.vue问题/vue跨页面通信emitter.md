**如何进行俩个页面间的通信,可以使用mitt**



安装和导入

```bash
npm i mitt
```

在src/uitls/emitter.js

```js
// 引入mitt (这是实现不同页面(非父子组件)通信的一种方式)
import mitt from "mitt";

// 创建emitter
const emitter = mitt()

// 创建并暴露mitt
export default emitter
```



![image-20240110142959666](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240110142959666.png)



例子 点击添加后会跳转到添加页面,添加完成后发布事件并跳转回展示页面

展示页面

```vue
<script setup>
import { ref, onMounted,onUnmounted } from "vue"
import BigEventList from "../../components/BigEventList.vue";
import { getBigEventList } from "@/api/memorabilla.js";
import { useRouter } from "vue-router";
import emitter from "@/utils/emitter";

const router = useRouter()
const bigList = ref([])

onMounted(async () => {
  const res = await getBigEventList()
  bigList.value = res.data.data.memorabilias

  emitter.emit('listUpdate',async () => {
  // 重新请求列表
  const res =  await getBigEventList()
  bigList.value = res.data.data.memorabilias
})
})

const addBigEvent = () => {
  router.push("/dsj/add")
}

emitter.on('listUpdate',async () => {
  // 重新请求列表
  const res =  await getBigEventList()
  bigList.value = res.data.data.memorabilias
})

// 组件卸载的时候解绑事件    
onUnmounted(() => {
    emitter.off('listUpdate')
})
</script>

<template>
  <div class="header">
    大事件展示页面
    </div>
  <div class="top">
    <el-button type="primary" @click="addBigEvent">添加事件</el-button>
  </div>
  <div class="content">
    <BigEventList :list="bigList"></BigEventList>
  </div>
</template>

<style lang="scss" scoped>
.header{
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
  text-align: center;
}
.top{ 
  display: flex;
  justify-content: flex-end;
  margin-bottom: 10px;
  height: 30px;
}
</style>
```

BigEventList

```vue
<script setup>
const props = defineProps({
    list: Array
})
</script>

<template>
  <div class="content" v-for="item in props.list" :key="item.id">
    <el-card>
        <div class="top">
            id: {{ item.id }}
        </div>
        <div class="main">
            content: {{ item.content }}
        </div>
    </el-card>
  </div>
</template>

<style lang="scss" scoped>
.top{
    margin-top: 5px;
}
</style>
```

添加页面

```vue
<script setup>
// 这里我没有使用父子组件通信 而是使用了
import { ref, onUnmounted } from 'vue'
import { addBigEvent } from "@/api/memorabilla.js";
import emitter from "@/utils/emitter";
import { useRouter } from 'vue-router'

const router = useRouter()

const content = ref('')

const onSubmit = () => {
    // 提交分为俩步
    // 1. 将数据提交给后台
    // 2. 通知T-Dsj更新列表数据
    // 3. 跳转到列表页
    addBigEvent({
        content: content.value,
        // createTime: new Date(),
        happenTime: '2024-01-10',
        // id: nanoid(),
        // updateTime: new Date(),
        userId: 42
    })
    ElMessage.success('添加成功')

    // 创建事件:通知T-Dsj更新列表数据
    emitter.emit('listUpdate', () => {
        console.log('T-Dsj请更新列表数据');
    })

    // 跳转到列表页
    router.push('/dsj')
}
</script>

<template>
    <div class="header">
        大事件添加页面
    </div>
    <div class="content">
        <el-input v-model="content" placeholder="请输入内容Content" :rows="4" type="textarea"></el-input>
        <div class="btn">
            <el-button type="primary" @click="onSubmit">提交事件</el-button>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.header {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 30px;
    text-align: center;
}
.btn {
    display: flex;
    justify-content: center;
    margin-top: 20px;
}
</style>
```

