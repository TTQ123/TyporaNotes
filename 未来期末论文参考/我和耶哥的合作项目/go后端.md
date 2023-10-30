1.go环境配置

[超详细go语言环境配置！！！_go环境配置-CSDN博客](https://blog.csdn.net/qq_57287010/article/details/128690648)



实际操作

![1698197203528](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1698197203528.png)

![1698197232547](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1698197232547.png)

![1698197248352](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1698197248352.png)





**拉取最新后台项目**

```bash
1.git pull ....
2.进入项目终端  配置go env -w GO111MODULE=on go env -w GOPROXY=https://goproxy.cn,direct(go镜像)
3.下载依赖  go mod tidy
4.运行项目  go run app.go
```

