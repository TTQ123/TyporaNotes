Vue CLI3 中可以通过设置环境变量和模式，可以根据不同模式加载不同的 baseUrl 地址。



参考文档:https://juejin.cn/post/6997587279468314660



## 1.项目环境

![image-20240305142639790](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305142639790.png)



**在Vue-cli中如何进行处理各个环境的配置**

![image-20240305142913993](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305142913993.png)



.env相当于是公共配置文件   .env.development相当于是生产环境变量

![image-20240305145000165](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145000165.png)



```json
package.json
  "scripts": {
    "dev": "vue-cli-service serve --open",  #默认启动开发环境服务
    "build": "vue-cli-service build", #默认启动生产环境 
    "production": "vue-cli-service serve --open --mode production", #启动生产环境服务
    "test":"vue-cli-service serve --open --mode test" #启动测试环境服务
  },
```



**权重:相同配置项会被替换,不同配置项会合并**

**注意是指定环境和公共环境的配置项有不同才会合并**

![image-20240305145039061](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145039061.png)



## 2.webpck环境注入

vue-cli封装了部分webpack配置 

![image-20240305145608379](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145608379.png)

**注意这个BASE_URL是在vue.config.js中配置的  不是在.env配置文件**

![image-20240305145653910](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145653910.png)

![image-20240305145732092](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145732092.png)



## 3.额外配置  使用动态参数

![image-20240305145930567](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145930567.png)

![image-20240305145953979](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305145953979.png)



## 4.实际使用

![image-20240305150029244](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305150029244.png)



## 5.总结

![image-20240305150510190](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305150510190.png)



**(2)在封装请求的时候，将baseURL替换为环境变量**

![image-20240305150803536](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305150803536.png)



![image-20240305151101728](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305151101728.png)

**target 配置表示:后端服务器地址**





## 补充:vue.cpnfig.js配置

官网 https://cli.vuejs.org/zh/config/#vue-config-js

![image-20240305151429724](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305151429724.png)

![image-20240305151718204](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240305151718204.png)



**整个vue-cli就是基于webpack封装的**