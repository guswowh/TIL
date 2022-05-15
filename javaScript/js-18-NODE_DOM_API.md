# javaScript NODE, DOM API

<br />

## Element vs Node

### Node
  - 엘리먼트의 그룹

### Element
  - 그룹의 요소 들

> 예제
```html
<div>
  123
  <span>abc</span>
</div>
```
```js
const divEl = document.querySelector('div')
console.log('Element: ', divEl)

const div = document.querySelectorAll('div')
console.log('', div)

/*
"Element: "
<div>
  123
  <span>abc</span>
</div>

"" // [object NodeList] (1)
["<div/>"]
*/

```

<br />

##  DOM API

<br />

### 선택자

  문법 | 내용
  --|--
  엘리먼트.querySelector('선택자') | 도큐먼트에서 특정 css 선택자를 찾아서 반환한다.
  엘리먼트.getElementById('아이디') | 도큐먼트에서 특정 아이디를 찾아서 반환한다.
  <br />

### 생성자

  문법 | 내용
  --|--
  엘리먼트.createElement('엘리먼트') | 특정 html 엘리먼트를 메모리에 생성한다.
  <br />

### id

  문법 | 내용
  --|--
  엘리먼트.id | html요소의 아이디 값을 문자열로 반환한다.
  <br />

### class

  문법 | 내용
  --|--
  엘리먼트.className | html요소의 클레스 값을 문자열로 반환한다.
  엘리먼트.className.split(' ') | 멀티 클레스 값을 스플릿 메소드로 끊어서 문자열로 반환한다.
  엘리먼트.classList.add('클레스이름') | html요소의 클레스를 추가한다.
  엘리먼트.classList.remove('클레스이름') | html요소의 클레스를 삭제한다.
  엘리먼트.classList.contains('클레스이름') | html요소의 해당 클레스가 있는지 확인한다.
  <br />

  - 자바스크립트로 추가한 클레스명(카멜케이스)을 케밥케이스로 변경할 때 사용하는 라이브러리  

    > [lodash →](https://lodash.com/docs/4.17.15#kebabCase)
    ```js
    _.kebabCase('Foo Bar');
    // => 'foo-bar'
    
    _.kebabCase('fooBar'); 
    // => 'foo-bar'
    
    _.kebabCase('__FOO_BAR__');
    // => 'foo-bar'
    ```

  <br />

### Node, Element

  문법 | 내용
  --|--
  엘리먼트.parentNode | 특정요소를 감싸고 있는 부모 요소를 찾아서 반환한다.
  엘리먼트.previousElementSibling | 이전 형제 요소를 찾아서 반환한다.
  엘리먼트.nextElementSibling | 다음 형제 요소를 찾아서 반환한다.
  <br />

### 엘리먼트 컨텐츠 제어
  - getter

    문법 | 내용
    --|--
    엘리먼트.innerHTML | 특정 엘리먼트의 내부 html 구조를 문자열로 반환한다.
    엘리먼트.textContent | 특정 엘리먼트의 내용을 문자열로 반환한다.
    <br />

  - setter

    문법 | 내용
    --|--
    엘리먼트.innerHTML = ' ... ' | 특정 엘리먼트의 내부 html 구조를 수정 할 수 있다.
    엘리먼트.textContent = ' ... ' | 특정 엘리먼트의 내용을 수정할 수 있다.
    <br />

### 엘리먼트 속성 제어
  - getter

    문법 | 내용
    --|--
    엘리먼트.getAttribute('속성') | 특정 엘리먼트 요소의 속성을 반환한다.
    <br />

  - setter

    문법 | 내용
    --|--
    엘리먼트.setAttribute('속성', '값') | 특정 엘리먼트 요소의 속성을 할당한다.
    <br />

### 엘리먼트 구조에 특정 요소 추가

  문법 | 내용
  --|--
  엘리먼트.prepend(' ... ') | 특정 엘리먼트 내부 구조 앞쪽에 특정 요소를 문자열로 추가할 수 있다.
  엘리먼트.append(' ... ') | 특정 엘리먼트 내부 구조 뒤쪽에 특정 요소를 문자열로 추가할 수 있다.
  <br />

### JSON
  - ㅁㅇㄴㄹ

    문법 | 내용
    --|--
    데이터.JSON.stringify(데이터이름) | 문자열을 JSON 문법으로 반환된 문자 데이터 반환
    데이터.JSON.parse(데이터이름) | JSON 문법으로 반환된 문자 데이터를 js문법의 데이터로 변환
    <br />
    > 예제

    ```js
    const divEl = document.querySelector('div')

    const user = {
      name: 'guawowh',
      age: 85
    }
    divEl.dataset.user = JSON.stringify(user)

    console.log(JSON.parse(divEl.dataset.user))
    ```
  <br />

### 엘리먼트 데이터 속성 제어
  - 자바스크립트는 html에서 __데쉬케이스로 작성된__ 이름을 __카멜케이스로 변경__ 하여 조회 한다. 

#### html

  문법 | 내용
  --|--
  `<tag data-user-name=''>` | user-name이란 빈 데이터를 선언
  <br />

#### javaScript

  - getter

    문법 | 내용
    --|--
    const userName = { ... } | html 엘리먼트의 data 속성명 user-name에 데이터를 메모리에 추가
    <br />

  - setter

    문법 | 내용
    --|--
    엘리먼트.dataset.userName | html 엘리먼트에 데이터를 추가한다. 
    <br />

### 요소의 크기
  
  문법 | 내용
  --|--
  엘리먼트.clientWidth | 요소의 너비 반환
  엘리먼트.clientHeight | 요소의 높이 반환
  <br />

### 요소의 렌더링 정보
  
  문법 | 내용
  --|--
  엘리먼트.getVoundingClientRect() | 요소의 사각형 정보를 알 수 있다.
  ---
  - 속성이 아닌 함수 임으로 사용할 때 주의를 요함
  ---
  <br />

### 이벤트 핸들러

문법 | 내용
--|--
addEventListener(타입, 함수(){}, { 옵션 }) | 이벤트를 제어 하는 함수
removeEventListener(타입, 함수(){}, { 옵션 }) | 이벤트를 제거 하는 함수
<br />

  - 타입

    타입 | 내용
    --|--
    click | 해당 요소를 클릭 했을 때
    input.target.value | 사용자가 입력 했을 때의 값을 반환
    keydown | 키를 누를 때
    keyup | 키를 땔 때
    <br />

  - 옵션

    옵션 | 내용
    --|--
    capture: true | __이벤트 켑처링 현상__ 발생시 해당 이벤트 실행
    once: true | 이벤트를 단 한번만 실행한다.
    passive: true | 화면을 움직이는 동작과 로직이 움직이는 동작을 분리 한다.
    <br />

    주의사항 | 내용
    --|--
    capture | 삭제하려는 이벤트에 capture 옵션이 걸려 있는경우 반드시 이벤트 제거 함수에  capture 옵션이 걸려 있어야 한다.
    <br />

    > capture, once 예제
    ```js
    const parentEl = document.querySelector(".parent")
    const childEl = document.querySelector(".child")

    window.addEventListener("click", () => {
      console.log("Window")
    }, {
      capture: true,
      once: true
    })
    document.body.addEventListener("click", () => {
      console.log("Body!")
    })
    parentEl.addEventListener("click", () => {
      console.log("Parent!")
    })
    childEl.addEventListener("click", () => {
      console.log("Child!")
    })
    ```
    > [코드펜 →](https://codepen.io/bbxkoulf/pen/QWQKzwM?editors=0012)

    <br />

    > passive 예제
    ```js
    const parentEl = document.querySelector(".parent")
    const childEl = document.querySelector(".child")

    parentEl.addEventListener("wheel", event => {
      for (let i = 0; i < 10000; i += 1) {
        console.log(event)
      }
    }, {
      passive: true
    })
    ```
    > [코드펜 →](https://codepen.io/bbxkoulf/pen/eYVdXPy?editors=0010)

    <br />

  - 이벤트 위임(Event Deligation)
    - 이벤트 __버블링 현상__ 을 이용한 효율적인 데이터 처리 방법

      > 예제
      ```js
      const parentEl = document.querySelector(".parent")
      const childEl = document.querySelector(".child")

      const ulEl = document.querySelector("ul")

      // event 객체데이터 확인
      ulEl.addEventListener("click", event => {
        console.log(event)
      })

      // event 객체데이터의 타겟 실행
      ulEl.addEventListener("click", event => {
        console.log(event.target)
      })
      ```
      > [코드펜 →](https://codepen.io/bbxkoulf/pen/wvyzNOb?editors=0010)
      
      <br />

  - stopPropagation

    문법 | 내용
    --|--
    이벤트함수.stopPropagation() | 이벤트 버블링 현상을 멈추는 메소드
    <br />

    > 예제
    ```js
    const parentEl = document.querySelector(".parent")
    const childEl = document.querySelector(".child")

    childEl.addEventListener("click", event => {
      event.stopPropagation()
      console.log("child!")
      
    })
    parentEl.addEventListener("click", event => {
      console.log("Parent!")
    })
    ```
    > [코드펜 →](https://codepen.io/bbxkoulf/pen/OJQRqOJ?editors=0011)

    <br />

  - preventDefault

    문법 | 내용
    --|--
    이벤트함수.preventDefault() | 기본동작을 정지시키고 새로운 기능을 추가 할 수 있다.
    <br />

    > 예제
    ```js
    const parentEl = document.querySelector(".parent")
    const childEl = document.querySelector(".child")

    parentEl.addEventListener("wheel", event => {
      event.preventDefault()
    })
    ```
    > [코드펜 →](https://codepen.io/bbxkoulf/pen/gOvwEay?editors=0010)

    <br />

  - 한글을 입력시 두번 선택되는 이슈 해결법

    - isComposing

      문법 | 내용
      --|--
      이벤트함수.isComposing | 입력을 __받을 때 true__ 입력을 enter로 __종료 할 때 false__
      <br />

    > 해결 패턴
    ```js
    inpuEl.addEventListener('keydown', event => {
      if (event.isComposing) return
      console.log(event.target.value)
    })
    ```

