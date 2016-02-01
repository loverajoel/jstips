---
layout: post

title: Sorting strings with accented characters(강조된 캐릭터로 문자열 정렬)
tip-number: 04
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 자바스크립트는 배열을 정렬하는 **sort**라는 함수를 내장하고있다. 간단한 `array.sort()`는 배열의 각각의 항목을 문자열로 보고 알파벳 순으로 정리한다. 하지만 ASCII가 아닌 문자에 대해서는 의도치 않은 결과를 얻을 수 있다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

자바스크립트는 배열을 정렬하는 **[sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)**라는 함수를 내장하고있다. 간단한 `array.sort()`는 배열의 각각의 항목을 문자열로 보고 알파벳 순으로 정리한다. [또한 직접 커스텀 정렬을 만들어 제공 할 수 있다.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort#Parameters)

```javascript
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```

하지만 다음과 같이 ASCII가 아닌 문자`['é', 'a', 'ú', 'c']`를 정렬하게 되면 의도치 않은 결과`['c', 'e', 'á', 'ú']`를 초래 할 수 있다. 영어를 기준으로 짜여있기 때문이다.

다음 예제를 보자:

```javascript
// Spanish
['único','árbol', 'cosas', 'fútbol'].sort();
// ["cosas", "fútbol", "árbol", "único"] // bad order

// German
['Woche', 'wöchentlich', 'wäre', 'Wann'].sort();
// ["Wann", "Woche", "wäre", "wöchentlich"] // bad order
```

다행히도 두가지 대체 방법이 있다. ECMAScript Internationalization API에서 제공한 [localeCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) 과 [Intl.Collator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator)이다.

> 두가지 방법 다 적절한 사용을 위해 각각의 커스텀 매개변수를 받는다.

### `localeCompare()` 사용하기

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

### `Intl.Collator()` 사용하기

```javascript
['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
// ["árbol", "cosas", "fútbol", "único"]

['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
// ["Wann", "wäre", "Woche", "wöchentlich"]
```

- 각각의 함수에 위치를 지정 할 수 있다.
- [Firefox](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Performance)에 의하면 Intl.Collator이 많은 양의 문자열을 비교할때 더 빠르다.

결론적으로 영어 외의 다른 언어를 비교할때에는, 의도하지 않은 결과를 피하기 위해 잊지 않고 위 함수를 사용하면 된다.