---
layout: post

title: Get File Extension
tip-number: 53
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: How to get the file extension more efficiently?

redirect_from:
  - /en/get-file-extension/

categories:
    - en
    - javascript
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

Those two solutions couldnot handle some edge cases, here is another more robust solution.

### Solution3: String `slice`, `lastIndexOf` methods

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

_How does it works?_

- [String.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) method returns the last occurrence of the specified value (`'.'` in this case). Returns `-1` if the value is not found.
- The return values of `lastIndexOf` for parameter `'filename'` and `'.hiddenfile'` are `-1` and `0` respectively. [Zero-fill right shift operator (>>>)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E%3E_%28Zero-fill_right_shift%29) will transform `-1` to `4294967295` and `-2` to `4294967294`, here is one trick to insure the filename unchanged in those edge cases.
- [String.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) extracts file extension from the index that was calculated above. If the index is more than the length of the filename, the result is `""`.

### Comparison

| Solution                                  | Paramters           | Results  |
| ----------------------------------------- |:-------------------:|:--------:|
| Solution 1: Regular Expression            | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext' | undefined <br> undefined <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| Solution 2: String `split`                | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> 'filename' <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| Solution 3: String `slice`, `lastIndexOf` | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> '' <br> 'txt' <br> '' <br> 'ext' <br> |

### Live Demo and Performance

[Here](https://jsbin.com/tipofu/edit?js,console) is the live demo of the above codes.

[Here](http://jsperf.com/extract-file-extension) is the performance test of those 3 solutions.

### Source

[How can I get file extensions with JavaScript](http://stackoverflow.com/questions/190852/how-can-i-get-file-extensions-with-javascript)
