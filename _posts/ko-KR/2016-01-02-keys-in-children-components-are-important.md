---
layout: post

title: 자식 컴포넌트의 Key는 중요하다
tip-number: 02
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: key는 배열에서 동적으로 생성된 모든 컴포넌트에 전달해야할 속성이다. React가 DOM안에 각각의 컴포넌트를 구별하고 같거나 다른 컴포넌트인지 비교하기 위해 사용하는 유니크하고 상수인 id 이다. key는 자식 컴포넌트가 보호되고 다시 만들어지지 않고, 그리고 이상한 일이 일어나지 않게 보장해준다.

categories:
    - ko
---
<translator: https://github.com/tisohjung>

[key](https://facebook.github.io/react/docs/multiple-components.html#dynamic-children)는 배열에서 동적으로 생성된 모든 컴포넌트에 전달해야할 속성이다. React가 DOM안에 각각의 컴포넌트를 구별하고 같거나 다른 컴포넌트인지 비교하기 위해 사용하는 유니크하고 상수인 id 이다. key는 자식 컴포넌트가 보호되고 다시 만들어지지 않고, 그리고 이상한 일이 일어나지 않게 보장해준다.

> Key는 성능에 대한 문제가 아니다, 아이덴티티(정체)의 문제이다 (결국에는 성능에 긍정적인 영향을 끼친다). 무작위로 할당되고 변화되는 값들은 아이덴티티를 가지지 않는다 - [Paul O’Shannessy](https://github.com/facebook/react/issues/1342#issuecomment-39230939)

- 이미 존재하는 객체의 유니크 값을 사용해라.
- Key를 부모 컴포넌트에서 정의해라, 자식에서 하지말것.

```javascript
//bad
...
render() {
	<div key={{item.key}}>{{item.name}}</div>
}
...

//good
<MyComponent key={{item.key}}/>
```
- [배열 인덱스를 사용하는건 안좋은 연습이다.](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318#.76co046o9)
- `random()` 은 안된다.

```javascript
//bad
<MyComponent key={{Math.random()}}/>
```

- 직접 유니크 id 를 생성 할 수 있다. 빠른 메서드로 만들고 객체에 연결시켜라.
- 자식의 숫자가 많거나 복잡한 컴포넌트라면, key를 사용해서 성능을 높여라.
- [ReactCSSTransitionGroup 의 모든 자식에는 키값을 지정해주어야 한다.](http://docs.reactjs-china.com/react/docs/animation.html)