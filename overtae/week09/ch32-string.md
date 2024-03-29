---
week: 9주차
---

# 모던 자바스크립트 Deep Dive CH32. String

## 목차

- [String 생성자 함수](#string-생성자-함수)
  - [length 프로퍼티](#length-프로퍼티)
- [String 메서드](#string-메서드)

## String 생성자 함수

표준 빌트인 객체 String은 원시 타입인 문자열을 다룰 때 유용한 프로퍼티와 메서드를 제공하며, 생성자 함수 객체다. 따라서 new 연산자와 함께 호출해 인스턴스를 생성할 수 있다.

* new 연산자 사용
  - String 생성자 함수에 인수를 전달하지 않고 호출하는 경우
    + `[[StringData]]` 내부 슬롯에 빈 문자열을 할당한 String 래퍼 객체 생성
  - String 생성자 함수에 문자열을 인수로 전달하면서 호출하는 경우
    + `[[StringData]]` 내부 슬롯에 인수로 전달받은 문자열을 할당한 String 래퍼 객체 생성
  - String 생성자 함수에 문자열이 아닌 값을 인수로 전달하면서 호출하는 경우
    + 인수를 문자열로 강제 변환한 후, `[[StringData]]` 내부 슬롯에 변환된 문자열을 할당한 String 래퍼 객체 생성
* new 연산자 사용 X
  - String 인스턴스가 아닌 문자열 반환

### length 프로퍼티

length 프로퍼티는 문자열의 문자 개수를 반환한다. String 래퍼 객체는 length 프로퍼티를 갖고, 인덱스를 나타내는 숫자를 프로퍼티 키로, 각 문자를 프로퍼티 값으로 가지므로 유사 배열 객체이면서 이터러블이다. 따라서 인덱스를 사용하여 각 문자에 접근할 수 있지만, 문자열은 원시 값이므로 변경은 불가하다.

## String 메서드

배열과 다르게 String 객체에는 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다. 즉, String 객체의 메서드는 언제나 새로운 문자열을 반환한다. 문자열은 변경 불가능한 원시 값이기 때문에 String 래퍼 객체도 **읽기 전용**<sup>read-only</sup> 객체로 제공된다. 

* `String.prototype.indexOf`
  - 대상 문자열(메서드를 호출한 문자열)에서 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환하고, 검색 실패시 -1을 반환한다.
    ```js
    const str = 'Ice Coffee';

    str.indexOf('C'); // 4
    str.indexOf('ff'); // 6
    str.indexOf('g'); // -1
    ```
  - 대상 문자열에 특정 문자열이 존재하는지 확인할 때 유용하다.
    ```js
    // 문자열에 'Coffee'가 포함되어 있는지 확인하는 경우
    if (str.indexOf('Coffee') !== -1) { ... }
    // ES6에서 도입된 String.prototype.includes 메서드를 사용하면 가독성이 더 좋다.
    if (str.includes('Coffee')) { ... }
    ```
* `String.prototype.search`
  - 대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열의 인덱스를 반환하고, 검색 실패시 -1을 반환한다.
    ```js
    const str = 'Ice Coffee';
    
    str.search(/c/); // 1
    ```
* `String.prototype.includes` (ES6)
  - 대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인하여 그 결과를 불리언 값으로 반환한다.
  - 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
* `String.prototype.startsWith` (ES6)
  - 대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 그 결과를 불리언 값으로 반환한다.
  - 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
* `String.prototype.endsWith` (ES6)
  - 대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 불리언 값으로 반환한다.
  - 2번째 인수로 검색할 문자열의 길이를 전달할 수 있다.
* `String.prototype.charAt`
  - 대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.
  - 인덱스가 문자열의 범위를 벗어난 경우 빈 문자열(`''`)을 반환한다.
  - `String.prototype.charCodeAt`, `String.prototype.codePointAt`과 유사하다.
* `String.prototype.substring`
  - 대상 문자열에서 첫 번재 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.
  - 두 번째 인수는 생략이 가능하며, 생략한 경우 첫 번째 인수로 전달한 인덱스에 위치하는 문자부터 마지막 문자까지의 부분 문자열을 반환한다.
  - 첫 번째 인수는 두 번째 인수보다 작은 정수여야 정상이지만, 아래와 같은 경우에도 정상 동작한다.
    + 첫번째 인수 > 두 번째 인수: 두 인수 교환
    + 인수 < 0(음수) 또는 NaN: 0으로 취급
    + 인수 > 문자열의 길이: 문자열의 길이로 취급
* `String.prototype.slice`
  - substring 메서드와 동일하게 동작하지만 음수인 인수를 전달할 수 있다.
  - 음수인 인수를 전달할 경우 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내 반환한다.
* `String.prototype.toUpperCase`
  - 대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.
* `String.prototype.toLowerCase`
  - 대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.
* `String.prototype.trim`
  - 대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.
  - 공백 문자 제거시, replace 메서드에 정규 표현식을 인수로 전달하는 방법도 있다.
* `String.prototype.repeat` (ES6)
  - 대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환한다.
    + 인수가 0인 경우: 빈 문자열 반환
    + 인수가 음수인 경우: RangeError 발생
    + 인수를 생략한 경우: 기본값 0, 빈 문자열 반환
* `String.prototype.replace`
  - 대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규 표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환한다.
  - 검색 결과가 여러개인 경우 첫 번째로 검색된 문자열만 치환한다.
  - 특수한 교체 패턴을 사용할 수 있다. — [참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/replace#%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98%EA%B0%80_string%EC%9C%BC%EB%A1%9C_%EC%A7%80%EC%A0%95%EB%90%98%EC%97%88%EC%9D%84_%EB%95%8C)
  - 두 번째 인수로 치환 함수를 전달할 수 있다. 
    > 첫 번째 인수로 전달한 문자열(또는 정규 표현식에 매치한 결과)을 두 번째 인수로 전달한 치환 함수의 인수로 전달하면서 호출하고, 치환 함수가 반환한 결과와 매치 결화를 치환한다.
* `String.prototype.split`
  - 대상 문자열에서 첫 번째 인수로 전달한 문자열 또는 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.
    + 빈 문자열을 인수로 전달한 경우: 각 문자를 모두 분리
    + 인수를 생략한 경우: 대상 문자열 전체를 단일 요소로 하는 배열을 반환
  - 두 번째 인수로 배열의 길이를 지정할 수 있다.
