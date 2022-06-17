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

## 컴포지션 API
API 옵션의 로직을 읽기 쉽게 로직을 정리해 줄 수 있다.

  __setup()__
  - `import { 반응형-데이터 } = vue`
    - vue페키지에서 반응성을 가진 데이터를 객체 구조분해로 가져온다.
  - 활용하려는 데이터를 `반응형-데이터`에 `변수로 할당`하여 반응성을 부여한다.
  - `변수명.value`로 데이터를 호출 할 수 있다.
  - `반응형-데이터`

    __ref__
    - `ref(값)` : 데이터

    __computed__
    - `computed(() => {})` : 계산된 데이터

    __watch__
    - `watch(감시할-데이터, () => {})` : 감시할 데이터

    __mounted__
    - `onMounted() => {}` : 라이프사이클 훅

    __created__
    - `setup() {}` : 라이프사이클 훅

  __setup(props, context)__
  - 첫번째 매개변수로 `props`를 받고
  - 두번째 매개변수로 `this`를 받는다.
    - `context.속성명`으로 접근 할 수 있다.
  
  __$emit__
  - `context.emit('전달할-데이터')`로 데이터를 전달 할 수 있다.

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

## API 레퍼런스

### Vue 인스턴스 속성

  __$refs__
  - DOM요소에 직접 접근하여 엘리먼트를 제어한다.
  - 컴포넌트 메소드 영역에서 요소를 지칭하는 ref속성을 참조하여 데이터를 사용 할 수 있다.
    - `<input ref="데이터이름">` html 요소에 `ref속성` 지정  
    - `this.$refs.데이터이름` js 컴포턴트 메소드 영역에서 `$refs` 속성으로 html `ref속성` 참조

  __$attrs__
  - 부모 컴포넌트 속성 상속

### Vue 인스턴스 메서드

  __$nextTick()__
  - setTimeOut()과 같은 기능
  - 반응형 데이터의 변경사항이 생겼을 때 화면 갱신 후 처리를 지정 할 수 있다.
  - 콜백 함수 패턴으로 사용 할 수 있지만 `$nextTick()`은 프로미스 인스턴스를 반환한다. 따라서 명시적으로 비동기 패턴을 지정하여 사용 할 수 있다.

***

## Teleport
컴포넌트를 원하는 html테그 구조에 이동시킬 수 있다.

> html
```html
<Teleport to="css선택자"> ... </Teleport>
```
- 해당 html테그 마지막 자식요소로 밀어 넣는다

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
        ...
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