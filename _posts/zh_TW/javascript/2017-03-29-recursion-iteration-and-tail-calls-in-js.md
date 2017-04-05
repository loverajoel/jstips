---
layout: post

title: 在 JavaScript 遞歸、反覆運算並尾呼叫
tip-number: 67
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: 如果你已經有一段實務經驗了，你最有可能會遇到遞迴，給定一個數字來定義階乘（factorial），`n! = n * n - 1 * ... * 1` 就是一個標準的例子...
tip-md-link: https://github.com/loverajoel/jstips/blob/master/_posts/en/javascript/2017-03-29-recursion-iteration-and-tail-calls-in-js.md

categories:
    - zh_TW
    - javascript
---

如果你已經有一段實務經驗了，你最有可能會遇到遞迴，給定一個數字來定義階乘（factorial），`n! = n * n - 1 * ... * 1` 就是一個標準的例子...

``` javascript
function factorial(n) {
    if (n === 0) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

上面的範例是最常見的階乘 function。

為了更完整理解，讓我們來看 `n = 6` 是如何執行的：

- factorial(6)
  - 6 * factorial(5)
    - 5 * factorial (4)
      - 4 * factorial(3)
        - 3 * factorial(2)
          - 2 * factorial(1)
            - 1 * factorial(0)
              - 1
            - （恢復先前的執行） 1 * 1 = 1
          - （恢復...） 2 * 1 = 2
        - (...) 3 * 2 = 6
      - ... 4 * 6 = 24
    - 5 * 24 = 120
  - 6 * 120 = 720
- factorial(6) = 120

現在，我們必須非常謹慎的知道發生了什麼事，我們會在下個部分理解到。

當我們在調用一個 function 時，會發生許多事。根據目前的資訊（例如： n 的值），我們在呼叫下一個 function 時必須儲存目前位置。然後空間被分配到新的 function 並產生一個新的 frame。

它仍然繼續執行，我們一直堆積這些 frame 然後並放開，透過它們取代 function 呼叫和被回傳的值。

另一件要注意的事情是，透過我們的 function 處理所產生的 shape。
如果我呼叫這些*遞歸*的 shape 你應該不會很驚訝。因為我們有一個*遞歸的過程*。

讓我們看一下第二種方式實作的 function：

``` javascript
function factorial(n, res) {
    if (n === 0) {
        return res;
    }
    return factorial(n - 1, res * n);
}
```

我們可以透過定義一個內建 function 更進一步封裝功能。

``` javascript
function factorial(n) {
    function inner_factorial(n, res) {
        if (n === 0) {
            return res;
        }
        return inner_factorial(n - 1, res * n);
    }
    return inner_factorial(n, 1);
}
```

讓我們看一下它是如何執行的：

- factorial(6)
  - 內部匿名 function（iaf）和（n = 6, res = 1）被呼叫
    - iaf(5, 1 * 6)
      - iaf(4, 6 * 5)
        - iaf(3, 30 * 4)
          - iaf(2, 120 * 3)
            - iaf(1, 360 * 2)
              - iaf(0, 720)
                - 720
              - 720
            - 720
          - 720
        - 720
      - 720
    - 720
  - iaf (6, 1) = 720
- factorial(6) = 720

你可能會注意到，我們不需要在回傳 stack 時執行任何計算。我們只是回傳值。但是根據我們的規則，我們儲存 state 最為一個 stack frame，即使它在這個中 chain 最後沒有被任何的使用。

然而根據規則，不適用於每一個語言。事實上，在 Schema 中，對於這樣的 chain 是必須優化的，在尾呼叫時被優化。這是確保我們的 stack 不會有不必要的 frame。
因此，我們在先前的計算會看到這種方式︰

- factorial(6)
- iaf(6, 1)
- iaf(5, 6)
- iaf(4, 30)
- iaf(3, 120)
- iaf(2, 360)
- iaf(1, 720)
- iaf(0, 720)
- 720

事實上，看起來實在很像：

``` javascript
res = 1;
n = 6;

while(n > 1) {
    res = res * n;
    n--;
}
```

意思是，我們確實有一個*反覆運算的處理*，即使我們使用遞歸。這是多麽酷啊？

好消息是，這是 ES6 的 feature。只要你在尾部遞歸呼叫而且你的 function 是 strict 模式，尾呼叫優化將從 `超過 stack 最大的大小` 踢除錯誤並儲存。
