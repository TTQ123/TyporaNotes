![image-20231211082428634](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231211082428634.png)



在index.html里面加上这俩行

```html
// 第一行目前好像不一定,如果你不修改样式的话可以不加
<link rel="stylesheet" href="<%= BASE_URL %>static/index.<%= VUE_APP_INDEX_CSS_HASH %>.css" />
<link rel="icon" href="./static/image/customer.png">
```

