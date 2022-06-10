import { nanoid } from 'https://cdn.jsdelivr.net/npm/nanoid/nanoid.js'

## Vue 애플리케이션 생성
  > html
  ```html
  <tag id="id명"></tag>
  ```

  > js
  ```js
  const 변수명 = {
    data() {
      return {
      	...
      }
    }
  }
  Vet.createApp(변수명).mount(“#id명”)
  ```
  - 변수에 할당하는 패턴도 사용 할 수 있다.
    ```js
    const app = Vue.createApp(변수명)
    app.mount('#id명')
    ```
  - 통상 최상위 컴포넌트 변수명은 "App"으로 사용한다.

***

## 기본 구조 테그
  __`<template>`__
  - html 구조를 작성 할 수 있다.  
    > Note : 최상위 요소 템플릿은 v-if를 사용 할 수 없다.
    
  __`<script>`__
  - 자바스크립트를 작성 할 수 있다.

  __`<style>`__ 
  - css를 작성 할 수 있다.
  - 옵션
    - scoped : 부여된 컴포넌트의 값이 고유해 진다.
      - 싱글파일 컨포는트 사용시 필수로 부여 해주어야 한다.
    - lang : scss

***

## API 옵션
  __data__
  - 데이터는 함수여야 함다.

  __computed__
  - 반응형 데이터를 기준으로 계산된 데이터를 반환 한다.
  - Getter 와 Setter를 사용 할 수 있다.
  > [Computed Caching](https://v3.ko.vuejs.org/guide/computed.html#computed-%E1%84%89%E1%85%A9%E1%86%A8%E1%84%89%E1%85%A5%E1%86%BC%E1%84%8B%E1%85%B4-%E1%84%8F%E1%85%A2%E1%84%89%E1%85%B5%E1%86%BC-vs-%E1%84%86%E1%85%A6%E1%84%89%E1%85%A5%E1%84%83%E1%85%B3)

  __methods__
  - 일반 함수여야 한다.

  __watch__
  - 반응형 데이터의 변경사항을 감지한다.
  - `newValue`, `oldValue` 내장 객체데이터를 사용 할 수 있다.  

    __매개변수__
    - `newValue` : 변경후 데이터
    - `oldValue` : 변경전 데이터

    __옵션__
    - `deep: boolean` : 깊게 감시, 데이터의 아이템까지 변경을 감지 할 수 있다.

    > [공식문서 →](https://v3.ko.vuejs.org/api/options-data.html#watch)

  __props__
  - 자식 컴포넌트에 데이터 전달

  __emits__
  - 부모 컴포넌트에 데이터 전달
***

## 데이터 접근
  __this.데이터명__
  - Vue에서 데이터에 접근하기 위해서는 `this`키워드를 사용해야 한다.  
  여기서 `this`는 해당 컨포넌트를 가리킨다.
  - this키워드가 없을 시 전역 변수

***

## 디렉티브

###  단방향 데이터 바인딩
  데이터가 한쪽 방향으로 전달되는 구조

  - `v-bind:html속성=“데이터명”` : html 속성에 데이터 전달  
  - `v-bind:[데이터이름]` : 데이터 전달

  __html 클래스. 바인딩__
  - 객체 구문
    - `v-bind:class=“{ html속성: 데이터명, … }”` : boolean을 판별 한다.
  - 배열 구문
    - `v-bind:class=“[객체데이터, …]”` : boolean을 판별 한다.
  - 컴포넌트 구문
    - 

  __인라인 스타일 바인딩__
  - 객체 구문
    - `v-bind:style=“{ html속성: 데이터명, … }”`
      - html속성명 : 케밥 케이스 혹은 카멜 케이스로 작성 해야한다.
  - 배열 구문
    - `v-bind:style=“[객체데이터, …]”`

***

### 양방향 데이터 바인딩
  데이터가 양 방향으로 주고 받을 수 있는 구조로  
  사용자가 실제 입력한 데이터를 갱신해준다.

#### 폼 입력 바인딩

  __병렬방식__
  - `v-model=“데이터명”` : 
  - `type=“checkbox” v-model=“불린 데이터명”`
  - `type=“select” v-model=“불린 데이터명”`

  __직렬방식__ 
  > html
  ```html
  <input v-bind:value=“데이터명” v-on:input=“데이터명” = $event.target.value />
  ```
  - `type=“input”` 태그에는 `value` 와 `input` 이벤트 사용
  - `type=“checkbox”` 태그에는 `checked` 와 `change` 이벤트 사용
  - `type=“select”` 태그에는 `value` 와 `change` 이벤트 사용
  > Note : 한글, 일본어, 중국어 입력시 직렬방식 사용

  __수식어__
  - `.lazy` : 사용자가 입력을 완료하면 갱신된다.
    - 직렬방식 사용시 `change`이벤트를 사용하면 된다.
  - `.number` : 사용자가 입력한 데이터를 숫자형 데이터로 형변환 한다.
  - `.trim` : 사용자가 입력한 데이터의 앞뒤 공백 문자를 제거하여 반환한다.

***

### 조건부 렌더링

  __`v-if`__
  - Truth일 경우 화면에 렌더링한다.
  - Falsy일 경우 화면에 렌더링하지 않는다.

  __`v-else-if`, `v-else`__
  - `v-if`밑에 붙어 있어야 실행된다.

  __`<template>`__
  - 두개 이상의 엘리먼트를 사용해야 할때 템플릿 테그로 묶어준다
    - 템플릿 테그는 화면에 렌더링 되지 않는다.

  __`v-show`__
  - Truth일 경우 `display: block`
  - Falsy일 경우 `display: none`

***

### 리스트 렌더링

  __`<tag v-for=“아이템 in 아이템스>”`__
  - html엘리먼트를 반복 할 수 있다.

  __`v-for=“(아이템, 매개변수) in 아이템스”`__
  - 두번째 매개변수
    - 배열 반복시 두번째 매개변수로 배열의 인덱스 번호를 반환 받을 수 있다.
    - 객체 반복시 두번째 매개변수로 객체의 키값을 반환 받을 수 있다.

  __`<template>`__
  - 두개 이상의 html엘리먼트를 사용해야 할때 템플릿 테그로 묶어서 반복 출력 할 수 있다.
  - 템플릿 태그는 화면에 렌더링 되지 않는다.

  __`<tag. :key=“아이템.고유값”>`__
  - 리스트 렌더링 시 반드시 고유값을 부여해줘야 한다.

***

### 이벤트 핸들링

  __`v-on:이벤트명=“함수명()”`__
  - 자바스크립트 addEventListener와 동일한 기능

  __인라인 메소드 핸들러__
  - `<tag v-on:이벤트명=“함수명”>` : 인수를 재공 하지 않고 연결된 메소드 실행
  - 매소드의 첫번째 매개 변수로 해당 이벤트 객체가 반환된다. 여러개의 매개변수 지정시 `$event`이벤트 객체를 사용한다.

  __복합 이벤트 핸들러__
  - `<tag v-on:키 수식어=“함수명”, 키 수식어=“함수명”>` : 한개 이상의 여러개의 함수를 동시에 실행 할 수 있다.
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

  __시스템 수식어__
  - .ctrl
  - .alt
  - .shift
  - .meta : 동작을 명확하게 보장하지 않는다.

  __exact 수식어__
  - `<button v-on:키 명령어.시스템 수식어.exact>` : 명령어와 수식어만 함깨 눌렀을 때 동작

***

### 원시 html
  - `v-html=“데이터명”` : 문자열 데이터를 html 구조로 변환해 준다.
    - XSS 보안에 취약하다.

***

### 디렉티브 약어
  - `:` : `v-bind`의 약어
  - `@` : `v-on`의 약어

***

## 보간법
- `{{ 데이터 }}` : html 구조에서 사용
- `{{ 표현식 }}` : JavaScript 표현식이 사용 가능하다.

***
## 라이프 사이클
Vue 인스턴스나 컴포넌트가 생성되고 소멸 되기까지의 단계를 말한다.

### 라이프사이클 훅
라이프 사이클의 각 단계에서 실행되는 함수들

  __beforeCreate()__
  - 컴포넌트가 생성되기 직전에 실행 
  - 활용도 떨어짐

  __created()__
  - 컴포넌트가 생성된 직후에 실행
  - 활용도 높음

  __beforMount()__
  - 컴퍼넌트가 html에 연결 되기 직전에 실행
  - 활용도 떨어짐
  
  __mounted()__
  - 컴퍼넌트가 html에 연결 된 후 실행
  - 활용도 높음

***

## 컴포넌트
컴포넌트(Component)란 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈

  - 컨포넌트 이름은 "케밥 케이스" 혹은 "파스칼 케이스"로 표기 해야 동작한다.

> Vue.js를 CDN으로 사용시 컴포넌트테그를 홀테그로 사용 할 수 없다.

### 전역 등록
전역(Global) 컴포넌트 : 여러 인스턴스에서 공통으로 사용할 수 있는 컴포넌트

  __컴포넌트 생성__
  > js
  ```js
  const 옵션명 = {
    template: ' ... ',
    data() {
      return {
        ...
      }
    }
  }
  
  Vue.createApp(App).component(‘컴포넌트명’, 옵션명)
  ```

  __컴포넌트 사용__
  > html
  ```html
  <컴포넌트명 />
  ```

***

### 지역 등록
지역(Local) 컴포넌트 : 특정 인스턴스에서만 유효한 범위를 가짐

  __컴포넌트 생성__
  > vue
  ```js
  <script>
    import 컴포넌트명 from './컴포넌트명.vue'
    export default {
      components: {
        컴포넌트명
      },
      data() {
        return {
          ...
        }
      }
    }
  </script>
  ```

***

### Props
자식 컴포넌트에 데이터 전달

  __html 자식 컴포넌트 테그__
  - `디렉티브:속성명="데이터"`  
  부모로 부터 넘어온 데이터를 테그 속성에 할당한다.
    

  __js 자식 컴포넌트 속성__
  - 컨포넌트 속성 `template`안에 `props:{ 속성명: 데이터타입 }`객체 선언
  - 속성명을 호출하여 반응형 데이터로 사용 할 수 있다.
  - 프롭스 규칙을 지켜서 사용해야 한다.

  > [공식문서 참조 →](https://v3.ko.vuejs.org/guide/component-basics.html#props%E1%84%85%E1%85%B3%E1%86%AF-%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A2-%E1%84%8C%E1%85%A1%E1%84%89%E1%85%B5%E1%86%A8-%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3%E1%84%8B%E1%85%A6%E1%84%80%E1%85%A6-%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5-%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%83%E1%85%A1%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5)  
  > [프롭스 규칙 →](https://v3.ko.vuejs.org/guide/component-props.html#prop-%E1%84%8B%E1%85%B2%E1%84%92%E1%85%AD%E1%84%89%E1%85%A5%E1%86%BC-%E1%84%80%E1%85%A5%E1%86%B7%E1%84%89%E1%85%A1)

***
### 하위 컴포넌트 이벤트 수신
#### Emit
부모 컨포넌트에 데이터 전달  
전달하는 데이터는 부모 컨포넌트에!!

  __js 자식 컴포넌트 속성__
  - `this.$emit('커스텀-이벤트', 전달할-데이터)` 데이터 전달
  메소드 영역에서 내장 이벤트 객체(`$event`)에 데이터를 할당한다.  

  __html 부모 컴포넌트 테그__
  - `v-on:커스텀-이벤트="전달할-데이터($event)"` 전달 받은 데이터
  - 이벤트 객체(`$event`)를 인수로 받아 데이터를 갱신해 준다.
  

  > [공식문서 참조 →](https://v3.ko.vuejs.org/guide/component-basics.html#%E1%84%92%E1%85%A1%E1%84%8B%E1%85%B1-%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%89%E1%85%AE%E1%84%89%E1%85%B5%E1%86%AB)

***

#### 컴포넌트에서 v-model 사용하기
  - 원칙적으로 `props`를 통하여 부모 컴포넌트로 부터 전달 받은 데이터는 자식 컴포넌트에서 수정 할 수 있는 권한이 없어, 양방향 데이터 바인딩 `v-model`을 사용 할 수 없다.

  __update.modelValue__
  - 해당 속성을 통하여 v-model을 사용할 수 있다

    __html 자식 컴포넌트 테그__
    - 부모로 부터 넘어온 데이터를 테그 속성에 할당한다.
      - `v-model:속성명="데이터"`

    __js 자식 컴포넌트 영역__
    - 컴포넌트 영역의 사용할 테그 속성에  
    `디렉티브="$emit('update:modelValue', 전달할-데이터")`를 할당하여 사용할 수 있다.

***

### Slot
컴포넌트의 컨텐츠를 컴포넌트 안에 담아서 출력 한다.
  > html
  ```html
  <컴포넌트>
    <slot>컨텐츠</slot>
  </컴포넌트>
  ```
  > [slot 공식문서 →](https://v3.ko.vuejs.org/guide/component-slots.html)

***

### 동적 컴포넌트
컴포넌트를 동적으로 렌더링 해야할때 사용한다.

  __동적 컴포넌트 생성__
  - 자식 컴포넌트 생성

  __부모 컴포넌트__
  - `<Component :is="'컴포넌트명'">`  
  컴포넌트 테그를 사용하여 동적 컴포넌트를 생성한다.
    - :is에는 동적 컴포넌트를 가진 함수를 사용 할 수 도 있다.

  __keep-alive__
  - 동적 컴포넌트를 `keep-alive`테그로 바인딩 하면  
  동적컴포넌트를 한번 렌더링된 상태로 컴포넌트를 유지한다.
    > html
    ```html
    <keep-alive>
      <Component :is="'컴포넌트명'">
    </keep-alive>
    ```

***

## DOM 템플릿 파싱 주의사항
`ul`테그와 같이 부모, 자식 테그 조합으로 이루어진 테그는  
컴포넌트로 자식 테그`li`를 렌더링 하면 에러가 발생하는데  
이때 발생 에러는 기능적 에러가 아닌 html 구조에서 발생하는 에러로  
다음과 같이 사용하면 에러를 막을 수 있다.

  >html
  ```html
  <ul>
    <li v-is="'컴포넌트명'"></li>
  </ul>
  ```

***

## 컴포지션 API

  __Teleport__
  - 컴포넌트를 원하는 html테그 구조에 이동시킬 수 있다.
  >html
  ```html
  <Teleport to="css선택자"> ... </Teleport>
  ```
  - 해당 html테그 마지막 자식요소로 밀어 넣는다

***

## SFC(Single-File Components)
컴포넌트를 파일단위로 만드는 것을 말한다.

  __파일생성__
  - `컨포넌트명.vue`
  - 싱글파일 컴포넌트에서는 컴포넌트명 앞자리를 대문자로 표기해준다.

***

## 애플리케이션

  __로컬스토리지__
  - 해당하는 주소, 로컬호스트 환경에 남아있는 데이터

    __접근 방법__
    - `window.localStorage.함수()`
      - `window.`는 생략이 가능하다.

  __세션스토리지__
  - 브라우저를 종료하면 데이터는 초기화 된다.

  __세션 스토리지와 로컬 스토리지__
  - 로컬 스토리지와 세션 스토리지의 데이터는 참조형 데이터는 담을 수 없다.
  - 참조형 데이터 사용시 제이슨 문자 데이터로 변경해야 하며 그때 사용 할수 있는 메소드는
  `JSON.stringify`이다. 참조형 데이터를 제이슨 문자 데이터로 변환해 준다.

***


## Vue 비동기
  - Vue.js의 반응형 데이터는 화면이 갱신될 때 비동기 상황이 발생하며 화면 갱신 후 동작상황을 처리 할때는 Vue 인스턴스 메서드 `$nextTick()` 사용하여 문제를 해결 할 수 있다.

***

## Vue 인스턴스 속성

  __$refs__
  - DOM요소에 직접 접근하여 엘리먼트를 제어한다.
  - 컴포넌트 메소드 영역에서 요소를 지칭하는 ref속성을 참조하여 데이터를 사용 할 수 있다.
    - `<input ref="데이터이름">` html 요소에 `ref속성` 지정  
    - `this.$refs.데이터이름` js 컴포턴트 메소드 영역에서 `$refs` 속성으로 html `ref속성` 참조

***

## Vue 인스턴스 메서드

  __$nextTick()__
  - setTimeOut()과 같은 기능

  __$nextTick()__
  - 반응형 데이터의 변경사항이 생겼을 때 화면 갱신 후 처리를 지정 할 수 있다.
  - 콜백 함수 패턴으로 사용 할 수 있지만 `$nextTick()`은 프로미스 인스턴스를 반환한다. 따라서 명시적으로 비동기 패턴을 지정하여 사용 할 수 있다.

***

## 플러그인
플러그인은 Vue 전역에 기능을 추가하는 방식이다.  
플러그인 생성시 이름 앞에는 `$`를 붙인다.  
ex)`$이름`

  __플러그인 생성__
  > 플러그인.js
  ```js
  export default {
    // install 플러그인 설치 메소드
    install: (app, options) => { 
      // 플러그인 코드는 여기에
      // globalProperties : 전역 맴버를 등록할 수 있다.
      app.config.globalProperties.$플러그인명 = () => {

      }
    }
  }
  ```

  __플러그인 연결__
  > main.js
  ```js
  import { createApp } from 'vue'
  import 플러그인명 from './주소'
  import App from './App.vue'

  createApp(App)
    .use(플러그인명) // 플러그인 연결
    .mount('#app')
  ```

  > [플러그인 작성하기 →](https://v3.ko.vuejs.org/guide/plugins.html)  
  > [애플리케이션 설정 →](https://v3.ko.vuejs.org/api/application-config.html)

  __플러그인 사용__
  - `$플러그인명`을 호출 하여 전역에서 사용 할 수 있다.

***

## Composition API

  > [공식문서 →](https://v3.ko.vuejs.org/api/composition-api.html#setup)

***

## CRUD

  - Read : 조회
  - Create : 추가
  - Update : 수정
  - Delet : 삭제

***

## API method 방식 
기능 적으로는 `POST`방식만 사용해도 되지만 명시적으로 `RESTFULL`하게 작성 해야한다.

  - GET : 읽기
  - POST : 쓰기
  - PUT : 수정
  - DELETE : 삭제

> 하나의 API를 생성하여 재사용 한다.

***

# Veux
한 컴포넌트에서 여러 데이터를 주고 받을 때 데이터의 흐름을 추론하기 어려워저
데이터의 상태를 관리하기 위해 만들어진 플러그인이다.

## 설치 및 사용

  __Veux 설치__
  > 터미널
  ```bash
  npm i veux
  ```
  
  __store생성__
  > src/store/index.js
  ```js
  // vue 객체를 package.json에서 가져온다.
  // createStore를 실행하면 "store"인스턴스를 반환한다.
  import { createStore } from 'vuex'

  export default createStore({

  })
  ```

  __플러그인 연결__
  > main.js
  ```js
  // vue 객체를 package.json에서 가져온다.
  import { createApp } from 'vue' 
  import store from './store'
  import App from './App.vue'

  createApp(App)
    .use(store) // 플러그인 연결
    .mount('#app')
  ```

***

## Core Concepts

  __state() {}__
  - 반응형 데이터

    __store__
    - 데이터 상점, 다른 컴포넌트가 접근이 가능하도록 만든다.
    - state 반응형 데이터의 수정권한은 해당 store의 컨포넌트에게 있다.

    __computed__
    - 일반 컴포넌트에서 store에 접근하기 위해선  
    계산된 데이터(computed)로 접근 해야 한다.
    - `this.$store` 스토어 접근하기

    __this__
    - Vuex에서는 `this`키워드 대신 `state`로 데이터를 호출 한다.

  __getters__
  - 계산된 상태

  __mutations: {}__
  - state 반응형 데이터의 수정권한이 있는 메소드
  - 첫번째 인수로 `state`객체를 받아서 수정한다.
  - 두번째 인수로 매개변수(payload)를 받아 인수를 활용한다.

  __actions: {}__
  - state 반응형 데이터의 수정권한이 없는 메소드
  - `actions` 안에서 컴포넌트와 `mutations`를 사용하는 것을 권장
  - 통상 함수처럼 동작하는 로직은 모두 `actions`에 부여한다.

    __context__
    - `actions`의 매개변수로 받을 수 있는 객체 데이터
    > context 구조
    ```js
    const {
      state, // state에 접근할 수 있는 객체
      getters, // getters에 접근할 수 있는 객체
      commit, // `mutations`를 호출 할 수 있는 함수
      dispatch // `actions`을 호출 할 수 있는 함수
    } = context
    ```
    
  __modules__ 

***


22.05.26

Veux

포스트 방식으로만 해도 가능

암묵적으로 지키자  get, post, put?, delete

curl 표기법
주소

@ret… : 타입 설명 

플러그인 : 외부에서 만들어진 기능을 사용

1. src 파일 안에 plugins폴더 생성 > guswowh.js 
2. guswowh.js
export default{install((app){

}}

app : 현재 vue 프로젝트를 의미

globalProperties : 전역 맴버를 등록할 수 있다.
  현재 vue 프로젝트에 연결 해야한다.

터미널 오류로 경로가 잘못 되어 있을 수 있다 경로 체크 필수!

vue.js 플러그인은 앞에 “$”인을 붙인다.
$는 vue.js 내부기능 이거나 플러그인 이다.

npm i veux : 설치해도 4버전 설치됨

.use : 플러그인 연결

nom info vuex

latest 뒷 버전 next 다음버전

모듈화 : 파일로 만들어 관리

index.js는 import로 가져올 때 생략이 가능하다.

core concepts
  state : 반응형 데이터 || 상태
    store : 데이터 상점, 다른 컴포넌트가 접근이 가능하도록 만든다.
      - store의 수정권한은 선언되어 있는 컨포넌트에게 있다.
      - 비동기에도 많이 사용
    computed : store에 접근하기 위해선 계산된 데이터로 접근 해야 한다.
  getters : 계산된 상태
  mutations : 수정권한이 있는 메소드
  actions : 수정권한이 없는 메소드
    
  modules : 

Vuex 에서는 this를 사용하지 않는다.
  - state를 매개변수로 받아서 사용한다.

commit( 매개변수 ) : mutations 호출할때 사용
dispatch : actions 호출할때 사용

payload : veux에서 매개변수를 말한다.

no-props : 프롭스가 아닌 속성, 최상위 컴포넌트에 붇는다.
  - v-bind=“$attrs” : 템플릿 테그 안에 2개 이상의 컴포넌트가 있을 경우 사용하고 싶은 컴포넌트에 선언한다.

# Vue Router

- vue Router : 페이지를 관리하는 플러그인
  - <RouterLink /> : 라우터 관리가 가능하게 페이지 이동
    - to : 이동 페이지
    - active-class : 현재 주소와 페이지 버튼이 같은 위치 일때 router-link-active를 클레스에 넣어준다
      - router-link-active(기본 값) : 프롭스로 변경 가능
    - 내부페이지 이동은 <a>를 사용한다.
  - <RouterView /> : 렌더링 되는 영역을 지정해 준다.

- npm i vue-router : 라우터 설치
- 라우트 뜻 : 페이지 정보
- createRouter
  - history: : 히스토리 모드 혹은 해쉬 모드 사용 여부
    - createWebHashHistory
    - createWebHistory

  - routes: [] : 
    - path : ‘/’ : 주소
    - component : ‘컴포넌트명’ : 컴포넌트 연결

- 히스토리 모드 : http://주소
- 해쉬 모드 : http://주소/#/
- SPA : 싱글페이지 에플리케이션
  - 해쉬 모드 : 화면의 페이징 처리에 해시모드 주소가 필요하다.
  - 히스토리 모드 : 화면의 페이징 처리하기 위해선 서버 세팅이 필요하다.

- 트리쉐이킹 : 개념 검색

- 내장 객체
  - this.$router : 페이지 이동 명령(함수)이 들어있다.
    - push()
  - this.$route : 현재 페이지 정보가 들어있다.


- 파라미터 동적 페이지 주소 메칭(Dynamic Route Matching with params)

- 404 Not found Route : 페이지를 찾을 수 없는 상태 코드(status code)



22.06.02


## vite js 시작
- nom create vite@latest vite-test
- cd vite-test
-
- npm i vue-router

## 패키지 설치
- nom i -D aslant aslant-plugin-vue sass

## vite.config.js : 경로 별칭 설정
  - 

## .eslintrc.json : 기본 구조 설정
  - 

## src/routes 폴더 생성
  > index.js 파일 생성
```
  import {.createRouter, createWebHistory } from ‘vue-router’
  import Home from ‘./App.vue’

  export default createRouter({
    history: createWebHistory(),
    routes: [
      {
        path: ‘/’,
        component: Home
      }
    ]
  })
```

## main.js: 설정
  - 

