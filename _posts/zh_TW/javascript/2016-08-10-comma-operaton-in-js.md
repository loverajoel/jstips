---
layout: post

title: JavaScript 的逗號操作符
tip-number: 57
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 在一個表達式中，由左到右計算每個表達式並回傳最後的一個。

redirect_from:
  - /zh_tw/comma-operaton-in-js/

categories:
    - zh_TW
    - javascript
---
除了分號之外，逗號允許你在同一個地方放多個語句。
例如：

```js
for(var i=0, j=0; i<5; i++, j++, j++){
  console.log("i:"+i+", j:"+j);
}
```

輸出：

```js
i:0, j:0
i:1, j:2
i:2, j:4
i:3, j:6
i:4, j:8
```

當放置一個表達式時，它由左到右計算每個表達式，並回傳最右邊的表達式。

例如：

```js
function a(){console.log('a'); return 'a';}
function b(){console.log('b'); return 'b';}
function c(){console.log('c'); return 'c';}

var x = (a(), b(), c());

console.log(x);      // 輸出「c」
```
輸出：

```js
"a"
"b"
"c"

"c"
```

* 注意：逗號（`,`）操作符在 JavaScript 所有 的操作符是最低的優先順序，所以如果沒有括號表達式將變成：`(x = a()), b(), c();`。

##### Playground
<div>
  <a class="jsbin-embed" href="http://jsbin.com/vimogap/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
