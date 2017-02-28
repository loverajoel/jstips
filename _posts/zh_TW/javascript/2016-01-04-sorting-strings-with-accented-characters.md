---
layout: post

title: 將帶有音節字元的字串進行排序
tip-number: 04
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript 原生的 **sort** 方法讓我們可以排序陣列。做一個簡單的 `array.sort()`， 將每一個陣列元素視為字串並依字母排序。但是當你嘗試排序一個非 ASCII 字元陣列時，你會得到一個奇怪的結果。
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/sorting-strings-with-accented-characters/

categories:
    - zh_TW
    - javascript
---

JavaScript 原生的 **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)** 方法讓我們可以排序陣列。做一個簡單的 `array.sort()`， 將每一個陣列元素視為字串並依字母排序。你可以提供你的[自定義排序](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters)函式。

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

但是當你嘗試排序一個非 ASCII 字元陣列像是： `['é', 'a', 'ú', 'c']`，你會得到奇怪的結果： `['c', 'e', 'á', 'ú']`。這個問題是因為排序功能只適用於英語。

請看以下的範例：

```javascript
// 西班牙語
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // bad order

// 德文
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // bad order
```

幸運的是，有兩種方法可以解決這個問題，由 ECMAScript 國際化 API 提供的 [localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) 和 [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator)。

> 這兩種方法都有他們自己的自定義參數設置可以更有效的解決這個問題。

### 使用 `localeCompare()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(function (a, b) {
  return a.localeCompare(b);
});
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

### 使用 `Intl.Collator()`

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- 對於每一個方法，你可以自定義位置。
- 根據 [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance)，當比對大量的字串時，Intl.Collator 會更加快速。

所以，當你在處理非英文語系的字串陣列時，記得使用這個方法來避免排序出現異常。
