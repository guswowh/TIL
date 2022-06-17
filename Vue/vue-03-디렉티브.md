## 디렉티브
> 구조
```html
<template>
  <tag v-디렉티브=""></tag>
</template>
```

***

## `v-one` :  단 한번만 렌더링
브라우저에 한번만 렌더링하며 반응성을 갖지 않는다.

***

## `v-html` : 원시 html
문자열 데이터를 html 구조로 변환해 준다.

  > 구조
  ```html
  <template>
    <tag v-html="데이터명"></tag>
  </template>
  ```
  ```html
  <script>
    const 옵션명 = {
      data() {
        return {
          데이터명: '<tag> html 구조 </tag>'
        }
      }
    }
  </script>
  ```
  
  __취약점__
  -  XSS 보안에 취약하여, 반드시 방어코드를 작성 하여야한다.

***

## 단방향 데이터 바인딩
데이터가 한쪽 방향으로 전달되는 구조

### `v-bind` : 단방향 데이터 바인딩
데이터가 한쪽 방향으로 전달되는 구조

  > 구조
  ```html
  <template>
    <tag v-bind:데이터명="데이터"></tag>
  </template>
  ```
  ```html
  <script>
    const 옵션명 = {
      data() {
        return {
          데이터명: 데이터
        }
      }
    }
  </script>
  ```

  __`v-bind:html속성=“데이터명”`__
  - html 속성에 데이터 전달  

  __`v-bind:[데이터이름]`__
  - 데이터 전달

  __html 클래스. 바인딩__
  > 일반 구문
  ```html
  <template>
    <tag v-bind:class=“데이터명"></tag>
  </template>
  ```
  
  > 객체 구문
  ```html
  <template>
    <tag v-bind:class=“{ 데이터명: 데이터, … }></tag>
  </template>
  ```
  - 데이터의 boolean을 판별 한다.

  > 배열 구문
  ```html
  <template>
    <tag v-bind:class=“[데이터명-01, 데이터명-02 …]”></tag>
  </template>

  <script>
    data() {
      return {
        데이터명-01: '데이터',
        데이터명-02: '데이터'
      }
    }
  </script>
  ```

  > 컴포넌트 구문
  - 추가 예정

  __인라인 스타일 바인딩__
  > 객체 구문
  ```html
  <template>
    <tag v-bind:style=“{ 속성명: 데이터명, … }”></tag>
  </template>

  ```

  > 배열 구문
  ```html
  <template>
    <tag v-bind:style=“[데이터명-01, 데이터명-02 …]”></tag>
  </template>

  <script>
    data() {
      return {
        데이터명-01: '데이터',
        데이터명-02: '데이터'
      }
    }
  </script>
  ```
  - 스타일 구문 표기법
    - 케밥 케이스 혹은 카멜 케이스로 작성 해야한다.
    - 케밥 케이스 사용시 따옴표로 묶어서 사용한다.

***

## 양방향 데이터 바인딩
데이터가 양 방향으로 주고 받을 수 있는 구조로  
사용자가 실제 입력한 데이터를 갱신해준다.

### `v-model` : 폼 입력 바인딩

  __병렬방식__
  > html
  ```html
  <template>
    <input
      type="text"
      v-model="데이터명" />
    <input
      type="checkbox"
      v-model="체크" />
  </template>

  <script>
    data() {
      return {
        데이터명: '문자',
        체크: false
      }
    }
  </script>
  ```
  - `type=“checkbox”`와 `type=“select”` 태그에는  
  `v-model=“불린 데이터명”`를 사용

  __직렬방식__ 
  > html
  ```html
  <template>
    <input
      type="test"
      v-bind:value="데이터명"
      v-on:input="데이터명 = $event.target.value" />
  </template>

  <script>
    data() {
      return {
        데이터명: '문자'
      }
    }
  </script>
  ```
  - `type=“checkbox”` 태그에는 `v-bind:checked` 와 `v-on:change` 이벤트 사용
  - `type=“select”` 태그에는 `v-bind:value` 와 `v-on:change` 이벤트 사용
  > Note : 한글, 일본어, 중국어 입력시 직렬방식 사용

  __수식어__
  - `.lazy` : 사용자가 입력을 완료하면 갱신된다.
    - 직렬방식 사용시 `change`이벤트를 사용하면 된다.
  - `.number` : 사용자가 입력한 데이터를 숫자형 데이터로 형변환 한다.
  - `.trim` : 사용자가 입력한 데이터의 앞뒤 공백 문자를 제거하여 반환한다.

***

## `v-if` : 조건부 렌더링
- Truth일 경우 화면에 렌더링한다.
- Falsy일 경우 화면에 렌더링하지 않는다.

  __`v-else-if`, `v-else`__
  - `v-if`밑에 붙어 있어야 실행된다.
  > 구문
  ```html
  <template>
    <tag v-if="불린데이터">문자</tag>
    <tag v-else-if="불린데이터">문자</tag>
    <tag v-else="불린데이터">문자</tag>
  </template>
  ```

  __`<template></template>`__
  - 두개 이상의 엘리먼트를 사용해야 할때 템플릿 테그로 묶어준다
    - 템플릿 테그는 화면에 렌더링 되지 않는다.
  > 구문
  ```html
  <template>
    <template v-if="불린데이터">
      <tag>문자</tag>
      <tag>문자</tag>
      <tag>문자</tag>
    </template>
    <tag v-else-if="불린데이터"></tag>
    <tag v-else="불린데이터"></tag>
  </template>
  ```

  __`v-show`__
  > 구문
  ```html
  <template>
    <tag v-show="불린데이터">문자</tag>
  </template>
  ```
  - Truth일 경우 `display: block`
  - Falsy일 경우 `display: none`

***

## `v-for` : 리스트 렌더링

  __html엘리먼트를 반복 할 수 있다.__
  > 구문
  ```html
  <template>
    <tag v-for=“아이템 in 아이템스></tag>
  </template>
  ```

  __매개변수__
  > 구문
  ```html
  <template>
    <tag v-for=“(아이템, 매개변수) in 아이템스”></tag>
  </template>
  ```
  - 첫 번째 인수 : 반복되는 아이템스의 아이템을 받는다.
  - 두 번째 인수 : 각 아이템의 배열의 인덱스 번호와 객체의 키 값을 반환 한다.

  __복합 엘리먼트__
  > 구문
  ```html
  <template>
    <template v-for=“(아이템, 매개변수) in 아이템스”>
      <tag>문자</tag>
      <tag>문자</tag>
      <tag>문자</tag>
    </template>
  </template>
  ```
  - 두개 이상의 html엘리먼트를 사용해야 할때 템플릿 테그로 묶어서 반복 출력 할 수 있다.
  - 템플릿 태그는 화면에 렌더링 되지 않는다.

  __고유값__
  > 구문
  ```html
  <template>
    <tag v-for="" :key=“아이템.고유값”></tag>
  </template>
  ```
  - 리스트 렌더링 시 반드시 고유값을 부여해줘야 한다.

***

## `v-on` : 이벤트 핸들링

  __자바스크립트 addEventListener와 동일한 기능__
  > 구문
  ```html
  <template>
    <tag v-on:click="함수명 $event"></tag>
  </template>

  <script>
    data() {
      return {
        데이터: 데이터
      }
    },
    methods: {
      함수명(이벤트 event) {
        데이터 + '문자'
        console.log(event)
      }
    }
  </script>
  ```
  __매개변수__
  - 첫 번째 인수 : 해당 이벤트 객체를 반환한다.
  - 두 번째 인수 : 함수 호출 전달 인자를 받는다.

  __v-on 내장 API__
  - `$event` : 호출 함수의 두번째 인수로, 해당 이밴트 객체를 할당한다.

  __인라인 메소드 핸들러__
  - `<tag v-on:이벤트명=“함수명”>`
    - 인수를 재공 하지 않고 연결된 메소드 실행
  - 매소드의 첫번째 매개 변수로 해당 이벤트 객체가 반환된다.
  - 매개 변수로 해당 이벤트 객체를 `$event`에 담아서 사용 할 수 있다.

  __복합 이벤트 핸들러__
  - `<tag v-on:키 수식어=“함수명(), 함수명()”>` : 한개 이상의 여러개의 함수를 동시에 실행 할 수 있다.
  > [__자바스크립트 이벤트 참조__](https://developer.mozilla.org/ko/docs/Web/Events)  

  __이벤트 수식어__
  - `.stop` : 이벤트 버블링 방지
  - `.capture` : 이벤트 켑처링 방지
  - `.prevent` : Vue 기본동작 방지
  - `.self` : event.target 과 event.currentTarget이 같을 때 동작
  - `.once` : 이벤트 한번만 동작
  - `.passive` : 화면을 움직이는 동작과 로직을 처리하는 동작을 분리

  __키 명령어__
  - .enter
  - .tab
  - .delete (“Delete” 와 “Backspace” 키 모두를 캡처합니다)
  - .esc
  - .space
  - .up
  - .down
  - .left
  - .right
  > 구문
  ```html
  <button v-on:키-명령어>
  ```

  __시스템 수식어__
  - .ctrl
  - .alt
  - .shift
  - .meta : 동작을 명확하게 보장하지 않는다.
  > 구문
  ```html
  <button v-on:키-명령어.시스템-수식어>
  ```

  __exact 수식어__
  - 명령어와 수식어만 함깨 눌렀을 때 동작
  > 구문
  ```html
  <button v-on:키-명령어.시스템-수식어.exact>
  ```

<br />

### `v-slot, <slot>` : 컴포넌트 컨텐츠 수신
상위 컴포넌트의 컨텐츠(내용)를 하위 컴포넌트의 컨텐츠(내용)로 갱신 하거나  
상위 컴포넌트의 컨텐츠(내용)가 없을 때 하위 컴포넌트 내용으로 갱신 할 수 있다.

  __기본구조__
  > 상위 컴포넌트 html
  ```html
  <template>
    <컴포넌트>컨텐츠</컴포넌트>
  </template>
  ```
  > 하위 컴포넌트 html
  ```html
  <컴포넌트>
    <slot>컨텐츠</slot>
  </컴포넌트>
  ```

  __`v-slot`__ : 이름을 갖는 슬롯
  - `name`속성을 이용하여 특정 요소에 접근 할 수 있다
  > 상위 컴포넌트 html
  ```html
  <template v-slot:슬롯명>
    <컴포넌트>컨텐츠</컴포넌트>
  </template>
  ```
  > 하위 컴포넌트 html
  ```html
  <컴포넌트>
    <slot name="슬롯명">컨텐츠</slot>
  </컴포넌트>
  ```

***

## `v-is` : DOM 템플릿 파싱 주의사항
`ul li`테그와 같이 세트 테그 조합으로 이루어진 테그는  
컴포넌트를 자식 자식 요소로 마크업 했을때 에러가 발생하는데  
이때 발생 에러는 기능적 에러가 아닌 html 구조에서 발생하는 에러로  
다음과 같이 사용하면 에러를 막을 수 있다.

  >html
  ```html
  <ul>
    <li v-is="'컴포넌트명'"></li>
  </ul>
  ```

***

## 디렉티브 약어

  __`:`__
  - `v-bind`의 약어

  __`@`__
  - `v-on`의 약어

  __`#`__
  - `v-slot`의 약어

***