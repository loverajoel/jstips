---
layout: post

title: 使用JSON.Stringify
tip-number: 40
tip-username: vamshisuram
tip-username-profile: https://github.com/vamshisuram
tip-tldr: 将JSON对象的参数选择性地生成字符串。


redirect_from:
  - /zh_cn/using-json-stringify/

categories:
    - zh_CN
    - javascript
---

假如有一个对象具有参数"prop1", "prop2", "prop3"。
我们可以通过传递 __附加参数__ 给 __JSON.stringify__ 来选择性地将参数生成字符串，像这样：

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

 __"str"__ 将只包含选择的参数。

除了传递数组，我们也可以传递函数。

```javascript

function selectedProperties(key, val) {
    // the first val will be the entire object, key is empty string
    if (!key) {
        return val;
    }

    if (key === 'prop1' || key === 'prop2') {
        return val;
    }

    return;
}
```

最后一个参数，可以修改生成字符串的方式。

```javascript
var str = JSON.stringify(obj, selectedProperties, '\t\t');

/* str output with double tabs in every line.
{
        "prop1": "value1",
        "prop2": "value2"
}
*/

```

