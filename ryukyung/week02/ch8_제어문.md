### ✏️ 블록문: block/compound statement

0개 이상의 문을 중괄호로 묶은 것을 코드 블록이라고 하고 자바스크립트는 블록문을 하나의 실행 단위로 취급한다. 문의 끝에는 세미콜론을 붙이는 것이 일반적이지만 블록문은 문의 종료를 의미하는 자체 종결성을 가지기 때문에 세미콜론을 붙이지 않는다.

### ✏️ 조건문

1. if … else

   if문의 조건식은 불리언 값으로 평가된다.(불리언 값이 아닌 값으로 평가될 경우 자바스크립트 엔진에 의해 암묵적으로 강제 형 변환되어 실행할 코드 블록을 결정)

   대부분의 if…else문은 삼항 연산자로 바꿔 쓸 수 있고 단순히 값을 결정하여 변수에 할당하는 경우 if…else문보다 삼항 연산자를 사용하는 편이 가독성에 좋다.

2. switch

   주어진 조건식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮기고 일치하는 case문이 없다면 default문으로 이동한다. if…else문과 다르게 switch문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.

### ✏️ 반복문

1. for

   for문의 변수 선언문, 조건식, 증감식 모두 옵션이므로 반드시 사용할 필요는 없으며 어떤 식도 선언하지 않으면 무한루프가 된다.

2. while

   while문은 반복 횟수가 불명확할 때 주로 사용하며 평가 결과가 계속해서 참이라면 무한루프가 되고 무한루프를 탈출하기 위해서는 코드 블록 내에 if문으로 탈출 조건을 넣어줘야 한다.

3. do…while

   코드 블록을 먼저 실행하고 조건식을 평가하는데 쉽게 말해서 무조건 한 번 이상 코드 블록을 실행한다.

### ✏️ break문

레이블, 반복문, switch문의 코드 블록을 탈출한다. 앞의 경우가 아니라면 SyntaxError가 발생할 수 있다.

### ✏️ continue문

반복문의 코드 블록 실행을 중단하고 반복문의 증감식으로 실행 흐름을 이동시키는데 break문처럼 반복문을 탈출하지는 않는다.
