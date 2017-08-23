# webSocket
> WebSocket 是 HTML5 一种新的协议。它实现了浏览器与服务器全双工通信(客户端可以给服务器发消息，服务器也可以给客户端发消息)，能更好的节省服务器资源和带宽并达到实时通讯，它建立在 TCP 之上，同 HTTP 一样通过 TCP 来传输数据。

## 简介
- WebSocket 是一种双向通信协议，在建立连接后，WebSocket 服务器和 Browser/Client Agent 都能主动的向对方发送或接收数据，就像 Socket 一样；
- WebSocket 需要类似 TCP 的客户端和服务器端通过握手连接，连接成功后才能相互通信。
- 相对于传统 HTTP 每次请求-应答都需要客户端与服务端建立连接的模式，WebSocket 是类似 Socket 的 TCP 长连接的通讯模式，一旦 WebSocket 连接建立后，后续数据都以帧序列的形式传输。在客户端断开 WebSocket 连接或 Server 端断掉连接前，不需要客户端和服务端重新发起连接请求。
##  创建一个Socket实例
```javascript
var socket = new WebSocket('ws://localhost:80');
```

### 属性

|属性|含义|
|:----:|:----:|
|binaryType|一个字符串表示被传输二进制的内容的类型。取值应当是"blob"或者"arraybuffer"。|
|bufferedAmount|调用 send() 方法加入到队列中等待传输，但是还没有发出的字节数。|  
|extensions|服务器选定的扩展。目前这个属性只是一个空字符串，或者是一个包含所有扩展的列表。|
|protocol|一个表明服务器选定的子协议名字的字符串。|
|readyState	|连接的当前状态。|
|url|传入构造器的URL。它必须是一个绝对地址的URL。只读。|

### 方法

|方法|含义|
|:----:|:----:|
|close()|关闭WebSocket连接或停止正在进行的连接请求。|
|send()|通过WebSocket连接向服务器发送数据。|

### 事件

|事件|含义|
|:----:|:----:|
|onclose|用于监听连接关闭事件监听器。当WebSocket对象的readyState状态变为CLOSED时会触发该事件。这个监听器会接收一个叫close的CloseEvent对象。|
|onerror|当错误发生时用于监听error事件的事件监听器。会接受一个名为error的event对象。|
|onmessage|一个用于消息事件的事件监听器，这一事件当有消息到达的时候该事件会触发|
|onopen|一个用于连接打开事件的事件监听器。当readyState的值变为OPEN的时候会触发该事件。|

## Socket.io
> Socket.IO是Guillermo Rauch创建的WebSocket API，Guillermo Rauch是LearnBoost公司的首席技术官以及LearnBoost实验室的首席科学家。Socket.IO使用检测功能来判断是否建立WebSocket连接，或者是AJAX long-polling连接，或Flash等。可快速创建实时的应用程序。Socket.IO还提供了一个NodeJS API，它看起来非常像客户端API。

- 引入
```html
 <script src="http://cdn.socket.io/stable/socket.io.js"></script>
```
- 使用
```javascript
// 创建Socket.io实例，建立连接
var socket= new io.Socket('localhost',{
port: 8080
});
socket.connect();
// 添加一个连接监听器
socket.on('connect',function() {
console.log('Client has connected to the server!');
});
// 添加一个连接监听器
socket.on('message',function(data) {
console.log('Received a message from the server!',data);
});
// 添加一个关闭连接的监听器
socket.on('disconnect',function() {
console.log('The client has disconnected!');
});
// 通过Socket发送一条消息到服务器
function sendMessageToServer(message) {
socket.send(message);
}
```


## TCP协议三次握手
[三次握手](http://www.cnblogs.com/Jessy/p/3535612.html)是为了确认客户端跟服务器都能接受到对方的信息。

- 第一次握手，客户端给服务器发包SYN。   此时服务器确认自己可以接收客户端的包，客户端不确认服务器是否接收到了自己发的包。
- 第二次握手，服务器端回复客户端SYN+ACK。  此时客户端确认自己发的包被服务器收到，也确认自己可以正常接收服务器包，客户端对此次通信没有疑问了。服务器可以确认自己能接收到客户端的包，但不能确认客户端能否接收自己发的包。
- 第三次握手，客户端回复服务器ACK。  客户端已经没有疑问了，服务器也确认刚刚客户端收到了自己的包。两边都没有问题，开始通信。
