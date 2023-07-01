객체는 프로퍼티와 메서드로 구성된 집합체다.  
<img src="data:image/jpeg;base64,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">

- 프로퍼티: 객체의 상태를 나타내는 값(data)
- 메서드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)

이처럼 객체는 객체의 상태를 나타내는 값(프로퍼티)과 프로퍼티를 참조하고 조작할 수 있는 동작(메서드)을 모두 포함할 수 있기 때문에 상태와 동작을 하나의 단위로 구조화할 수 있어 유용하다.

## 객체 리터럴

객체 리터럴을 사용하는 것은 객체 생성 방법 중에서 가장 일반적이고 간단한 방법으로, 객체를 생성하기 위한 표기법이다.

- 객체 리터럴은 중괄호({...})내에 0개 이상의 프로퍼티를 정의한다.
- 객체 리터럴에 프로퍼티를 포함시켜 객체를 생성함과 동시에 프로퍼티를 만들 수도 있고, 객체를 생성한 이후에 프로퍼티를 동적으로 추가할 수도 있다.
- 변수에 할당되는 시점에 자바스크립트 엔진은 객체 리터럴을 해석해 객체를 생성한다.

```javascript
var person = {
  name: "Lee",
  sayHello: function () {
    console.log(`Hello! My name is ${this.name}.`);
  },
};

console.log(typeof person); // → object
console.log(person); // → {name: "Lee", sayHello: f}
```

객체 리터럴은 값으로 평가되는 표현식이다. 따라서 객체 리터럴의 닫는 중괄호 뒤에는 세미콜론을 붙인다.

## 프로퍼티(Property)

객체는 프로퍼티의 집합이며, 프로퍼티는 `키`와 `값`으로 구성된다. 프로퍼티를 나열할 때는 쉼표(,)로 구분한다.

- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 or 심벌 값

  - 프로퍼티 키는 프로퍼티 값에 접근할 수 있는 이름으로서 `식별자` 역할을 한다.
  - 프로퍼티 키에 문자열이나 심벌 값 외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.
  - 이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 **덮어쓴다**. 이때 에러는 발생하지 않는다.

- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

## 메서드(Method)

`프로퍼티 값이 함수일 경우` 일반 함수와 구분하기 위해 `메서드`라 부른다. 즉, 메서드는 **객체에 묶여 있는 함수**를 말한다.

```javascript
var circle = {
    radius: 5; // ← 프로퍼티

    getDiameter: function() { // ← 메서드
        return 2* this.radius; // this는 circle을 가리킨다.
    }
};

console.log(circle.getDiameter()); // → 10
```

## 프로퍼티 접근

프로퍼티에 접근하는 방법은 다음과 같이 두 가지다.

1. 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법
2. 대괄호 프로퍼티 접근 연산자([...])를 사용하는 대괄호 표기법

```javascript
var person = {
  name: "Lee",
};

// 마침표 표기법에 의한 프로퍼티 접근
console.log(person.name); // → Lee
// 대괄호 표기법에 의한 프로퍼티 접근
console.log(person["name"]); // → Lee
```

대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 `반드시 따옴표로 감싼 문자열`이어야 한다. 따옴표로 감싸지 않은 이름을 프로퍼티 키로 사용하면 자바스크립트 엔진은 **식별자**로 해석한다.

객체에 존재하지 않는 프로퍼티에 접근하면 "undefined"를 반환한다.

```javascript
var person = {
  "last-name": "Lee",
  1: 10,
};

person.last - name; // → 브라우저 환경: NaN
// → Node.js 환경: ReferenceError: name is not defined
```

위 예제에서 person.last-name의 실행 결과는 환경에 따라 다르다. 그 이유는 무엇일까?

person.last-name을 실행할 때 자바스크립트 엔진은 먼저 person.last를 평가한다. person 객체에는 프로퍼티 키가 last인 프로퍼티가 없기 때문에 person.last는 `undefined`로 평가된다. **따라서 person.last-name은 `undefined-name`과 같다.** 다음으로 자바스크립트 엔진은 name이라는 식별자를 찾는다.

Node.js 환경에서는 현재 어디에도 name이라는 식별자(변수, 함수 등의 이름) 선언이 없으므로 "ReferenceError: name is not defined"라는 에러가 발생한다.  
그런데 브라우저 환경에서는 name이라는 전역 변수(전역 객체 window의 프로퍼티)가 암묵적으로 존재한다. 전역 변수 name은 window(창)의 이름을 가리키며, 기본값은 빈 문자열이다. **따라서 person.last-name은 `undefined-''`과 같으므로 `NaN`이 된다.**

## 프로퍼티 동적 생성 & 삭제

- 프로퍼티 동적 생성: 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.
- 프로퍼티 삭제: `delete 연산자`를 사용해서 객체의 프로퍼티를 삭제한다. 만약 존재하지 않는 프로퍼티를 삭제하면 에러x 무시된다.

## ES6에서 추가된 객체 리터럴의 확장 기능

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다.

```javascript
let x = 1,
  y = 2;

const obj = { x, y };
console.log(obj); // → {x: 1, y: 2}
```

ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

```javascript
const prefix = "prop";
let i = 0;

const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
};

console.log(obj); // → {prop-1: 1, prop-2: 2, prop-3: 3}
```

ES6에서는 메서드를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.

```javascript
const obj = {
    name = 'Lee',

    sayHi() {
        console.log('Hi!'+ this.name);
    }
};

obj.sayHi(); // → Hi! Lee
```
