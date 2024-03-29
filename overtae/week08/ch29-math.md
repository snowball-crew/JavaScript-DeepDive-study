---
week: 8주차
---

# 모던 자바스크립트 Deep Dive CH29. Math

## 목차

- [표준 빌트인 객체 Math](#표준-빌트인-객체-math)
- [Math 프로퍼티](#math-프로퍼티)
- [Math 메서드](#math-메서드)

## 표준 빌트인 객체 Math

Math는 수학적인 상수와 함수를 위한 프로퍼티와 메서드를 제공한다. Math는 생성자 함수가 아니기 때문에, 정적 프로퍼티와 정적 메서드만 제공한다.

## Math 프로퍼티

* `Math.PI`: 원주율 PI값(`π ≈ 3.141592653589793`)을 반환한다.

## Math 메서드

* `Math.abs`: 인수로 전달된 숫자의 절대값을 반환
* `Math.round`: 인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환
* `Math.ceil`: 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환
* `Math.floor`: 인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환
* `Math.sqrt`: 인수로 전달된 숫자의 제곱근을 반환
* `Math.random`: 임의의 난수를 반환(0에서 1미만의 실수)
* `Math.pow`: 첫 번째 인수를 밑으로, 두 번째 인수를 지수로 거듭제곱한 결과를 반환
  > ES7에서 도입된 지수 연산자를 사용하면 가독성이 더 좋다.
  > ```js
  > Math.pow(Math.pow(2, 2), 2); // 16
  > 2 ** 2 ** 2; // 16
  > ```
* `Math.max`: 전달받은 인수 중 가장 큰 수를 반환 (인수가 전달되지 않은 경우 `-Infinity`를 반환)
* `Math.min`: 전달받은 인수 중 가장 작은 수를 반환 (인수가 전달되지 않은 경우 `Infinity`를 반환)

> ⭐ **배열 요소 중 최대값/최소값 구하기**
>
> `Function.prototype.apply` 메서드 또는 스프레드 문법 사용
> 
>   ```js
>   // apply 메서드
>   Math.max.apply(null, [1, 2, 3]);
>   Math.min.apply(null, [1, 2, 3]);
> 
>   // 스프레드 문법 (ES6)
>   Math.max(...[1, 2, 3]);
>   Math.min(...[1, 2, 3]);
>   ```
