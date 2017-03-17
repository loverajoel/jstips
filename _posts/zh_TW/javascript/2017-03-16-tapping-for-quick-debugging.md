---
layout: post

title: 使用監聽（tap）來快速 debug
tip-number: 65
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 一個相當有用 function 用來快速 debung 一連串的 function 呼叫、匿名函式，實際上你可能只是想要列印而已。

categories:
    - zh_TW
    - javascript
---

一個相當有用 function 用來快速 debung 一連串的 function 呼叫、匿名函式，實際上你可能只是想要列印而已。

``` javascript
function tap(x) {
    console.log(x);
    return x;
}
```

為什麼你不使用 `console.log` 的老方式呢？讓我示範一個範例：

``` javascript
bank_totals_by_client(bank_info(1, banks), table)
            .filter(c => c.balance > 25000)
            .sort((c1, c2) => c1.balance <= c2.balance ? 1 : -1 )
            .map(c =>
                 console.log(`${c.id} | ${c.tax_number} (${c.name}) => ${c.balance}`));
```

現在，假設你從一連串的 function 呼叫確沒有得到任何東西（可能是一個錯誤）。
哪裡失敗了？或許是 `bank_info` 沒有回傳任何東西，所以我們將監聽它：

``` javascript
bank_totals_by_client(tap(bank_info(1, banks)), table)
```

根據我們部份的實作，它可能會列印出一些東西或者什麼都沒有。
我假設我們監聽得到的資訊是正確的，因此 bank_info 並不會產生任何結果。

我們必須移到下一個 filter function。

``` javascript
            .filter(c => tap(c).balance > 25000)
```

我們實際上有接收到任何的 client 資訊嗎？如果有，bank_totals_by_client 正常的工作。或許它是 filter 內的條件？

``` javascript
            .filter(c => tap(c.balance > 25000))
```

啊！我們沒看到其他東西，但是 `false` 被列印出來，所以沒有 client 是大於 25000，這也是為什麼 function 沒有回傳任何東西。

## 更進階的監聽

``` javascript
function tap(x, fn = x => x) {
    console.log(fn(x));
    return x;
}
```

現在我們討論一個更進階的，如果我們想要執行某個運算符*事先*到 tap（監聽）？例如，我需要存取目前 object 的屬性，執行一個邏輯運算等等。與被我們監聽的 object？然後我們呼叫 tap 和一個額外的參數，在監聽的時候應用這個 function。

``` javascript
tap(3, x => x + 2) === 3; // 列印 5，但是表達是計算為 true，為什麼 :-)？
```
