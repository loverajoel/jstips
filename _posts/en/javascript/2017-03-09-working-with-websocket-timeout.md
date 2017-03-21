---
layout: post

title: Working With Websocket Timeout
tip-number: 63
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: A trick to control the timeout

categories:
    - en
    - javascript
---

In case of established websocket connection, server or firewall could timeout and terminate the connection after a period of inactivity. To deal with this situation, we send periodic message to the server. To control the timeout we will add two functions in our code : one to make sure connection keep alive and another one to cancel the keep alive. Also we need a common ```timerID``` variable.
Let’s have a look on implementation-

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

Now as we have both of our desired function for the task, we will place ```keepAlive()``` function at the end of ```onOpen()``` method of websocket connection and ```cancelKeepAlive()``` function at the end of ```onClose()``` method of  websocket connection. 

Yes! We have perfectly implemented hack for websocket timeout problem.
