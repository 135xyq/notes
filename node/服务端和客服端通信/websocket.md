# 三种连接

## socket

1. 客户端连接服务器（TCP / IP），三次握手，建立了连接通道
2. 客户端和服务器通过socket接口发送消息和接收消息，任何一端在任何时候，都可以向另一端发送任何消息
3. 有一端断开了，通道销毁



## http

1. 客户端连接服务器（TCP / IP），三次握手，建立了连接通道
2. 客户端发送一个http格式的消息（消息头 消息体），服务器响应http格式的消息（消息头 消息体）
3. 客户端或服务器断开，通道销毁



实时性的问题

1. 轮询
2. 长连接



## websocket

专门用于解决实时传输的问题

1. 客户端连接服务器（TCP / IP），三次握手，建立了连接通道
2. 客户端发送一个http格式的消息（特殊格式），服务器也响应一个http格式的消息（特殊格式），称之为http握手
3. 双发自由通信，通信格式按照websocket的要求进行
4. 客户端或服务器断开，通道销毁


在websocket的http握手阶段，服务器响应头中需要包含如下内容：

```
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: [key]
```

其中，`Sec-WebSocket-Accept`的值来自于以下算法：

```js
base64(sha1(Sec-WebSocket-Key) + "258EAFA5-E914-47DA-95CA-C5AB0DC85B11") 
```

在`node`中可以使用以下代码获得：

```js
const crypto = require("crypto");
const hash = crypto.createHash("sha1");
hash.update(requestKey + "258EAFA5-E914-47DA-95CA-C5AB0DC85B11");
const key = hash.digest("base64");
```

其中，`requestKey`来自于请求头中的`Sec-WebSocket-Key`

