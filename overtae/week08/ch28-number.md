---
week: 8주차
---

# 모던 자바스크립트 Deep Dive CH28. Number

## 목차

- [Number 생성자 함수](#number-생성자-함수)
- [Number 프로퍼티](#number-프로퍼티)
  - [Number.EPSILON (ES6)](#numberepsilon-es6)
  - [Number.MAX\_VALUE](#numbermax_value)
  - [Number.MIN\_VALUE](#numbermin_value)
  - [Number.MAX\_SAFE\_INTEGER](#numbermax_safe_integer)
  - [Number.MIN\_SAFE\_INTEGER](#numbermin_safe_integer)
  - [Number.POSITIVE\_INFINITY](#numberpositive_infinity)
  - [Number.NEGATIVE\_INFINITY](#numbernegative_infinity)
  - [Number.NaN](#numbernan)
- [Number 메서드](#number-메서드)
  - [Number.isFinite (ES6)](#numberisfinite-es6)
  - [Number.isInteger (ES6)](#numberisinteger-es6)
  - [Number.isNaN (ES6)](#numberisnan-es6)
  - [Number.isSafeInteger (ES6)](#numberissafeinteger-es6)
  - [Number.prototype.toExponential](#numberprototypetoexponential)
  - [Number.prototype.toFixed](#numberprototypetofixed)
  - [Number.prototype.toPrecision](#numberprototypetoprecision)
  - [Number.prototype.toString](#numberprototypetostring)

## Number 생성자 함수

표준 빌트인 객체 Number는 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다.

Number 객체는 생성자 함수 객체로, `new` 연산자와 함께 호출하여 Number 인스턴스를 생성할 수 있다.

* 인수를 전달하지 않은 경우
  - `[[NumberData]]` 내부 슬롯에 0을 할당한 Number 래퍼 객체 생성
* 인수로 숫자를 전달한 경우
  - `[[NumberData]]` 내부 슬롯에 인수로 전달받은 숫자를 할당한 Number 래퍼 객체 생성
* 인수로 숫자가 아닌 값을 전달한 경우
  - 인수를 숫자로 강제 변환한 후, `[[NumberData]]` 내부 슬롯에 변환된 숫자를 할당한 Number 래퍼 객체 생성 (변환할 수 없다면 `NaN`을 할당)

`new` 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 숫자를 반환한다. 이를 이용해 명시적으로 타입을 변환할 수 있다.

## Number 프로퍼티

### Number.EPSILON (ES6)

1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다. 약 <code>2.2204460492503130808472633361816 * 10<sup>-16</sup></code>이다. 

부동소수점 산술 연산은 정확한 결과를 기대하기 어려운데, `Number.EPSILON`은 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.

```js
function isEqual(a, b){
  // a와 b를 뺀 값의 절대값이 Number.EPSILON보다 작으면 같은 수로 인정
  return Math.abs(a - b) < Number.EPSILON;
}

isEqual(0.1 + 0.2, 0.3); // true
```

### Number.MAX_VALUE

자바스크립트에서 표현할 수 있는 가장 큰 양수 값(<code>1.7976931348623157 * 10<sup>308</sup></code>)이다. `Number.MAX_VALUE`보다 큰 숫자는 `Infinity`다.

### Number.MIN_VALUE

자바스크립트에서 표현할 수 있는 가장 작은 양수 값(<code>5 * 10<sup>-324</sup></code>)이다. `Number.MIN_VALUE`보다 작은 숫자는 0이다.

### Number.MAX_SAFE_INTEGER

자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값(9007199254740991)이다.

### Number.MIN_SAFE_INTEGER

자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값(-9007199254740991)이다.

### Number.POSITIVE_INFINITY

양의 무한대를 나타내는 숫자값 `Infinity`와 같다.

### Number.NEGATIVE_INFINITY

음의 무한대를 나타내는 숫자값 `-Infinity`와 같다.

### Number.NaN

숫자가 아님(Not-a-Number)을 나타내는 숫자값으로, `window.NaN`과 같다.

## Number 메서드

### Number.isFinite (ES6)

인수로 전달된 숫자값이 정상적인 유한수(`Infinity` 또는 `-Infinity`가 아닌)인지 검사하여 결과를 불리언 값으로 반환한다. 만약 인수가 `NaN`이면 언제나 `false`를 반환한다.

> ⭐ **`Number.isFinite` vs. 빌트인 전역 함수 `isFinite`**
>
> * 빌트인 전역 함수 `isFinite`: 전달 받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행
> * `Number.isFinite`: 전달 받은 인수를 숫자로 암묵적 타입 변환하지 않음(숫자가 아닌 인수가 주어지면 언제나 `false` 반환)

### Number.isInteger (ES6)

인수로 전달된 숫자값이 정수인지 검사하여 결과를 불리언 값으로 반환한다. 검사 전, 인수를 숫자로 암묵적 타입 변환하지 않는다.

### Number.isNaN (ES6)

인수로 전달된 숫자값이 NaN인지 검사하여 결과를 불리언 값으로 반환한다.

> ⭐ **`Number.isNaN` vs. 빌트인 전역 함수 `isNaN`**
>
> * 빌트인 전역 함수 `isNaN`: 전달받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행
> * `Number.isNaN`: 전달 받은 인수를 숫자로 암묵적 타입 변환하지 않음(숫자가 아닌 인수가 주어지면 언제나 `false` 반환)

### Number.isSafeInteger (ES6)

인수로 전달된 숫자값이 안전한 정수인지 검사하여 결과를 불리언 값으로 반환한다. 검사 전, 인수를 숫자로 암묵적 타입 변환하지 않는다.

> 💭 안전한 정수값?
> 
> — *-(253 - 1)과 253 - 1 사이의 정수값*

### Number.prototype.toExponential

숫자를 지수 표기법으로 변환하여 문자열로 반환한다.

> 💭 지수 표기법?
> 
> — *매우 크거나 작은 숫자를 표기할 때 주로 사용하며 e(Exponent) 앞에 있는 숫자에 10의 n승을 곱하는 형식으로 수를 나타내는 방식*

```js
(12.34567).toExponential(); // 1.234567e+1
(12.34567).toExponential(2); // 1.23e+1
```

### Number.prototype.toFixed

숫자를 반올림하여 문자열로 반환한다. 반올림하는 소수점 이하 자릿수를 나타내는 0~20사이의 정수값을 인수로 전달할 수 있으며, 생략할 경우 기본값은 0이다.

### Number.prototype.toPrecision

인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다. 전체 자릿수를 나타내는 0~21 사이의 정수값을 인수로 전달할 수 있으며, 생략할 경우 기본값은 0이다.

인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.

```js
// 전체 자릿수 유효 (기본값 0)
(123.456).toPrecision(); // 123.456
// 전체 4자릿수 유효, 나머지 반올림
(123.456).toPrecision(4); // 123.5
```

### Number.prototype.toString

숫자를 문자열로 변환하여 반환한다. 진법을 나타내는 2~36 사이의 정수값을 인수로 전달할 수 있으며, 생략할 경우 기본값은 10진법이다.
