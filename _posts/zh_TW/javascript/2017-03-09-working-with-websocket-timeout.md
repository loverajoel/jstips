---
layout: post

title: 處理 Websocket 超時
tip-number: 63
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 一個控制 timeout 的技巧

categories:
    - zh_TW
    - javascript
---

在 websocket 連接被建立的情況下，如果一段時間處於非活動狀態，伺服器或防火牆可能超時或終止連接。為了要處理這個情況，我們向伺服器週期性的傳送訊息。為了控制超時，我們將新增兩個 function 再我們的程式碼：一是確認連接持久連線（keep alive)，另一個則是取消持久連線。我們也還需要一個共同的 `timerID` 變數。
讓我們來實作看看：

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
        cancelTimeout(timerId);  
    }  
}
```

現在我們在 task 有兩個我們需要的 function，我們將放置 ```keepAlive()``` function 在 ```onOpen()``` 方法的 websocket 連接之後以及 ```cancelKeepAlive()``` function 在 ```onClose()``` 方法的 websocket 連接後面。

沒錯！我們完美實作了 websocket 超時問題的方法。
