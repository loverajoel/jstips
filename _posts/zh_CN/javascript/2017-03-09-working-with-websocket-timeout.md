---
layout: post

title: 处理 Websocket 超时问题
tip-number: 63
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 一个控制超时的技巧

categories:
    - zh_CN
    - javascript
---

在 websocket 连接被建立后，如果一段时间未活动，服务器或防火墙可能会超时或终止连接。想要解决这个问题， 我们可以周期性地给服务器发消息。我们需要两个方法实现：一个来确保连接不会中断，，另一个用来取消此设定。同我们也需要一个 ```timerID``` 变量.

让我们来看一下具体实现：

```js
var timerID = 0; 
function keepAlive() { 
    var timeout = 20000;  
    if (webSocket.readyState == webSocket.OPEN) {  
        webSocket.send('');  
    }  
    timerId = setTimeout(keepAlive, timeout);  
}  
function cancelKeepAlive() {  
    if (timerId) {  
        clearTimeout(timerId);  
    }  
}
```

现在我们实现了我们需要的两个方法，我们可以在 ```onOpen()``` 的最后面调用 ```keepAlive()``` ，在```onClose()``` 的组后面调用 ```cancelKeepAlive()```。

好了！我们我们完美的解决了 websocket 超时的问题。
