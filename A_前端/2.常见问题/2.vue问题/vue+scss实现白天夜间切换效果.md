# 1.方式1 vue+scss切换白天黑夜效果

可参考：https://juejin.cn/post/7270800456862908455

可参考：https://www.jianshu.com/p/a33338f723aa

1. 安装Scss

注：若安装失败可以考虑使用cnpm，或者切换npm源等方式安装。

```nginx
pnpm add -D sass
npm install node-sass --save-dev    //安装node-sass
npm install sass-loader --save-dev  //安装sass-loader
npm install style-loader --save-dev //安装style-loader
```



2. 新建页面DarkModelPage.vue

> 文件所在位置：src/DarkModelPage.vue
>
> 命名路由路径：/dark-model-page

```vue
<template>
    <div id="DarkModelPage">
        
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped lang="scss">

</style>
```



3. 在src/assets新建目录scss
4. 在src/assets/scss新建目录common
5. 然后需要新建三个scss文件分别是

```bash
_themes.scss

_handle.scss

common.scss
```



6._themes.scss

```scss
$themes: (
  light: (
    background_color: #cccccc,//背景色
    text-color: rgba(0, 0, 0, 0.65), // 主文本色
  ),
  dark: (
    background_color: #181c27,//背景
    text-color: rgba(255, 255, 255, 0.65), // 主文本色
  )
);

```

7._handle.scss

```scss
@import "./_themes.scss";

//遍历主题map
@mixin themeify {
  @each $theme-name, $theme-map in $themes {
    //!global 把局部变量提升为全局变量
    $theme-map: $theme-map !global;
    //判断html的data-theme的属性值  #{}是sass的插值表达式
    //& sass嵌套里的父容器标识   @content是混合器插槽，像vue的slot
    [data-theme="#{$theme-name}"] & {
      @content;
    }
  }
}

//声明一个根据Key获取颜色的function
@function themed($key) {
  @return map-get($theme-map, $key);
}

//获取背景颜色
@mixin background_color($color) {
  @include themeify {
    background: themed($color)!important;
  }
}
//获取字体颜色
@mixin font_color($color) {
  @include themeify {
    color: themed($color)!important;
  }
}
```

8.common.scss

```scss
@import "@/assets/scss/common/_handle.scss";

/**
自定义的公共样式...
**/
*{
    margin:0;
    padding:0;
}
```



9. DarkModelPage.vue中使用

```vue
<template>
    <div id="DarkModelPage">
        <div>
            <h1 class="title">天小天个人网</h1>
            <a  class="btn" @click="modelBrn">模式切换</a>
        </div>
    </div>
</template>

<script>
export default {
    name: "DarkModelPage",
    data(){
        return {
          dark:false,
        }
    },
    methods:{
        modelBrn(){
            this.dark = !this.dark;
            if(this.dark){
                window.document.documentElement.setAttribute( "data-theme", 'dark' );
            }else{
                 window.document.documentElement.setAttribute( "data-theme", 'light' );
            }
        },
    },
    mounted() {
        window.document.documentElement.setAttribute( "data-theme", 'light' );
    },
}
</script>

<style scoped lang="scss">
@import '@/assets/scss/common/common';

#DarkModelPage{
    //在此使用了背景颜色变量
    @include background_color("background_color");
    //再次使用了文字颜色变量
    @include font_color("text-color");

    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content:center;
    align-items: center;
    transition: background 1s , color 0.6s;
    .title{
        margin-bottom: 20px;
    }
    .btn{
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100px;
        height: 40px;
        margin:  0 auto;
    }
}
</style>
```

如需更多颜色及样式切换，在_themes.scss设置好变量，通过_handle.scss设置切换函数，即可以在页面中通过该函数对指定样式进行设置。



# 2.多种主题效果

可参考：https://www.jianshu.com/p/a33338f723aa

![image-20231126171519874](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231126171519874.png)

安装sass什么的和上面一样

1._handle.scss

```scss
// 主题变量
$themes: (
  light: (
    background_color: #cccccc,//背景色
    text_color: rgba(0, 0, 0, 0.65), // 主文本色
  ),
  dark: (
    background_color: #181c27,//背景
    text_color: rgba(255, 255, 255, 0.65), // 主文本色
  ),
  red:(
    background_color: rgb(230, 27, 27),//背景
    text_color: rgba(255, 255, 255, 0.65), // 主文本色
  )
);

//定义混合
@mixin useTheme {
    // 遍历主题map $theme-name属性名 $theme-map属性值
  @each $theme-name, $theme-map in $themes {
    // ！global 把局部变量提升为全局变量
    $theme-map: $theme-map !global;
    //判断html的data-theme的属性值(切换主题就是给它加上不同的值)  #{}是sass的插值表达式
    //& sass嵌套里的父容器标识 这里的意思是谁使用了这个mixin，就给谁加上data-theme属性
    html[data-theme="#{$theme-name}"] & {
        //@content是混合器插槽，像vue的slot
        @content;
    }
  }
}

//声明一个根据Key获取颜色的function
@function themed($key) {
  @return map-get($theme-map, $key);
}

//获取背景颜色
@mixin background_color($color) {
  @include useTheme {
    background: themed($color) !important;
  }
}
//获取字体颜色
@mixin font_color($color) {
  @include useTheme {
    color: themed($color) !important;
  }
}
```

2.common.scss

```scss
@import "./_handle.scss";

/**
自定义的公共样式...
**/
*{
    margin: 0;
    padding: 0;
}
```

3.main.js

```js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
// 引入文件
import "@/assets/scss/common/common.scss"

import App from './App.vue'
import router from './router'

const app = createApp(App)

app.use(createPinia())
app.use(router)

app.mount('#app')
```

4.组件引用

```vue
<template>
  <div id="ModelPage">
    <div>
      <h1 class="title">切换主题</h1>
      <a class="btn" @click="theme('dark')">黑色</a>
      <a class="btn" @click="theme('light')">白色</a>
      <a class="btn" @click="theme('red')">红色</a>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
const theme = (type) => {
  window.document.documentElement.setAttribute("data-theme", type);
}
onMounted(()=>{
  // 默认挂载白色
  window.document.documentElement.setAttribute("data-theme", 'light');
})

</script>

<style scoped lang="scss">
// 引入文件
@import "@/assets/scss/common/common";

#ModelPage {
  //在此使用了背景颜色变量
  @include background_color("background_color");
  //在此使用了文字颜色变量
  @include font_color("text_color");

  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  // 动画切换效果
  transition: background 1s, color 0.6s;

  .title {
    margin-bottom: 20px;
  }

  .btn {
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    height: 40px;
    margin: 0 auto;
  }
}
</style>
```

