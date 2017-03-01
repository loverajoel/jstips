---
layout: post

title: 取得文件扩展名
tip-number: 53
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: 如何更加高效的取得文件扩展名呢？

redirect_from:
  - /zh_cn/get-file-extension/

categories:
    - zh_CN
    - javascript
---

### 问题 1: 怎样取得文件扩展名?

```javascript
var file1 = "50.xsl";
var file2 = "30.doc";
getFileExtension(file1); //returs xsl
getFileExtension(file2); //returs doc

function getFileExtension(filename) {
  /*TODO*/
}
```

### 解决方法 1: 正则表达式

```js
function getFileExtension1(filename) {
  return (/[.]/.exec(filename)) ? /[^.]+$/.exec(filename)[0] : undefined;
}
```

### 解决方法 2: String的`split`方法

```js
function getFileExtension2(filename) {
  return filename.split('.').pop();
}
```

这两种解决方法不能解决一些边缘情况，这有另一个更加强大的解决方法。

### 解决方法 3: String的`slice`、`lastIndexOf`方法

```js
function getFileExtension3(filename) {
  return filename.slice((filename.lastIndexOf(".") - 1 >>> 0) + 2);
}

console.log(getFileExtension3(''));                            // ''
console.log(getFileExtension3('filename'));                    // ''
console.log(getFileExtension3('filename.txt'));                // 'txt'
console.log(getFileExtension3('.hiddenfile'));                 // ''
console.log(getFileExtension3('filename.with.many.dots.ext')); // 'ext'
```

_这是如何实现的呢?_

- [String.lastIndexOf()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) 方法返回指定值（本例中的`'.'`）在调用该方法的字符串中最后出现的位置，如果没找到则返回 -1。
- 对于`'filename'`和`'.hiddenfile'`，`lastIndexOf`的返回值分别为`0`和`-1`[无符号右移操作符(>>>)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E%3E_%28Zero-fill_right_shift%29) 将`-1`转换为`4294967295`，将`-2`转换为`4294967294`，这个方法可以保证边缘情况时文件名不变。
- [String.prototype.slice()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/slice) 从上面计算的索引处提取文件的扩展名。如果索引比文件名的长度大，结果为`""`。

### 对比

| 解决方法                                  | 参数           | 结果  |
| ----------------------------------------- |:-------------------:|:--------:|
| 解决方法 1: Regular Expression            | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext' | undefined <br> undefined <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| 解决方法 2: String `split`                | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> 'filename' <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| 解决方法 3: String `slice`, `lastIndexOf` | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> '' <br> 'txt' <br> '' <br> 'ext' <br> |

### 实例与性能

[这里](https://jsbin.com/tipofu/edit?js,console) 是上面解决方法的实例。

[这里](http://jsperf.com/extract-file-extension) 是上面三种解决方法的性能测试。

### 来源

[How can I get file extensions with JavaScript](http://stackoverflow.com/questions/190852/how-can-i-get-file-extensions-with-javascript)
