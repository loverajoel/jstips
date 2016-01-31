---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: 자바스크립트 모듈과 빌드 과정은 더욱더 복잡해지고 다양해지고 있다. 하지만 새로운 프레임워크 안에 보일러 템플릿은?

categories:
    - ko
---
<translator: https://github.com/tisohjung>

AngularJS의 좋은 기능중 하나는 two-way data binding(양바향 데이터 바인딩)이다. AngularJS는 이 기능을 위해 사이클(`$digest`)에서 모델과 뷰의 변경을 확인한다. 프래임워크가 뒤에서 어떻게 동작하는지 알기 위해 이 개념을 이해할 필요가 있다.

Angular는 이벤트가 일어날때 각각의 watcher(감시자)을 평가한다. 이것이 `$digest`사이클 이라고 한다.
가금은 새로운 사이클을 위해 수동적으로 돌려줘야하고, 맞는 옵션들을 줘야한다. 성능적인 측면에서 많은 영향을 끼치기 때문이다.

### `$apply`
이 코어 함수는 digestion을 명시적으로 시작하게 해준다. 모든 watcher가 체크가된다; 어플리케이션 전체가 `$digest loop`를 시작한다는 뜻이다. 내부적으로 선택적 매개 변수를 실행한 뒤에 `$rootScope.$diget();`를 부른다.

### `$digest`
여기서는 `$digest` 메서드가 현재 스코프와 하위 자식들에게 `$digest`사이클을 시작한다. 부모 스코프는 확인되지 않는고 영향이 없다는 것을 볼 수있다.

### Recommendations
- `$apply` 혹은 `$digest`를 브라우저 DOM 이벤트가 AngularJS 밖에서 발생할때만 불러라.
- Function expression(함수표현)을 `$apply`로 전달해라. 오류를 처리하고, 변화를 digest 사이클에 통합 할 수 있다.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- 만일 현재 스코프와 자식들만 업데이트 해야된다면 `$digest`를 사용해서 전체 어플리케이션에 새로운 digest 사이클이 도는것을 방지해라. 성능적 차이가 확연하다.
- `$apply()`는 무거운 프로세스이고 바인딩이 많을 시에 성능 문제를 일으킬 수 있다.
- AngularJS 1.2.x 보다 높은 버젼을 사용한다면 `$evalAsync`를 사용해라, 표현식을 현재 또는 다음사이클에 평가할 코어 메서드이다. 어플리케이션 성능을 높여줄것이다.