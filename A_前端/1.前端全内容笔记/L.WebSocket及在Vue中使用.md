# 基本概念

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





# 在Vue中使用

假设有以下一种场景，我们有一个大屏的Echarts页面，它的数据需要实时刷新，此时如果使用传统的方法，是前端设置一个定时器，一段时间内就像服务端请求数据，但是这种方法对服务器端的性能要求太高了。

以下是例子

```vue
<script setup>
import { tryOnUnmounted } from "@vueuse/core";

// 进入页面后这里会自动执行创建连接(setup钩子执行)
const uid = "ttq123";
let isHandle = false; // 标记是否为手动关闭
let ws = new WebSocket(`ws://localhost:3000/ws?uid=${uid}`);
let timer = null;
ws.addEventListener("open", openHandle);
ws.addEventListener("close", closeHandle);
ws.addEventListener("message", messageHandle);
ws.addEventListener("error", errorHandle);

const openHandle = () => {
  console.log("连接成功");
};

const closeHandle = () => {
  console.log("连接关闭");
  // 如果不是认为的关闭，则需要自动重新建立连接
  if (!isHandle) {
    restart();
  }
  isHandle = false;
};

const messageHandle = ({ data }) => {
  // 接口中提供数据的方法 假设的(会更新页面图表数据)
  changeXisDta();
  //可以从事件对象中结构出data
  console.log("收到消息", data);
};

const errorHandle = (e) => {
  console.log("连接错误", e);
};

const changeXisDta = () => {
  // 假设的(会更新页面图表数据)
  console.log("图表数据更新");
};

const sendMsg = () => {
  // 主动像服务器发送数据
  ws.send("hello, 服务器,我是客户端");
};

const closeWs = () => {
  isHandle = true;
  // 手动关闭
  ws.close();
};

// 保持长连接的心跳机制
// 实现方法有俩种
// 方式1:  setInterval 持续给websocket发送心跳包
// const heartBeat = () => {
//   console.log("客户端与服务端断开，正在准备重连");
//   if (ws.readyState === 1) {
//     ws.send("heartBeat");
//   }
// };
// timer = setInterval(heartBeat, 3000);

// 方式2:  自动重新连接服务器
const restart = () => {
  console.log("客户端与服务端断开，正在准备重连");

  timer = setInterval(() => {
    console.log("重连中");
    // ws提供的这个方法可以判断当前连接是否为正常状态
    // 如果当前连接状态为0，则说明连接已经关闭，需要重新建立连接
    // 如果当前连接状态为1，则说明连接正常，不需要重新建立连接
    if (ws.readyState === 0) {
      clearInterval(timer);
      timer = null;
      ws = new WebSocket(`ws://localhost:3000/ws?uid=${uid}`);
      ws.addEventListener("open", openHandle);
      ws.addEventListener("close", closeHandle);
      ws.addEventListener("message", messageHandle);
      ws.addEventListener("error", errorHandle);
    }
  }, 3000);
};

// 组件卸载时需要卸载ws  正常是用onUnMounted 但是可以用vueuse库中的tryOnUnmounted(安全的onUnMounted)更好
tryOnUnmounted(() => {
  closeWs();
});
</script>

<template>
  <div class="main">
    <!-- 图表区域 -->
    <button @click="sendMsg">给服务器发消息</button>
    <button @click="closeWs">手动关闭连接</button>
  </div>
</template>
```

