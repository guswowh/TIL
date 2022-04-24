# javaScript practice

<br />

### - 콜백 함수

```js
// 함수sum은 매개변수 a, b를 받는다.
// 매개변수 a, b를 더한 값을 출력한다.
function sum(a, b) { 
  console.log(a + b) 
}

// sum 함수표현
console.log(sum) 

// 함수 runFn은 매개변수 callback을 받는다
// 매개변수 callback은 반환값 2, 4를 갖는다.
function runFn(callback) { 
  callback(2, 4)
}

// 함수 runFn에 sum함수를 호출한다
callFn(sum)
```

<br />

### - 함수 리턴 : 함수 표현을 자신에게 반환한다.
 > 함수 리턴이 없을 때 값으로 undefined를 반환한다.

```js
// sum이란 함수는 매개변수 a, b를 갖는다
// 매개변수 a, b를 더한 값을 함수에 리턴한다.
function sum(a, b) {
  return a + b
}

// sum 함수 출력
console.log(sum)

// 변수 res는 sum 함수에 인자 2, 4를 반환한다.
const res = sum(2, 4)

// 변수 res가 갖고 있는 반환값을 호출한다.
console.log(res)

// 값은 6이다
```

<br />

### - 매개변수 기본 값 : 매개변수에 "변수 = 값"으로 표현한다.

```js
function sum(a = 1, b = 3) {
  return a + b
}

console.log(sum(2, 4))
console.log(sum(5, 7))
console.log(sum(4))
console.log(sum())
```

<br />

### - 구조 분해 할당(Destructuring assignment)

```js
// 객체 user는 key로 name, age를 갖는다.
const user = {
  name: 'guswowh',
  age: 85
}

console.log(user) // user 객체 확인
```
> 객체 구조 분해하여 객체의 키값을 변수로 할당한다
```js
// 함수 getName은 객체 user의 key값을 매게변수로 받는다
// 매게변수 name과 age를 배열로 리턴한다.
function getName({ name, age }) {
  return [name, age]
}

console.log(getName) //getName 함수 확인

// 함수 getName에 user객체 호출한다.
console.log(getName(user))
```

<br />

### - 생성자 함수

```js
// 생성자함수 User는 매개변수로 first, last를 받는다
// this는 User이며 아래 객체 프로퍼티를 생성한다.
function User(first, last) {
  this.firstName = first
  this.lastName = last
}

// 클레스 User의 프로토타입에 getFullName 메서드를 할당한다.
User.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`
}

// 생성자 함수 반환 값을 변수에 할당(인스턴스) 한다
const guswowh = new User('guswowh', 'Cho')
const amy = new User('Amy', 'Clarke')
const neo = new User('Neo', 'Smith')

// 인스턴스의 프로퍼티에서 getFullName 함수를 호출한다.
console.log(guswowh.getFullName())
console.log(amy.getFullName())
console.log(neo.getFullName())

```
```js
// 익명함수는 매개변수 msg를 받아 변수 abc에 할당한다
// 함수를 리턴하여 클로저를 발생시켜 매개변수 msg를 보존한다
// 매개변수 msg를 출력한다
const abc = function (msg) {
  return function () {
    console.log(msg) 
  }
}

// 클레스 스트링의 프로토타입 guswowh에 함수의 반환값을 할당한다.
String.prototype.heropy = abc('Good~')

// 문자열은 클레스 스트링과 비슷하다 이는 자바스크립트라는 언어적 특성이다.
// 문자열은 스트링 클레스에서 guswowh메서드를 찾고 프로토타입에서 guswowh메서드를 찾고 호출한다.
'test'.heropy()
```