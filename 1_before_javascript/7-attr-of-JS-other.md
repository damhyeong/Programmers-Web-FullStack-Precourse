## 제목 : JavaScript 언어의 특징 - 그 외

### 유형 : 동영상

---

|             |                                       |
|-------------|---------------------------------------|
| **변수의 타입**  | 동적 타입 언어                              |
| **함수의 특징**  | 일급 객체                                 |
| **상속의 형태**  | 프로토타입 기반의 상속                          |
| **패러다임 지원** | 함수형 프로그래밍, 명령형 프로그래밍, 객체지향 프로그래밍, ... |

<br/>

### 동적 타입 언어

변수에 들어가는 값에 따라서, 런타임에 타입이 추론된다.

```javascript
let variable = 1;
typeof variable;

// Result : 'number'
```

<br/>

```javascript
let variable = 1;
variable = 'abc'; // 재할당 

typeof variable;

// Result : 'string'
```

<br/>

### 일급 객체

함수는 **일급 객체**의 특징을 가진다.

함수는 **객체**와 동일하게 사용 할 수 있다.

함수는 **값** 과 동일하게 취급한다.

* 변수 할당문
* 객체 프로퍼티 값
* 배열의 요소
* 함수 호출의 인수
* 함수 반환문 
* 등등

**Example**

```javascript
const func1 = function (element) {
    return element();
};

const func2 = function () {
    return func3;
};

const func3 = function () {
    return 'apple';
};

func1(func2());

// Result : 'apple'
```

<br/>

### 프로토타입 기반의 상속

언어가 갖고 있는, 프로토타입 **chaining**(체이닝) 구조를 통하여 상속이 가능하다.

```javascript
const object = {
    var1: 'apple',
    var2: 'banana',
};

object.hasOwnProperty('var1');

// Result : true
```

<br/>

## 여러 프로그래밍 패러다임 지원

* 명령형 프로그래밍
* 함수형 프로그래밍
* 객체지향 프로그래밍
* ...

```javascript
const array = [1, 2, 3];
const func = function (element) {
    return element + 1;
};

array.map(func);

// Result : [ 2, 3, 4 ]
```

