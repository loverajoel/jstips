---
layout: post

title: 过滤并排序字符串列表
tip-number: 26
tip-username: davegomez
tip-username-profile: https://github.com/davegomez
tip-tldr: 你可能有一个很多名字组成的列表，需要过滤掉重复的名字并按字母表将其排序。

redirect_from:
  - /zh_cn/filtering-and-sorting-a-list-of-strings/

categories:
    - zh_CN
    - javascript
---

你可能有一个很多名字组成的列表，需要过滤掉重复的名字并按字母表将其排序。

在我们的例子里准备用不同版本语言的**JavaScript 保留字**的列表，但是你能发现，有很多重复的关键字而且它们并没有按字母表顺序排列。所以这是一个完美的字符串列表([数组](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array))来测试我们的JavaScript小知识。

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

因为我们不想改变我们的原始列表，所以我们准备用高阶函数叫做[`filter`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)，它将基于我们传递的回调方法返回一个新的过滤后的数组。回调方法将比较当前关键字在原始列表里的索引和新列表中的索引，仅当索引匹配时将当前关键字push到新数组。

最后我们准备使用[`sort`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)方法排序过滤后的列表，`sort`只接受一个比较方法作为参数，并返回按字母表排序后的列表。

```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.lastIndexOf(keyword) === index;
    })
  .sort(function (a, b) {
      return a < b ? -1 : 1;
    });
```

在**ES6** (ECMAScript 2015)版本下使用[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)看起来更简单:

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.lastIndexOf(keyword) === index)
  .sort((a, b) => a < b ? -1 : 1);
```

这是最后过滤和排序后的JavaScript保留字列表：

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```

*感谢[@nikshulipa](https://github.com/nikshulipa)、[@kirilloid](https://twitter.com/kirilloid)、[@lesterzone](https://twitter.com/lesterzone)、[@tracker1](https://twitter.com/tracker1)、[@manuel_del_pozo](https://twitter.com/manuel_del_pozo)所有的回复与建议！*
