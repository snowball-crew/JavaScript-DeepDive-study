---
week: 4주차
---

# 모던 자바스크립트 Deep Dive CH15. let, const 키워드와 블록 레벨 스코프

## 목차

- [var 키워드로 선언한 변수의 문제점](#var-키워드로-선언한-변수의-문제점)
  - [1. 변수 중복 선언 허용](#1-변수-중복-선언-허용)
  - [2. 함수 레벨 스코프](#2-함수-레벨-스코프)
  - [3. 변수 호이스팅](#3-변수-호이스팅)
- [let 키워드](#let-키워드)
  - [1. 변수 중복 선언 금지](#1-변수-중복-선언-금지)
  - [2. 블록 레벨 스코프](#2-블록-레벨-스코프)
  - [3. 변수 호이스팅](#3-변수-호이스팅-1)
- [const 키워드](#const-키워드)
  - [1. 선언과 초기화](#1-선언과-초기화)
  - [2. 재할당 금지](#2-재할당-금지)
  - [3. 상수](#3-상수)
  - [객체](#객체)
- [var vs. let vs. const](#var-vs-let-vs-const)

## var 키워드로 선언한 변수의 문제점

### 1. 변수 중복 선언 허용

`var` 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.

```js
var x = 2;
var y = 5;

// a. 초기화 문이 있는 경우
// var 키워드가 없는 것처럼 동작, x = 3;
var x = 3;
// b. 초기화 문이 없는 경우
// 무시됨, 에러 X
var y;
```

### 2. 함수 레벨 스코프

`var` 키워드로 선언한 변수는 **함수의 코드 블록만을 지역 스코프로 인정**한다. `for`문이나 `if`문에서 선언한 변수는 전역 변수가 된다.

### 3. 변수 호이스팅

변수 호이스팅에 의해 `var` 키워드로 선언한 변수는 변수 선언문 이전에 참조할 수 있다. 

## let 키워드

`var` 키워드의 단점을 보완하기 위해 ES6에서는 `let`과 `const`를 도입했다.

### 1. 변수 중복 선언 금지

`let` 키워드로 변수 중복 선언시 문법 에러가 발생한다.

### 2. 블록 레벨 스코프

`let` 키워드로 선언한 변수는 모든 코드 블록(함수, if문, for문 등)을 지역 스코프로 인정한다.

### 3. 변수 호이스팅

`let` 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작한다. `let` 키워드로 선언한 변수는 선언 단계와 초기화 단계가 분리되어 진행되기 때문에 변수 선언문 이전에 변수를 참조하면 참조 에러가 발생한다. 스코프의 시작 지점부터 초기화 단계 시작 지점(변수 서언문)까지 변수를 참조할 수 없는데, 이 구간을 **일시적 사각지대**<sup>Temporal Dead Zone, TDZ</sup>라 한다.

```js
let x = 2; // 전역 변수

{
  // 지역 변수 x가 호이스팅되어 전역 변수 값 출력 대신 참조 에러 발생
  console.log(x); // 참조 에러
  let x = 1; // 지역 변수
}
```

## const 키워드

`const` 키워드는 상수를 선언하기 위해 사용하며 `let` 키워드와 대부분 동일한 특징을 갖는다.

### 1. 선언과 초기화

`const` 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다.

### 2. 재할당 금지

`const` 키워드로 선언한 변수는 재할당이 금지된다.

### 3. 상수

상수는 재할당이 금지된 변수를 말하며, 상태 유지와 가독성, 유지보수의 편의성을 위해 사용을 권장한다.

일반적으로 상수의 이름은 대문자로 선언하고, 여러 단어일 경우 언더스코어로 구분한 스네이크 케이스로 표현한다.

### 객체

`const` 키워드로 선언된 변수에 원시값을 할당한 경우 값을 변경할 수 없지만, 객체를 할당한 경우에는 가능하다. 원시값은 재할당 없이는 변경할 수 없지만, 객체는 재할당 없이도 변경이 가능하기 때문이다. 이때 객체가 변경되더라도 변수에 할당된 참조 값은 변하지 않는다.

따라서 `const` 키워드는 재할당을 금지할 뿐이지 불변을 의미하는 것은 아니다.

## var vs. let vs. const

|       `var`       |        `let`         |                 `const`                 |
| :---------------: | :------------------: | :-------------------------------------: |
| ES6 사용시 사용 X | 재할당이 필요한 경우 | 기본 변수 선언(재할당이 필요 없는 상수) |