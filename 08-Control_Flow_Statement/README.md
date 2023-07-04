제어문(control flow statement)은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다.  
일반적으로 코드는 `위 → 아래` 방향으로 순차적으로 실행된다. 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어할 수 있다.

제어문의 종류는 다음과 같다.

- 블록문(block statement/compound statement)
- 조건문(conditional statement)
  - if...else문
  - switch문
- 반복문(loop statement)
  - for문
  - while문
  - do...while문
  - break문
  - continue문

### if...else문 vs. switch문

if...else문의 조건식은 불리언 값으로 평가되어야 하지만 switch문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.  
다시 말해, if..else 문은 `논리적 참, 거짓`으로 실행할 코드 블록을 결정한다.

switch문은 논리적 참, 거짓보다는 `다양한 상황(case)`에 따라 실행할 코드 블록을 결정할 때 사용한다.
