## WebSocket之前的实时通信如何解决

![image-20231119140433591](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140433591.png)



## 1.什么是WebSocket

WebSocket是一种在单个TCP连接上进行全双工通信的协议，它允许在客户端和服务器之间进行双向实时通信。相比传统的基于HTTP的通信方式，WebSocket提供了更低的延迟和更高的效率。

WebSocket协议的特点包括：

1. **全双工通信**：客户端和服务器可以同时向对方发送和接收消息，实现实时的双向通信。
2. **低延迟**：相比传统的基于HTTP轮询的通信方式，WebSocket可以减少通信的延迟，因为它在建立连接后可以持续保持连接状态，避免了重复建立连接的开销。
3. **轻量级**：WebSocket协议相对轻量，它的消息头部相对较小，减少了通信时的额外开销。
4. **跨域支持**：WebSocket协议可以支持跨域通信，因此可以在不同域名的服务器间进行实时通信。

![image-20240104165406593](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240104165406593.png)

![image-20240104165431211](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240104165431211.png)



## 2.websocket的优势

![image-20240104165511739](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20240104165511739.png)



## 3.实例

前端

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WebSocket</title>
</head>
<body>
    <button onclick="onMsg()">发送消息</button>

    <script>
        // 定义新的WebSocket实例，并通过该实例尝试建立到指定地址（
        const ws = new WebSocket('ws://localhost:3000');

        // 和服务器取得连接
        ws.onopen = function(e) {
            console.log('WebSocket连接已打开');
        }

        // 获取服务器的消息
        ws.onmessage = function(e) {
            console.log('收到消息：', e.data);
        }

        // 关闭和服务器的连接
        ws.onclose = function(e) {
            console.log('WebSocket连接已关闭');
        }

        function onMsg() {
            ws.send('你好服务器');
        }
    </script>
</body>
</html>
```



后端使用node

```js
// 使用express框架实现
const express = require('express');
const http = require('http');
const WebSocket = require('ws');

// 创建 Express 应用
const app = express();

// 创建 HTTP 服务器并将 Express 应用绑定到服务器
const server = http.createServer(app);

// 创建 WebSocket 服务器并将其与 HTTP 服务器关联
const wss = new WebSocket.Server({ server });

// Express 路由处理 HTTP 请求
app.get('/', (req, res) => {
    res.send('Hello World');
});

// WebSocket 服务器处理 WebSocket 连接
wss.on('connection', (socket) => {
    console.log('WebSocket连接已打开');

    socket.on('message', (message) => {
        console.log(`收到消息：${message}`);
        // 在这里可以对接收到的消息进行处理
        socket.send('你好,客户端');
    });

    socket.on('close', () => {
        console.log('WebSocket连接已关闭');
        // 在这里可以进行连接关闭后的清理工作   
    });
});

// 启动服务器，监听在 3000 端口上
server.listen(3000, () => {
    console.log('服务器已启动，监听端口3000');
});
```



## 4.心跳机制

![image-20231119140235327](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140235327.png)

![image-20231119140253804](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140253804.png)



## 5.websocket的限制

![image-20231119140337775](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119140337775.png)