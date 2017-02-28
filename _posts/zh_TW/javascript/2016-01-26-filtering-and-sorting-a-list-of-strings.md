---
layout: post

title: 過濾和排序字串清單
tip-number: 26
tip-username: davegomez
tip-username-profile: https://github.com/davegomez
tip-tldr: 你可能有一份很大的清單，而你需要過濾重複的內容並移除，再依字母排序。

redirect_from:
  - /zh_tw/filtering-and-sorting-a-list-of-strings/

categories:
    - zh_TW
    - javascript
---

你可能有一份很大的清單，而你需要過濾重複的內容並移除，再依字母排序。

在我們的範例，我使用了不同版本的 **JavaScript 保留字元** 的清單，但你要注意到，這裡有一些重複的字元而且他們不是依字母排序的。所以，這裡有一個相當棒的字串[陣列](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)清單來測試這個 JavaScript tip。

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

因為我們不想改變我們原有的清單，所以我們使用高階函式叫做 [`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)，它會基於我們傳送的陣列（*函式*）並回傳一個過濾後的新陣列。基於目前的清單和新的清單索引 `index` 的比較，會把和 index 相符的元素 push 到新陣列成為新的清單。

最後，我們使用 [`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) 函式來排序過濾後的結果，將比較函式當作唯一的參數，回傳依字母排序後的清單。

```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.indexOf(keyword) === index;
    })
  .sort(function (a, b) {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
});
```

使用 **ES6**（ECMAScript 2015）版本的[箭頭函式](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)看起來更簡潔：

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.indexOf(keyword) === index)
  .sort((a, b) => {
      if (a < b) return -1;
      else if (a > b) return 1;
      return 0;
    });
```

這是最後過濾以及排序後的 JavaScript 保留字元清單：

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```
