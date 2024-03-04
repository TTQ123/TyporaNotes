```vue
<template>
<!-- 可以调用别人写好的组件 -->
<!-- 参考:  https://juejin.cn/post/7018841640085241893   -->
  <div>
    <div>
      <button @click="toggleFullscreen">全屏</button>
    </div>

    <div>
      正常内容
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    toggleFullscreen() {
      const elem = document.documentElement; // 使用document.documentElement实现全屏

      if (!document.fullscreenElement) {
        // 如果非全屏模式则进入全屏
        elem.requestFullscreen().catch((err) => {
          alert(`Error 你的浏览器不支持全屏 mode: ${err.message} (${err.name})`);
        });
      } else {
        document.exitFullscreen();
      }
    },
  },
};
</script>

<style>
/* 有时候需要加上这段代码 */
/* :not(:root):fullscreen::backdrop{
  background: white;
} */
</style>
```

