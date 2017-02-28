---
layout: post

title: 使用 JSON.Stringify
tip-number: 40
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: 從 JSON 物件中，將被選到的屬性建立成字串。


redirect_from:
  - /zh_tw/using-json-stringify/

categories:
    - zh_TW
    - javascript
---

假設有一個物件有「prop1」、「prop2」、「prop3」屬性。
我們傳送__額外的參數__到 __JSON.stringify__ 將物件的屬性變成字串，像是：

```javascript
var obj = {
    'prop1': 'value1',
    'prop2': 'value2',
    'prop3': 'value3'
};

var selectedProperties = ['prop1', 'prop2'];

var str = JSON.stringify(obj, selectedProperties);

// str
// {"prop1":"value1","prop2":"value2"}

```

__"str"__ 只包含被選擇到的屬性的資訊。

除了傳送陣列，我們也可以傳送函式。

```javascript

function selectedProperties(key, val) {
    // 第一個數值是整個物件，key 是空的字串
    if (!key) {
        return val;
    }

    if (key === 'prop1' || key === 'prop2') {
        return val;
    }

    return;
}
```

最後一個可選參數式是修改物件寫入字串的方式。

```javascript
var str = JSON.stringify(obj, selectedProperties, '\t\t');

/* str 每個輸出會有 doube tabs。
{
        "prop1": "value1",
        "prop2": "value2"
}
*/

```
