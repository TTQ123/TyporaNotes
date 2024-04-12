# 服务端和客户端通过token进行通信的情况

![1712675238869](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1712675238869.png)

```bash
1.用户登录: 用户在客户端提供用户名和密码进行登录。
2.服务端验证: 服务端接收到用户名和密码后，进行验证，并生成一个 token。这个 token 包含了用户的身份信息，以及可能的其他信息（比如权限等）。
3.返回 token: 如果验证成功，服务端将生成的 token 返回给客户端。
4.客户端存储 token: 客户端收到 token 后，通常会将其存储在本地，比如 localStorage 或者 sessionStorage 中。
5.每次请求携带 token: 客户端在每次与服务端通信时，都会将 token 放入请求的头部或者作为参数发送给服务端。
6.服务端验证 token: 服务端在接收到请求时，会验证 token 的有效性。如果 token 有效，服务端会处理请求；如果 token 无效，服务端会返回相应的错误信息。
7.刷新token: 当当服务端验证 token 成功后，可以生成一个新的时效的 token，并将其返回给客户端。客户端可以使用这个新 token 替换旧的 token。
```

一般是通过JWT来进行通信的

## **后端操作**

JWT文件

```js
const jsonwebtoken = require('jsonwebtoken');
const secret = 'ttq';

const JWT = {
    // 生成token
    generate(value, expires){
        // token/签名/过期时间
        return jsonwebtoken.sign(value, secret, { expiresIn: expires });
    },
    // 解密
    verify(token){
        try {
            return jsonwebtoken.verify(token, secret);
        } catch (error) {
            return false;
        }
    }
}

module.exports = JWT;
```

登录接口

```js
const UserService = require("../../services/admin/UserService");
const JWT = require("../../utils/JWT")

const UserController = {
    login:async(req, res)=> {
        // 测试后端能否拿到数据
        console.log(req.body)
        // 调用login函数时需要进行数据库验证(service层)
        // 参数在请求体中，传递给该方法
        var result =  await UserService.login(req.body)

        if(result.length===0){
            res.send({
                code:"-1",
                error:"用户名密码不匹配"
            })
        }else{
            // 登录成功 生成token
            const token = JWT.generate({
                // mongoDB中的_id
                _id:result[0]._id,
                username:result[0].username,
            }, '1d')

            // 授权成功
            res.header("Authorization",token)

            res.send({
                ActionType:"OK"
            })
        }
      }
}
module.exports = UserController;
```

**app.js统一校验**

```js
// 在进入所有路由之前统一进行是否授权的判断
// req请求对象 res响应对象
app.use((req, res, next) => {
    // 如果token有效 ,next() 
  // 如果token过期了, 返回401错误
  // 排除特殊情况login接口
  if(req.url==="/adminapi/user/login"){
    next()
    return;
  }

  // 取出token
  const token = req.headers["authorization"].split(" ")[1]
  if(token){
    var payload = JWT.verify(token)

    // 如果token有效, 继续向下执行
    // 登录以后会拿到token 如果token有限(payload),执行逻辑，同时更新token的时效性
    if(payload){
      // 生成新token
      const newToken = JWT.generate({
        _id:payload._id,
        username:payload.username
      },"1d")
      res.header("Authorization",newToken)
      next()
    }else{
      // token无效时(超过token有效时间且还直接请求服务器旧会返回401  前端此时就需要重新登录)
      res.status(401).send({errCode:"-1",errorInfo:"token过期"})
    }
  }
})

// 路由配置 ......
app.use(UserRouter)
// ......
```



## **前端操作**

在axios实例中配置统一拦截器

```js
import axios from 'axios';

// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么 -> 带上token
    const token = localStorage.getItem("token")
    // Bearer ${token} 是一种约定的格式
    config.headers.Authorization = `Bearer ${token}`

    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });


// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么 -> 存储token
	
    // 从headers中取出token
    const { authorization } = response.headers

    authorization && localStorage.setItem("token",authorization)
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么

    const {status} = error.response
    // 401表示token过期
    if(status===401){
        localStorage.removeItem("token")
        window.location.href="#/login"
    }
  })

  export default axios;
```





# 单点登录理论

主流的做法有以下几种

1.session+cookie 大公司用的成本很高 优点是控制力强，可以强制控制用户(删除session表里的记录即可)

![image-20240410181950991](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240410181950991.png)

2.token做法

2.1  单token模式，对用户可控度低

![image-20240410182106307](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240410182106307.png)

认证中心和子系统共用同一个秘钥就可以让子系统实现单独认证

```bash
1.用户登录成功后，认证成功后会返回一个token
2.用户以后发请求时需要带上token，子系统和认证中心都认识这个token，所以子系统和用户可以自由通信
3.验证通过后会返回对应保密的资源
```





2.2 双token模式  保持了对用户一定的控制力度

![image-20240410182328160](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240410182328160.png)

![image-20240410182346956](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240410182346956.png)

```bash
1.用户登录成功后，认证中心会返回token(时效短)和refreshtoken(时效长)
2.用户发请求时需要带上token，子系统只认识token
3.一段时间后token会失效，用户需要携带和refreshtoken前往认证中心获取新的token
4.用户使用新token发送请求
```

