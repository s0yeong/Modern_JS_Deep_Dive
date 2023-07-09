## 내부 슬롯과 내부 메서드

모든 객체는 [[Prototype]]이라는 내부 슬롯을 갖는다. 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 원칙적으로 직접 접근할 수 없지만 [[Prototype]] 내부 슬롯의 경우, `__proto__`를 통해 간접적으로 접근할 수 있다.

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.

```
프로퍼티의 상태란 프로퍼티의 값(value), 값의 갱신 가능 여부(writable), 열거 가능 여부(enumerable), 재정의 가능 여부(configurable)를 말한다.
```

프로퍼티 어트리뷰트는 자바스크립트 엔진이 관리하는 내부 상태 값인 내부 슬롯 [[Value]], [[Writable]], [[Enumerable]], [[Configurable]]이다.  
따라서 프로퍼티 어트리뷰트에 직접 접근할 수 없지만 `Object.getOwnPropertyDescriptor` 메서드를 사용하여 간접적으로 확인할 수 있다.

Ex)

```javascript
const person = {
  name: "Lee",
};

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.
console.log(Object.getOwnPropertyDescriptor(person, "name"));
// {value: "Lee", writable: true, enumerable: true, configurable: true}
```

Object.getOwnPropertyDescriptor 메서드를 호출할 때

- 첫 번째 매개변수: 객체의 참조를 전달
- 두 번째 매개변수: 프로퍼티 키를 문자열로 전달

이때 Object.getOwnPropertyDescriptor 메서드는 프로퍼티 어트리뷰트 정보를 제공하는 `프로퍼티 디스크립터 객체`를 반환한다. 만약 존재하지 않는 프로퍼티나 상속받은 프로퍼티에 대한 프로퍼티 디스크립터를 요구하면 undefined가 반환된다.

Ex)

```javascript
const person = {
  name: "Lee",
};

// 프로퍼티 동적 생성
person.age = 20;

// 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
    name: {value: "Lee", writable: true, enumerable: true, configurable: true},
    age: {value: 20, writable: true, enumerable: true, configurable: true}
}
*/
```

## 데이터 프로퍼티와 접근자 프로퍼티

- 데이터 프로퍼티: 키와 값으로 구성된 일반적인 프로퍼티
- 접근자 프로퍼티: 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 **접근자 함수**로 구성된 프로퍼티

### 데이터 프로퍼티

[[Value]]

- 프로퍼티 키를 통해 프로퍼티 값에 접근하면 반환되는 값
- 프로퍼티 키를 통해 프로퍼티 값을 변경하면 [[Value]]에 값을 재할당한다. 이때 프로퍼티 키가 없으면 프로퍼티를 동적 생성하고 생성된 프로퍼티의 [[Value]]에 값을 저장한다.

[[Writable]]

- 프로퍼티 값의 변경 가능 여부를 나타내며 불리언 값을 갖는다.
- 값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없는 읽기 전용 프로퍼티가 된다.

[[Enumerable]]

- 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다.
- 값이 false인 경우 해당 프로퍼티는 for...in문이나 Object.keys 메서드 등으로 열거할 수 없다.

[[Configurable]]

- 프로퍼티의 재정의 가능 여부를 나타내며 불리언 값을 갖는다.
- 값이 false인 경우 해당 프로퍼티의 삭제, 프로퍼티 어트리뷰트 값의 변경이 금지된다. 단, [[Writable]]이 true인 경우 [[Value]]의 변경과 [[Writable]]을 false로 변경하는 것은 허용된다.

```
프로퍼티가 생성될 때 [[Value]]의 값은 프로퍼티 값으로 초기화되며 [[Writable]], [[Enumerable]], [[Configurable]]의 값은 true로 초기화된다.
```

### 접근자 프로퍼티

자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티다.

[[Get]]

```
접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 "읽을 때" 호출되는 접근자 함수.
즉, 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.
```

[[Set]]

```
접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 "저장할 때" 호출되는 접근자 함수.
즉, 접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰트 [[Set]]의 값, 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다.
```

[[Enumerable]]

```
데이터 프로퍼티의 [[Enumerable]]과 같다.
```

[[Configurable]]

```
데이터 프로퍼티의 [[Configurable]]과 같다.
```

접근자 함수는 getter/setter 함수라고도 부른다. 접근자 프로퍼티는 getter와 setter 함수를 모두 정의할 수도 있고 하나만 정의할 수도 있다.
메서드 앞에 get, set을 붙인 메서드가 바로 getter/setter 함수다. 그리고 아래의 예제에서 getter/setter 함수의 이름 fullname이 접근자 프로퍼티다.  
접근자 프로퍼티는 자체적으로 값(프로퍼티 어트리뷰트 [[Value]])을 가지지 않으며 다만 데이터 프로퍼티의 값을 읽거나 저장할 때 관여할 뿐이다.

Ex)

```javascript
const person = {
  firstName: "Ungmo",
  lastName: "Lee",

  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(" ");
  },
};

console.log(person.firstName + " " + person.lastName); // Ungmo Lee

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
person.fullName = "Heegun Lee";
console.log(person); // {firstName: "Heegun", lastName: "Lee"}
console.log(person.fullName); // Heegun Lee

// firstName은 데이터 프로퍼티다.
let descriptor = Object.getOwnPropertyDescriptor(person, "firstName");
console.log(descriptor);
// {value: "Heegun", writable: true, enumerable: true, configurable: true}

// fullName은 접근자 프로퍼티다.
descriptor = Object.getOwnPropertyDescriptor(person, "fullName");
console.log(descriptor);
// {get: f, set: f, enumerable: true, configurable: true}
```

일반 객체의 `__proto__`는 접근자 프로퍼티다.  
함수 객체의 `__proto__`는 데이터 프로퍼티다.

```javascript
Object.getOwnPropertyDescriptor(Object.prototype, "__proto__");
Object.getOwnPropertyDescriptor(function () {}, "prototype");
```

## 프로퍼티 정의

**프로퍼티 정의란?**  
새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기존 프로퍼티의 프러퍼티 어트리뷰트를 재정의할 것을 말한다.

```javascript
const person={};

// 데이터 프로퍼티 정의
Object.defineProperty(person, 'firstName', {
    value: 'Ungmo',
    writable: true,
    enumerable: true,
    configurable: true,
});

Object.defineProperty(person, 'lastName', {
    value: 'Lee'
});

let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
console.log('firstName', descriptor);
// firstName {value: "Ungmo", writable: true, enumerable: true, configurable: true}

// 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
console.log('lastName', descriptor);
// lastName {value: "Lee", writable: false, enumerable: false, configurable: false}

// 접근자 프로퍼티 정의
Object.defineProperty(person, 'fullName', {
    // getter 함수
    get() {
        return `${this.firstName} ${this.lastName}`;
    }
    // setter 함수
    set(name) {
        [this.firstName, this.LastName] = name.split(' ');
    },
    enumerable: true,
    configurable: true
});
```

[[Enumerable]]의 값이 false인 경우

- for...in 문이나 Object.keys 등으로 열거할 수 없다.

[[Writable]]의 값이 false인 경우

- 해당 프로퍼티의 값 [[Value]]의 값을 변경할 수 없다.
- 이때 값을 변경하면 에러는 발생하지 않고 무시된다.

[[Configurable]]의 값이 false인 경우

- 해당 프로퍼티를 삭제할 수 없다.
- 해당 프로퍼티를 재정의할 수 없다.
- 이때 프로퍼티를 삭제하면 에러는 발생하지 않고 무시된다.

Object.defineProperty 메서드는 한번에 하나의 프로퍼티만 정의할 수 있다. Object.defineProperties 메서드를 사용하면 여러 개의 프로퍼티를 한 번에 정의할 수 있다.

```javascript
Object.defineProperties(person, {
    // 데이터 프로퍼티 정의
    firstName: {
        value: 'Ungmo',
        writable: true,
        enumerable: true,
        configurable: true
    },
    lastName: {
        value: 'Lee',
        writable: true,
        enumerable: true,
        configurable: true
    },
    // 접근자 프로퍼티 정의
    fullName: {
        // getter 함수
        get() {
            return `${this.firstName} ${this.lastName}`;
        }
        // setter 함수
        set(name) {
            [this.firstName, this.LastName] = name.split(' ');
        },
        enumerable: true,
        configurable: true
    }
});

person.fullName='Heegun Lee';
console.log(person); // {firstName: "Heegun", lastName: "Lee"}
```

## 객체 변경 방지

객체는 변경 가능한 값이므로 재할당 없이 직접 변경할 수 있다.  
즉, 프로퍼티를 추가하거나 삭제할 수 있고, 프로퍼티 값을 갱신할 수 있으며, Object.defineProperty 또는 Object.defineProperties 메서드를 사용하여 프로퍼티 어트리뷰트를 재정의할 수도 있다.

자바스크립트는 객체의 변경을 방지하는 다양한 메서드를 제공한다.  
|구분|메서드|프로퍼티 추가|프로퍼티 삭제|프로퍼티 값 읽기|프로퍼티 값 쓰기|프로퍼티 어트리뷰트 재정의|
|---|---|:---:|:---:|:---:|:---:|:---:|
|객체 확장 금지|Object.preventExtensions|X|O|O|O|O|
|객체 밀봉|Object.seal|X|X|O|O|X|
|객체 동결|Object.freeze|X|X|O|X|X|

### 객체 확장 금지 `Object.preventExtensions`

확장이 금지된 객체는 프로퍼티 추가가 금지된다.  
즉, 프로퍼티 동적 추가와 Object.defineProperty 메서드로 추가하는 방법 두 가지 모두 금지된다.

확장이 가능한 객체인지 여부는 `Object.isExtensible` 메서드로 확인할 수 있다.

### 객체 밀봉 `Object.seal`

객체 밀봉이란 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지를 의미한다.

> 즉, 밀봉된 객체는 읽기와 쓰기만 가능하다.

밀봉된 객체인지 여부는 `Object.isSealed` 메서드로 확인할 수 있다.

### 객체 동결 `Object.freeze`

객체 동결이란 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지를 의미한다.

> 즉, 동결된 객체는 읽기만 가능하다.

동결된 객체인지 여부는 `Object.isFrozen` 메서드로 확인할 수 있다.

### 불변 객체

위의 변경 방지 메서드들은 얕은 변경 방지로 직속 프로퍼티만 변경이 방지되고 중첩 객체까지는 영향을 주지 못한다.

```
객체의 중첩 객체까지 동결하여 변경이 불가능한 읽기 전용의 불변 객체를 구현하려면 객체를 값으로 갖는 모든 프로페티에 대해 재귀적으로 Object.freeze 메서드를 호출해야 한다.
```

```javascript
function deepFreeze(target) {
  if (target && typeof target === "object" && !Object.isFrozen(target)) {
    Object.Freeze(target);

    Object.keys(target).forEach((key) => deepFreeze(target[key]));
  }
  return target;
}

const person = {
  name: "Lee",
  address: { city: "Seoul" },
};

// 깊은 객체 동결
deepFreeze(person);

console.log(Object.isFrozen(person)); // true
console.log(Object.isFrozen(person.address)); // true
```
