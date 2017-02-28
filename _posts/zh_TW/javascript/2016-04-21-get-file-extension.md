---
layout: post

title: 取得檔案的副檔名
tip-number: 53
tip-username: richzw
tip-username-profile: https://github.com/richzw
tip-tldr: 如何更有效的取得檔案的附檔名？

redirect_from:
  - /zh_tw/get-file-extension/

categories:
    - zh_TW
    - javascript
---

### 問題：如何取得檔案的副檔名？

```javascript
var file1 = "50.xsl";
var file2 = "30.doc";
getFileExtension(file1); //returs xsl
getFileExtension(file2); //returs doc

function getFileExtension(filename) {
  /*TODO*/
}
```

### 解決方案一：正規表達式

```js
function getFileExtension1(filename) {
  return (/[.]/.exec(filename)) ? /[^.]+$/.exec(filename)[0] : undefined;
}
```

### 解決方案二：String 的 `split` 方法

```js
function getFileExtension2(filename) {
  return filename.split('.').pop();
}
```

那些兩個解決方案不能處理一些邊緣情況，這裡是另一個更好的解決方案。

### 解決方案三：String 的 `slice`、`lastIndexOf` 方法

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

_它是如何處理的呢？_

- [String.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf) 方法回傳最後一個符合指定的值（在範例中的 `'.'`）。如果找不到值則回傳 `-1`。
- 對於參數 `'filename'` 和 `'.hidden'` 的 `lastIndexOf` 的回傳值，分別為 `0` 和 `1`。[無符號右移運算子（>>>）](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E%3E_%28Zero-fill_right_shift%29) 會將 `-1` 轉換成 `4294967295` 和將 `-2` 轉換成 `4294967294`，這裡是一個小技巧來確保在邊緣情況下檔案名稱不會改變。
- [String.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) 從上面計算的索引中提取檔副檔名。如果索引超過檔案的長度，那結果會是 `""`。

### 比較

| 解決方案                                  | 參數           | 結果  |
| ----------------------------------------- |:-------------------:|:--------:|
| 解決方案一：正規表達式                    | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext' | undefined <br> undefined <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| 解決方案二：String 的 `split` 方法        | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> 'filename' <br> 'txt' <br> 'hiddenfile' <br> 'ext' <br> |
| 解決方案三：String 的 `slice`、`lastIndexOf` 方法 | ''<br>  'filename' <br> 'filename.txt' <br> '.hiddenfile' <br> 'filename.with.many.dots.ext'            | '' <br> '' <br> 'txt' <br> '' <br> 'ext' <br> |

### 實際範例和效能

[這裡](https://jsbin.com/tipofu/edit?js,console)是上方程式碼的實際範例。

[這裡](http://jsperf.com/extract-file-extension)是三個解決方案的效能測試。

### 來源

[如何使用 JavaScript 來取得檔案副檔名](http://stackoverflow.com/questions/190852/how-can-i-get-file-extensions-with-javascript)
