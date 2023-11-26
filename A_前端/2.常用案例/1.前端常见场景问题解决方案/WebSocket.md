## WebSocket之前的实时通信如何解决

![image-20231119140433591](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140433591.png)



## 1.什么是WebSocket

WebSocket是一种在单个TCP连接上进行全双工通信的协议，它允许在客户端和服务器之间进行双向实时通信。相比传统的基于HTTP的通信方式，WebSocket提供了更低的延迟和更高的效率。

WebSocket协议的特点包括：

1. **全双工通信**：客户端和服务器可以同时向对方发送和接收消息，实现实时的双向通信。
2. **低延迟**：相比传统的基于HTTP轮询的通信方式，WebSocket可以减少通信的延迟，因为它在建立连接后可以持续保持连接状态，避免了重复建立连接的开销。
3. **轻量级**：WebSocket协议相对轻量，它的消息头部相对较小，减少了通信时的额外开销。
4. **跨域支持**：WebSocket协议可以支持跨域通信，因此可以在不同域名的服务器间进行实时通信。



## 2.实例

![1700373484949](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/1700373484949.png)



后端使用node

**![image-20231119135948098](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119135948098.png)**



## 3.心跳机制

![image-20231119140235327](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140235327.png)

![image-20231119140253804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140253804.png)



## 4.websocket的限制

![image-20231119140337775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140337775.png)