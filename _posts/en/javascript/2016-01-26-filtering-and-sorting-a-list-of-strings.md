---
layout: post

title: Filtering and Sorting a List of Strings
tip-number: 26
tip-username: davegomez
tip-username-profile: https://github.com/davegomez
tip-tldr: You may have a big list of names you need to filter in order to remove duplicates and sort them alphabetically.

credirect_from:
  - /en/filtering-and-sorting-a-list-of-strings/

categories:
    - en
    - javascript
---

You may have a big list of names you need to filter in order to remove duplicates and sort them alphabetically.

In our example we are going to use the list of **JavaScript reserved keywords** we can find across the different versions of the language, but as you can notice, there is a lot of duplicated keywords and they are not alphabetically organized. So this is a perfect list ([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)) of strings to test out this JavaScript tip.

```js
var keywords = ['do', 'if', 'in', 'for', 'new', 'try', 'var', 'case', 'else', 'enum', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'delete', 'export', 'import', 'return', 'switch', 'typeof', 'default', 'extends', 'finally', 'continue', 'debugger', 'function', 'do', 'if', 'in', 'for', 'int', 'new', 'try', 'var', 'byte', 'case', 'char', 'else', 'enum', 'goto', 'long', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'final', 'float', 'short', 'super', 'throw', 'while', 'delete', 'double', 'export', 'import', 'native', 'public', 'return', 'static', 'switch', 'throws', 'typeof', 'boolean', 'default', 'extends', 'finally', 'package', 'private', 'abstract', 'continue', 'debugger', 'function', 'volatile', 'interface', 'protected', 'transient', 'implements', 'instanceof', 'synchronized', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof', 'do', 'if', 'in', 'for', 'let', 'new', 'try', 'var', 'case', 'else', 'enum', 'eval', 'null', 'this', 'true', 'void', 'with', 'await', 'break', 'catch', 'class', 'const', 'false', 'super', 'throw', 'while', 'yield', 'delete', 'export', 'import', 'public', 'return', 'static', 'switch', 'typeof', 'default', 'extends', 'finally', 'package', 'private', 'continue', 'debugger', 'function', 'arguments', 'interface', 'protected', 'implements', 'instanceof'];
```

Since we don't want to change our original list, we are going to use a high order function named [`filter`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), which will return a new filter array based in a predicate (*function*) we pass to it. The predicate will compare the index of the current keyword in the original list with its `index` in the new list and will push it to the new array only if the indexes match.

Finally we are going to sort the filtered list using the [`sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) function which takes a comparison function as the only argument, returning a alphabetically sorted list.

```js
var filteredAndSortedKeywords = keywords
  .filter(function (keyword, index) {
      return keywords.lastIndexOf(keyword) === index;
    })
  .sort(function (a, b) {
      return a < b ? -1 : 1;
    });
```

The **ES6** (ECMAScript 2015) version using [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) looks a little simpler:

```js
const filteredAndSortedKeywords = keywords
  .filter((keyword, index) => keywords.lastIndexOf(keyword) === index)
  .sort((a, b) => a < b ? -1 : 1);
```

And this is the final filtered and sorted list of JavaScript reserved keywords:

```js
console.log(filteredAndSortedKeywords);

// ['abstract', 'arguments', 'await', 'boolean', 'break', 'byte', 'case', 'catch', 'char', 'class', 'const', 'continue', 'debugger', 'default', 'delete', 'do', 'double', 'else', 'enum', 'eval', 'export', 'extends', 'false', 'final', 'finally', 'float', 'for', 'function', 'goto', 'if', 'implements', 'import', 'in', 'instanceof', 'int', 'interface', 'let', 'long', 'native', 'new', 'null', 'package', 'private', 'protected', 'public', 'return', 'short', 'static', 'super', 'switch', 'synchronized', 'this', 'throw', 'throws', 'transient', 'true', 'try', 'typeof', 'var', 'void', 'volatile', 'while', 'with', 'yield']
```

*Thanks to [@nikshulipa](https://github.com/nikshulipa), [@kirilloid](https://twitter.com/kirilloid), [@lesterzone](https://twitter.com/lesterzone), [@tracker1](https://twitter.com/tracker1), [@manuel_del_pozo](https://twitter.com/manuel_del_pozo) for all the comments and suggestions!*
