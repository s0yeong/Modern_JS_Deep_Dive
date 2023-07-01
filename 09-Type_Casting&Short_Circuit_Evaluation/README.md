## 타입 변환

타입 변환이란 기존 원시 값을 사용해 **다른 타입의 새로운 원시 값**을 생성하는 것이다.

- `명시적 타입 변환(explicit coercion)` or `타입 캐스팅(type casting)`: 개발자가 의도적으로 값의 타입을 변환하는 것

  ```javascript
  var x = 10;

  // 명시적 타입 변환: 숫자를 문자열로 타입 캐스팅
  var str = x.toString();
  console.log(typeof str, str); // → string 10

  // x 변수의 값이 변경된 것은 아님
  console.log(typeof x, x); // → number 10
  ```

- `암묵적 타입 변환(implicit coercion)` or `타입 강제 변환(type coercion)`: 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암목적으로 타입이 자동 변환되는 것

  ```javascript
  var x = 10;

  // 암묵적 타입 변환
  // 문자열 연결 연산자는 숫자 타입 x의 값을 바탕으로 새로운 문자열을 생성한다.
  var str = x + "";
  console.log(typeof str, str); // → string 10

  // x 변수의 값이 변경된 것은 아님
  console.log(typeof x, x); // → number 10
  ```

  - 기존 변수 값을 재할당하여 변경하는 것x
  - 자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 피연산자의 값을 암묵적 타입 변환해 새로운 타입의 값을 만들어 단 한 번 사용하고 버린다.

```
때로 명시적 타입 변환보다 암묵적 타입 변환이 가독성 측면에서 더 좋을 수도 있다.
예를 들어, 자바스크립트 문법을 잘 이해하고 있는 개발자에게는 (10).toString() 보다 10+''이 더 간결하고 이해하기 쉽다.

중요한 것은 동료가 작성한 코드를 정확히 이해할 수 있어야 하고 자신이 작성한 코드도 동료가 쉽게 이해할 수 있어야 한다.
```

## 암묵적 타입 변환

자바스크립트는 가급적 에러를 발생시키지 않도록 암묵적 타입 변환을 통해 표현식을 평가한다. 이때 코드 문맥에 부합하도록 암묵적 타입 변환을 실행한다.

암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환한다.

### 불리언 타입으로 변환

자바스크립트 엔진은 불리언 타입이 아닌 값을 `Truthy 값(참으로 평가되는 값)` or `Falsy 값(거짓으로 평가되는 값)`으로
구분한다. 즉, 제어문의 조건식과 같이 불리언 값으로 평가되어야 할 문맥에서 Truthy 값은 true로, Falsy 값은 false로 암묵적 타입 변환된다.

- false로 평가되는 Falsy 값  
   `false`, `undefined`, `null`, `0`, `-0`, `NaN`, `''(빈 문자열)`

## 단축 평가(short-circuit evaluation)

논리곱(`&&`) 연산자와 논리합(`||`) 연산자는 이처럼 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축 평가라 한다.

**단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.**

| 단축 평가 표현식      | 평가 결과 |
| --------------------- | --------- |
| `true \|\| anything`  | true      |
| `false \|\| anything` | anything  |
| `true && anything`    | anything  |
| `false && anything`   | true      |

단축 평가를 사용하면 if문을 대체할 수 있다.

- 어떤 조건이 Truthy 값일 때 무언가를 해야 한다면 논리곱(&&) 연산자 표현식으로 if문을 대체할 수 있다.

  ```javascript
  var done = true;
  var message = "";

  //주어진 조건이 true일 때
  if (done) message = "완료";

  // if문 단축 평가로 대체 → done이 true라면 message에 '완료'를 할당
  message = done && "완료";
  console.log(message);
  ```

- 어떤 조건이 Falsy 값일 때 무언가를 해야 한다면 논리합(||) 연산자 표현식으로 if문을 대체할 수 있다.

  ````javascript
  var done = false;
  var message = '';

      //주어진 조건이 false일 때
      if(!done) message = '미완료';

      // if문 단축 평가로 대체 → done이 false라면 message에 '완료'를 할당
      message = done || '미완료';
      console.log(message);
      ```

  위의 예제를 if...else문으로 합칠 경우 삼항 조건 연산자로 대체할 수도 있다.

  ````

- 단축 평가를 사용하는 경우

  1. 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

     ```javascript
     var elem = null;

     // elem이 Falsy값이면 elem으로 평가되고, truthy값이면 elem.value로 평가된다.
     var value = elem && elem.value;
     ```

  2. 함수 매개변수에 기본값을 설정할 때

     단축 평가를 사용해서 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.

     ```javascript
     function getStringLength(str) {
       str = str || "";
       return str.length;
     }

     getStringLength(); // → 0
     getStringLength("hi"); // → 2
     ```

### 옵셔널 체이닝 연산자(optional chaining)

ES11(ECMAScript2020)에서 도입된 옵셔널 체이닝(`?.`)는 좌항의 피연산자가 `null` or `undefined`인 경우 "undefined"를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```javascript
var elem = null;

// elem이 null 또는 undefined면 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
var value = elem?.value;
console.log(value); // → undefined
```

### null 병합 연산자

ES11(ECMAScript2020)에서 도입된 null 병합 연산자 `??`는 좌항의 피연산자가 `null` or `undefined`인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 우항의 피연산자를 반환한다. null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용한다.

```javascript
var foo = null ?? "default string";
console.log(foo);
```

- null 병합 연산자 `??`가 도입되기 이전에는 논리 연산자 `||`를 사용한 단축 평가를 통해 변수에 기본값을 설정했다.
  - 만약 Falsy인 값인 0이나 ''도 기본값으로서 유효하다면 예기치 않은 동작이 발생할 수 있다.
- 하지만 null 병합 연산자 `??`는 좌항의 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, '', -0, NaN)이라도 `null` 또는 `undefined`가 아니면 좌항의 피연산자를 그대로 반환한다.

```javascript
// Falsy 값인 0이나 ''도 기본값으로서 유효하다면 예기치 않은 동작이 발생할 수 있다.
var foo = "" || "default string";
console.log(foo); // "default string"

// 좌항의 피연산자가 Falsy 값이라도 null 또는 undefined가 아니면 좌항의 피연산자를 반환한다.
var foo = "" ?? "default string";
console.log(foo); // ""
```
