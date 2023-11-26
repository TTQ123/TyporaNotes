# 1.方式1 自己封装了一个暗黑组件出来

参考文章

[vue3 element-plus 暗黑模式（主题切换）简易版_vue深色模式_Raywh的博客-CSDN博客](https://blog.csdn.net/wanghu20150107010129/article/details/131110061)

在vue3文件夹下大事件项目进行了实战使用



实例

1.mian.js引入暗黑主题

![image-20231119224509609](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119224509609.png)



2.创建暗黑组件  使用了vueuse来动态切换主题颜色,如果只需要深色模式,在index.html的html标签加上 class='drak'

参考地址

https://vueuse.org/core/useDark/

组件

```vue
<template>
  <div class="dark-box">
    <el-button text class="switch" :class="isDark ? 'isDark-switch' : 'noDark-switch'" @click="toggleDark">
      <el-icon v-if="isDark">
        <svg viewBox="0 0 24 24">
          <path
            d="M6.05 4.14l-.39-.39a.993.993 0 0 0-1.4 0l-.01.01a.984.984 0 0 0 0 1.4l.39.39c.39.39 1.01.39 1.4 0l.01-.01a.984.984 0 0 0 0-1.4zM3.01 10.5H1.99c-.55 0-.99.44-.99.99v.01c0 .55.44.99.99.99H3c.56.01 1-.43 1-.98v-.01c0-.56-.44-1-.99-1zm9-9.95H12c-.56 0-1 .44-1 .99v.96c0 .55.44.99.99.99H12c.56.01 1-.43 1-.98v-.97c0-.55-.44-.99-.99-.99zm7.74 3.21c-.39-.39-1.02-.39-1.41-.01l-.39.39a.984.984 0 0 0 0 1.4l.01.01c.39.39 1.02.39 1.4 0l.39-.39a.984.984 0 0 0 0-1.4zm-1.81 15.1l.39.39a.996.996 0 1 0 1.41-1.41l-.39-.39a.993.993 0 0 0-1.4 0c-.4.4-.4 1.02-.01 1.41zM20 11.49v.01c0 .55.44.99.99.99H22c.55 0 .99-.44.99-.99v-.01c0-.55-.44-.99-.99-.99h-1.01c-.55 0-.99.44-.99.99zM12 5.5c-3.31 0-6 2.69-6 6s2.69 6 6 6s6-2.69 6-6s-2.69-6-6-6zm-.01 16.95H12c.55 0 .99-.44.99-.99v-.96c0-.55-.44-.99-.99-.99h-.01c-.55 0-.99.44-.99.99v.96c0 .55.44.99.99.99zm-7.74-3.21c.39.39 1.02.39 1.41 0l.39-.39a.993.993 0 0 0 0-1.4l-.01-.01a.996.996 0 0 0-1.41 0l-.39.39c-.38.4-.38 1.02.01 1.41z"
            fill="currentColor"></path>
        </svg>
      </el-icon>
      <el-icon v-else>
        <svg viewBox="0 0 24 24">
          <path
            d="M11.01 3.05C6.51 3.54 3 7.36 3 12a9 9 0 0 0 9 9c4.63 0 8.45-3.5 8.95-8c.09-.79-.78-1.42-1.54-.95A5.403 5.403 0 0 1 11.1 7.5c0-1.06.31-2.06.84-2.89c.45-.67-.04-1.63-.93-1.56z"
            fill="currentColor"></path>
        </svg>
      </el-icon>
    </el-button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const isDark = ref(true)
const toggleDark = () => {
  isDark.value = !isDark.value
  const html = document.querySelector('html')
  if (html) {
    if (isDark.value) {
      html.classList.remove("dark");
      html.classList.add("light");
    } else {
      html.classList.remove("light");
      html.classList.add("dark");
    }
}
}

</script>

<style scoped lang="scss">
.dark-box {
  margin-right: 20px;
}
.switch {
  width: 40px;
  height: 20px;
  border: 1px solid #dcdfe6;
  border-radius: 10px;
  box-sizing: border-box;
  cursor: pointer;
  padding-bottom: 0;
  padding-top: 0px;

  background-color: #ebeef5 !important;
  font-size: 12px;
}

.isDark-switch {
  .el-icon {
    background-color: #fff !important;
    padding: 2px;
    border-radius: 50%;
    color: #000;
    margin-left: -8px;
  }
}

.noDark-switch {
  background-color: rgb(8, 8, 8) !important;

  .el-icon {
    color: #fff;
    margin-left: 15px;
  }
}
</style>
```



3.在项目中使用

![image-20231119224805008](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119224805008.png)

# 2.方式2 看官网