# javaScript NODE, DOM API

<br />

## - Element vs Node
  > Node
  - 엘리먼트의 그룹

  > Element
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

## -  DOM API

  <br />

  > 선택자

  문법 | 내용
  --|--
  엘리먼트.querySelector('선택자') | 도큐먼트에서 특정 css 선택자를 찾아서 반환한다.
  엘리먼트.getElementById('아이디') | 도큐먼트에서 특정 아이디를 찾아서 반환한다.
  <br />

  > 생성자

  문법 | 내용
  --|--
  엘리먼트.createElement('엘리먼트') | 특정 html 엘리먼트를 메모리에 생성한다.

  > id

  문법 | 내용
  --|--
  엘리먼트.id | html요소의 아이디 값을 문자열로 반환한다.
  <br />

  > class

  문법 | 내용
  --|--
  엘리먼트.className | html요소의 클레스 값을 문자열로 반환한다.
  엘리먼트.className.split(' ') | 멀티 클레스 값을 스플릿 메소드로 끊어서 문자열로 반환한다.
  엘리먼트.classList.add('클레스이름') | html요소의 클레스를 추가한다.
  엘리먼트.classList.remove('클레스이름') | html요소의 클레스를 삭제한다.
  엘리먼트.classList.contains('클레스이름') | html요소의 해당 클레스가 있는지 확인한다.

  - 자바스크립트로 추가한 클레스명(카멜케이스)을 케밥케이스로 변경할 때 사용하는 라이브러리  

    > [lodash link](https://lodash.com/docs/4.17.15#kebabCase)
    ```js
    _.kebabCase('Foo Bar');
    // => 'foo-bar'
    
    _.kebabCase('fooBar'); 
    // => 'foo-bar'
    
    _.kebabCase('__FOO_BAR__');
    // => 'foo-bar'
    ```

  <br />

  > Node, Element

  문법 | 내용
  --|--
  엘리먼트.parentNode | 특정요소를 감싸고 있는 부모 요소를 찾아서 반환한다.
  엘리먼트.previousElementSibling | 이전 형제 요소를 찾아서 반환한다.
  엘리먼트.nextElementSibling | 다음 형제 요소를 찾아서 반환한다.
  <br />

  > 엘리먼트 컨텐츠 제어
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

  > 엘리먼트 속성 제어
  - getter

    문법 | 내용
    --|--
    엘리먼트.getAttribute('속성') | 특정 엘리먼트 요소의 속성을 반환한다.

  - setter

    문법 | 내용
    --|--
    엘리먼트.setAttribute('속성', '값') | 특정 엘리먼트 요소의 속성을 할당한다.


  > 엘리먼트 구조에 특정 요소 추가

  문법 | 내용
  --|--
  엘리먼트.prepend(' ... ') | 특정 엘리먼트 내부 구조 앞쪽에 특정 요소를 문자열로 추가할 수 있다.
  엘리먼트.append(' ... ') | 특정 엘리먼트 내부 구조 뒤쪽에 특정 요소를 문자열로 추가할 수 있다.
  <br />

  > JSON

  JSON 문법 | 내용
  --|--
  데이터.JSON.stringify(데이터이름) | 문자열을 JSON 문법으로 반환된 문자 데이터 반환
  데이터.JSON.parse(데이터이름) | JSON 문법으로 반환된 문자 데이터를 js문법의 데이터로 변환
  - >페턴  

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

  > 엘리먼트 데이터 속성 제어
  - 자바스크립트는 html에서 __데쉬케이스로 작성된__ 이름을 __카멜케이스로 변경__ 하여 조회 한다. 

    > html

      문법 | 내용
      --|--
      `<tag data-user-name=''>` | user-name이란 빈 데이터를 선언

    > javaScript

      - getter

        문법 | 내용
        --|--
        const userName = { ... } | html 엘리먼트의 data 속성명 user-name에 데이터를 메모리에 추가

      - setter

        문법 | 내용
        --|--
        엘리먼트.dataset.userName | html 엘리먼트에 데이터를 추가한다. 

  > 요소의 크기
  
  문법 | 내용
  --|--
  엘리먼트.clientWidth | 요소의 너비 반환
  엘리먼트.clientHeight | 요소의 높이 반환

  > 요소의 렌더링 정보
  
  문법 | 내용
  --|--
  엘리먼트.getVoundingClientRect() | 요소의 사각형 정보를 알 수 있다.
  
  - 속성이 아닌 함수 임으로 사용할 때 주의를 요함

> 이벤트 핸들러

문법 | 내용
--|--
addEventListener(타입, 함수());

  - 타입

    타입 | 내용
    --|--
    click | 해당 요소를 클릭 했을 때
    input.target.value | 사용자가 입력 했을 때의 값을 반환
    keydown | 키를 누를 때
    keyup | 키를 땔 때

  - 한글을 입력시 두번 선택되는 이슈 해결법

    - isComposing

      문법 | 내용
      --|--
      이벤트함수.isComposing | 입력을 __받을 때 true__ 입력을 enter로 __종료 할 때 false__

    > 해결 패턴
    ```js
    inpuEl.addEventListener('keydown', event => {
      if (event.isComposing) return
      console.log(event.target.value)
    })
    ```

