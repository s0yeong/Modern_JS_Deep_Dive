## 함수란?

**프로그래밍 언어의 함수: 일련의 과정을 문으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것.**

- 매개변수(parameter): 함수 내부로 입력을 전달받는 변수
- 인수(argument): 입력
- 반환값(return value): 출력

함수는 `함수 정의(function definition)`를 통해 생성한다. 그리고 인수(argument)를 매개변수를 통해 함수에 전달하면서 함수의 실행을 명시적으로 지시한다. 이를 `함수 호출(function call/invoke)`이라 한다.

함수를 호출하면 코드 블록에 담긴 문들이 일괄적으로 실행되고, 실행 결과 즉, 반환값을 반환한다.

```
함수는 몇 번이든 홈출할 수 있으므로 "코드의 재사용"이라는 측면에서 매우 유용하다.
코드의 중복을 억제하고 재사용성을 높이는 함수는 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높이는 효과가 있다.
```

## 함수 리터럴

함수 리터럴은 function 키워드, 함수 이름, 매개 변수 목록, 함수 몸체로 구성된다.

| 구성 요소     | 설명                                                                                                                                                                                                                                                                                                        |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 함수 이름     | • 함수 이름은 식별자다. 따라서 식별자 네이밍 규칙을 준수해야 한다.<br>• 함수 이름은 함수 몸체 내에서만 참조할 수 있는 식별자다. <br>• 함수 이름은 생략할 수 있다. 이름이 있는 함수를 기명 함수, 이름이 없는 함수를 무명/익명 함수라 한다.                                                                   |
| 매개변수 목록 | • 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분한다.<br>• 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당된다. 즉, 매개변수 목록은 순서에 의미가 있다. <br>• 매개변수는 함수 몸체 내에서 변수와 동일하게 취급된다. 따라서 매개변수도 변수와 마찬가지로 식별자 네이밍 규칙을 준수해야 한다. |
| 함수 몸체     | • 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행 단위로 정의한 코드 블록이다. <br>• 함수 몸체는 함수 호출에 의해 실행된다.                                                                                                                                                                       |

- 함수는 객체지만 일반 객체와 다르다.
  - 일반 객체는 호출할 수x, 함수는 호출할 수o
  - 일반 객체에는 없는 함수 객체만의 고유한 프로퍼티를 갖는다.

## 함수 정의

함수 정의란 함수를 호출하기 이전에 인수를 전달받을 매개변수와 실행할 문들, 그리고 반환할 값을 지정하는 것을 말한다.

### 함수 선언문

- 함수 선언문은 함수 리터럴과 달리 함수 이름을 생략할 수 없다.
- 함수 선언문은 "표현식이 아닌 문"이다.

```javascript
// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 참조
console.log(add); // → f add(x, y)
// 함수 호출
console.log(add(3, 2)); // → 5
```

```
자바스크립트 엔진은 함수 이름이 있는 함수 리터럴을 단독으로 사용(함수 리터럴을 피연산자로 사용x)하면 함수 선언문으로 해석하고, 함수 리터럴이 값으로 평가되어야 하는 문맥이면 함수 리터럴 표현식으로 해석한다.
```

자바스크립트 엔진은 함수 선언문을 해석해 함수 객체를 생성한다.  
다시 말해, 자바스크립트 엔진은 생성된 함수를 호출하기 위해 **함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고, 거기에 함수 객체를 할당**한다.

### 함수 표현식

자바스크립트의 함수는 일급 객체다.

- 일급 객체: 값의 성질을 갖는 객체
- 함수 표현식은 "표현식인 문"이다.
  > 함수가 일급 객체라는 것은 함수를 값처럼 자유롭게 사용할 수 있다는 의미다.

```javascript
// 함수 표현식
var add = function (x, y) {
  return x + y;
};

console.log(add(2, 5)); // → 7

// 함수 이름은 함수 몸체 내부에서만 유효한 식별자다. ⇒ 함수 이름으로 호출하면 ReferenceError 발생.
console.log(foo(2, 5)); // → ReferenceError: foo is not defined
```

함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다.

#### 함수 생성 시점과 함수 호이스팅

```javascript
// 함수 참조
console.dir(add); // → f add(x,y)
console.dir(sub); // → undefined

// 함수 호출
console.log(add(2, 5)); // → 7
console.log(sub(2, 5)); // TypeError: sub is not a function

// 함수 선언문
function add(x, y) {
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x - y;
};
```

위 예제와 같이 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있다. 그러나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없다.  
이는 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문이다.

`함수 호이스팅(function hoisting)`: 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징

```
함수 선언문을 통해 암묵적으로 생성된 식별자는 함수 객체로 초기화된다.

따라서 var 키워드를 사용한 변수 선언문 이전에 변수를 참조하면 변수 호이스팅에 의해 undefined로 평가되지만 함수 선언문으로 정의한 함수를 함수 선언문 이전에 호출하면 함수 호이스팅에 의해 호출이 가능하다.
```

변수 선언은 런타임 이전에 실행되어 undefined로 초기화되지만 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 된다.

> 따라서 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.

### 화살표 함수(arrow function)

ES6에서 도입된 화살표 함수는 function 키워드 대신 화살표를 사용해 좀 더 간략한 방법으로 함수를 선언할 수 있다.

```javascript
const add = (x, y) => x + y;

console.log(add(2, 5)); // → 7
```

화살표 함수는 기존의 함수보다 표현만 간략한 것이 아니라 내부 동작 또한 간략화되어 있다.

- 화살표 함수는 생성자 함수로 사용할 수x
- 기존 함수와 this 바인딩 방식이 다르다.
- prototype 프로퍼티가 없으며 arguments 객체를 생성하지 않는다.

## 함수 호출

함수는 함수를 가리키는 식별자와 한 쌍의 소괄호인 함수 호출 연산자로 호출한다.

### 매개변수와 인수

- 함수를 실행하기 위해 필요한 값을 함수 외부에서 함수 내부로 전달할 필요가 있는 경우, 매개변수를 통해 인수를 전달한다.
- 인수는 값으로 평가될 수 있는 표현식이어야 한다.
- 인수는 함수를 호출할 때 지정하며, 개수와 타입에 제한이 없다.

인수가 부족해서 인수가 할당되지 않은 매개변수의 값은 `undefined`다.  
매개변수보다 인수가 더 많은 경우 초과된 인수는 무시된다. 단, 모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관된다.

매개변수는 순서에 의미가 있다. 따라서 매개변수가 많아지만 함수를 호출할 때 전달해야 할 인수의 순서를 고려해야 한다.

```
함수의 매개변수는 코드를 이해하는 데 방해되는 요소이므로 이상적인 매개변수 개수는 0개이며 적을수록 좋다. 매개변수의 개수가 많다는 것은 함수가 여러가지 일을 한다는 증거이므로 바람직하지 않다.

이상적인 함수는 한 가지 일만 해야 하며 가급적 작게 만들어야 한다.
```

### 반환문

반환문은 두 가지 역할을 한다.

1. 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다.
2. 반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다. return 키워드 뒤에 반환값으로 사용할 표현식을 명시적으로 지정하지 않으면 undefined가 반환된다.

- 반환문은 생략할 수 있다.
- 반환문은 함수 몸체 내부에서만 사용할 수 있다.

📌 [NOTE]

```
참고로, Node.js에는 모듈 시스템에 의해 파일별로 독립적인 파일 스코프를 갖는다.따라서 Node.js 환경에서는 파일의 가장 바깥 영역에 반환문을 사용해도 에러가 발생하지 않는다.
```

## 참조에 의한 전달과 외부 상태의 변경

> 원시 값은 값에 의한 전달, 객체는 참조에 의한 전달 방식으로 동작한다.

원시 타입 인수는 **값 자체가 복사되어 매개변수에 전달되기 때문**에 함수 몸체에서 그 값을 변경(재할당을 통한 교체)해도 원본은 훼손되지 않는다.  
다시 말해, 외부 상태, 즉 함수 외부에서 함수 몸체로 전달한 원시 값의 원본을 변경하는 어떠한 부수 효과도 발생하지 않는다.

하지만 객체 타입 인수는 **참조 값이 복사되어 매개변수에 전달되기 때문**에 함수 몸체에서 참조 값을 통해 객체를 변경할 경우 원본이 훼손된다.  
다시 말해, 외부 상태, 즉 함수 외부에서 함수 몸체로 전달한 참조 값에 의해 원본 객체가 변경되는 부수 효과가 발생한다.

```
이러한 문제의 해결 방법 중 하나는 객체를 "불변 객체"로 만들어 사용하는 것이다. 객체의 복사본을 새롭게 생성하는 비용은 들지만 객체를 마치 원시 값처럼 변경 불가능한 값으로 동작하게 만드는 것이다.

이를 통해 객체의 상태 객체의 상태 변경을 원천봉쇄하고 객체의 상태 변경이 필요한 경우에는 객체의 방어적 복사를 통해 원본 객체를 완전히 복제, 즉 깊은 복사를 통해 새로운 객체를 생성하고 재할당을 통해 교체한다.
```

## 다양한 함수의 형태

### 즉시 실행 함수

함수 정의와 동시에 즉시 호출되는 함수로, 단 한번만 호출되며 다시 호출할 수 없다.

- 일반적으로 즉시 실행 함수는 함수 이름이 없는 익명 함수를 사용한다.
- 즉시 실행 함수는 반드시 그룹 연산자`(...)`로 감싸야 한다. 그렇지 않으면 에러 발생.  
   그룹 연산자로 함수를 묶은 이유는 먼저 함수 리터럴을 평가해서 함수 객체를 생성하기 위함이다.

### 재귀 함수(recursive function)

재귀 함수는 자기 자신을 호출하는 행위, 즉 재귀 호출을 수행하는 함수를 말한다.

- 반복되는 처리를 위해 사용한다.

Ex) 팩토리얼

```javascript
// 함수 표현식
var factorial = function foo(n) {
  if (n <= 1) return 1;

  // 함수를 가리키는 식별자로 자기 자신을 재귀 호출
  return n * factorial(n - 1);
};

console.log(factorial(5)); // → 5!=5*4*3*2*1=120
```

> 재귀 함수는 자신을 무한 재귀 호출한다. 따라서 재귀 함수 내에는 재귀 호출을 멈출 수 있는 탈출 조건을 반드시 만들어야 한다.

재귀 함수는 무한 반복에 빠질 위험이 있고, 이로 인해 스택 오버플로 에러를 발생시킬 수 있으므로 주의해서 사용해야 한다.  
따라서 재귀 함수는 반복문을 사용하는 것보다 재귀 함수를 사용하는 편이 더 직관적으로 이해하기 쉬울 때만 한정적으로 사용하는 것이 바람직하다.

### 중첩 함수

함수 내부에 정의된 함수를 중첩 함수(nested function) or 내부 함수(inner function)이라 한다. 그리고 중첩 함수를 포함하는 함수는 외부 함수(outer function)라 부른다.

- 중첩 함수는 외부 함수 내에서만 호출할 수 있다.
- 일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 `헬퍼 함수(helper function)의 역할`을 한다.

단, 호이스팅으로 인해 혼란이 발생할 수 있으므로 if문이나 for문 등의 코드 블록에서 함수 선언문을 통해 함수를 정의하는 것은 바람직하지 않다.

### 콜백 함수(callback function)

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 `콜백 함수`라고 하며, 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 `고차 함수(Higher-Order Function, HOF)`라고 한다.

```javascript
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i);
  }
}

var logAll = function (i) {
  console.log(i);
};

repeat(5, logAll); // → 0, 1, 2, 3, 4

// logOdds 함수는 단 한 번만 생성된다.
var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 고차 함수에 함수 참조를 전달한다.
repeat(5, logOdds); // → 1, 3
```

- 고차 함수는 콜백 함수를 자신의 일부분으로 합성한다.
- 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다.

> 다시 말해, 콜백함수는 고차 함수에 의해 호출되며 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다.

콜백 함수는 함수형 프로그래밍 패러다임뿐만 아니라 비동기 처리(이벤트 처리, Ajax 통신, 타이머 함수 등)에 활용되는 중요한 패턴이다.

```javascript
// 콜백 함수를 사용한 이벤트 처리
document.getElementById("myButton").addEventListener("click", function () {
  console.log("button clicked!");
});

// 콜백 함수를 사용한 비동기 처리
setTimeout(function () {
  console.log("1초 경과");
}, 1000);
```

### 순수 함수 vs. 비순수 함수

순수 함수(pure function): 어떤 외부 상태에 의존하지도 않고 변경하지도 않는, 즉 부수 효과가 없는 함수

- 동일한 인수가 전달되면 언제나 동일한 값을 반환하는 함수다.
- 일반적으로 최소 하나 이상의 인수를 전달받는다.
- 함수의 외부 상태를 변경하지 않는다.

비순수 함수(impure function): 외부 상태에 의존하거나 외부 상태를 변경하는, 즉 부수 효과가 있는 함수

함수가 외부 상태를 변경하면 상태 변화를 추적하기 어려워진다. 따라서 함수 외부 상태의 변경을 지양하는 **순수 함수를 사용하는 것이 좋다.**