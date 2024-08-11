## 제목 : 변수 생성 방법과 호이스팅

### 유형 : 동영상

---

### log의 위치, 변수 키워드가 다른 것 뿐인데, 왜 결과가 다를까?

<br/>

**Example 1**

```javascript
var a;
var b = 1;
const c = 2;

console.log(a);
console.log(b);
console.log(c);
```

```text
undefined
1
2
```

<br/>

**Example 2**

```javascript
console.log(a);
console.log(b);
console.log(c);

var a;
var b = 1;
var c = 2;
```

```text
ReferenceError: Cannot access 'c' before initialization
undefined
undefined
```

<br/>

## 3 단계를 거쳐 생성되는 변수

1. 선언 단계 : Register
2. 초기화 단계 : Initialization
3. 할당 단계 : Assignment

<br/>

1. 선언 단계 : 변수를 변수 객체에 등록한다.
2. 초기화 단계 : 변수를 메모리에 할당하고, `undefined` 로 초기화한다.
3. 할당 단계 : `undefined` 로 초기화된 변수에 실제로 값을 할당한다.

<br/>

**위의 변수 생성 3단계는 키워드별로 다르게 동작한다 : (var, const, let)**

<br/>

## var 키워드

1. **코드 평가단계** : 선언과 동시에 초기화 진행
2. **코드 실행단계** : 값 할당 진행

```mermaid
flowchart LR

subgraph 코드-평가
    1-1["1. 선언단계"]
    1-2["2. 초기화 단계"]
        
    subgraph 변수객체-1
        foo("foo")
    end
    subgraph 변수객체-2
        foo1("foo = undefined")
    end
        
    1-1 --- 변수객체-1
    1-2 --- 변수객체-2
end

subgraph 코드-실행
    2-1("3. 할당단계")
        
    subgraph 변수-객체
        foo2("foo = 1")
    end
        
        2-1 --- 변수-객체
end

코드-평가 --> 코드-실행
```

그런데, 이미 코드 평가시점에 선언과 동시에 **초기화** 가 진행되었으므로,

**변수의 할당문이 실행되기 전에도 참조가 가능하다.**

이러한 현상을 **호이스팅** 이라고 한다.

### 호이스팅이란?

밑에 선언되어 있는 변수들이 마치,

맨 위에 선언되어 쓸 수 있는 형태로 되어있는 것을 호이스팅이라고 한다.

**호이스팅** :== 맨 위로 끌어올리다. 

```javascript
console.log(a);
console.log(b);

var a = 1;
var b = 2;
```

```text
undefined
undefined
```

<br/>

## var 키워드의 호이스팅이란? (Hoisting)

모든 선언문이 해당 **Scope** 의 선두로 옮겨진 것처럼 동작하는 특성을 지닌다.

**함수 호이스팅**, **변수 호이스팅**, 등등 

<br/>

## var 키워드의 단점

* 키워드 생략이 가능하다. : ex - `a = 1`
* 중복 선언이 가능하다.
* 변수 호이스팅의 특성을 지닌다.

이 모든것들의 단점의 특성은 하나를 가르키는데,

**변수의 결과 예측에 혼선을 준다** 라는 것이다. ==> 가독성이 현저히 떨어진다.

```javascript
a = 1; // var 키워드를 생략했다.
var a = 2; // 중복 선언이 허용되었다.
console.log(window.a); // var로 선언된 변수는, 전역변수화된다.

const b = 1;
console.log(window.b);
```

```text
2
undefined
```

## var 키워드의 단점 - 전역변수화

`var` 키워드는 **전역 변수화** 되어, 무분별하게 변수에 접근이 가능하다.

**Scope**(스코프) 영역으로 살펴보자면,

코드가 실행되는 과정에서, 변수와 같은 식별자를 찾아야 하는 코드가 있을 때,

어떠한 코드 블록에서도 접근이 가능하고 실행이 가능하다는 것을, **전역**(Global) 스코프라고 한다.

하지만, 선언된 코드 블록에서만 접근이 가능하다고 한다면, 이를 **지역**(local) 스코프라고 한다.

`var` 로 선언되는 모든 값은 **전역 스코프** 이다.

따라서, 어디에서든 **의도치 않은 변수값 변경** 을 신경써야 하며, 코드 예측이 어려워진다.

<br/>

## const, let 키워드

**단계** :

* **코드 평가** : 선언 진행
* **코드 실행** : 초기화 진행, 값 할당 진행

```mermaid
flowchart LR

subgraph 코드-평가
    1-1["1. 선언단계"]
   
        
    subgraph 변수객체-1
        foo("foo")
    end
    
        
    1-1 --- 변수객체-1
end

subgraph 코드-실행
    1-2["2. 초기화 단계"]
    2-1("3. 할당단계")

    subgraph 변수객체-2
        foo1("foo = undefined")
    end
        
    subgraph 변수-객체
        foo2("foo = 1")
    end

    1-2 --- 변수객체-2
    2-1 --- 변수-객체
end

코드-평가 --> 코드-실행
```

<br/>

이러한 흐름을 기반으로,

**코드 평가** 시점에서 **선언** 만 진행되므로, 

**변수의 할당문이 실행되기 전에 참조가 불가능하다.**

==> **ReferenceError** 발생 

**Example** : 

```javascript
console.log(a);
const a = 1;
```

**Result** : 

```text
ReferenceError: a is not defined
```

이러한 상황이 일어나는 것은, `const`, `let` 키워드가 **블록 레벨 스코프** 에 해당하기 때문이다.

**블록 레벨 스코프** 란, 코드 블록 내에서 접근 가능한 스코프를 의미한다.

변수에 한정적으로 접근이 가능하므로, **예측 가능한 범위 내** 에서 변수 변경이 일어난다.

```javascript
// 전역 스코프 
var a = 1;

function foo() {
    // 함수 레벨 스코프
    let b = 0;
    
    while(b < 3) {
        // 블록 레벨 스코프 
        console.log(b);
        b++;
    }
}

foo();
```

```text
0
1
2
```

<br/>

### const 키워드

수정이 **불가능**한 **"상수 변수"** 를 선언 할 때 사용한다.

선언과 함께 무조건 값을 할당 해 준다.

### let 키워드

재할당이 가능한 변수 타입을 의미한다.

선언과 함께 **값을 할당하지 않아도** 생성된다. 

