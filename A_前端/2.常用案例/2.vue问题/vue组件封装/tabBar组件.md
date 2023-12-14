```vue
<style scoped>
/* 这里应该搞到公共样式的 懒得搞 */
* {
  margin: 0;
  padding: 0;
  /* content-box：默认值，元素的宽度和高度只包括内容区域，不包括内边距和边框。 */
  /* border-box：元素的宽度和高度包括内容区域、内边距和边框。
  也就是说，指定的宽度和高度就是元素的最终尺寸，内边距和边框会从指定的宽度和高度中减去。 */
  box-sizing: border-box;
}

.navbar {
  background-color: #f0f0f0;
  width: 470px;
  height: 70px;
  padding: 12px 40px;
  position: relative;
}

/* 尝试 */
/* .nav-item::after {
  content: "";
  display: block;
  width: 20px;
  height: 1px;
  background-color: black;
} */

/* 左按钮样式 */
.scroll-button1 {
  position: absolute;
  top: 30px;
  left: 5px;
  /* 元素的背景将变为透明 */
  background-color: transparent;
  border: none;
  /* 鼠标变手指 */
  cursor: pointer;
}

/* 右边按钮样式 */
.scroll-button2 {
  position: absolute;
  top: 30px;
  right: 5px;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.navbar-scroll {
  /* 开启空白不换行 */
  /* white-space: nowrap; */
  overflow-x: auto;
}

.navbar-scroll::-webkit-scrollbar {
  display: none;
}

.navbar-nav {
  display: flex;
  list-style: none;
  align-items: center;
}

.nav-item {
  opacity: 0.4;
  transition: all 0.8s;
}

.nav-link {
  width: 60px;
  margin-right: 20px;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  text-decoration: none;
}


.nav-img {
  height: 15px;
  width: 15px;
}

.nav-span {
  font-size: 10px;
  font-weight: bold;
}

.icon-left,
.icon-right {
  width: 15px;
  height: 15px;
}

/* 第二种解决方法 塞一个空白内容 给个外边距 */
.nav-bottom {
  content: '';
  margin-top: 15px;
}
/* 设置a标签下面的黑线 */
.nav-bottom.bottom {
  margin-left: -1px;
  width: 24px;
  border-bottom: 1px solid black;
}

/* 点击的时候全黑 */
.nav-item.active {
  opacity: 1;
}
</style>

<template>
  <nav class="navbar">
    <!-- 按钮 -->
    <div @click="scrollLeft">
      <button class="scroll-button1">
        <img class="icon-left" src="../assets/left.png">
      </button>
    </div>

    <!-- 导航条 -->
    <!-- 这个盒子必须开启导航条 -->
    <div class="navbar-scroll" ref="currencyItemsRef">
      <ul class="navbar-nav">
        <li v-for="(item, index) in navItems" :key="index" class="nav-item" :class="{ active: activeItem === index }"
          @click="onClick(index)">
          <a class="nav-link">
            <img src="../assets/love.png" class="nav-img">
            <span class="nav-span">喜欢</span>
            <!-- 法一 -->
            <!-- <span class="nav-bottom" :class="{ bottom: activeItem === index }">&nbsp;</span> -->
            <!-- 法二 -->
            <span class="nav-bottom" :class="{ bottom: activeItem === index }"></span>
          </a>
        </li>
      </ul>
    </div>
    <!-- 按钮 -->
    <div @click="scrollRight">
      <button class="scroll-button2">
        <img class="icon-right" src="../assets/right.png">
      </button>
    </div>

  </nav>
</template>

<script setup>
import { ref, onMounted } from 'vue'
// 被点击的项
const activeItem = ref(null)
// 这个严格意义要是一个数组
const navItems = ref([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]) // 导航项的索引数组
// dom元素
const currencyItemsRef = ref(null)

const onClick = (index) => {
  // 如果有一项被点击了 其它项全部取消
  if (activeItem.value === index) {
    activeItem.value = null
  } else {
    // 反之就给新的一项赋值
    // 对比的条件是:class="{ active: activeItem === index }"
    // 只有index相等的时候才会被选中
    activeItem.value = index
  }
}

const scrollLeft = () => {
  if (currencyItemsRef.value) {
    // 只有开启了滚动条的dom元素才能设置scroll
    currencyItemsRef.value.scroll({
      // scrollLeft是一个元素的可滚动内容在水平方向上被隐藏的左侧部分的像素数。
      // 它表示元素在水平方向上滚动的距离。当元素的内容水平滚动时，scrollLeft属性可以用来获取或设置滚动位置。
      // offsetWidth是一个元素的可见宽度，包括元素的内容区域、内边距和边框。
      // 它表示元素在水平方向上的总宽度。
      left:
        // 当前滚动位置减去100.
        currencyItemsRef.value.scrollLeft - 100,
      behavior: 'smooth'
    });
  }
}

const scrollRight = () => {
  if (currencyItemsRef.value) {
    currencyItemsRef.value.scroll({
      // 容器元素的宽度，即向右边滚动一个容器宽度的距离
      // currencyItemsRef.value.offsetWidth
      left:
        currencyItemsRef.value.scrollLeft + 100,
      behavior: 'smooth'
    });
  }
}

onMounted(() => {
  // 默认选中第一项
  activeItem.value = 0
})
</script>
```

