 1、当你尝试给饿了么ui加上一些样式时，有时候是不生效的，它的原因一般是有的饿了么组件之间有时候是互相引用的

比如el-form-item中套了一个el-input  你想给label设置样式是设置不上的

![image-20240331221824782](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240331221824782.png)

这是因为我们设置了scoped以后，vue会自动给外层元素带上一个[data-v-xxxxxxx]

![image-20240331222011705](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240331222011705.png)





我们如果想要给label设置样式，直接使用

```vue
<style>
    ::v-deep .el-from-item-label{
        ....
    }
</style>
```



完整https://blog.csdn.net/oYinHeZhiGuang/article/details/135420064



官网原理

![image-20240331223359509](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240331223359509.png)

![image-20240331223708877](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240331223708877.png)

```css
.login ::v-deep .el-form-item__label {
  color: #fff;
  font-size: 18px;
}

/*编译为*/

.login[data-v-xxxxx] .el-form-item__label{}
```

