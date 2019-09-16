# 使用 WebSocket 进行聊天

## 一、WebSocket介绍

### 什么是 WebSocket

WebSocket 是⼀种⽹络通信协议。在 2009 年诞⽣，于 2011 年被 IETF 定为标准 RFC 6455 通信标准。
WebSocket API 也被 W3C 定为标准。
WebSocket 是 HTML5 开始提供的⼀种在单个 TCP 连接上进⾏全双⼯ (full-duplex) 通讯的协议。没有
了 Request 和 Response 的概念，两者地位完全平等，连接⼀旦建⽴，就建⽴了持久性连接，浏览器和
服务器双⽅可以随时向对⽅发送数据。
HTML5 是 HTML 最新版本，包含⼀些新的标签和全新的 API。HTTP 是⼀种协议，⽬前最新版本是
HTTP/2 ，所以 WebSocket 和 HTTP 有⼀些交集，两者相异的地⽅还是很多。两者交集的地⽅在 HTTP
握⼿阶段，握⼿成功后，数据就直接从 TCP 通道传输。

### Web上的即时通信

在没有 WebSocket 之前，服务器很难主动向客户端推送数据。
Web 为了实现即时通信，经历了最初的 polling, 到之后的 Long polling，等若⼲种⽅式。

1. 短轮询 Polling

![1568633827387](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1568633827387.png)

这种⽅式下，是不适合获取实时信息的，客户端和服务器之间会⼀直进⾏连接，每隔⼀段时间就询
问⼀次。客户端会轮询，有没有新消息。这种⽅式连接数会很多，⼀个接受，⼀个发送。⽽且每次
发送请求都会有 HTTP 的 Header，会很耗流量，也会消耗 CPU 的利⽤率。
在 Web 端，短轮询⽤ AJAX JSONP Polling 轮询实现。

![1568634088561](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1568634088561.png)

2.长轮询Long Polling

![1568634317850](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1568634317850.png)

长轮询是对轮询的改进版，客户端发送HTTP给服务器之后，看有没有新消息，如果没有新消息，就一直等待。直到有消息或者超时了，才会返回给客户端。消息返回后，客户端再次建立连接，如此反复。这种做法在某种程度上减小了网络带宽和cpu利用率等问题。

这种方式也有一定的弊端，实时性不高，如果是高实时系统，肯定不会采用这种办法。因为一个GET请求来回需要2个RTT，很可能在这段时间内，数据变化很大，客户端拿到数据以经延后很多了。

+ 优点：减少轮询次数，低延迟，浏览器兼容性较好。
+ 缺点：服务器需要保持⼤量连接。

3.WebSocket

![1568634845046](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1568634845046.png)

为了解决其他机制的各种问题，⼈们设计出了 WebSocket 协议。
WebSocket 是 HTML5 开始提供的⼀种独⽴在单个 TCP 连接上进⾏全双⼯通讯的有状态的协议 (它
不同于⽆状态的 HTTP)，并且还能⽀持⼆进制帧、扩展协议、部分⾃定义的⼦协议、压缩等特性。

### 与普通 HTTP 协议的异同

1. WebSocket 协议的 URL 是 ws:// 或者 wss:// 开头的，⽽不是 HTTP:// 或者 HTTPS://
2. WebSocket 使⽤与普通 HTTP 或 HTTPS 协议相同的 80 端⼝和 443 端⼝进⾏连接
3. WebSocket 的 Header 中有连个特殊字段, 代表它是由 HTTP 协议升级为 WebSocket 协议

```
Connection: Upgrade
Upgrade: websocket
```

### 通过js建立一个简单的Websocket连接

```{}
var ws = new WebSocket('ws://example.com/socket');
ws.onopen = function () {
 ws.send("Connection established. Hello server!");
}
ws.onmessage = function(event) {
 console.log('client recv: ', event.data);
}
ws.onclose = function () { ... }
ws.onerror = function (error) { ... }
```

###  Tornado中使用WebSocket

```
class WebsockHandler(tornado.websocket.WebSocketHandler):
 def open(self):
 '''该⽅法处理建⽴连接时执⾏的操作'''
 pass
 def on_close(self):
 '''该⽅法处理断开连接时执⾏的操作'''
 pass
 def on_message(self, message):
 '''该⽅法处理收到消息时进⾏的操作'''
 pass
 def write_message(self, message):
 '''该⽅法可以给其他⼈发送消息'''
 pass
```

## ⼆、任务⽬标

1. 通过 Tornado 开发⼀个聊天室程序
2. 通过 WebSocket 进⾏⻓连接通信
3. 使⽤ Redis 保留 100 条离线消息

