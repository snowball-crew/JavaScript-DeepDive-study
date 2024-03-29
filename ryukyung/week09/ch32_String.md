### ✏️ String 생성자 함수

표준 빌트인 객체인 String 객체는 생성자 함수 객체이므로 `new` 연산자와 함게 호출하여 String 인스턴스를 생성한다.

String 생성자 함수에 인수를 전달하거나 전달하지 않고 호출하면 `[[StringData]]` 내부슬롯에 빈 문자열이나 인수로 받은 문자열을 할당한 String 래퍼 객체를 생성한다. 이때 문자열이 아닌 값을 전달하면 문자열로 강제 변환 후 래퍼 객체를 생성한다.

### ✏️ length 프로퍼티

String 래퍼 객체는 배열과 마찬가지로 `length` 프로퍼티를 갖는다. 인덱스를 나타내는 숫자를 프로퍼티 키로, 각 문자를 프로퍼티 값으로 가지기 때문에 String 래퍼 객체는 **유사 배열 객체**다.

🪝 **유사 객체 배열**: 배열처럼 보이지만 사실 `key`가 숫자, `length` 값을 가지고 있는 객체

### ✏️ String 메서드

1. **String.prototype.indexOf**

   대상 문자열에서 인수로 전달받은 **문자열**을 검색하여 첫번째 인덱스를, 검색 실패 시 -1을 반환한다.

2. **String.prototype.search**

   대상 문자열에서 인수로 전달받은 **정규 표현식과 매치하는 문자열**을 검색하여 일치하면 문자열의 인덱스를, 실패하면 -1을 반환한다.

3. **String.prototype.includes**

   대상 문자열에 인수로 전달받은 문자열이 포함되어 있는지 확인 후 불리언 값으로 반환한다.

   2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

4. **String.prototype.startsWith**

   대상 문자열이 인수로 전달받은 문자열로 시작하는지 확인하여 불리언 값으로 반환한다.

   2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

5. **String.prototype.endsWith**

   대상 문자열이 인수로 전달받은 문자열로 끝나는지 확인하여 그 결과를 불리언 값으로 반환한다.

   2번째 인수로 검색할 문자열의 길이를 전달할 수 있다.

6. **String.prototype.charAt**

   대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자열을 검색하여 반환하는데 인덱스가 문자열의 범위를 벗어난 경우 빈 문자열을 반환한다.

7. **String.prototype.subString**

   대상 문자열에서 첫 번째 인수로 전달받은 인덱스가 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지의 부분 문자열을 반환한다.

   두 번째 인수는 생략할 수 있다.(첫 번째 인수부터 끝까지 반환)

   - 첫 번째 인수 > 두 번째 인수 : 인수 교체
   - 인수 < 0 | NaN : 0
   - 인수 > 문자열 길이 : 문자열의 길이로 취급

8. **String.prototype.slice**

   subString 메서드와 동일하게 동작하지만 음수인 인수를 전달할 수 있다.

   음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라내 반환한다.

9. **String.prototype.toUpperCase**

   대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.

10. **String.prototype.toLowerCase**

    대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

11. **String.prototype.trim**

    대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

12. **String.prototype.repact**

    대상 문자열을 인수로 전달받은 정수만큼 반복해 새로운 문자열을 반환한다.

    - 인수가 0 : 빈 문자열 반환
    - 인수가 음수 : RangeError 발생
    - 인수 생략 : 기본값인 0

13. **String.prototype.replace**

    대상 문자열에서 첫 번째 인수로 전달받은 문자열이나 정규표현식을 검색하여 두 번재 인수로 전달한 문자열로 치환한 문자열을 반환한다.

    - 검색된 문자열이 여러 개인 경우 첫 번째로 검색된 문자열만 치환한다.
    - 특수한 교체 패턴을 사용할 수 있다.
    - 두 번째 인수로 치환 함수를 전달할 수 있다.

14. **String.prototype.split**

    대상 문자열에서 첫 번째 인수로 전달한 문자열이나 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환한다.(두 번째 인수로 배열의 길이를 지정할 수 있다.)

    - 빈 문자열을 인수로 전달할 경우 각 문자를 모두 분리한다.
    - 인수를 생략하면 대상 문자열 전체를 단일 요소로 하는 배열을 반환한다.
