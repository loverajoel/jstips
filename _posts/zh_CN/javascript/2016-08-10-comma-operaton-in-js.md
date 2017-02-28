---
layout: post

title: JavaScript 的逗号操作符
tip-number: 57
tip-username: bhaskarmelkani
tip-username-profile: https://www.twitter.com/bhaskarmelkani
tip-tldr: 在一个表达式中，由左到右计算每个表达式并返回最后一个。

redirect_from:
  - /zh_cn/comma-operaton-in-js/

categories:
    - zh_CN
    - javascript
---
除了分号之外，逗号允许你在同一个地方放多个语句。
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

当放一个表达式时，它由左到右计算每个表达式，并传回最右边的表达式。

例如：

```js
function a(){console.log('a'); return 'a';}
function b(){console.log('b'); return 'b';}
function c(){console.log('c'); return 'c';}

var x = (a(), b(), c());

console.log(x);      // 输出「c」
```
输出：

```js
"a"
"b"
"c"

"c"
```

* 注意：逗号（`,`）操作符在 JavaScript 中所有的操作符里是最低的优先顺序，所以没有括号表达式将变为：`(x = a()), b(), c();`。

##### 实验
<div>
  <a class="jsbin-embed" href="http://jsbin.com/vimogap/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.11"></script>
</div>
