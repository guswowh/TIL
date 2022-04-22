# javaScript

<br />

### - 코드 관행(code convention)

  - 표기법

    - camelCase : JS
    - ParcelCase : JS(생성자 함수)


<br />

### - JS 데이터(자료형, Date Type)

  - 문자형

    1. 문자(String)

  - 원시형

    2. 숫자(Number)
    3. 불린(Boolean)
    4. null
    5. undefined
    6. <span style="color:#ccc">심볼(Symbol)</span>
    7. <span style="color:#ccc">지수, 큰(BigInt)</span>

  - 참조형

    8. 배열(Array)
    9. 객체(Object)
    10. 함수(function)

<br />

### - 문자 데이터

> 문자 데이터는 따옴표로 묶여 있어야 함!

```js
const int = int

"guswowh" + int + "guswowh"
'guswowh' + int + "guswowh"
`guswowh ${int} guswowh` // 보간
```

<br />

### - 원시형 데이터

- NaN : 숫자 데이터 / 숫자로 표기 불가!
- Boolean : True, false
- null :값을 빈값으로 __정의함__(명시적)
- nullable :값이 __정의되어 있지 않음__(암시적)
- symbol : 유일한 식별자
- BigInt : 지수, 큰(Big) 정수(Integer)
  ```js
  console.log(1n + 2n)
  console.log(Number(1n + 2n))
  ```

- 부동소수점 오류
  ```js
  const a = 0.1
  const b = 0.2
  console.log(a + b) //0.30000000000000004
  ```
  - 해결법
    ```js
    const a = 0.1
    const b = 0.2
    console.log(
      (a + b).toFixed(1)
    ) //0.3
    ```

<br />

### - 참조형 데이터

  - 배열
    - 용어
      - [] : array
      - [, , , ] : items, elments
      <br /><br />
    - 리터럴 방식
      - new Array('', '', '') // 생성자 방식
      - __[, , , ] // 리터럴 방식 : 기호로 표기__

  - 객체

    > key : 고유함, 중복이 안됨

    ```js
    const obj = {
      Key: 'Value', // { Key: 'value' }
    }
    ```

  - 함수

<br />

### - 형(Type)변환

  ```js
  const a = 123
  const b = '123'
  console.log(a == b) // true // 자동 형변환

  const c = 123
  const d = '123'
  console.log(c === d) // false // 동등 형변환
  ```

<br />

### - Truthy & Falsy

  - Truthy : 사실상 무한대와 가깝다
    - (' ')

  - Falsy
    - false
    - null
    - undefined
    - 0
    - -0
    - NaN
    - 0n
    - ('')

<br />

### - 자료형 확인

  - typeof 데이터
    ```js
    console.log(typeof '123') // "string"
    console.log(typeof 123) // "number"
    console.log(typeof true) // "boolean"
    console.log(typeof null) //"object"
    console.log(typeof undefined) //"undefined" *
    console.log(typeof Symbol('sdkjfn')) // "symbol"
    console.log(typeof 123n) // "bigint"
    console.log(typeof []) // "object"
    console.log(typeof {}) //"object"
    console.log(typeof function () {}) // "function"
    ```
  - 배열 데이터 확인
    ```js
    console.log([].constructor === Array) // true
    console.log(Array.isArray([])) // true
    ```

  - 모든 확인
    ```js
    function checkType(data) {
      return Object.prototype.toString.call(data).slice(8, -1)
    }
    ```

<br />

### - 변수
  - const : 상수
    - 유효범위 : 블록 레벨
    - 재할당 : X
    - 중복 선언 : X
    - 호이스팅(Hoisting) : X
    - 전역 등록 : X
  - let : 변수(호이스팅 되지 않는다)
    - 유효범위 : 블록 레벨
    - 재할당 : O
    - 중복 선언 : X
    - 호이스팅(Hoisting) : X
    - 전역 등록 : X
  - var : 변수(호이스팅 된다)
    - 유효범위 : 함수 레벨
    - 재할당 : O
    - 중복 선언 : O
    - 호이스팅(Hoisting) : O
    - 전역 등록 : O
  <br /><br />

  > 변수 사용법 : const로 선언하고 "재할당"이 필요할 때 let으로 변경
  
  > 전역(Global) 선언시 전역 객체(`window`)의 속성으로 등록

<br />

### - 함수
```js
// 함수 선언 : 호이스팅 된다.
function abc() {

}

// 함수 표현 (익명함수) : 호이스팅 되지 않는다.
const abc = function () {

}
```

<br />

### - 함수
```js
function hello(){} // 기명함수

function (){} // 익명함수
```

<br />

### - new Function()

> 생성자 함수 호출로 함수를 만드는 법! (자주 안씀.)

  ```js
  const sum = new Function('a', 'b', 'console.log(a + b)')
  sum(2, 4)
  ```

<br />

### - 반환과 종료

`return`: `undefined`

`return`: 키워드를 사용하면 함수 종료

<br />

### - 선언과 표현

<br />

### - 매개변수 패턴

- 매개변수 기본값
  - 문법 : (a = 기본값, b = 기본값)
  <br /><br />
- 구조 분해 할당(Destructuring assignment)
  - 구조 분해 할당 구문은 배열이나 객체의 속성을 분해하여
    그 값을 변수에 담을 수 있게 하는 표현식
    <br /><br />
- 나머지 매개변수(Rest parameter) : arguments 대신 사용을 권장
  - ...매개변수 : "전계연산자"를 사용하여 나머지 인자를 받는다.

- `arguments`객체
  - 함수로 들어오는 모든 인수를 가지고 있는 암시적인 객체

<br />

### - IIFE

  - Immediately-Invoked Function Expression(직시 실행 함수)

```js
;(익명함수)()
;(익명함수())
```

<br />

### - 호이스팅

<br />

### - 콜백 함수(Callback function) === 함수 데이터
  - 함수를 인수로 사용되는 함수

<br />

### - this

- 일반 함수에서 `this`는 호출되는 위치에서 정의됨!
- 화살표 함수에서 `this`는 자신이 선언된 함수(렉시컬) 범위에서 정의됨

  > 렉시컬영역 : 자신을 감싸고 있는영역

<br />

### - 비교 연산자

연산자 | 이름
--|--
`==` | 동등 : 형변환으로 인하여 사용하지 않는다
`!=` | 부등
`===` | 일치
`!==` | 불일치
`a > b`
`a >= b`
`a < b`
`a <= b`

<br />

### - 논리 연산자

연산자 | 이름
--|--
a && b | 그리고(And) : 가장 먼저 찾은 Falsy를 반환, 못 찾으면 마지막..반환
a &#124;&#124; b | 또는(Or) : 가장 먼저 찾은 Truthy를 반환, 못 찾으념 마지막..반환
!a | 부정(Not) : a가 Truthy면 `false`로, Falsy면 `true`로 바뀜

<br />

### - 삼항 연산자

- 문법 : 조건 ? 2항 : 3항

<br />

### - if문

  - 조건에 따라 switch문으로 바꿀 수 없을 수 있다.

  종류 | 문법
  --|--
  if문 | if() {}
  if else문 | if() else {}
  else if문 | else if() {}

<br />

### - switch문 : 
  - 조건이 어떤 값으로 딱 떨어질 때
  - 언제나 if문으로 바꿀 수 있다.

  종류 | 문법
  --|--
  switch문 | switch()
  switch case braek문 | switch() { case "값": braek }
  switch default문 | switch() { default: }

<br />

### - for문 

  종류 | 문법
  --|--
  반복문 | for(시작조건; 종료조건; 변화조건) {}