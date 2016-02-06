---
layout: post

title: 賦值運算符
tip-number: 35
tip-username: hsleonis
tip-username-profile: https://github.com/hsleonis
tip-tldr: 賦值是相當常見的。有時候我們這些「懶惰的開發者」覺得打字是很耗時得。所以我們使用一些技巧來幫助我們讓程式碼更乾淨簡單。

categories:
    - zh_TW
---

賦值是相當常見的。有時候我們這些「懶惰的開發者」覺得打字是很耗時得。所以我們使用一些技巧來幫助我們讓程式碼更乾淨簡單。

這是類似的方法

````javascript
x += 23; // x = x + 23;
y -= 15; // y = y - 15;
z *= 10; // z = z * 10;
k /= 7; // k = k / 7;
p %= 3; // p = p % 3;
d **= 2; // d = d ** 2;
m >>= 2; // m = m >> 2;
n <<= 2; // n = n << 2;
n ++; // n = n + 1;
n --; n = n - 1;

````

### If-else （使用三元運算符）

這是我們一般常見的寫法：

````javascript
var newValue;
if (value > 10)
  newValue = 5;
else
  newValue = 2;
````

我們可以使用三元運算符看起來更棒：

````javascript
var newValue = (value > 10) ? 5 : 2;
````

### Null、Undefined、Empty 確認

````javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     var variable2 = variable1;
}
````

簡化後：

````javascript
var variable2 = variable1  || '';
````
P.S.：假設 variable1 是數字，首先會檢查是否為 0 。

### 物件陣列表示

不是使用：

````javascript
var a = new Array();
a[0] = "myString1";
a[1] = "myString2";
````
而是這樣使用：

````javascript
var a = ["myString1", "myString2"];
````

### 關聯陣列

不是使用：

````javascript
var skillSet = new Array();
skillSet['Document language'] = 'HTML5';
skillSet['Styling language'] = 'CSS3';
````

而是這樣使用：

````javascript
var skillSet = {
    'Document language' : 'HTML5',
    'Styling language' : 'CSS3'
};
````
