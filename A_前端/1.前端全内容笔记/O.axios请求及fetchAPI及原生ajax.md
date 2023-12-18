# 1.axios

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



# 2.原生AJAX

## 1.发送get请求

```bash
1.send方法发送请求
```

![image-20231217194447467](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217194447467.png)

## 2.发送post请求

```bash
1.post请求发送请求的时候要说明发送的参数的格式(类型) -- 其实就是设置请求头
```

![image-20231217194602496](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217194602496.png)



# 3.axios实例

**一般是把实例提出来作为一个公共函数**

```js
const getNumber = async () => {
    // 配置请求实例
    const ins = axios.create({
        // 配置请求基地址
        baseURL:'https://www.baidu.com',
        // 超时时间
        timeout: 10000
    })

    // 配置请求拦截器
    ins.interceptors.request.use(config => {
        console.log('请求拦截器')
        // 配置token
        const userStore = useUserStore()
        // 如果用户token存在
        if (userStore.token) {
          // 发送请求携带请求头
          config.headers.Authorization = userStore.token
        }
        return config;
    })

    // 配置响应拦截器
    ins.interceptors.response.use(config => {
        // 一般在这里处理鉴权
        console.log('响应拦截器')
        return config;
    })

    // get请求 携带参数俩种方式
    // const res = await ins.get('/get?name=张三&age=18')
    const res1 = await ins.get('/get', {
        params: {
            name: '张三',
            age: 18
        }
    })
    console.log(res1.data);

    // post请求
    const res2 = await ins.post('/post', {
        name: '张三',
        age: 18
    })
    console.log(res2.data);
}
```



# 4.fetchAPI

**返回的也是promise,用then接收和async和await都一样**

## 1.get

默认发送的就是get请求

![image-20231217200845835](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217200845835.png)

## 2.post

**body配置的就是发送的参数**

![image-20231217200936907](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231217200936907.png)
