vue2在b站收藏夹



vue3

APP.VUE

10版本安装只要 `npm i swiper`

```VUE
<script setup>
import axios from 'axios'
import { ref, onUpdated } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
// 引入swiper样式（按需导入）
import 'swiper/css/pagination' // 轮播图底面的小圆点
import 'swiper/css/navigation' // 轮播图两边的左右箭头
// import 'swiper/css/scrollbar'  // 轮播图的滚动条， 轮播图里一般不怎么会使用到滚动条，如果有用到的话import导入就行
// 引入swiper核心和所需模块
import { Pagination, Navigation, Autoplay } from 'swiper/modules'

const navigation = ref({
  nextEl: ".swiper-button-next",
  prevEl: ".swiper-button-prev",
});

// 在modules加入要使用的模块
const modules = [Pagination, Navigation, Autoplay]

// 左箭头事件
const prevEl = (item, index) => {
  // console.log('上一张' + index + item)
};
// 右箭头事件
const nextEl = () => {
  // console.log('下一张')
};
// 更改当前活动swiper
const onSlideChange = (swiper) => {
  // swiper是当前轮播的对象，里面可以获取到当前swiper的所有信息，当前索引是activeIndex
  console.log('当前是第:' + swiper.activeIndex + '张')
}

// 发请求
const data = ref([])
const getData = async () => {
  let res = await axios.get('http://shibe.online/api/shibes?count=5')
  data.value = res.data
}
getData()
</script>

<template>
  <div v-if="data.length">
    <!--
      modules：
      loop： 是否循环播放
      slides-per-view：控制一次显示几张轮播图
      space-between： 每张轮播图之间的距离，该属性不可以和margin 属性同时使用；
      autoplay： 是否自动轮播， delay为间隔的毫秒数；disableOnInteraction属性默认是true，也就是当用户手动滑动后禁用自动播放， 设置为false后，将不会禁用，会每次手动触发后再重新启动自动播放。
      navigation： 定义左右切换箭头
      pagination： 控制是否可以点击圆点指示器切换轮播
      scrollbar： 是否显示轮播图的滚动条， draggable设置为 true就可以拖动底部的滚动条（轮播当中，一般不怎么会使用到这个属性）
    -->
    <swiper :modules="modules" :loop="true" :slides-per-view="1" :space-between="50" :navigation="navigation"
      :autoplay="{ delay: 4000, disableOnInteraction: false }" :pagination="{ clickable: true }" class="swiperBox"
      @slideChange="onSlideChange">
      <swiper-slide v-for="(item, index) in data" :key="index">
        <img :src="item">
      </swiper-slide>
      <div class="swiper-button-prev" @click.stop="prevEl(item, index)" />
      <!--左箭头。如果放置在swiper外面，需要自定义样式。-->
      <div class="swiper-button-next" @click.stop="nextEl" />
    </swiper>
  </div>
  <div v-else>
    没有数据
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
}

.swiper {
  margin-top: 50px;
  width: 500px;
  height: 300px;
  background-color: beige;
}

.swiper-slide {
  text-align: center;
  line-height: 300px;
}

.swiper-slide img {
  width: 500px;
  height: 300px;
}
</style>
```

main.js

```js
import {createApp} from 'vue'
import App from './App.vue'
import 'swiper/css';
createApp(App).mount('#app')
```

