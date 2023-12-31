- 연산자(operator): 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다.
- 피연산자(operand): 연산의 대상으로, `값으로 평가될 수 있는 표현식`이어야 한다.

```
연산자는 값으로 평가된 피연산자를 연산해 "새로운 값"을 만든다.
```

## 7.1 산술 연산자(arithmetic operator)

산술 연산자는 피연산자를 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만든다. 산술 연산이 불가능한 경우, `NaN`을 반환한다.  
산술 연산자는 피연산자의 개수에 따라 이항 산술 연산자와 단항 산술 연산자로 구분할 수 있다.

```
모든 이항 산술 연산자는 피연산자의 값을 변경하는 부수 효과(side effect)가 없다.
다시 말해, 어떤 산술 연산을 해도 피연산자의 값이 바뀌는 경우는 없고 언제나 새로운 값을 만들 뿐.
```

| 이항 산술 연산자 | 의미   | 부수 효과 |
| ---------------- | ------ | --------- |
| `+`              | 덧셈   | X         |
| `-`              | 뺄셈   | X         |
| `*`              | 곱셈   | X         |
| `/`              | 나눗셈 | X         |
| `%`              | 나머지 | X         |

| 단항 산술 연산자 | 의미                                                 | 부수 효과 |
| ---------------- | ---------------------------------------------------- | --------- |
| `++`             | 증가                                                 | O         |
| `--`             | 감소                                                 | O         |
| `+`              | 어떠한 효과도 없다. 음수를 양수로 반전하지도 않는다. | X         |
| `-`              | 피연산자의 부호를 반전한 값을 반환한다.              | X         |

- 증가/감소(++/--)연산자의 위치에 따른 의미 변화

  - 피연산자 앞: `전위 증가/감소 연산자(prefix increment/decrement operator)` 먼저 피연산자의 값을 증가/감소시킨 후, 다른 연산를 수행한다.
  - 피연산자 뒤: `후위 증가/감소 연산자(postfix increment/decrement operator)` 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킨다.

- `+` 연산자
  - 피연산자 중 하나 이상이 문자열일 경우엔 `문자열 연결 연산자`로 동작한다.

```javascript
// true는 1로 타입 변환한다.
1 + true; // → 2

// false는 0으로 타입 변환한다.
1 + false; // → 1

// null은 0으로 타입 변환한다.
1 + null; // → 1

//undefined는 숫자로 타입 변환되지 않는다.
+undefined; // → NaN
1 + undefined; // → NaN
```

위 예제처럼 개발자의 의도와 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다. 이를 `암묵적 타입 변환(implicit coercion)` 또는 `타입 강제 변환(type coercion)`이라고 한다.

## 7.2 할당 연산자

할당 연산자는 좌항의 변수에 값을 할당하므로 변수 값이 변하는 부수 효과가 있다.

### 할당문은 표현식인 문일까, 표현식이 아닌 문일까?

```javascript
var x;

//할당식은 표현식인 문이다.
console.log((x = 10)); // → 10
```

위 예제에의 할당문 `x=10`은 x에 할당된 숫자 값 10으로 평가된다. 따라서 할당문을 다른 변수에 할당할 수도 있다.

> 할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다.

## 7.3 비교 연산자

동등 비교(loose equality)와 일치 비교(strict equality) 연산자는 좌항과 우항의 피연산자가 같은 값으로 평가되는지 비교해 불리언 값을 반환한다.

- 동등 비교(`==`) 연산자: 좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교한다.
  - 좌항과 우항의 피연산자가 타입은 다르더라도 암묵적 타입 변환 후에 같은 값일 수 있다면 `true`를 반환.
  - 편리한 경우도 있지만 결과를 예측하기 어렵고 실수하기 쉽다. → 일치 비교 연산자 사용
- 일치 비교(`===`) 연산자: 좌항과 우항의 피연산자가 **타입도 같고 값도 같은 경우**에 한하여 true를 반환.

### 일치 비교 연산자에서 주의할 값

- `NaN`: 자신과 일치하지 않는 유일한 값이다. 따라서 숫자가 NaN인지 조사하려면 빌트인 함수 `Number.isNaN`을 사용한다.

- `0`: 자바스크립트에는 양의 0과 음의 0이 있는데 이들을 비교하면 true를 반환한다.

ES6에서 도입된 Object.is 메서드는 다음과 같이 예측 가능한 정확한 비교 결과를 반환한다. 그 외에는 일치 비교 연산자와 동일하게 동작한다.

```javascript
-0 === +0; // → true
Object.is(-0, +0); // → false

NaN === NaN; // → false
Object.is(NaN, NaN); // → true
```

## 7.4 삼항 조건 연산자

`(조건식) ? (조건이 true일때 반환값) : (조건이 false일때 반환값)`

- 조건식: 불리언 타입의 값으로 평가될 표현식

삼항 조건 연산자는 조건식의 평가 결과에 따라 반환할 값을 결정한다.

- 자바스크립트의 유일한 삼항 연산자이며, 부수 효과x
- 두 번째 피연산자 또는 세 번째 피연산자로 평가되는 표현식
- 삼항 조건 연산자의 첫 번째 피연산자는 조건식이므로 삼항 조건 연산자 표현식은 조건문이다.

### 삼항 조건 연산자 표현식 vs. if...else문

삼항 조건 연산자 표현식은 값처럼 사용할 수 있지만, if...else문은 값처럼 사용할 수 없다.  
즉, if...else문은 표현식이 아닌 문이다.

```javascript
var x = 10;


var result = if (x%2) {result='홀수';} else {result='짝수';}; // SyntaxError: Unexpected token if

var result = x % 2 ? '홀수' : '짝수';
```

## 7.5 논리 연산자

논리 부정(`!`) 연산자는 언제나 불리언 값을 반환한다. 단, 피연산자가 반드시 불리언 값일 필요는 없다.  
논리합(`||`) 또는 논리곱(`&&`) 연산자 표현식의 평가 결과는 불리언 값이 아닐 수도 있다. 해당 표현식은 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.

## 7.6 쉼표 연산자

쉼표(`,`)연산자는 왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피연산자의 평가가 끝나면 마지막 피연산자의 평가 결과를 반환한다.

```javascript
var x, y, z;

(x = 1), (y = 2), (z = 3); // → 3
```

## 7.8 typeof 연산자

```javascript
typeof NaN; // → "number"
typeof undefined; // → "undefined"
typeof null; // → "object"
typeof []; // → "object"
typeof {}; // → "object"
typeof new Date(); // → "object"
typeof function () {}; // → "function"
```

typeof 연산자로 `null` 값을 연산해 보면 "null"이 아닌 "object"를 반환한다. 이것은 자바스크립트의 첫 번째 버전의 버그다. 기존 코드에 영향을 줄 수 있기 때문에 아직까지 수정되지 못하고 있다.

> 따라서 값이 null 타입인지 확인할 때는 typeof 연산자가 아닌 일치 연산자(`===`)를 사용하자.

선언하지 않은 식별자를 typeof 연산자로 연산해 보면 ReferenceError가 발생하지 않고 "undefined"를 반환한다.

## 7.11 연산자의 부수 효과

일부 연산자는 다른 코드에 영향을 주는 부수 효과가 있다.
부수 효과가 있는 연산자는 `할당 연산자(=)`, `증가/감소 연산자(++/--)`, `delete 연산자`다.

- 할당 연산자: 변수 값이 변하는 부수 효과
- 증가/감소 연산자: 피연산자의 값이 재할당되어 변경되는 부수 효과
- delete 연산자: 객체의 프로퍼티를 삭제하는 부수 효과
