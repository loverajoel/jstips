---
layout: post

title: Get File Extension
tip-number: xx
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: How to get the file extension more efficiently?

categories:
    - en
---

### Question: How to get the file extension?

```javascript
var file1 = "50.xsl";
var file2 = "30.doc";
getFileExtension(file1); //returs xsl
getFileExtension(file2); //returs doc

function getFileExtension(filename) {
  /*TODO*/
}
```

### Solution 1: Regular Expression

```js
function getFileExtension1(filename) {
  return (/[.]/.exec(filename)) ? /[^.]+$/.exec(filename)[0] : undefined;
}
```

### Solution 2: String `split` method

```js
function getFileExtension2(filename) {
  return filename.split('.').pop();
}
```

### Solution3: String `slice`, `lastIndexOf` methods

```js
function getFileExtension3(filename) {
  return filename.slice((filename.lastIndexOf(".") - 1 >>> 0) + 2);
}

console.log(getFileExtension3(''));                         // ''
console.log(getFileExtension3('name'));                     // ''
console.log(getFileExtension3('name.txt'));                 // 'txt'   
console.log(getFileExtension3('.htpasswd'));                // ''
console.log(getFileExtension3('name.with.many.dots.myext'));// 'myext'
```

_How does it works?_

- [`String.lastIndexOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) method returns the last position of the substring (i.e. `"."`) in the given string (i.e. `filename`). If the substring is not found method returns `-1`.
- The `"unacceptable"` positions of dot in the filename are `-1` and `0`, which respectively refer to names with no extension (e.g. `"name"`) and to names that start with dot (e.g. `".htpasswd"`).
- [Zero-fill right shift operator (>>>)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E%3E_%28Zero-fill_right_shift%29) if used with zero affects negative numbers transforming `-1` to `4294967295` and `-2` to `4294967294`, which is useful for remaining the filename unchanged in the edge cases (sort of a trick here).
- [String.prototype.slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) extracts the part of the filename from the position that was calculated as described. If the position number is more than the length of the string method returns `""`.

[Here](https://jsbin.com/tipofu/edit?js,console) is the live demo of the above codes.

[Here](http://jsperf.com/extract-file-extension) is the performance test of those 3 solutions.

### Source

[How can I get file extensions with JavaScript](http://stackoverflow.com/questions/190852/how-can-i-get-file-extensions-with-javascript)

