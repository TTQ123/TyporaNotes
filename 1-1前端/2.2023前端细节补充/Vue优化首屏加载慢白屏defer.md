有的首屏要一次性加载很多很多组件，这不可避免的导致了首屏加载太慢了，因为vue是单页面应用(首页的大部分东西你用异步组件没办法优化)

**解决方法:通过渲染帧(16毫秒渲染一次)**

![image-20231019183623684](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231019183623684.png)

useDefer

```js
import { ref } from 'vue'

// 观察的最大时间帧
export function useDefer(maxFrameCount) {
  // 帧数
  const frameCount = ref(0)
  // 计数函数
  const refreshFrameCount = () => {
    // 按帧对网页进行重绘
    requestAnimationFrame(() => {
      // 每次重绘+1
      frameCount.value++
      // 如果没有超过最大时间就一直重绘
      if (frameCount.value < maxFrameCount) {
        refreshFrameCount()
      }
    })
  }
  refreshFrameCount()
  // 返回一个函数给 v-if 使用
  return function (showInFrameCount) {
    // 当前渲染的关键帧有没有大于传递的参数n
    // 第一次传递的是1  1=1 为true 这就表示第一帧只渲染一个组件
    return frameCount.value >= showInFrameCount
  }
}
```

