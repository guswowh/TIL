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
  - 통상 최상위 컴포넌트 변수명은 "App"으로 사용한다.

***
## 기본 구조 테그
  - `<template>` : html 구조를 작성 할 수 있다.
    
    > Note : 최상위 요소 템플릿은 v-if를 사용 할 수 없다.
    
  - `<script></script>` : 자바스크립트를 작성 할 수 있다.

  - `<style></style>` : css를 작성 할 수 있다.
    - 옵션
      - scoped : 부여된 컴포넌트의 값이 고유해 진다.
      - lang : scss

***

## API 옵션
  - data
    - 데이터는 함수여야 함다.
  - computed
    - 반응형 데이터를 기준으로 계산된 데이터를 반환 한다.
    - Getter 와 Setter를 사용 할 수 있다.
    - Computed Caching
      - 한번 사용된 데이터를 재사용 한다.
  - methods
    - 일반 함수여야 한다.
 - watch
    - 반응형 데이터의 변경사항을 감지한다.
    - newValue, oldValue 내장 객체데이터를 사용 할 수 있다.
      - newValue : 변경후 데이터
      - oldValue : 변경전 데이터
  - props
  - emits

***

## 데이터 접근
  - this.데이터명 
     - Vue에서 데이터에 접근하기 위해서는 this키워드를 사용해야 한다
     - this키워드가 없을 시 전역 변수

***

## 디렉티브

###  단방향 데이터 바인딩
데이터가 한쪽 방향으로 전달되는 구조

  - `v-bind:html속성=“데이터명”` : html 속성에 데이터 전달
  - `v-bind:[데이터이름]` : 데이터 전달

  - __html 클래스. 바인딩__
    - 객체 구문
      - `v-bind:class=“{ html속성: 데이터명, … }”` : boolean을 판별 한다.
    - 배열 구문
      - `v-bind:class=“[객체데이터, …]”` : boolean을 판별 한다.
    - 컴포넌트 구문
      - 

  - __인라인 스타일 바인딩__
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

  - __병렬방식__
    - `v-model=“데이터명”` : 
    - `type=“checkbox” v-model=“불린 데이터명”`
    - `type=“select” v-model=“불린 데이터명”`

  - __직렬방식__ 
  > html
  ```html
  <input v-bind:value=“데이터명” v-on:input=“데이터명” = $event.target.value />
  ```
    - `type=“input”` 태그에는 `value` 와 `input` 이벤트 사용
    - `type=“checkbox”` 태그에는 `checked` 와 `change` 이벤트 사용
    - `type=“select”` 태그에는 `value` 와 `change` 이벤트 사용
    > Note : 한글, 일본어, 중국어 입력시 직렬방식 사용

  - __수식어__
    - `.lazy` : 사용자가 입력을 완료하면 갱신된다.
      - 직렬방식 사용시 `change`이벤트를 사용하면 된다.
    - .`number` : 사용자가 입력한 데이터를 숫자형 데이터로 형변환 한다.
    - .trim : 사용자가 입력한 데이터의 앞뒤 공백 문자를 제거하여 반환한다.

***

### 조건부 렌더링
  - `v-if` : Truth일 경우 화면에 렌더링한다.
      - `v-else-if`, `v-else` : `v-if`밑에 붙어 있어야 실행된다.
  - `<template>` : 두개 이상의 엘리먼트를 사용해야 할때 템플릿 테그로 묶어준다
    - `<template>`는 화면에 렌더링 되지 않는다.
  - `v-show` : Truth일 경우 css display 값을 block으로 할당 한다.

***

### 리스트 렌더링
  - `<tag v-for=“아이템 in 아이템스>”` : html엘리먼트를 반복 할 수 있다.
  - `<tag. :key=“아이템.고유값”>` : 리스트 렌더링 시 반드시 고유값을 부여해줘야 한다.
  - `v-for=“아이템 in 아이템스”` : 반복문
  - `v-for=“(아이템, 매개변수) in 아이템스”` : 두번째 매개변수
    - 배열 반복시 두번째 매개변수로 배열의 인덱스 번호를 반환 받을 수 있다.
    - 객체 반복시 두번째 매개변수로 객체의 키값을 반환 받을 수 있다.
  - `<template>` : 두개 이상의 html엘리먼트를 사용해야 할때 템플릿 테그로 묶어서 반복 출력 할 수 있다.
    - `<template>`는 화면에 렌더링 되지 않는다.

***

### 이벤트 핸들링
  - `v-on:이벤트명=“함수명()”` : 자바스크립트 addEventListener와 동일한 기능

  - __인라인 메소드 핸들러__
    - `<tag v-on:이벤트명=“함수명”>` : 인수를 재공 하지 않고 연결된 메소드 실행
    - 매소드의 첫번째 매개 변수로 해당 이벤트 객체가 반환된다. 여러개의 매개변수 지정시 `$event`이벤트 객체를 사용한다.

  - __복합 이벤트 핸들러__
      - `<tag v-on:키 수식어=“함수명”, 키 수식어=“함수명”>` : 한개 이상의 여러개의 함수를 동시에 실행 할 수 있다.
  - [__이벤트 참조__](https://developer.mozilla.org/ko/docs/Web/Events)
  - __이벤트 수식어__
    - `.stop` : 이벤트 버블링 방지
    - `.capture` : 이벤트 켑처링 방지
    - `.prevent` : Vue 기본동작 방지
    - `.self` : event.target 과 event.currentTarget이 같을 때 동작
    - `.once` : 이벤트 한번만 동작
    - `.passive` : 화면을 움직이는 동작과 로직을 처리하는 동작을 분리

  - __키 명령어__
    - .enter
    - .tab
    - .delete (“Delete” 와 “Backspace” 키 모두를 캡처합니다)
    - .esc
    - .space
    - .up
    - .down
    - .left
    - .right

  - __시스템 수식어__
      - .ctrl
      - .alt
      - .shift
      - .meta : 동작을 명확하게 보장하지 않는다.

  - __exact 수식어__
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
  - beforeCreate()
    - 컴포넌트가 생성되기 직전에 실행 
    - 활용도 떨어짐
  - created()
    - 컴포넌트가 생성된 직후에 실행
    - 활용도 높음
  - beforMount()
    - 컴퍼넌트가 html에 연결 되기 직전에 실행
    - 활용도 떨어짐
  - mounted()
    - 컴퍼넌트가 html에 연결 된 후 실행
    - 활용도 높음

***

## Vue 인스턴스 메서드
- $nextTick() : setTimeOut()과 같은 기능

***

## 컴포넌트
컴포넌트(Component)란 프로그래밍에 있어 재사용이 가능한 각각의 독립된 모듈

  - 컨포넌트 이름은 "케밥 케이스" 혹은 "파스칼 케이스"로 표기 해야 동작한다.

### 전역 등록
  - __컴포넌트 생성__
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
    
    Vue.createApp(App).component(‘컴포넌트이름’, 옵션명)
    ```
  - __컴포넌트 사용 __
    > html
    ```html
    <컴포넌트이름 />
    ```
		- Vue.js를 CDN으로 사용시 컴포넌트를 홀테그로 사용 할 수 없다.

***

### 지역 등록

***

### Props
자식 컴포넌트에 데이터 전달

[공식문서 참조 →](https://v3.ko.vuejs.org/guide/component-basics.html#props%E1%84%85%E1%85%B3%E1%86%AF-%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A2-%E1%84%8C%E1%85%A1%E1%84%89%E1%85%B5%E1%86%A8-%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3%E1%84%8B%E1%85%A6%E1%84%80%E1%85%A6-%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5-%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%83%E1%85%A1%E1%86%AF%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5)

***

### Emit
부모 컨포넌트에 데이터 전달

[공식문서 참조 →](https://v3.ko.vuejs.org/guide/component-basics.html#%E1%84%92%E1%85%A1%E1%84%8B%E1%85%B1-%E1%84%8F%E1%85%A5%E1%86%B7%E1%84%91%E1%85%A9%E1%84%82%E1%85%A5%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%89%E1%85%AE%E1%84%89%E1%85%B5%E1%86%AB)

***












22.05.26

# Veux

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

nom i veux : 설치해도 4버전 설치됨

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

