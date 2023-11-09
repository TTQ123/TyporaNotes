![image-20231026123628076](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231026123628076.png)

axios.post(请求地址,参数,配置对象)



## 1.axios发送get请求

axios.get(请求地址,配置对象)

```js
// 定义查询参数
const params = {
  key1: 'value1',
  key2: 'value2'
};

// 发送带有查询参数的 GET 请求 并且带上token
axios.get('https://api.example.com/data', {
  params: params,
  headers: {
    'Authorization': 'Bearer your_token',
    'Content-Type': 'application/json' // 可选的其他头信息
  }
})
  .then(function (response) {
    // 处理成功的响应
    console.log(response.data);
  })
  .catch(function (error) {
    // 处理错误
    console.error(error);
  });
```

配置了axios实例后 不用我们自己带token 统一带上token了

![image-20231108131222035](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231108131222035.png)



## 2.axios发送post请求

axios.post(请求地址,参数,配置对象)

```js
// 定义要发送的数据
const postData = {
  key1: 'value1',
  key2: 'value2'
};

// 发送带有请求头的 POST 请求
axios.post('https://api.example.com/postEndpoint', postData, {
  headers: {
    'Authorization': 'Bearer your_token',
    'Content-Type': 'application/json' // 可选的其他头信息
  }
})
  .then(function (response) {
    // 处理成功的响应
    console.log(response.data);
  })
  .catch(function (error) {
    // 处理错误
    console.error(error);
  });
```



配置了axios实例后 不用我们自己带token 统一带上token了

![image-20231108131154806](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231108131154806.png)





## 3.接口

### 1.三种参数

![image-20231102214725589](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231102214725589.png)

header存在http请求头，一般我们会为每个请求带上header统一设置

![image-20231102214954170](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231102214954170.png)



query参数存在url地址中(一般是get请求使用，显示在url地址上)



body参数存在http请求体中

![image-20231102214742577](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231102214742577.png)

